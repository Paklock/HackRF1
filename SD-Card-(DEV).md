## About

Reading and writing to the SD card is a great way for your application to save progress or reference data that might be to too large to fit in the firmware. Below are examples on how to interface with the SD card using the Mayhem code base.

## File Class

Most of the heavy lifting for working with files on the SD Card is done by the [File](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/file.cpp) class. This helper class which simplifies the `FatFs - Generic FAT file system module` which can found at [`firmware/chibios-portapack/ext/fatfs/src/ff.c`](https://github.com/eried/portapack-mayhem/blob/next/firmware/chibios-portapack/ext/fatfs/src/ff.c). Below are some examples on how to read and write files to the SD card.

Continuing with the [Create a Simple App](Create-a-simple-app) the code bellow will outline what is required to manipulate the file system. The first thing you'll need to do is include the File class and SD Card helper functions to your application's hpp file. 

#### ui_newapp.hpp
```
// Add these to include File Class and SD Card helper functions.
#include "file.hpp" 
#include "sd_card.hpp"
```

### Check SD Card

Before reading and writing from the SD Card it's ideal to do a quick check to see if the SD card is mounted on the device. There is error handing working in the background that keeps things from crashing however this will give people a better idea if there's a problem or not. The function below dose a quick check to see if the SD Card is showing a status of being Mounted. This will return true if sd_card::status() returns "Mounted" or false if sd_card::status() returns any other status. SD Card statuses are defined in [firmware/application/sd_card.hpp](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/sd_card.hpp).    


#### ui_newapp.cpp
```
// Checks SD Card, returns true if Mounted, false if otherwise
bool NewAppView::check_sd_card() {
    return (sd_card::status() == sd_card::Status::Mounted) ? true : false; 
}
```

Below is a quick example on how this error check could be used. 
#### ui_newapp.cpp
```
// Check SD Card
if(check_sd_card()) {                                       // Check to see if SD Card is mounted
    // Logic if SD Card is mounted 
} else {                                                    // Else, check_sd_card() returned false 
    // Logic if SD Card is NOT mounted
}
```

### List Directory Contents

To make things easier to use we're going to use a method from [firmware/application/apps/ui_fileman.cpp](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/apps/ui_fileman.cpp) to list the contents of the SD Card. First thing we'll need to do is create a Struct that outlines the pertinent information of the SD Card's contents. Each struct will include the file path, size, and if the item is a directory or not.  

#### ui_newapp.hpp
```
// Struct that outlines file information
struct file_entry {
    std::filesystem::path entry_path { };
    uint32_t size { };
    bool is_directory { };
};
```

Below is an function that will return a [Vector](https://www.geeksforgeeks.org/vector-in-cpp-stl/) (simmer to a list) of `file_entry` Struts. The input for this function needs a `std::filesystem::path` which can be `UTF-16 string literal`. The root of the SD Card is `u""` and any directory beyond that is `u"DIRECTORY/SUB_DIRECTORY"`. 

This function will also place any directorys at the front of the Vector and files in the back. This will also skip any files that are hidden as in anything with a `.` in front of the file name.     

#### ui_newapp.cpp
```
// Lists all files and directorys in path
std::vector<file_entry> NewAppView::list_dir(const std::filesystem::path& path) {

    // Files and directories list
    std::vector<file_entry> entry_list { };

    // For each entry in the file system's directory
    // Adds files in directorys into entry_list{} 
    // Directorys are inserted infront of files
    for (const auto& entry : std::filesystem::directory_iterator(path, u"*")) {

        // Dose not add directorys or files starting with '.' (hidden / tmp)
        if (entry.path().string().length() && entry.path().filename().string()[0] != '.') {

            // If file 
            if (std::filesystem::is_regular_file(entry.status())) {
                entry_list.push_back({ entry.path(), (uint32_t)entry.size(), false });

            // Else If directory    
            } else if (std::filesystem::is_directory(entry.status())) {
                entry_list.insert(entry_list.begin(), { entry.path(), 0, true });
            
            // Other
            } else {
                continue;
            }
        }

    }
    return entry_list;
}
```

### Create Directory

To create a directory we can use the `make_new_directory()` function from [File](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/file.cpp). The helper function below will return true if `make_new_directory()` succeeds (Success from `make_new_directory()` returns a 0, other values means failure) and takes two variable inputs for file path and directory name. Again the input for the file path is a `std::filesystem::path` which can be `UTF-16 string literal`. The root of the SD Card is `u""` and any directory beyond that is `u"DIRECTORY/SUB_DIRECTORY"`.      

#### ui_newapp.cpp
```
// Creates dir, returns true if successful 
bool NewAppView::create_dir(const std::filesystem::path& path, std::string name) {  // make_new_directory() returns 0 for success
    return !(make_new_directory(path.string() + "/" + name));                       // and other values means failure. Not operation  
}                                                                                   // will return true only when 0 is returned. 
```

Below is an example on how the `create_dir()` function can be used with basic error handling.  

#### ui_newapp.cpp
```
// New directory
if(check_sd_card()) {                     // Check to see if SD Card is mounted
    if(create_dir(u"", "NEW_DIR")) {      // New dir in root of SD Card, returns true if successful
        // Logic if new dir succeeded 
    } else {
        // Logic else new dir failed
    } 
} else {                                  // Else, check_sd_card() returned false
    // Logic else SD Card is NOT mounted
}
```

### Delete Directory

   

### Create File

### Read File   

### Write File  

### Delete File   


## Wrap Up

### ui_newapp.hpp

    #include "ui.hpp"
    #include "ui_widget.hpp"
    #include "ui_navigation.hpp"
    #include "string_format.hpp"

    // Add this to include the File Class.
    #include "file.hpp" 

    namespace ui
    {
        class NewAppView : public View                                // App class declaration
        {
        public:
            NewAppView(NavigationView &nav);                          // App class init function declaration
            std::string title() const override { return "New App"; }; // App title

        private:
            void update();                                            // Function declaration
            MessageHandlerRegistration message_handler_update{        // Example, not required: MessageHandlerRegistration class
                Message::ID::DisplayFrameSync,                        // relays messages to your app code from baseband. Every time you 
                [this](const Message *const) {                        // get a  DisplayFrameSync message the update() function will
                    this->update();                                   // be triggered.  
                }};
        };
    } 

### ui_newapp.cpp

    #include "ui_newapp.hpp"
    #include "portapack.hpp"
    #include <cstring>

    using namespace portapack;

    namespace ui
    {

        NewAppView::NewAppView(NavigationView &nav) // Application Main
        {
             // App code
        }

        void NewAppView::update()                   // Every time you get a DisplayFrameSync message this function will be ran
        {
             // Message code
        }
    }

   