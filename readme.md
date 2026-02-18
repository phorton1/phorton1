# My Github Repos

**Home** --
[**vGuitar**](vGuitar/vGuitar.md) --
[**Artisan**](Artisan.md)


This page provides a bit of an overview of my repos here on Github.

This page was last updated on **2026-02-18**.
As of this writing I have **86 Public Repos** on Github.

I write a **lot** of code and programs.  Although the code I write is generally
based on my own interests and needs at any given point in time, I generally
try to present them as **Open Source** that others can build and use
and perhaps extend or modify according to their own needs and interests.

The **code** I write is generally in the following program languages
and development environments:

- **C/C++** for embedded processors like Arduino, Teensy, and ESP32's using
  the Arduino IDE 1.8.13
- **C/C++** for machine specific programs and libraries like MS Windows,
  Linux or running in bare metal on a Raspberry Pi using various
  *specific tool chains*, *make systems*, **virtual machines** and so on,
- **Perl** for programs and services that run on established operating
  systems like MS Windows (using ActivePerl 5.12 or Strawberry Perl) and
  Linux (using Raspberry Pi's included Perl)
- **HTML/Javascript** for web pages  that run in a user's browser that are
  served by various programs and systems in these repos.
- **Java** for specific Android Studio apps I write that run on
  Android phones
- **Python/Javascript** for add-ins or extensions to specific
  programs I use like Firefox, Komodo Edit, and Fusion 360
- **Batch/Shell Scripts** in a variety of languages from *Bash*
  (Linux shell script) to *Windows CMD language* (windows Batch files)
  or a host of other "languages" including some invented and used
  within these repositories.

As well as whatever language/application/API I may find that I need in
a project to accomplish a particular goal, ranging from programs like
Google Earth and openCPN, to APIs to things like GitHub, Google Maps, etc.

So these repos often contain much more than just code.  They run the gamut
from **Pure Programs and Systems** that run on MS Windows or Linux that provide
services or functionality that I want, to **DIY Things** that represent
finished physical objects in the real world that do things that I want them
to do, and everything in-between. Thus these repos tend to include things like
**Libraries** and other *shared software* as well as other *pieces* of the puzzle,
including Fusion 360 CAD files, Prusa 3D Printing and Lightburn Laser Cutting files,
Kicad Schematics and PCB (Printed Circuit Board Designs) as well as significant
documentation on how to build, configure, use, troubleshoot, and
modify the contents of the repos.

Whew.  It's a lot to document.  As a rule the documentation lags behind the
development as I am constantly starting new projects, writing new code,
and making new repos faster than I can document them.

Nonetheless, this readme file attempts to give some coherence to the
entirety of my repos on Github.

The repos tend to fall into a number of groups of related projects
based on my longer term interests and needs.  Roughly they can be
grouped into a number of **Project Groups** that are somehow related:

- **Boat Things** - physical devices (things) I make for my boat
  like the Bilge Pump Alarm, Refrigerator Controller, and so on,
  that are typically reasonably well documented so that other people
  can make them as DIY projects.
- **Boat Instruments/Protocols** - software and hardware I make that range
  from actual hardware/firmware devices (things) that exist on the
  boat like a GPS device or a general purpose Marine Protocol
  converter/hub, to applications with full User Interfaces that
  run on my laptop or as web-servers, to major **reverse engineering**
  efforts to expose and utilize otherwise undocumented or poorly
  documented **proprietary protocols**, particularly from, but
  not limited to understanding and using *historical Raymarine
  proprietary protocols*.
- **CNC Machines** - A Series of CNC machines (things) I have
  designed and built, along with their underlying firmware
  and libraries as more or less completely documented DIY projects
  that others can build.
- **Clocks** - A series of *magnetically driven **wooden geared
  clocks*** that I designed and implemented as complete DIY things
  that other people can make.
- **vGuitar systems** - *guitar foot pedals, loopers, etc* culminating
  in the teensyExpression3 *electric guitar synthesizer and effects*
  foot pedal and looper system presented as completely documented DIY things.
- **Artisan** - A multi-platform *Music Server* that I use to organize
  and play my music library (MP3s) from a local library on a hard-disk
  or USB memory device on a MS Windows or Raspberry Pi hardware platform
  that is reasonably documented and could be considered a DIY system.
- **Utilities** - that tend to be complete **MS Windows** applications,
  sometimes include complete documentation as well a complete released
  **Installer Program** that can easily be run on any Windows machine,
  to not-so-well documented utilities I write for my own purposes.
  This group includes things like Console (Serial and Telnet Terminal)
  programs, UI programs to interface with Git (and Github), Remote File
  management on a variety of platforms, and so on.
- **Add Ins** - Add Ins / Extensions that I have written, documented, and
  published for 3rd party applications including Fusion 360, Komodo Edit,
  Firefox, and so on.
- **Other Projects** like one-off **things** I make for my own use and/or
  Arduino/rPi **experiments** in hardware/software to test a particular
  component, module, or concept, to specific instances of distinctly
  not-code-like things, like the plans to make a particular wooden engraving
  or inlayed wooden box (**artsy stuff**)

So, yeah, some kind of an overview (this document) is in order.


## Architectural Overview Documents

In some cases it is particularly difficult to present to you, the reader,
the over-arching concept behind a group of repositories.  Typically each
repo has its own documentation, but it is not always obvious how they all
fit together to create a final product.

Also there are some repos that cross the above Project Group
boundaries and are used by more than one class of projects and it
can be difficult to discern those patterns from the raw repos themselves.

So, in certain cases, in THIS repo there may be a subpage which describes
in more detail the overall architecture of one of the above project groups,
or an underlying common sub-group, that would be otherwise difficult for
the reader (you) to piece together without a roadmap of some kind.

- [**vGuitar**](vGuitar/vGuitar.md) - an overview of my vGuitar System
- [**Artisan**](Artisan.md) - an overview of my Artisan Music Server system

## Project Groups

Without further ado, here is the list of Project Groups, and the
top level repos within those groups;

- **Boat Things**
  - [**bilgeAlarm.ino**](https://github.com/phorton1/Arduino-bilgeAlarm) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
	Bilge Pump Alarm and remote monitor/controller as used on my boat.
  - [**fridgeController.ino**](https://github.com/phorton1/Arduino-fridgeController) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
    controller/remote/monitor for Danfoss BD50 and related Refrigerator Compressors
	as used on my boat.
  - [**lightController.ino**](https://github.com/phorton1/Arduino-lightController) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
    remote controller for various lights (Anchor, Deck, etc), as installed on my boat
	as part of its completely custom designed and re-implemented DC Electrical Panel.
  - [**tempController.ino**](https://github.com/phorton1/Arduino-tempController)
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
	general purpose, controller/remote/monitor for temperature sensing and controlling
	a 12V fan that I use in the Inverter Compartment on my boat to aid in cooling the
	2000W Inverter/Charger.
  - [**drainPump.ino**](https://github.com/phorton1/Arduino-boat-drainPump) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
    controller/remote/monitor for a 12V Air Conditioning Condensate Pump
	using a custom designed DIY water level sensor.
  - [**airco.ino**](https://github.com/phorton1/Arduino-boat-airco) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
	remote/monitor, where I reverse engineered the RS485 protocol between my newly
	installed **Webasto** FCF 10000btu Marine Air Conditioner and its **Control Panel**
	to be able to monitor the state of the Air Conditioner remotely.  This will be
	combined with the **drainPump** above in future iterations of the system.
  - **Fans** a series of custom designed and 3D Printed 12V Brushless Fans in use on my boat:
    - [fan1.ino](https://github.com/phorton1/projects-fan1) - initial Arduino
	  Nano Brushless Motor PWM controller and 3D printed fan design
	- **Fan Designs** (TBD) - Subsequent refined and more robust 3D printed fan designs that
	  I am currently using.
- **Boat Instruments**
  - [**teensyBoat.ino**](https://github.com/phorton1/Arduino-boat-teensyBoat) and
    [**teensyBoat.pm**](https://github.com/phorton1/base-apps-teensyBoat) -
    A *do-everything* multi-protocol, multi-port, based general purpose ***device***
	consisting of a teensy4.0 Arduino INO program with Firmware, Schematics, PCB Designs,
	and 3D Printed enclosure for **NMEA2000, NMEA0183,** and **Seatalk1** protocols,
	largely encapsulated in my
	[**Arduino Boat Library**](https://github.com/phorton1/Arduino-libraries-Boat)
	along with a Serial Console and Windowed (wxPerl based) ***UI application*** that
	runs on my laptop.
	- The *device* is used on my boat to bridge Instruments and Displays using various
	  protocols together and to allow me to monitor the state of the boat, and 
	  in certain cases, to control those Instruments and Displays as I see fit.
	- Also functions as a complete **desktop testing** device and UI to allow
	  me to test and drive various Instruments and Chartplotters over any of the
	  protocols, and includes a sophisticated **physical boat simulator** and
	  **nine instrument simulators** that work across all three protocols
	  that allow me to drive a *virtual boat* around manually or by simulated
	  autopilot with realistic instrument outputs for all the virtual instruments.
	- Finally, it also presents the **GP8 generalized hardware interface** (to other circuits
	  in other repos) that allow me to test a variety of Raymarine Instruments,
	  specifically ST50/60 Speed/Log and Wind Instruments, by driving their
	  **sensors inputs** to be able to test those devices on my desktop in the
	  absence of their "real" transducers.
  - [**tbESP32.ino**](https://github.com/phorton1/Arduino-boat-tbESP32) -
    a [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) based
    device that plugs into **teensyBoat's GP8** plug that uses TCP/IP and UDP
	protocols to allow for monitoring of the teensyBoat device on my boat
	via Wifi, including allowing the teensyBoat.pm program to be used remotely.
  - [**teensyGPS.ino**](https://github.com/phorton1/Arduino-boat-teensyGPS) -
    a **Marine Grade**, teensy4.0/Neo6M based **GPS device**
	based on my [**Arduino Boat Library**](https://github.com/phorton1/Arduino-libraries-Boat)
	that can transmit NMEA2000 and/or Seatalk1, that includes the Firmware, Schematics,
	and soon-to-be 3D printing information and documentation as a complete DIY project.
	*Will soon be installed on my boat as the primary GPS device.*
  - [**teensyWind.ino**](https://github.com/phorton1/Arduino-boat-teensyWind) - interfaces
    directly to an **ST50**/ST60 Wind Vane (the **Wind Transducer** on the top of a mast) to allow
	me to (a) test the Wind Vane on my desk, but that also (b) resolves the Vane's sensor
	outputs into the apparent wind angle, and thus (c) could, in the future, provide a
	**complete replacement for Raymarine ST50/ST60** and even more recent **Wind Instruments**
	and interfaces.
  - [**raymarine**](https://github.com/phorton1/base-apps-raymarine) -
    This repo contains a variety of applications and knowledge that have been developed
	over my last 20 years of owning and using *Raymarine Instruments and Chartplotters*.
	In some cases it provides the **most complete and/or most current reference** materials
	regarding Raymarine's proprietary **protocols** and **file formats** available anywhere
	on the internet (in the world). ***Note:** Sorry but this repo is currently **private**,
	and will return a **404 Not found** when you click on the links here, as I work out
	the documentation presentation to a form I am satisfied with*.
	- [**NET**](https://github.com/phorton1/base-apps-raymarine/tree/master/NET) -
	  This folder contains the world's first comprehensive reverse engineering
	  and documentation effort regarding Raymarine's **SeatalkHS** ethernet protocols.
	  - **shark.pm** - this program is used to probe, expose, and utilize the ethernet
	    protocol(s). It uses Wireshark to sniff and analyze TCP/UDP traffic which it then
		formally encapsulates into several sub-protocols that **I reverse engineered and understand**
		and have named as follows.
		- **RAYDP** - the Multicast UDP **device and discovery** protocol within Seatalk HS
		- **FILESYS** - a UDP protocol that gives read-only access to the **CF card** in an E80
		  (E120 and potentially other) Raymarine MFDs (Chartplotters)
		- **DB** - a set of TCP and UDP protocols where the E80/E120 Database can be queried,
		  and/or by which E80/E120 blasts database (navigation) information over UDP
		- **WPMGR** - a TCP protocol that allows for the reading, and importantly, writing,
		  of **Waypoints, Groups(Folders), and Routes** to/from the E80/E120.
		- **TRACK** - a TCP protocol that allows for control (starting, stopping, saving,
		  and renaming) of tracks on the E80/E120 as well as an important ability to
		  download them over ethernet to my laptop for further processing.
	- [**FSH**](https://github.com/phorton1/base-apps-raymarine/tree/master/FSH) -
	  This folder, initially based on [**parseFSH**](https://github.com/rahra/parsefsh)
	  provides *updated*, perhaps *crucial*, information regarding the **FSH file structure** used
	  by E80/E120 Chartplotters to store Waypoint, Group(Folder), Route, and Track information
	  on the CF card (which can now be gotten with Ethernet directly from the Chartplotter using
	  **shark.pm** above). This repo (and the **shark.pm** program above) are the first I know of
	  in the world to *write* FSH files accurately.
	  - **fshConvert.pm** - converts an FSH file to KML, GPX, or CSV formats
	  - **kmlToFSH.pm** - reads a KML (Google Earth) file and writes an FSH file
	- [**CSV**](https://github.com/phorton1/base-apps-raymarine/tree/master/CSV)
	  This folder contains a single utility program I have used that converts a
	  Google Earth **KML File** into a **Raymarine Raytech RNS** compatible **CSV file** for
	  input into a Raymarine based system.  
	  - **kmlToCSV.pm**
	- **NMEA_Monitor.ino** - vestigial General Purpose NMEA2000 monitor based on an ESP32 and
	  a MCP2515 CANBUS Module that has been superseded by the teensyBoat PCB.
	- **NMEA_Sensor.ino** - vestigial simulated Instrument using an ESP32 and a
	  MCP2515 CANBUS Module  that has been superseded by the teensyBoat PCB.
	- **Seatalk.ino** - vestigial early program to read and write **Seatalk1** using
	  an opto-isolator interface that I developed that is now part of the teensyBoat PCB
- **CNC Machines** - a series of CNC machines, their firmware, design, 3D printing information,
    and supporting documentation that I have created based on my fork of the
	[**FluidNC Library**](https://github.com/phorton1/Arduino-libraries-FluidNC) and my
	[**extensions**](https://github.com/phorton1/Arduino-libraries-FluidNC_extensions) to it:
  - [**vMachine.ino**](https://github.com/phorton1/Arduino-vMachine) - the first "cnc" machine
    I created that provides a port of the *Maslow CNC Machine* **kinematics** to make a
	pen-plotter using two stepper motors.
  - [**cnc3018.ino**](https://github.com/phorton1/Arduino-esp32_cnc3018) - the second cnc machine
    I created that I now use primarily to mill my own PCB (Printed Circuit Boards) that
	(a) milled ITS OWN PCB lol, and (b) which I used to create parts for the subsequent
	**cnc20mm** below. Most of the PCB designs that I present on other pages are milled
	on this machine.
  - [**cnc20mm.ino**](https://github.com/phorton1/Arduino-esp32_cnc20mm) - a *large* CNC machine
    that I designed and created that can work on pieces up to 50x50 inches, allowing a complete
	4x8 foot sheet to be worked on by doing it in two 4x4 foot halves, that currently sports a
	500W 100V DC spindle for machining and a 30W optical power laser that is capable of cutting
	through up to 1/2" of plywood.
- **Clocks** - The series of *magnetically driven **wooden geared clocks*** that I designed and
  implemented as complete DIY things, including the Architectures, Build Process, the *Fusion 360
  CAD* files behind the overall clocks, the *Lightburn files* I used to **laser cut the wooden parts**
  on my cnc20mm machine, and the Prusa configuration and gcode files I used to 3D Print the plastic,
  along with the *Kicad Schematics and PCB Designs* that used to **mill the PCBs** on my cnc3018
  machine, as well as additional End User documents on Maintaining and Tuning the clocks for people
  who might receive one of these DIY projects as a gift from another person.  These clocks
  make use of my [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) library
  to provide a Web Based configuration and monitoring UI.
  - [**theClock.ino**](https://github.com/phorton1/Arduino-theClock) -
    the first clock I made.  I made two of these and gave one away as a gift.
  - [**theClock3.ino**](https://github.com/phorton1/Arduino-theClock3) -
    the next two iterations of the clock design. I have made four of the v3
	clocks and given several away as gifts.
  - [**coilWinder.ino**](https://github.com/phorton1/Arduino-coilWinder) -
    a quick and dirty coil winding machine I made using laser-cut plywood and
	a stepper motor and a simple Arduino-Nano based control program, that I used
	to wind the electromagnet coils for the clocks.
- **vGuitar System**
  - [**TE3.ino**](https://github.com/phorton1/Arduino-TE3) - the current, final generation of
    the evolution of the vGuitar system.  It is beyond the scope of this outline to present
	the details and dependencies, but it is worth noting that there is a fairly comprehensive
	[**documentation**](https://phorton1.github.io/Arduino-TE3/#home.htm) page available
	separate from the repo, as well as a separate
	[**vGuitar System Overview**](vGuitar/vGuitar.md)
	document available within THIS repository regarding the overall system.
  - [**teensyExpression.ino**](https://github.com/phorton1/Arduino-teensyExpression) - vestigial -
    the initial teensyExpression foot pedal part of the vGuitar system that received a bit of
	note on Hackaday.
  - [**teensyExpression2.ino**](https://github.com/phorton1/Arduino-teensyExpression2) - vestigial -
    A second generation instance of the foot pedal part of the vGuitar system.
  - [**circle**](https://github.com/phorton1/src-circle) - my fork of the **circle Raspberry PI
    bare metal C++ system/library** and
	[**my extensions to it**](https://github.com/phorton1/src-circle-_prh) that	are both
	still used in the most current and final version (TE3) of the vGuitar system.
  - the bare metal based [**Looper**](https://github.com/phorton1/src-circle-_prh-apps-looper) that is
	still used in the most current and final version (TE3) of the vGuitar system.
- **Artisan** - Please see the [**Overview Document**](Artisan.md) for more information about
  my Artisan Music (MP3) Server
  - [**artisan.pm**](https://github.com/phorton1/base-apps-artisan) - current Artisan Server that I run on a rPi 4B at home and on the boat
  - [**artisanWin.pm**](https://github.com/phorton1/base-apps-artisanWin) - vestigial Windows UI and Server
  - [**android-Artisan**](https://github.com/phorton1/Android-Artisan) - vestigial Android UI and Server
- **Utilities**
  - [**buddy.pm**](https://github.com/phorton1/base-apps-Buddy) and
    [**fileClient.pm**](https://github.com/phorton1/base-apps-fileClient) - A *Putty-like* **Serial
	and Telnet** terminal **Console Program**, with additional File Transfer capabilities (for TE3 and other programs I've
	written) that can be run from its Perl source, but is also released as an **installable MS Windows Application**
	and that *plays well* with the Arduino Development Environment (to close the COM port when an
	Arduino build is in process).
  - [**gitMUI.pm**](https://github.com/phorton1/base-apps-gitMUI) - a replacement for the **gitUI** User Interface
    provided with most installations of **Git** that I use almost every day to update GitHub from my local repos.
	As opposed to the standard UI, my *gitMUI* program allows one to
	- commit, push, and pull **multiple repos simultaneously**
	- **instantanously see** any changed files (diffs) or uncommitted changes as soon as files are
	  written to disk (saved from an editor) without needing to "rescan" repos each time you make changes
	- provides a process to **manage and normalize submodules** (code that is explicitly shared and
	  included in more than one repo) without confusing and onerous jumping through hoops.
  - [**myIOTServer.pm**](https://github.com/phorton1/base-apps-myIOTServer) - A *service* that
    works with my [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) library
	to aggregate and forward myIOT devices to a HTTPS (encrypted, protected) Machine on
	the internet at large so that I can access myIOT devices from anywhere on the planet.
- **Add Ins** and extensions
  - My Fusion 360 [**prhParams**](https://github.com/phorton1/fusionAddIns-prhParams) Add In
    that allows me to work with, sort, comment, and modify the parameters that drive a Fusion
	360 design.
  - My Fusion 360 [**pyJoints**](https://github.com/phorton1/fusionAddIns-pyJoints) Add In that allows
    me to animate designs in ways that normally don't work in Fusion 360 so as to better judge
	the performance of mechanical designs.  Used extensively in **theClock3**'s design process.
- **Other Projects**
  - [**wireStripper.ino**](https://github.com/phorton1/Arduino-wireStripper) - a **thing** I made,
    based on my [**ESP32 myIOT**](https://github.com/phorton1/Arduino-libraries-myIOT) library
	to provide a UI, with complete Fusion 360 Designs, 3D printing information, Schematics and PCB
	designs, to **cut and strip** 22ga **wires for use on breadboards** and on the many one sided
	PCBs that I make for these projects. It uses a typical RC Servo and commonly available
	inexpensive wire stripper, along with an extruder from a 3D printer and some Infrared
	sensors to automate this otherwise tedious process.
  - [**useless.ino**](https://github.com/phorton1/Arduino-useless) - An **Arduino Nano** based
    **Useless Box** that I designed and implemented, that kids find really fun, and of which
	I have built 4 units, giving 3 away as gifts (or even selling one!).
  - [**ws2812bSwitchArray1**](https://github.com/phorton1/projects-ws2812bSwitchArray1) -
    a proof of concept project that shows how to 3D Print and attach these Buttons I designed
	to a ws2812B array (or light strip) and use the signals to the LEDs to drive an array
	of buttons using only a single wire (instead of the typical array of row and column
	wires arranged in a grid).





