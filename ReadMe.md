**Notice:** This repo is a clone of the one on [Dominic Radermacher's website](https://mockmoon-cybernetics.ch/computer/p-touch2430pc/), and he is the author. It is available here (https://github.com/clarkewd/ptouch-print/), with his permission, to help increase visibility of the project and to encourage collaboration and further development.


# ptouch

ptouch is a command line tool to print labels on Brother P-Touch
printers on Linux.

There is no need to install the printer via CUPS, the printer is accessed
directly via libusb.

The tool was written for and tested with the `PT-2430PC`, but it should also
work with the `PT-1230PC` (untested so far). Maybe others work too (please report USB VID and PID so I can include support for further models, too).

**Models in `libptouch.c` include:**

- PT-2420PC
- PT-1230PC
- PT-2430PC
- PT-2730
- PT-2730
- PT-P700 ( see note below about mode switch )
- PT-D450

**Further info can be found at:**
https://mockmoon-cybernetics.ch/computer/p-touch2430pc/

## compile

    sudo apt update
    sudo apt install -y autopoint autoconf libgd-dev libusb-1.0-0-dev
    ./autogen.sh
    ./configure --prefix=/usr
    make

## use

first turn ON the P-Touch device
, then print examples:

    sudo ./ptouch-print --text "P-touch 2730"
    sudo ./ptouch-print --image brother.png
    sudo ./ptouch-print --image 12mm_GIMP.png
    sudo ./ptouch-print --image 24mm_tux.png

![tux for 24mm tape](24mm_tux.png)

### max. height for current tape

to get maximum height for the current tape inside the P-touch
, run a print with very high height
, e.g. for 24mm tape on P-touch 2730:

    sudo ./ptouch-print --image PIXmm_GIMP.png

    PT-2730 found on USB bus 3, device 52
    image is too large (16px x 512px)
    maximum printing width for this tape is 128px

For example on P-touch 2730,
tape of 12mm has 76px
and for tape 24mm, it's 128px.

## PT-P700

- As the PT-P700 does not have a toggle switch for the printer mode, you may need to switch the mode first
- If you plug in the PT-P700 and the green light above the PLite button is on, the printer won't be recognized by `ptouch`. You must hold down the PLite button for ~ 2 seconds and the light will turn off and the system will find the device again.
- This step allowed it to be detected as `vid 0x04F9 pid 0x2061` insetad of `vid 0x04F9 pid 0x2064`
- This allows it to be found, (eg: `./ptouch-print --info`) and also puts it into a mode that it can be interfaced with


# A Note from Dominic's website

"Dear visitor, currently I have absolutely no time for improvements on this project (my free time currently is about one or two hours PER MONTH)..."

# Collaboration

You may still, of course, contact Dominic directly if you'd like. But I think GitHub is easier for collaboration, and he has given me permission to host a clone of his repo here, passing code contributions back to him.

