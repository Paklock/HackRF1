## About

This wiki will go over how to create a simple application and show you the basics in the Mayhem code base. This is to be considered a "hello world" application. :)  

We are going to create few simple controls and link the app to the main menu. The idea is to get familiar with the way things work.

## First steps

There is a lot of flexibility, but for now we are going to follow patterns already found on the source code. For example, the name of the files and classes will be inspired by existing code.

## Application code

The following structure is the base of any application. Following the general structure, this files in this example will be created on `firmware\application\apps\`

### ui_newapp.hpp

    #include "ui.hpp"
    #include "ui_widget.hpp"
    #include "ui_navigation.hpp"
    #include "string_format.hpp"

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

## Entry in the main menu

For triggering your new app, you need to add an entry on the main menu. This menu resides on [`firmware\application\ui_navigation.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/ui_navigation.cpp). Check the current entries, and add a new one in a section you think is suitable for your new app.

#### firmware\application\ui_navigation.cpp 
```
// Add this to the top to link your new app's header file
#include "ui_newapp.hpp"

...

// Adding NewApp to the Transmitters Menu
TransmittersMenuView::TransmittersMenuView(NavigationView& nav) {
    add_items({

        ...

        { "NewApp", ui::Color::red(), &bitmap_icon_remote, [&nav](){ nav.push<NewAppView>(); } },
    });
}
``` 

## Early test

Remember to add your `apps/ui_newapp.cpp` to `firmware\application\CMakeLists.txt`

#### firmware\application\CMakeLists.txt
```
# C++ sources that can be compiled in ARM or THUMB mode depending on the global
# setting.
set(CPPSRC
    main.cpp

    ...

    apps/ui_newapp.cpp
)
``` 

In this moment you should be able to compile and test the app in your device. For your reference here's the link to the [Compile-firmware](https://github.com/eried/portapack-mayhem/wiki/Compile-firmware) wiki. The new app should appear in the menu you picked in `ui_navigation.cpp`.

## Adding Widgets and Basic Functionality

Widgets are the elements that compose the UI of your custom app. Widgets are defined inside [`firmware\common\ui_widget.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) and widget functions can be found inside [`firmware\common\ui_widget.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.cpp). In order to be able to use them, you must `#include "ui_widget.hpp"` into your app .hpp file.
There are different type of widget. here you will find a list of available widget, with their respecting constructor. For all the methods available, you should go and see the [ui_widget.hpp](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) file.

### Attach a Generic Widget to Your Application

In order to display a widget into your app, you can either use the function `add_child()` or `add_children()`. 
Both those functions shall be called within the code of your `NewAppGameView(NavigationView &nav){}` constructor. The difference between the two function is simple: the first one allows you to add a single widget, while the second one allows you to add an undefined number of widgets.
Widgets must be passed as pointers to the functions. A correct way of calling the two functions would then be: 
```
add_child(&my_widget);
```
or
```
add_children({
    &widget_1,
    &widget_2
});
```

There are several different widgets that we're going to use for our new app. A more complete list can be found on the [Widgets](https://github.com/eried/portapack-mayhem/wiki/Widgets) wiki. More might be added so you should always go and check whether new widgets have been added or not.


#### Button

Buttons allows you to do something when you press them. Here you can find it's declaration and prototype:
```
Button my_button_widget{
    Rect parent_rect,
    std::string text
};
```
Be aware that every time you create a button, you then have to implement this method: `my_button_widget.on_select = [&nav](Button &){}`. You can leave it empty (even though it should not, as here you define what action the button should perform), but it must be present in your code.

For example, let's say you want a button called `my_button`, with the same dimensions as the previous widget. You will then do:
```
Button my_button(
   {10, 10, 100, 24}, // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
   "my_button_text"
);
```


#### Labels

Labels are a text element that can be used to describe other widgets. Here you can find it's declaration and prototype:
```
Labels my_label_widget{
    std::initializer_list<Label> labels
};
```

For example, let's say you want a label called `my_label`. Because the constructor is looking for  list you'll need to add a set of brackets `{}` around each label.  You will need to add this to `apps/ui_newapp.hpp`:
```
Labels my_label{
    {{10, 10},            // Coordinates are: int:x (px), int:y (px)
    "my_label_text:",     // Label text
    Color::light_grey()}, // Label color
};
```

**Note:** Colors are defined in [`firmware/common/ui.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui.hpp).

In `apps/ui_newapp.cpp` you'll need to add the `my_label` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_label,
    });

}
```


#### LiveDateTime

LiveDateTime gives you the dynamic date and time. Here you can find it's declaration and prototype:
```
LiveDateTime my_liveDateTime_widget{
    Rect parent_rect
};
```

For example, let's say you want a label called `my_liveDateTime`. You will need to add this to `apps/ui_newapp.hpp`:
```
LiveDateTime my_liveDateTime {
    { 2, 10, 19*8, 16 },       // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
};
```

In `apps/ui_newapp.cpp` you'll need to add the `my_liveDateTime` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_liveDateTime,
    });

}
```

If you want to enable seconds you'll need use the `set_seconds_enabled(bool new_value)` function:
```
my_liveDateTime.set_seconds_enabled(true);
```


#### ProgressBar

Progress bars are a visual representation of progress that let us know how far a long a task is. Here you can find it's declaration and prototype:
```
Labels my_progressBar_widget{
    Rect parent_rect
};
```

For example, let's say you want a label called `my_progressBar`. You will need to add this to `apps/ui_newapp.hpp`:
```
ProgressBar my_progressBar {
    { 2, 10, 208, 16 },      // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
};
```

In `apps/ui_newapp.cpp` you'll need to add the `my_progressBar` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_progressBar,
    });

}
```

