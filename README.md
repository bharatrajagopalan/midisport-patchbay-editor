# midisport-patchbay-editor
## Introduction and Disclaimer
This is a Sysex generator to update Midisport 8x8 patches - first let's get the standard disclaimer out of the way

> If you choose to download and use this tool, then you are agreeing that you will use this at your own risk. The Author disclaims all responsibility and all liability (including liability for negligence) for all expenses, losses, damages and costs you might incur as a result of the use of the software provided

The sysex generated by this tool has been tested with my Midisport 8x8 device; It was built using the gudiance from [here](https://alsa.opensrc.org/USBMidiDevices#Midisport_8x8). I do not know if this works with other Midisport devices other than the 8x8.

## Howto
The steps to generate, load and check patch values on the Midisport 8x8 are as follows.

1. Open the `GenerateMidisportPatchSysex.ods`  file in Libreoffice Calc to configure your routing for a patch and generate the syx file containing sysex which needs to be sent to the Midisport. You can generate individual syx files for patch 1 to 8 with your desired configuration for each patch.
2. In order to send sysex to the midisport, you will first need to plugin the Midisport via USB. In order to get the Midisport working on the Mac M1 via USB, I used this [driver](https://github.com/leighsmith/midisport-macos)
3. Once you have this working via USB, you will need an application that can play sysex to a specified device/port as well as somehting that can monitor responses. I used Sysex Librarian and Midi Monitor for this; You will need to send the sysex to the `SMPTE Port` of the Midisport (and not port 1 to 8) for this to take effect.
4. You can confirm if the patch has been correctly loaded by playing the corresponding `retrieve_patch` syx file (there is one file for each patch 1-8 of the midisport) in the repository and check the response ; it should match the sysex already present in the corresponding `patch` syx file previously played. Or of course you can simply test directly on your midisport

## Background
I created this as the original patchbay editor provided by m-audio only runs on Windows XP/2000, I am using a Mac M1 and needed a way to setup my Midisport 8x8 as a midi patchbay in stand alone mode on my mac. Libreoffice calc is free and available across Windows/Linux/Mac so figured this was a good option to build a patchbay editor using spreadsheet and macros.
 
I am using a Midisport 8x8 with my Presonus Quantum 2626 which has only 1 midi input and output ; the patch i use is contained in `patch1.syx`, where i essentially merge inputs 2 to 8 on them midisport to output 1 which is then sent to the input of my presonus and take the output of the presonus and pass it into input 1 of the midisport which then routes to outputs 2 to 8.

I can now use my Midisport 8x8 as a bus to route different instruments inputs and outputs into the Presonus Midi ports rather than connecting the midipsort via USB (and consequently saving a USB port, with potentially lower latency than using Midi on USB).

I am running my Presonus at 96 khz/128 frames with 0.7 sec latency. Using the midi ports on my midisport routed to the presonus midi ports appears to give me almost instantaneous response (running an Xstation 25 with local control off, where when i press a key, it first sends a midi message to my DAW which then routes the midi message back to play the note on the X station - I hear no difference between playing it directly with local control on)

Please note that depending on which audio interface you are using and the latency on  the audio interface, your experience may be different - audio latency will be the bigger factor here than midi latency and hence in some use cases, you may actually get a better experience by running your midi interface as a seperate USB to the audio interface. The setup shown above is based on what works for me.


