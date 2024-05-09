## vGuitar - Virtual Guitar Rig I use in Live Performances


[**Home**](readme.md) --
**vGuitar** --
[**Artisan**](Artisan.md)

The vGuitar rig is a
[Foot Pedal](https://github.com/phorton1/Arduino-TE3) with a
[USB Audio and Midi](https://github.com/phorton1/Arduino-TE3_audio)
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
*teensyExpresssion3* repo, and apart from this document,
is the **main repository** in the system.  It contains the
code that runs on a *teensy 4.1* and the bulk of the documentation
of the device, along with all of the **3D printing** info and
materials, as well as (most or) all of the **PCB**
(printed circuit board) info and materials.
- [**TE3_audio**](https://github.com/phorton1/Arduino-TE3_audio)
contains the code for the **USB Audio and Midi** device that
runs on *teensy 4.0*. It *may or may not* contain a separated
*PCB* for that portion of the device.
- The [**circle-Looper**](https://github.com/phorton1/circle-prh-apps-Looper)
repo contains the source code for the *Looper application* that runs
on a Raspberry Pi.

**\[A diagram would be nice here]**


Here it is in a nutshell:

- (1) The input (analog) guitar signal goes into a 1/4 jack that is
  (directly or indirectly) connected to a **codec** that converts
  it into digital data.
- (2) The **TE3_audio** device receives the digital data for the
  guitar sound over the **I2S protocol** from the codec.
- (3) The TE3_audio device is also a **USB MIDI Host** that simultaneously
  receives **MIDI peformance data** (note on, note off, and so on) from the
  **FTP** synthesizer pickup.
- (4) The TE3_audio device sends the digital guitar signal
  and MIDI performance data to an **iPad** (or other computer) via USB.
- (5) The iPad receives the USB audio data and adds **guitar effects**
  to it. It simultaneously *plays* a **synthesizer** based on the
  MIDI performance data and also adds that sound to the data stream.
- (6) The iPad returns the combined audio data stream back to the
  TE3_audio device over USB.
- (7) The TE3_audio device receives the audio data from the iPad
  over USB and forwards it to the rPi **Looper** via the I2S protocol.
- (8) The Looper recieves the I2S stream, records data from it and/or
  mixes looping sounds back into it and returns a possibly modified
  I2S stream back to the TE3_audio device.
- (9) The TE3_audio device receives the I2S stream from the Looper
  and sends it to the codec via I2S.  Note that there are two
  separate simultaneous I2S streams running.
- (10) The codec converts the digital audio into an analog output
  signal which is sent out via a 1/8" jack or a pair of RCA
  plugs which is connected to an **external amplifier** (PA) and
  the sound becomes audible.

What about the foot pedal?

The **foot pedal** is essentially a *MIDI controller*. Pressing
the buttons, turning the knobs, or using the expression pedals
generate **MIDI messages**.  The simple explanation is that these
MIDI messaages are sent to the TE3_audio device over a **Serial Port**
where they are combined and sent to the iPad.

In reality **all three devices**, the TE3 (teensy 4.1 foot pedal),
TE3_audio device (teensy 4.0 USB Midi and Audio device with MIDI Host),
and the Looper (rPi) are all both **senders and receivers** of MIDI
messages over Serial ports.  The TE3_audio device (which *IS* the
USB Midi device and *HAS* the Midi Host) acts as the **MIDI router**
recieving  MIDI messages from the Host, TE3, and Looper, and
(acting on them or) forwarding them appropriately to the other
devices including the not only the TE3 and Looper, but also the
iPad and Host port.

**Its complicated!**

Basically it comes down to the fact that the TE3 (Pedal) and
Looper (rPi) are connected to the TE3_audio device by (separate)
bi-directional Serial ports, and that the TE3_audio device *"knows"*
how (can be configured) to route MIDI messages appropriately.

For example, say that a TE3 (pedal) button is pressed to start a
Looper track recording.

- A Serial MIDI message is sent from the TE3 (Pedal) to the TE3_audio
  device, which knows to forward it to the Looper device, which starts
  recording the track.
- In response, the Looper sends the TE3_audio a Serial MIDI message
  saying it has started recording a track.
- The TE3_audio knows to to send the "track recording" MIDI message
  back to the TE3 (pedal).
- The TE3 (pedal) receives the "track recording" message and
  turns the LED for that button **red** indicating that the track
  is recording.

Another illuminating example might be the expression pedals.
In my default configuration of the TE3 (pedal), one expression pedal
controls the Guitar volume and another controls the Loop volume.
When either expression pedal is moved it sends a (series of)
Serial MIDI messages to the TE3_audio.  The TE3 audio *knows*
to forward the Loop pedal MIDI messages to the Looper, but to
send the Guitar volume pedal messages to the iPad over USB.


Now, couple ALL OF THIS with the fact that the TE3 (Pedal) is
designed to be COMPLETELY GENERIZABLE and PROGRAMMABLE by the
end user, and you end up with a very complicated system indeed.

- **Configuration of the T3_audio device MIDI routing is not trivial**
- With the MIDI routing now separate from the TE3 device, it's going
  to need a sophisticated protocol that somehow gets added to the
  rig configuration language.


**personal note** -  **sheesh**.  If only I had infinite processing
power. Decoupling the MIDI routing from the TE3 UI may not be the
best way to go.  There is already significant effort in TE2 for
user configuration of the MIDI routing. **Perhaps** the TE3 should
be the main MIDI router due to it having a UI and configuration
language.  **However** the FTP and things like **Tuning** and
**Sensitivity** settings get really complicated with the de-coupling.
Some serious thought needs to go into this.  I'm done writing
this document for today.




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
-  The **3D printing stuff** shall be provided as complete
  **Fusion 360** designs as well as **STL** files that
  are ready to slice and print.
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


### Printed Circuit Boards

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


### Raspberry Pi (kernel.img)

The *Looper* is a program running on a Raspberry Pi under
the *circle* bare metal development environment.  With
the ongoing evolution of the rPi (upto version 5 now),
it is not certain which rPi will be indicated for the
final assembly.

The Looper was originally implemented on an **rPi Zero**
and then moved to an **rPi 3B+** for it's *multi-core*
capabilities to run the audio system and UI on separate
cores.

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
pre-compiled kernels for a variety of different rPis.

So, at this time, as of this writing, this requirement
is not fully met.  I **am** publishing a **kernel7.img**
and supporting files that can be used with a **rPi 3B+**
and *I believe* that same image will be usable with the
**rPi Zero 2W**.





## Please Also See

- The original [**teensyExpression**](https://github.com/phorton1/Arduino-teensyExpression)
- An intermediate [teensyExpression2](https://github.com/phorton1/Arduino-teensyExpression2)
  that was recently made public, even though the organization and documentation is a mess
- My fork of the [**circle**](https://github.com/phorton1/circle) bare metal **Raspberry Pi**
  system
- My [**additions**](https://github.com/phorton1/circle-prh) to the circle bare metal
  rPi system.

[... Back](readme.md) to Overview of My Github Repos
