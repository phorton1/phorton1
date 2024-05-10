## vGuitar - Virtual Guitar Rig I use in Live Performances

**vGuitar** --
[**Artisan**](Artisan.md)

This is the home page for the overall design of the **vGuitar System**.
This folder contains *design* and *reference* documentation that is
common to the multiple parts of the system.

The vGuitar rig is a
[Foot Pedal](https://github.com/phorton1/Arduino-TE3) with a
[USB Audio and Midi](https://github.com/phorton1/Arduino-TE3_hub)
interface and a built in
[Looper](https://github.com/phorton1/circle-prh-apps-Looper)
that hooks up to an **iPad** which provides Guitar Effects
and a Synthesizer for an
[Fishman Triple Play](https://www.fishman.com/tripleplay/)
(FTP) guitar synthesizer pickup.

**PLEASE NOTE THAT THIS PROJECT IS IN A PROTOTYPE/DEVELOPMENT STAGE**


## Basic Architecture

There are three **MPUs** (computers) in the box, and there
are *github repositories* associated with each of them.

- [**TE3**](https://github.com/phorton1/Arduino-TE3) is the
*teensyExpresssion3* repo, containing the
code that runs on a *teensy 4.1* and the documentation
of that part of the system, along with all of the **3D printing** info and
materials for the Foot Pedal, as well as (most or) all of the **PCB**
(printed circuit board) design info and materials used in the Pedal.
- [**TE3_hub**](https://github.com/phorton1/Arduino-TE3_hub)
contains the code for the **USB Audio and Midi** device that
runs on *teensy 4.0*. It *may or may not* contain separate
detailed documentation and/or *PCB* designs for that portion
of the system.
- The [**circle-Looper**](https://github.com/phorton1/circle-prh-apps-Looper)
repo contains the source code for the *Looper application* that runs
on a Raspberry Pi.

**\[A diagram would be nice here]**


Here it is in a nutshell:

- (1) The input (analog) guitar signal goes into a 1/4 jack that is
  (directly or indirectly) connected to a **codec** that converts
  it into digital data.
- (2) The **TE3_hub** receives the digital data for the
  guitar sound from the codec using the **I2S protocol**
- (3) The TE3_hub is also a **USB MIDI Host** that simultaneously
  receives **MIDI peformance data** (note on, note off, and so on) from the
  **FTP** synthesizer pickup.
- (4) The TE3_hub sends the digital guitar signal and MIDI performance data
  to an **iPad** (or other computer) via USB.
- (5) The iPad receives the USB audio data and adds **guitar effects**
  to it. It simultaneously *plays* a **synthesizer** based on the
  MIDI performance data and also mixes that into the audio data stream.
- (6) The iPad returns the combined audio data stream back to the
  TE3_hub over USB.
- (7) The TE3_hub receives the audio data from the iPad
  over USB and forwards it to the rPi **Looper** via the I2S protocol.
- (8) The Looper recieves the I2S stream, records data from it and/or
  mixes looping sounds back into it and returns a (possibly modified)
  I2S stream back to the TE3_hub.
- (9) The TE3_hub receives the I2S stream from the Looper
  and sends it to the codec via I2S.
- (10) The codec converts the digital audio into an analog output
  signal which is sent out via a 1/8" jack or a pair of RCA
  plugs which is/are connected to an **external amplifier** (PA) and
  the sound becomes audible.

Note that there are two simultaneous separate bi-directional I2S streams
running. One I2S IO stream exists between the codec and the TE3_hub and
the second exists between the TE3_hub and the rPi (Looper).


## What about the foot pedal?

The **foot pedal** is essentially a *MIDI controller*. Pressing
the buttons, turning the knobs, or using the expression pedals
generate **MIDI messages**.  The simple explanation is that these
MIDI messaages are sent to the TE3_hub over a **Serial Port**
where they are combined and sent to the iPad.

In reality **all three devices**, the TE3 (teensy 4.1 foot pedal),
TE3_hub (teensy 4.0 USB Midi and Audio device with MIDI Host),
and the Looper (rPi) are all both **senders and receivers** of MIDI
messages over Serial ports.  The TE3_hub (which *IS* the
USB Midi device and *HAS* the Midi Host) acts as the **MIDI router**
recieving  MIDI messages from the Host, TE3, and Looper, and
(acting on them or) forwarding them appropriately to the other
devices including the the TE3, Looper, iPad, and Host port

**Its complicated!**

Basically (at this stage of the design) it comes down to the fact
that the TE3 (Pedal) and Looper (rPi) are connected to the TE3_hub by
separate bi-directional Serial ports, and that the TE3_hub  *"knows"*
how, and/or can be configured, to route MIDI messages appropriately.

For example, say that a TE3 (pedal) button is pressed to start a
Looper (rPi) track recording.

- A Serial "begin recording" MIDI message is sent from the TE3
  (Pedal) to the TE3_hub, which knows to forward it to the Looper device,
  which starts recording the track.
- In response, the Looper sends the TE3_hub a Serial "recording started"
  MIDI message saying it has started recording a track.
- The TE3_hub knows to to forward the Serial "recording started" MIDI
  message back to the TE3 (pedal).
- The TE3 (pedal) receives the "recording started" message and
  turns the LED for that button **red** indicating that the track
  is recording.

Another illuminating example might be the expression pedals.
In my default configuration of the TE3 (pedal), one expression pedal
controls the Guitar volume and another controls the Loop volume.
When either expression pedal is moved it sends a series of
Serial MIDI messages to the TE3_hub.  The TE3 audio *knows*
to forward the Loop pedal MIDI messages to the Looper, but to
send the Guitar volume pedal messages to the iPad over USB.


**Configuration of the TE3_hub MIDI routing is not trivial**
With the MIDI routing now separate from the TE3 device,
the TE3_hub is likely to need it's own protocol for
configuration and state messsages.



## Requirements

Not all of the requirements have been met, nor is it ready for
**makers** at this time.  I will update this document if, and
when it gets there.

There are many dependencies and other repositories involved
in the entire system.  It is beyond the scope of this overview
document to detail them.  Please see the above and other linked
repos for more information.


**External Connections**

- a single USBC power in plug that powers everything
- a single USBC cable to the iPad
- MIDI host port for the FTP
- Guitar-In 1/4" jack
- 1/8" jack or RCA-pair that connects to an external amplifier (PA)
- Four 1/4" jacks for Expression Pedals
- Micro USB port to the teensy 4.1

**Built-in UI and Controls**

- 25 buttons with addressable LEDs
- Two 3.5" ILI9488 TFT touch screens
- Four Rotary Controllers with built in buttons
- A variety of indicator LEDs and buttons, to be determined

**For Makers**

- The device shall be buildable by anyone with a decent
  **3D Printer** and experience using the **Arduino IDE**
  development environment.
- The **documentation** shall be *robust*, allowing
  for a good understanding of the functionality of all
  aspects of all systems involved.
- The **3D printing imformation** shall be provided as
  complete **Fusion 360** designs as well as **STL** files
  that are ready to slice and print.
- The **PCBs** (printed circuit boards) shall be provided
  as complete **kicad** schematics and **gerber** files that
  can be sent to any *PCB house* for fabrication and/or
  assembly (see notes below).
- The (Looper) code that runs on the Raspberry Pi shall be
  provided as a ready-to-go, completely compiled and linked
  **kernel.img** and *support files* that can just be *copied*
  to an SD card for installation onto a into the rPi (see
  notes below).
- The **cost** of the default configuration of the system
  shall be kept to a minimum. Ideally this device can be
  built for between $100 and $200.


## Restrictions

Note that I am explicitly NOT including any actual MIDI ports,
nor even a serial MIDI jack on the box in this design.

Synthesizer:

- The Synthesizer used by this system (to play the midi notes sent
  from the FTP) shall be a program running on the device connected
  via the USB cable (i.e. sampleTank running on an iPad).
- The Synthesizer program shall respond to MIDI NOTE_ON messages
  with Velocity and MIDI NOTE_OFF messages from the USB port
  for performance.
- The Synthesizer program shall respond to MIDI CC messages
  for controlling overall or per-channel volume.
  
Guitar Effects:

- The Guitar effects shall be a program running on a device
  connected via the USB cable (i.e. toneStack running on an iPad)
- The Guitar effects program shall respond to MIDI CC messages
  for controlling the on/off state of various effects and/or
  parameters of those effects (i.e. the guitar volume level,
  and the wah-wah expresion pedal position).

Implicit Limitations:

- Using channel and CC numbers within USB MIDI messages, and
  not relying on Midi "cable" or "port" numbers shall be sufficient
  to disambiguate any and all MIDI messages sent to the iPad.
- This is the case in current practice.  It *may* be possible
  with the **midiFire** iPad app to route specific MIDI ports
  to specific apps but otherwise I believe the iPad just
  gloms any and all MIDI messages from any and all  ports into
  a single MIDI stream.
- Fortunately, at this time, sampleTank and toneStack use disjoint
  sets of MIDI channels and CC numbers for control, and the
  only app responding to NOTE_ON and NOTE_OFF messages is
  sampleTank.



## Notes about Printed Circuit Boards (PCBs)

Providing the information for the creation of PCBs by makers
is a complicated issue, and the cost of creating them can
vary greatly depending on how the PCBs are made and assembled.
and the abilitiies of the person(s) making them.

I typically **mill** my own single sided PCBs, using **through hole**
technology wherever possible, particlarly in the *prototype*
stages of development and for small PCBs that are typically
used as **connectors** (like my *standard* ILI SPI LCD/TFT connector).
These single sided PCB layouts do not lend themselves to
publication for makers and/or fabrication and/or assembly
by outside **PCB houses**.

With the use of SMT devices and multi-layered PCBs from
*PCB houses*, and the difficulty of assembly (soldering)
them, the cost of a finished PCB can vary dramatically.

- Ordering a single PCB from a PCB House usually costs
  the same as ordering 4 of them.  They typically do their
  price breaks on 1-5 units, 6-10 units, and so on.
- A very small circuit board might from a PCB house
  might cost $17, regardless of the fact that you might
  need only one of them.
- I can probably mill that same small circuit board immediatly,
  with no delay for production or shipping, for under $1.
- If it contains only a few connectors and perhaps resistors,
  I can assemble that milled board for under another $1, because
  I keep a stock of connectors and resistors on-hand.
- If was from a PCB house and used SMT components, and
  the maker did not have the ability to solder SMT devices,
  and/or a stock of components,
  the cost of this single small PCB could skyrocket up
  to $70 or more, be complicated to order, and take weeks
  to get if the maker were to have the components sourced
  and assembled by the PCB house.

Because of these factors, the requirement that circuit
boards be provided as ready-to-go gerber files is **soft**,
particularly during my (current) prototype and development
phase.  As a result the **kicad PCBs** in the associated
repositories *may or may not* be *ready* for final
publication.

This is one of the *gotchas* of publishing in-progress
development efforts.


### Notes about pre-compiled Raspberry Pi kernel.img

The *Looper* **kernel.img** is a program running on a
Raspberry Pi under the *circle* bare metal development
environment.  With the ongoing evolution of the rPi
(upto version 5 now), it is not certain which rPi(s)
will be used in the final assembly.

The Looper was originally implemented on an **rPi Zero**
and then moved to an **rPi 3B+** for it's *multi-core*
capabilities in order to run the audio system and UI
on separate cores.

At the time of this writing the **rPI 4B** and its
variants are options, the **rPI 5** is considered
*too new* for production usage, and I will be evaluating
the **rPi Zero 2W**, which contains the same multi-core
MPU as the rPi 3B+.

Installing the development environment and building the
circle rPI program is complicated, and it is my goal to
provide the Looper as a pre-compiled, ready to install
**kernel.img** (and supporting files) that can merely
be copied to an SDCard and stuck in a rPi.

As such, for makers, the project is *not ready for
primetime* as of this writing, as I have not settled
on which rPI I will publish for.  I definitely **do
not** want to get into the business of trying to publish
pre-compiled kernels for all possible rPis.

So, at this time, as of this writing, this requirement
is not fully met.  I **am** publishing a **kernel7.img**
and supporting files that can be used with a **rPi 3B+**
and *I believe* that same image will be usable with the
**rPi Zero 2W**.



## Major Changes in this iteration

This is a major reworking of the entire system. Compared to
the previous iteration, the following major changes are
occuring in this iteration:

[**TE3**](https://github.com/phorton1/Arduino-TE3),
running on a **teensy 4.1** is replacing the previous
[teensyPiLooper](https://github.com/phorton1/Arduino-teensyPiLooper)
which ran on a *teensy 3.2* and all of the previous
[teensyExpression](https://github.com/phorton1/Arduino-teensyExpression)
[/2](https://github.com/phorton1/Arduino-teensyExpression2)
functions which ran on a *teensy 3.6*.

[**TE3_hub**](https://github.com/phorton1/Arduino-TE3_hub),
running on a **teensy 4.1**, with a *codec*, initially
the SGTL500 (teensy AudioShield), is replacing most of the
previous Looper guts including the *iRig2HD* USB Audio interface,
the Audio Injector *Octo sound card* and the 6 port *USB Hub* that
tied it all together.

The *circle*
[**Looper**](https://github.com/phorton1/circle-prh-apps-Looper)
program remains virtually unchanged in this iteration,
with the exception that instead of using the (6 in and 8 out)
CS42448 based *Octo sound card* it will use the **teensyQuad**
device to interface to the *TE3_hub** via I2S.

**This is a huge change** and will eliminate a ton of hardware
cables, as well as the whole separate **Looper Box**, combining
everything into a single foot pedal.   The goal is that the
single foot pedal will have the minimum number of connectors
to setup in a live setting while still retaining most or all
of the functionality of the previous vGuitar rig.


up   [... phorton1](readme.md) to Overview of My Github Repos
next [