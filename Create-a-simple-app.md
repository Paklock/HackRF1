This simple application will explain the basic of widgets and simple navigation. 

We are going to create few simple controls and link the app to the main menu. The idea is to get familiar with the way things work.

# First steps

There is a lot of flexibility, but for now we are going to follow patterns already found on the source code. For example, the name of the files and classes will be inspired by existing code.

## Application code

The following structure is the base of any application. Following the general structure, this files will be created on `\firmware\application\apps\`

### ui_newapp.hpp

    #include "ui.hpp"
    #include "ui_widget.hpp"
    
    namespace ui { }

### ui_newapp.cpp

    #include "ui_newapp.hpp"
    
    using namespace portapack;
    namespace ui { }

## Main class
