## About

Reading and writing to the SD card is a great way for your application to save progress or reference data that might be to too large to fit in the firmware. Below are examples on how to interface with the SD card using the Mayhem code base.

## File Class

Most of the heavy lifting for working with files on the SD card is done by the [File](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/file.cpp) class. This helper class which simplifies the `FatFs - Generic FAT file system module` which can found at [`firmware/chibios-portapack/ext/fatfs/src/ff.c`](https://github.com/eried/portapack-mayhem/blob/next/firmware/chibios-portapack/ext/fatfs/src/ff.c). Below are some examples on how to read and write files to the SD card.

### Directory(s)   

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

   