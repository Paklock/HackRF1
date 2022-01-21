## About

Widgets are the elements that compose the UI of your custom app. Widgets are defined inside [`firmware\common\ui_widget.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) and widget functions can be found inside [`firmware\common\ui_widget.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.cpp). In order to be able to use them, you must `#include "ui_widget.hpp"` into your app .hpp file.
There are different type of widget. here you will find a list of available widget, with their respecting constructor. For all the methods available, you should go and see the [ui_widget.hpp](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui_widget.hpp) file.

## Attach a Generic Widget to Your Application

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

## Available widgets
There are several different widgets, and more might be added, so you should always go and check whether new widgets have been added or not. Here you will find a list of most basic widgets.

### Text
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
  {10, 10, 100, 24},          // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
  "Hello world!"
);
```
### Button

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

### Labels

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

### LiveDateTime

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
### BigFrequency

BigFrequency is used for displaying a radio frequency. Here you can find it's declaration and prototype:
```
Labels my_bigFrequency_widget{
    Rect parent_rect, 
    rf::Frequency frequency
};
```

For example, let's say you want a label called `my_bigFrequency`. You will need to add this to `apps/ui_newapp.hpp`:
```
Labels my_bigFrequency(
    {10, 10, 28*8, 52}, // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
    0                   // Beginning frequency in hz
);
```

In `apps/ui_newapp.cpp` you'll need to add the `my_bigFrequency` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_bigFrequency,
    });

}
```

To set a frequency you can use the function `set(const rf::Frequency frequency)`:
```
my_bigFrequency.set(433000000); // 433MHz
```

### ProgressBar

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

### Console

Console can be used as large text field where you can output mutable lines of text. Here you can find it's declaration and prototype:
```
Console my_console_widget{
    Rect parent_rect
};
```

For example, let's say you want a label called `my_console`. You will need to add this to `apps/ui_newapp.hpp`:
```
Console my_console {
    { 2*8, 10, 208, 200 },    // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
};
```

In `apps/ui_newapp.cpp` you'll need to add the `my_console` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_console,
    });

}
```

To write to 'my_console' you'll need to use the `write(std::string message)` function:
```
my_console.write("Hello World");
```

For automatic new line, you can also use the `writeln(std::string message)` function if you don't want to add a `\n' at the end of every string:
```
my_console.writeln("Hello World but on a new line!");
``` 

To enable scrolling you can use the `enable_scrolling(bool enable)` function::
```
my_console.enable_scrolling(true);
```

### Checkbox

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
    {10, 20},           // Coordinates are: int:x (px), int:y (px)
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

### Image

Images can be displayed within your app. Here you can find it's declaration and prototype:
```
Image my_Image_widget{
    Rect parent_rect,
    Bitmap* bitmap,
    Color foreground,
    Color background
};
```

Images need to be a Bitmap object before they can be displayed. Bellow is an example of the code needed to create a Bitmap from [`firmware/application/bitmap.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/bitmap.hpp).
```
static constexpr uint8_t bitmap_stripes_data[] = {
	0xFF, 0x03, 0xC0, 
	0xFF, 0x01, 0xE0, 
	0xFF, 0x00, 0xF0, 
	0x7F, 0x00, 0xF8, 
	0x3F, 0x00, 0xFC, 
	0x1F, 0x00, 0xFE, 
	0x0F, 0x00, 0xFF, 
	0x07, 0x80, 0xFF, 
};
static constexpr Bitmap bitmap_stripes {
	{ 24, 8 }, bitmap_stripes_data
};
```

With the Bitmap object created we can now define the image `my_image`. You will need to add this to `apps/ui_newapp.hpp`:
```
Image my_image(
    {10, 10, 24, 8},    // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
    &Bitmap,            // Pointer to your bitmap
    Color::white(),     // Color Foreground
    Color::black()      // Color Background
);
```
**Note:** Colors are defined in [`firmware/common/ui.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui.hpp)


In `apps/ui_newapp.cpp` you'll need to add the `my_image` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_image,
    });

}
```

### OptionsField

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
    {10,10},                   // Coordinates are: int:x (px), int:y (px)
    7,                         // Char length for option title
    {
      {"option1",0},  
      {"option2",1},           // Options {"KEY", int VALUE}
      {"option3",2}
    }
};
```
Note that the number following the "option_x" string value, should be the value that you could retrieve from the optionField with the function `my_optionsField.selected_index_value();`

### NumberField

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

### Waveform

Waveforms are used to display a sign wave from a signal source. **Note:** The X axes represents time while the Y axes represents amplitude. Here you can find it's declaration and prototype:
```
Labels my_waveform_widget{
    Rect parent_rect,
    int16_t * data,
    uint32_t length,
    int32_t offset,
    bool digital,
    Color color
};
```

For example, let's say you want a Waveform called `my_waveform`. You will need to add this to `apps/ui_newapp.hpp`:
```
Waveform my_waveform(
    {0, 5*16, 240, 64},  // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
    waveform_buffer,     // RX data
    128,                 // Length, how many elements in the waveform_buffer array
    0,                   // Offset
    false,               // Digital
    Color::white()       // Sine wave color
);
```
**Note:** Colors are defined in [`firmware/common/ui.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/ui.hpp).


The data being displayed by `my_waveform` needs to be a `int16_t` array. You can declare this variable in `apps/ui_newapp.hpp`:
```
class NewAppView : public View
{
    public:

        ...

    private:
        int16_t waveform_buffer[128];  // Data for Waveform

        ...

};
```


In `apps/ui_newapp.cpp` you'll need to add the `my_waveform` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_waveform,
    });

}
```

If your input data has a variable length you can use the `set_length(const uint32_t new_length)` function to update the Waveform:
```
my_waveform.set_length(9001) // THAT'S OVER 18KB!!
```

### VuMeter

VuMeters are used to visually represent the sound intensity of an audio source. Here you can find it's declaration and prototype:
```
Labels my_vuMeter_widget{
    Rect parent_rect,
    uint32_t LEDs,
    bool show_max
};
```

For example, let's say you want a VuMeter called `my_vuMeter`. You will need to add this to `apps/ui_newapp.hpp`:
```
VuMeter my_vuMeter(
    { 0*8, 1*8, 2*8, 33*8},  // Coordinates are: int:x (px), int:y (px), int:width (px), int:height (px)
    12,                     // LEDs
    true                    // Show max
);
```

In `apps/ui_newapp.cpp` you'll need to add the `my_vuMeter` pointer to add_child() or add_children():
```
NewAppView::NewAppView(NavigationView &nav) {

    // Widget pointers
    add_children({
        &my_vuMeter,
    });

}
```

To set the value for `my_vuMeter` use the `set_value(const uint32_t new_value)` function:
```
my_vuMeter.set_value(123); // Max is 255
```