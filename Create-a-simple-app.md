This simple application will explain the basic of widgets and simple navigation. 

We are going to create few simple controls and link the app to the main menu. The idea is to get familiar with the way things work.

# First steps

There is a lot of flexibility, but for now we are going to follow patterns already found on the source code. For example, the name of the files and classes will be inspired by existing code.

## Application code

The following structure is the base of any application. Following the general structure, this files in this example will be created on `\firmware\application\apps\`

### ui_newapp.hpp

    #include "ui.hpp"
    #include "ui_widget.hpp"
    #include "ui_navigation.hpp"
    #include "string_format.hpp"

    namespace ui
    {
        class NewAppView : public View
        {
        public:
            NewAppView(NavigationView &nav);
            std::string title() const override { return "Block Game"; };

        private:
            void update();
            MessageHandlerRegistration message_handler_update{
                Message::ID::DisplayFrameSync,
                [this](const Message *const) {
                    this->update();
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
        NewAppView::NewAppView(NavigationView &nav)
        {
        }

        void NewAppView::update()
        {
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

In this moment you should be able to compile and test the app in your device. It should appear in the main menu and show an empty app upon entering to it.

# Adding functionality

## Widgets
Widgets are the elements that compose the UI of your custom app. Widgets are defined inside [`firmware\common\ui_widget.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) and widget functions can be found inside [`firmware\common\ui_widget.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.cpp). In order to be able to use them, you must `#include "ui_widget.hpp"` into your app .hpp file.
There are different type of widget. here you will find a list of available widget, with their respecting constructor. For all the methods available, you should go and see the [ui_widget.hpp](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) file.

### Attach a generic widget to you application

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

### Available widgets
There are several different widgets, and more might be added, so you should always go and check whether new widgets have been added or not. Here you will find a list of most basic widgets.

#### Text
The text widgets add a simple text area to your app. Here you can find it's declaration and prototype:
```
Text my_text_widget{
    Rect parent_rect,
    std::string text
};

```
To be noted that `Rect parent_rect` has it's own definition inside another file, but let's say that you would like to add a text widget with the text "Hello World", positioned at the top left corner (spaced 10 from both top margin and left margin), with width 100 and height 24, you cold do it in this way:
```
Text hello_world_text_widget(
  {10, 10, 100, 24}, // be aware that the coordinates are: int:x, int:y, int:width, int:height
  "Hello world!"
);
```
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
   {10, 10, 100, 24}, // be aware that the coordinates are: int:x, int:y, int:width, int:height
   "my_button_text"
);
```

#### Labels

Labels are a text element that can be used to describe other widgets. Here you can find it's declaration and prototype:
```
Labels my_label_widget{
    Point pos,
    std::string text,
    ui::Color color
};
```

For example, let's say you want a label called `my_label`. You will need to add this to `apps/ui_newapp.hpp`:
```
Labels my_label(
    {10, 10},           // Coordinates are: int:x, int:y
    "my_label_text:",   // Label text
    Color::light_grey() // Label color
);
```

Colors are defined in [`firmware/common/ui.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui.hpp) and the predefined colors include...  
* Color::black()
* Color::red()
* Color::dark_red()
* Color::orange()
* Color::dark_orange()
* Color::yellow()
* Color::dark_yellow()
* Color::green()
* Color::dark_green()
* Color::blue()
* Color::dark_blue()
* Color::cyan()
* Color::magenta()
* Color::dark_magenta()
* Color::white()
* Color::light_grey()
* Color::gray()
* Color::dark_gray()
* Color::purple()

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

#### BigFrequency

#### ProgressBar

#### Console

#### Checkbox

Checkboxs are a boolean (True/False) widget that allows you chose between one of two options . Here you can find it's declaration and prototype:
```
Checkbox my_checkbox_widget{
    Point parent_pos,
    size_t length,
    std::string text,
    bool small
};
```

For example, let's say you want a checkbox called `my_checkbox`. You will need to add this to `apps/ui_newapp.hpp`:
```
Checkbox my_checkbox(
    {10, 20},           // Coordinates are: int:x, int:y
    4,                  // Length
    "my_checkbox_text", // Title
    false               // Checkbox Size: true == small(16X16px), false == regular(24X24px) 
);
```

In `apps/ui_newapp.cpp` you'll need to add the `my_checkbox` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_checkbox,
    });

}
```

Functions within `apps/ui_newapp.cpp` are able to lookup the value of `my_checkbox` with Checkbox's `value()` function:
```
if(my_checkbox.value()) {
    do_a();                // If checkbox is selected (green check mark)
} else {
    do_b();                // If checkbox is NOT selected (red X)
}
```

You can also set the value for `my_checkbox` with the `set_value(const bool value)` function:
```
my_checkbox.set_value(true);  // Checkbox selected (green check mark)
my_checkbox.set_value(false); // Checkbox deselected (red X)
``` 

If you want your checkbox to automatically perform an action when toggled you can add this [Lambda](https://www.geeksforgeeks.org/lambda-expression-in-c/) to `apps/ui_newapp.cpp`:  
```
NewAppView::NewAppView(NavigationView &nav) {

    // Add widget pointers
    add_children({
        &my_checkbox,
    });

    // When checkbox is toggled do...
    my_checkbox.on_select = [this](Checkbox&, bool v) {
        if(v){
            do_a();                                      // If checkbox is selected (green check mark) 
        } else {
            do_b();                                      // If checkbox is NOT selected (red X)  
        }
    };

}
```







#### Image

#### OptionsField

OptionsField is a widget that allows you to create a field, in which you can change its value with the wheel on your portapack. Here you can find it's declaration and prototype:
```
 OptionsField my_OptionsField_widget{
   Point parent_pos, 
   int length, 
   options_t options
};
```
parent_pos is an array of two integer which tells where the top left corner of the widget should be positioned. The length is an integer which tells how many options you have into your options parameter. The options_t field is an array of options in which your portapack can choose to display. 
For example, let's say you want an optionsFild called `my_optionsField`, with 3 options, positioned at 10 from top and 10 from left:
```
OptionsField my_optionsField{
    {10,10}, 
    3, 
    {
      {"option1",0},  
      {"option2",1},
      {"option3",2}
    }
};
```
Note that the number following the "option_x" string value, should be the value that you could retrieve from the optionField with the function `my_optionsField.selected_index_value();`

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
    {10, 10},          // Coordinates are: int:x, int:y
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

#### Waveform

#### VuMeter

## Access radio hardware

### TX

### RX

## Dialogs

# Wrap up