To set the maximum value for the progress bar use the `set_max(const uint32_t max)` function:
```
my_progressBar.set_max(10); // 10 is 100%
```

To change the value of progress for the progress bar use the `set_value(const uint32_t value)` function:
```
my_progressBar.set_value(5); // 50% Complete
```


#### NumberField

NumberField is similar to the OptionsField widget except that it only deals with numbers. You can change its value with the wheel on your portapack. Here you can find it's declaration and prototype:
```
NumberField my_NumberField_widget{
    Point parent_pos, 
    int length, 
    range_t range, 
    int32_t step, 
    char fill_char, 
    bool can_loop
};
```

For example, let's say you want a NumberField called `my_numberField`. You will need to add this to `apps/ui_newapp.hpp`:
```
// Example 3 digit number starting at "000", ends at "255"
NumberField my_numberField(
    {10, 10},          // Coordinates are: int:x (px), int:y (px)
    3,                 // Length
    {0, 255},          // MIN -> MAX Range
    1,                 // Step
    '0',               // Fill Char
    false              // Can Loop
);
```

In `apps/ui_newapp.cpp` you'll need to add the `my_numberField` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_numberField,
    });

}
```

Functions within `apps/ui_newapp.cpp` are able to lookup the value of `my_numberField` with NumberField's `value()` function:
```
int number = my_numberField.value();
```

You can also set the value for `my_numberField` with the `set_value(int32_t new_value, bool trigger_change)` function:
```
my_numberField.set_value(123);
```

If you want your NumberField to change a value (int number for example) you'll need to add this [Lambda](https://www.geeksforgeeks.org/lambda-expression-in-c/) to `apps/ui_newapp.cpp`:  
```
NewAppView::NewAppView(NavigationView &nav) {

    // Add widget pointers
    add_children({
        &my_numberField,
    });

    // When NumberField is changed
    my_numberField.on_change = [this](int32_t v) {
        number = v;
    };

}
```

# Wrap up

Bellow is an example "Hello World" application that shows off a few widgets and logic that controls their functions.

### ui_newapp.hpp
```
#include "ui.hpp"
#include "ui_widget.hpp"
#include "ui_navigation.hpp"
#include "string_format.hpp"

// Define a constant
#define PROGRESS_MAX 100

namespace ui
{
    class NewAppView : public View                          // App class declaration
    {
    public:

        // Public declarations
    	void focus() override;                              // ui::View function override

        NewAppView(NavigationView &nav);                    // App class init function declaration
        std::string title() const override { 
            return "New App";                               // App Title
        };

    private:

        // Private declarations
        void update();                                      // Function declaration
        MessageHandlerRegistration message_handler_update{  // Example, not required: MessageHandlerRegistration class
            Message::ID::DisplayFrameSync,                  // relays machine states to your app code. Every time you 
            [this](const Message *const) {                  // get a  DisplayFrameSync message the update() function will
                this->update();                             // be triggered. 
            }
        };

        // Variables
        uint32_t progress = 0; 

        // Widgets
        // Note: Usable screen space is 240x304px
        // Note: Each char takes up 8x8px so you can multiply 
        //       the amount of spaces and rows you want by 8.
        //       This gives you 30x38 char

        Button button_helloWorld{
            {70, 128, 100, 24},            // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
            "Hello World!"                 // Title
        };

        LiveDateTime timestamp {
	    {6*8, 22*8, 19*8, 20 }         // Coordinates and Dimensions
	};

        Labels label_progress {
            {{8*8, 33*8},                  // Coordinates are: int:x(px), int:y(px)
            "Progress:     %",             // Title
            Color::light_grey()}           // Title color
        };

        NumberField numberField_progress {
            {18*8, 33*8},                  // Coordinates
            3,                             // Length of number
            {0,PROGRESS_MAX},              // Range
            1,                             // Step
            '0',                           // Fill Char
            false                          // Loop?
        };

        ProgressBar progressBar_progress {
            {2*8, 35*8, 208, 16 },         // Coordinates and Dimensions
        };
        
    };
} 
```

### ui_newapp.cpp
```
#include "ui_newapp.hpp"
#include "portapack.hpp"
#include <cstring>

using namespace portapack;

namespace ui
{

    void NewAppView::focus() {                               // Default selection to button_helloWorld when app starts
	    button_helloWorld.focus();
    }

    NewAppView::NewAppView(NavigationView &nav)              // Application Main 
    {
     
        add_children({                                       // Add pointers for widgets
            &button_helloWorld,
            &label_progress,
            &numberField_progress,
            &progressBar_progress,
            &timestamp,
        });

        progressBar_progress.set_max(PROGRESS_MAX);          // Set max for progress bar

        button_helloWorld.on_select = [this](Button &){      // Button logic
            if(progress < 100) { 
                numberField_progress.set_value(100);         // Because numberField_progress has an on_change function,
            } else {                                         // progressBar_progress will update automatically.
                numberField_progress.set_value(0);
            }
        };                                                  

        numberField_progress.on_change = [this](int32_t v) { // When NumberField is changed
            progress = v;
            progressBar_progress.set_value(progress);
        };

        timestamp.set_seconds_enabled(true);                 // DateTime enable seconds
    }

    void NewAppView::update()                                // Every time you get a DisplayFrameSync message this
    {                                                        // function will be ran.
         // Message code
    }
}
```