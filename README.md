# The DLNA/UPnP Media Browser
The DLNA Media Browser is a file explorer for files hosted via a dlna/upnp service. In the current version of the tool it is possible to view the folder structure and files on the server and download selected files one by one. You cannot edit or delete the files on the server. You can download this description including images as a PDF file in English or German language.

English: https://github.com/hswlab/dist-dlna-browser-.net/blob/main/about-en.pdf

German: https://github.com/hswlab/dist-dlna-browser-.net/blob/main/about-de.pdf

# Change language
In the current version, the language English or German can be set. The language can be changed in the header navigation and is remembered even after the application is closed.

# Configuration of the storage path for downloaded files.
Unless otherwise configured, downloaded files are stored in the default download directory: "C:\Users\username\Downloads". With the settings icon (1) you open the configuration view, in which the storage path can be changed. The memory path is remembered even after the application is closed.

# Find and browse dlna/upnp devices on the local network.
Clicking on the UPnP icon (1) opens the browser view. The button with the magnifying glass symbol (2) searches the local network and lists all found dlna/upnp devices as a new button to the right of the search button.

In the example, a TV set could be found. Clicking on the button with the device name starts a search for all data carriers connected to the device and the files contained therein. For example, a recording hard disk and a USB stick are connected to the TV, which are displayed as separate subfolders of the TV.

A label next to the folder name indicates the number of files contained in the folder. A click on the folder name opens a list with the files it contains.

Note: External drives will be put into a standby state if they are not used for a long time. Unfortunately, the DLNA/UPnP browser does not yet manage to wake up these devices. In this case, try to manually wake the drive from standby mode (e.g. turn off/turn on hard disk).

# Download files.
The download button is only visible when at least one file is selected. Individual files can be selected by clicking on the file name. Via the button in the menu bar all files in the current folder can be selected at once. With the 4 buttons next to the Multiselect checkbox, the file list can be sorted ascending or descending, alphabetically or by date.

The download will download the selected files one by one. Exiting the view causes the current download to be aborted. So that the view cannot be left during the download, all buttons except the pause button are deactivated (color of the buttons changes to light gray).

The download progress can be read on the label next to the date based on the already downloaded file size. For file streams, the information for the entire file size is not always available, so unfortunately no classic progress bar of 0-100% can be displayed at this point. Maybe a better solution for the progress bar will be found in the upcoming versions. The progress bar in the pause button shows what percentage of the selected files have already been completely downloaded. 
The download can be cancelled at any time by clicking on the pause button. Files that could not be fully downloaded are highlighted in red.

If a download is canceled, the download queue stops. Incompletely downloaded files are automatically removed from the hard disk. This is to prevent file fragments from being left on the hard drive. During the download, the file has the extension .part and is renamed after a successful download with the correct file extension. Successful downloads are highlighted in green.

Fully downloaded files will not be downloaded again as long as they remain in the download directory. The downloader detects complete files and skips them even if they are selected again for download.
Downloads are stored in subfolders of the same name. File names are automatically extended by a date text. When downloading TV recordings of a series, this has the advantage that all recordings of the same series can be found in a common folder sorted by recording date.

# Caching the file list
Searching the upnp/dlna devices for existing files can take some time, so I decided to cache the last found file list locally. This list is displayed again immediately after closing and opening the application. You can see that a previously saved state of the list is currently used when the reset button is visible. By clicking on this button, the cached list can be reset.  

# Updates / New Versions
For new updates, an update button appears to the left of the UPnP button. By clicking on this button, the new version will be downloaded. It may take a few minutes for the download to start. Unfortunately, I haven't figured out yet why Github makes you wait so long. If it takes too long for you, you can also download the current version manually under the following link.

https://github.com/hswlab/dist-dlna-browser-.net/releases

My versioning consists of 3 digits e.g.: "1.2.3" The last digit announces a bugfix, the middle digit a new feature and the first digit a major change.

# What is this app programmed with?
This is an Electron application in combination with a .NET6 MVC framework (electron.net). The business logic is mainly programmed with C#. In the frontend, Bootstrap and classic CSS are used. For frontend interactions, a little JQuery and Ajax were used. The local LiteDB database is used to persist user settings and the file list. The data is only stored locally, communication with the Internet does not take place! The library LibVLCSharp is used to determine the UPnP services in the local network and reading the files.

# Will there be a version for Linux?
Since it is an Electron application, a version for Linux or Mac OS can theoretically be provided. However, I have not yet tested whether the LibVLCSharp library works under Linux. But I will definitely deal with it. For now, however, it is important to me that the Windows version works without any problems. So far, this app has only been tested with a Panasonic TV.

# Known Issues
When clicking the device button, it can sometimes happen that not a single file from the disks of a DLNA/UPnP device are listed. This is because some drives go into standby mode when they are not used for a long time. Unfortunately, this app cannot yet reliably wake up such disks from standby mode. If this happens, try to manually turn off the affected hard drive and then turn it back on.
Another problem is the long waiting time when scanning a DLNA/UPnP device. The problem in this case is unfortunately again a disk in standby mode for which an attempt is made to wait. The search is usually aborted if the disk is unreachable for a longer period of time.
I hope to find a solution to speed up the search process a bit.
