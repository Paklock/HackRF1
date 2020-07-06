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

## Dialogs

# Wrap up