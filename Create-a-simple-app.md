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
            NewAppGameView(NavigationView &nav);
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

For triggering your new app, you need to add an entry on the main menu. This menu resides on `firmware\application\ui_navigation.cpp`. Check the current entries, and add a new one in a section you think is suitable for your new app. 

## Early test

Remember to add your `apps/ui_newapp.cpp` to `firmware\application\CMakeLists.txt`

In this moment you should be able to compile and test the app in your device. It should appear in the main menu and show an empty app upon entering to it.

# Adding functionality

## Widgets
Widgets are the elements that compose the UI of your custom app. Widgets are defined inside `firmware\common\ui_widget.hpp.txt`, so in order to be able to use them, you must `#include "ui_widget.hpp"` into your app .hpp file.
There are different type of widget. here you will find a list of available widget, with their respecting constructor. For all the methods available, you should go and see the ui_widget.hpp file.

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
#### Buttons

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

#### LiveDateTime

#### BigFrequency

#### ProgressBar

#### Console

#### Checkbox

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
#### Waveform

#### VuMeter

## Access radio hardware

## Dialogs

# Wrap up