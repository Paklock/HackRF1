
## About

Now we’re going to dive into something a little more complex and bring radios into the mix. If you’re not familiar with the LPC43xx please read up on the [Firmware Architecture](https://github.com/eried/portapack-mayhem/wiki/Firmware-Architecture) before continuing. 

So far we’ve only been dealing with application code with is ran on the M0 of the LPC43xx. Now we’re going to start working with the baseband side of the codebase which is ran on the LPC43xx’s M4 processor. Both of these processors use 8k worth of shared memory from `0x1008_8000` to `0x1008_a000` to pass messages to and from each other. The M0 controls **ALL** operations of the portapack while the M4 mostly handles the DSP and radio functions.  

Complexitys aside with the two processors, accessing the HackRF's radio hardware has been simplified with helper classes such as the [`TransmitterModel`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/transmitter_model.cpp) and [`ReceiverModel`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/receiver_model.cpp). Both of these classes interface with the M4 baseband processes and gives us a more piratical way to control the radio.

Other classes and structs such as [`baseband api`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/baseband_api.cpp) and [`SharedMemory`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/portapack_shared_memory.hpp) also bridge the gap between the M0 and M4. Even though the M4's primary responsability is to handle DSP with the radio hardware the M0 can still be used to decode data. For example, classes found in `firmware/application/protocols/` like [`encoders`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/protocols/encoders.cpp) still send data too and from the two processors but also encodes and decodes messages at the higher level protocols. 


## TX

The code bellow is an example OOK TX application using [`TransmitterModel`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/transmitter_model.cpp), [`encoders`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/protocols/encoders.cpp), and [`baseband`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/baseband_api.cpp). 

#### ui_newapp.hpp

    ....

    // Include TransmitterModel
    #include "transmitter_model.hpp"

    namespace ui
    {
        class NewAppView : public View                                                   // App class declaration
        {
        public:

            ....

        private:

            ....

            void start_tx(std::string& message);                                         // Function declarations
            void stop_tx();
            void on_tx_progress(const uint32_t progress, const bool done); 

            MessageHandlerRegistration message_handler_tx_progress {                     // MessageHandlerRegistration class which relays 
                Message::ID::TXProgress,                                                 // Message::ID::TXProgress messages to your app 
                [this](const Message* const p) {                                         // code from baseband. The Ternary Operator passes   
                    const auto message = *reinterpret_cast<const TXProgressMessage*>(p); // an uint32_t progressvalue and a bool stating if  
                    this->on_tx_progress(message.progress, message.done);                // TX progress has be complete.
		}};

        };
    } 

#### ui_newapp.cpp

    ....

    // Include encoders and baseband
    #include "encoders.hpp"
    #include "baseband_api.hpp"

    using namespace portapack;

    namespace ui
    {
         void NewAppView::start_tx(std::string& message)              // Message input as "101101"
         {
             size_t bitstream_length = make_bitstream(message);       // Function from encoders.hpp. Encodes then 
                                                                      // sets message to TX data pointer via... 	
                                                                      // uint8_t * bitstream = shared_memory.bb_data.data; 
                                                                      // on line 34 of encoders.cpp and returns length. 
	
             transmitter_model.set_tuning_frequency(433920000);       // Center frequency in hz
             transmitter_model.set_sampling_rate(OOK_SAMPLERATE);     // (2280000) Value from encoders.hpp
             transmitter_model.set_rf_amp(true);                      // RF amp on
             transmitter_model.set_baseband_bandwidth(1750000);       // Bandwidth
             transmitter_model.enable();                              // Radio enable
	
             baseband::set_ook_data(                                  // ASK/OOK TX function
                 bitstream_length,                                    // Length of message
                 OOK_SAMPLERATE / 1766,                               // Symble period (560us), Sample Rate / Baud 
                 4,                                                   // Repeat transmissions
                 100                                                  // Pause symbles
             );
        }

        void NewAppView::stop_tx()                                    // Stop TX function
        {
            transmitter_model.disable();                              // Disable transmitter_model

            // Add UI logic to let the user know the TX has stoped 
        } 
 
        NewAppView::NewAppView(NavigationView &nav)                   // Application Main
        {
            baseband::run_image(portapack::spi_flash::image_tag_ook); // M4 processor is being told to run proc_ook.cpp
                                                                      // found in the firmware/baseband/ folder. M4 is 
                                                                      // then reset after this command.
             // UI widget logic and calls to
             // start_tx() goes here.
             
        }

        void NewAppView::on_tx_progress(const uint32_t progress, const bool done)  // Function logic for when the message handler       
        {                                                                          // sends a TXProgressMessage.
             if(done) {
                 stop_tx();
             } else {
                 // UI logic, update ProgressBar with progress var
             }
        }
    }

## RX

Building from the example code for TX lets talk about how the baseband processes are started on the M4. The application code on the M0 uses the baseband api `baseband::run_image` to tell the M4 to run a process. The baseband images are defined in [`spi_image.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/spi_image.hpp) as the struct `image_tag_t`. These structs and have a 4 char array tag being used as an ID. Below is an example `image_tag_t` for AFSK RX.

```
constexpr image_tag_t image_tag_afsk_rx { 'P', 'A', 'F', 'R' };
```

Under  [`firmware/baseband/CMakeLists.txt`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/CMakeLists.txt) the following code snippet shows how the baseband processes are linked to the images defined in [`spi_image.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/spi_image.hpp).

```
### AFSK RX
set(MODE_CPPSRC
    proc_afskrx.cpp
)
DeclareTargets(PAFR afskrx)
``` 

In `firmware/baseband`, process or "proc" code for the M4 processor like [`proc_afskrx.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/proc_afskrx.cpp) for example can be found here. These proc classes are ran by [`BasebandThread`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/baseband_thread.cpp). All proc classes inherent [`BasebandProcessor`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/baseband_processor.hpp) and must include the parent functions. 

#### baseband_processor.hpp
```
#ifndef __BASEBAND_PROCESSOR_H__
#define __BASEBAND_PROCESSOR_H__

#include "dsp_types.hpp"
#include "channel_stats_collector.hpp"
#include "message.hpp"

class BasebandProcessor {
public:
    virtual ~BasebandProcessor() = default;               // Constructor 

    virtual void execute(const buffer_c8_t& buffer) = 0;  // DSP code for TX/RX, shared_memory messages can be sent to
                                                          // M0 application code from this function.

    virtual void on_message(const Message* const) { };    // Shared_memory messages from M0 application code

protected:
    void feed_channel_stats(const buffer_c16_t& channel);

private:
    ChannelStatsCollector channel_stats { };
};
```

Now that we have a better idea how M0 can drive the M4 lets talk about the Messaging between the two processors. The [`Message`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/message.hpp) class found under `firmware/common/`. Common code is used both by application (M0) and baseband (M4). Messages are handled by EventDispatcher found in [`event_m4.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/event_m4.cpp) for the baseband code and [`event_m0.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/event_m0.cpp) for the application code. Within the same file [`firmware/commen/message.hpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/message.hpp) you can find definitions for spacific message classes and ID. Bellow is an example message class for AFSK RX. 


#### message.hpp
```
class Message {
public:
    static constexpr size_t MAX_SIZE = 512;

    enum class ID : uint32_t {
        /* Assign consecutive IDs. IDs are used to index array. */

        ....

        AFSKRxConfigure = 22,
	AFSKData = 47,

        ....

    };
}

    ....

// Application Messages (M0) -> Baseband (M4)
class AFSKRxConfigureMessage : public Message {
    public:
        constexpr AFSKRxConfigureMessage(
            const uint32_t baudrate,
            const uint32_t word_length,
            const uint32_t trigger_value,
            const bool trigger_word
        ) : Message { ID::AFSKRxConfigure },
            baudrate(baudrate),
            word_length(word_length),
            trigger_value(trigger_value),
            trigger_word(trigger_word)
        {
        }
	
        const uint32_t baudrate;
        const uint32_t word_length;
        const uint32_t trigger_value;
        const bool trigger_word;
    };


// Baseband Messages (M4) -> Application (M0)
class AFSKDataMessage : public Message {
    public:
        constexpr AFSKDataMessage(
            const bool is_data,
            const uint32_t value
        ) : Message { ID::AFSKData },
            is_data { is_data },
            value { value }
        {
        }
	
        bool is_data;
        uint32_t value;
};
```   

[`SharedMemory`](https://github.com/eried/portapack-mayhem/blob/next/firmware/common/portapack_shared_memory.hpp) found in `firmware/common/` is used to pass data inbetween the application code (M0) to the baseband code (M4). Below is an example from [`proc_afskrx.cpp`](https://github.com/eried/portapack-mayhem/blob/next/firmware/baseband/proc_afskrx.cpp) on how data is sent back to the application [`AFSKRxView`](https://github.com/eried/portapack-mayhem/blob/next/firmware/application/apps/ui_afsk_rx.cpp). 

#### proc_afskrx.cpp
```
#include "portapack_shared_memory.hpp"

void AFSKRxProcessor::execute(const buffer_c8_t& buffer) {

    ....                                                 // RX Logic

    shared_memory.application_queue.push(data_message);  // data_message is an AFSKDataMessage object

    ....                                                 // MORE RX Logic

};
```

Continuing to use the same AFSK RX proc code above, below is an example of an RX AFSK application.


#### ui_newapp.hpp

    ....

    // Include ReceiverModel
    #include "receiver_model.hpp"

    namespace ui
    {
        class NewAppView : public View                                            // App class declaration
        {
        public:

            ....

        private:

            ....

            void start_rx();                                                      // Function declarations
            void stop_rx();
            void on_data();                   
            MessageHandlerRegistration message_handler_packet {                   // MessageHandlerRegistration class which relays
                Message::ID::AFSKData,                                            // relays messages to your app code from baseband.
                [this](Message* const p) {                                        // Every time you get a AFSKData message the
                    const auto message = static_cast<const AFSKDataMessage*>(p);  // on_data() function will be triggered. 
                    this->on_data(message->value, message->is_data);
            }};

        };
    } 

#### ui_newapp.cpp

    ....

    #include "modems.hpp"
    #include "audio.hpp"
    #include "string_format.hpp"
    #include "baseband_api.hpp"
    #include "portapack_persistent_memory.hpp"

    using namespace portapack;
    using namespace modems;

    namespace ui
    {
        void NewAppView::start_rx()                                                // Start RX function
        {
            auto def_bell202 = &modem_defs[0];                                     // Bell202 baud rate
            persistent_memory::set_modem_baudrate(def_bell202->baudrate);          // Set RX modem to 1200 baud

            serial_format_t serial_format;                                         // Declare packet format for message
            serial_format.data_bits = 7;                                           // Bit length
            serial_format.parity = EVEN;                                           // Even or odd parity bit
            serial_format.stop_bits = 1;                                           // Stop bit
            serial_format.bit_order = LSB_FIRST;                                   // LSB or MSB first
            persistent_memory::set_serial_format(serial_format);                   // Set RX packet format

            baseband::set_afsk(persistent_memory::modem_baudrate(), 8, 0, false);  // Baud rate, word length, trigger value, trigger word

            receiver_model.set_tuning_frequency(433920000);                        // Center frequency in hz
            receiver_model.set_sampling_rate(3072000);                             // Sampling rate
            receiver_model.set_baseband_bandwidth(1750000);                        // Bandwidth
            receiver_model.set_modulation(ReceiverModel::Mode::NarrowbandFMAudio); // Modulation
            receiver_model.enable();                                               // Start RX

            audio::set_rate(audio::Rate::Hz_24000);                                // Play RX audio to headphone jack
            audio::output::start();
        }

        void NewAppView::stop_rx()                                                 // Stop RX function
        {
            audio::output::stop();                                                 // Stop Audio
            receiver_model.disable();                                              // Stop RX
            baseband::shutdown();                                                  // Stop M4 proc process
        } 
 
        NewAppView::NewAppView(NavigationView &nav)                       // Application Main
        {
            baseband::run_image(portapack::spi_flash::image_tag_afsk_rx); // M4 processor is being told to run proc_afskrx.cpp
                                                                          // found in the firmware/baseband/ folder. M4 is 
                                                                          // then reset after this command.
             // UI widget logic and calls to start_rx()
             // and stop_rx() goes here.
             
        }

        void NewAppView::on_data(uint32_t value, bool is_data)            // Function logic for when the message handler       
        {                                                                 // sends a AFSKData.
             if(is_data) {
                // RX data handling Logic
             }
        }
    }
