# Artisan - Music Library System

[**Home**](readme.md) --
[**vGuitar**](vGuitar.md) --
**Artisan**


Artisan is a system for organizing and presenting a Music Library of
Audio files, like MP3s, contained in a single folder tree, on one or
more computers on a home network.

The system is built to be a completely compliant set of
[UPNP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play)
(Universal Plug and Play) standard
[DLNA](https://en.wikipedia.org/wiki/DLNA)
devices that present themsselves on the home network via
[SSDP](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol)
(Simple Service Discovery Protocol) devices as well as being generic
[HTTP](https://en.wikipedia.org/wiki/HTTP) and
[HTML](https://en.wikipedia.org/wiki/HTML) servers which present a
***Web User Interface*** accessible from a Browser anywhere on
the same network.


There are three main sub-repositories in the system:

- [**Artisan Perl**](https://github.com/phorton1/base-apps-artisan) contains
  the core Perl Library that scans the **Master Folder Tree** into a
  **SQLLite database**. This repo also includes a script that starts Artisan as a
  headless *Server* which can be run from the command line, or be installed as a *Service*.
  It implements the **HTTP/HTML, UPNP, DLNA,** and **SSDP** servers necessary
  to **be** a **DLNA Server** as well as being a **DLNA Controller** by virtue of
  **serving** a *WebUI* from a generic HTTP/HTML server to any browser
  on the network. Artisan Perl is **not** a *DLNA Renderer*.
- [**Artisan Win**](https://github.com/phorton1/base-apps-artisanWin) contains
  a Program that runs on Microsoft Windows as a
  [wxPerl](https://github.com/phorton1/src-wx-wxPerl)
  [wxWidgets](https://www.wxwidgets.org/) native Windows Application.
  It is derived from the
  [Artisan Perl](https://github.com/phorton1/base-apps-artisan) repo,
  so it already **is** a **DLNA Server**, and, via the WebUI, it *serves*
  a *DLNA Controller*. In addition it presents it's own Windows
  User Interface in order to **be** a **DLNA Renderer**.
  The UI **is** a *DLNA Controller*, with potential UI extensions that
  are not possible purely within DLNA.
  As such it Artisan Win constitutes a **complete stand-alone Music System**.
- [**Artisan Android**](https://github.com/phorton1/Android-Artisan)
  is a stand-alone native Android Application that can also provide all
  three DLNA roles ... it can be a *Server*, a *Renderer*, **and**
  a *Controller*, and so it also acts as a **complete stand-alone Music System**.
  This program was specifically built to run on an *Android based Car Stereo*.
  - If a Library is present, it implements the UPNP, DLNA, and SSDP servers
    necesary to **be** a **DLNA Server**.
  - It **is** a **DLNA Renderer** and **DLNA Controller**, so, even if there
    is no Library present, (i.e. if I run the app on my Phone with no Library),
	it can Control any other Artisan (DLNA) Renderer, and/or play music from any
	other Artisan (DLNA) Server.

Note that, even with a Library present, Artisan Android does **not** scan
the database but rather, it uses a copy of the *Master Folder Tree*
and the *SQLLite database* created by
[Artisan Perl](https://github.com/phorton1/base-apps-artisan).

Artisan Android does not currently include a generic HTTP/HTML server<sup>1</sup>,



## DLNA Servers, Renderers, Controllers vs HTTP/HTML Servers

**DLNA** defines three *roles* that a device may take on.

- **Server** - a DLNA Server can serve content,
  including streaming the audio itself, but also providing things
  like images, descriptions, folder trees and album context, playlists,
  and so on for the presentation of the content.
- **Renderer** - a DLNA Renderer is a device that can render audio streams
  from a Server so that you can hear them. It has a *context* for the
  things are playing, which includes things like the Album, folder tree, or playlist,
  and can serve as a pass through to the Server for things like
  images, descriptions, and so on.
- **Controller** - a DLNA Controller connects a Renderer to a Server
  and presents a User Interface. It generally controls the Renderer
  and shows context information, like the images and descriptions,
  for the current Track(s) being streamed by the Renderer and alows
  the Renderer to be "programmed" to play a given Track, folder tree,
  Album, playlist, and so on.

These DLNA roles should not be confused with the ability of a program
or library to be a *generic HTTP/HTML server* which **serves** a
DLNA Controller WebUI (or any other generic webpages and HTTP content it might
care to) to a Browser on the network

- All three repos **are** (or can be) DLNA Servers.
- Artisan Perl can **serve** a DLNA Controller WebUI to a browser
- Artisan Android, **is** a DLNA Controller and Renderer
- Artisan Win **is** a DLNA Controller and Renderer **plus**
  it can **serve** a DLNA Controller WebUI to a browser


## Interoperability

This architectures provides a high level of interoperability
with many options.

Note that Windows Media
Server is also all three (DLNA Server, Renderer, and Controller), that
my Samsung TV can act as a DLNA Renderer (with it's own control UI),
and that Android phones can also be DLNA Servers, Renderers and/or
Controllers, depending on the apps they are running.

For example, on the boat, I can start Artisan Win on my Laptop and
Artisan Android on the Car Stereo, and, simultaneously:

- play music from any of
	- the Laptop (Artisan Win DLNA Server)
	- the Car Stereo (Artisan Android DLNA Server)
	- Visitor's laptop (Windows Media or generic DLNA Server)
	- Visitor's phone (Generic DLNA Server)
- on any of the devices
    - the Laptop (Artisan Win DLNA Renderer)
	- the Car Stero (Artisan Android DLNA Renderer)
	- my Phone (Artisan Android DLNA Renderer)
	- the TV (Samsung DLNA Renderer)
	- Visitors Laptop or Phone (Windows Media or Generic DLNA Render)
- and Control them from any of
	- the Laptop (Artisan Win UI DLNA Controller)
	- the Car Stereo (Artisan Android DLNA Controller)
	- my Phone (Artisan Android DLNA Controller)
	- Visitors Laptop or Phone (Windows Media or Generic DLNA Controller)
	- a browser anywhere on the network (DLNA Controller served from Artisan Win)


## Key Concepts

This section describes some key concepts that are baked into
the Artisan DLNA Server, Renderer, and Controllers.

- **Master Folder Tree** - somewhere there exists a single folder tree
  containing all of the *Tracks* (MP3, M4A, and other Media Files) that
  acts as the *Master*. Tracks are only added, removed, or changed
  within this folder tree. I keep this on my main Windows laptop in
  **C:\\mp3s**, and this is called the **Root Folder**.

- **SQLite Database** and the **Scanner** - Only the
  [Artisan Perl](https://github.com/phorton1/base-apps-artisan)
  library can perform a *Scan* of the Tree. At startup, the Master
  Folder Tree is scanned and the Database is created or updated
  as necessary to match the Folder Tree.

- **Sanctity of Tracks** - We specifically **do not** modify any
  Track Media Files (like many other systems do). We *do not* change
  any of the *Tags* or *MetaData* in the original Media File, preferring
  to keep the media files *pristine* in their original state. We **use**
  certain of the Tags and MetaData in Track files if it is available,
  but we **never** modify that data.

- **Tracks, Albums, and Artists** - the names of the folders within the tree
  are important. All Tracks are kept in folders which are considered *Albums*.
  The name of the folder will the *Artist Name* followed by the *Album Name*,
  delineated by a **dash** (space-dash-space). Thus a folder of the name
  "John Prine - Souvenirs" is an album named "Souvenirs" from the artist
  "John Prine".

- **Classes and Genres** - All Albums are kept within subfolders
  under the Root Folder.  There are no Albums placed directly in the
  Root Folder. Between the Root Folder and the Albums are one or more
  levels of subfolders acting as containers.  These subfolders are
  considered the *Classes and Genres* of the Albums for categorization
  purposes.  For example, I have an Album in the following folder:
  ```
	C:\\mp3s\\albums\\Jazz\\Soft\\Al Jarreau - Tenderness
  ```
  This defines the album "Tenderness" by the artist "Al Jarreau" with
  a class of "albums", with a genre of "Jazz" and a sub-genre of
  "Jazz Soft".<sup>2</sup>

- **Uniqueness and Best Copies** - a considerable amoount of effort was
  put into identifying and removing duplicate Tracks from the Tree.
  Every Track is given a *Chromaprint* **Fingerprint** which will *be the same*
  for the same *recording*, irrespective of the *container* (MP3 vs M4A),
  *bitrate*, or *quality* of the recording.   The Scanner will give a
  *Warning* if it detects two Tracks that are the same recording
  within the Tree, allowing me (the user) to determine which of the
  two is the better copy and to eliminate the inferior copy, or possibly
  to allow the duplicates if the two Tracks are validly included in
  two separate Albums (i.e. 'Best Of' albums).

- **Playlists and Stations** - Two additional mechanisms are provided for
  grouping Tracks and Albums for playback.  *Playlists* consist of
  specific Tracks and Albums that are grouped together by the user,
  that can to be played together, in order, or in random Track or Album order.
  Stations consist of specific Genres (and Sub-Genres) that can be
  grouped together by the user that can be played togeter, in order, or in
  random Track or Album order, like a *Radio Station*.

- **Everyone is a Server** - all three repos present **DLNA Servers**
  that can serve Tracks and Albums on the home network.  For instance, I
  can play the music from Artisan on my **Samsung TV**, because the TV
  (and many other modern devices) are built to be *DLNA Renderers* that
  can play music (and present Albums, pictures, descriptions, etc)
  from DLNA Servers.

- **Not everyone is a Renderer** - Currently, only two of the three repos<sup>3</sup>
  present **DLNA Renderers** that can play music from a *DLNA Server*. This not
  only includes music from the Artisan DLNA server, but also includes
  **any other existing DLNA Servers on your home network**. One
  common example of a DLNA Server is the *Windows Media Server*. Thus
  in addition to being able to play the music presented by the Artistan
  Servers, [Artisan Win](https://github.com/phorton1/base-apps-artisanWin) and
  [Artisan Android](https://github.com/phorton1/Android-Artisan) also play
  music from the Windows Media DLNA Server.

Typically, if I want to listen to music on my home network, I run the
[Artisan Win](https://github.com/phorton1/base-apps-artisanWin) program which
turns my laptop into both a Server and a Renderer and allows me to play
the music from the Artisan Library on my laptop.  If I want it louder,
I typically use an external **Bluetooth** device.
I can then also control the music being played by accessing the HTML WebUI
in a Browser from any other device on my home network. or from
[Artisan Android](https://github.com/phorton1/Android-Artisan) on my phone.

I typically use [Artisan Android](https://github.com/phorton1/Android-Artisan)
in a stand-alone configuration on my boat where it runs on the *Car Stereo*,
and does not, per-se, require a network to function.  If the Car Stereo
**is** on a network however, I can control it via another instance
of the the Artisan Android application running on my Phone, or via
the various other WebUI or Artisan Win user interfaces.


## Summary and Footnotes

Please see the individual **repos** for more details on each
Program and Library

\[1]: *The Car Stereo (Artisan Android) should be modified to also serve
  the same webUI as Artisan Perl, so that I could simply access it via
  a Browser on the same network.*

\[2]: *Note that in Artisan an Album, and the tracks within it, fall into
  **exactly one** Genre and/or Sub-genre.  We intentionally **completely
  ignore** the genres provided by **Tags** within media files, having
  found that they are horribly inconsistent and all over the place.
  In the future I **may** implement a mechanism to allow something
  **like** Tags to provide additional genres for a given Track or Album,
  but I will **always** maintain the **sanctity** of the Media Files and
  will **never** use them to store such information. Note how we already
  provide a separate mechanism for the Artist, Album, and Track Names
  which has nothing to do with the Tags in the Media files.*

\[3]: *This is because to be a Renderer you need access to the machine's
  Audio device.  When I initially wrote Artisan, you could not dirctly
  access the machine's Audio device from a Browser.  That may have changed
  with later versions of HTML and needs to be re-explored.*


[... Back](readme.md) to Overview of My Github Repos
