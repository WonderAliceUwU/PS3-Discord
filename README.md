# PS3-Rich-Presence-for-Discord
Discord Rich Presence script for PS3 consoles on HFW&HEN or CFW.

Display what you are playing on your PS3 via Discord's game activity.

Script must be ran on a computer, it cannot be installed directly onto a PlayStation 3.

## Index
* [Features](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#features)
* [Display example](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#display-example)
* [Limitations](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#limitations)
* [Usage](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#usage)
* [Contact me](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#contact-me)
* [Additional Information](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#additional-information)

## Features
* Automatically find PS3 IP address (currently can be very slow, update in progress)
* Display the name and a game cover for currently open PS3 game
* Display PS3 temperatures (toggleable)
* Display the name, and either a shared cover, or an individual cover for currently mounted PSX and PS2 game (toggleable)

## Display Example
 No game 	| 	PS3 game 	|	PS2 game 	|	PS1 game 	|
 -----------|---------------|---------------|---------------|
 ![noGame](https://i.imgur.com/lw1vMGz.png) | ![ps3Game](https://i.imgur.com/aQxcbQG.png) | ![ps2Game](https://i.imgur.com/Z5vYdog.png) | ![ps1Game](https://i.imgur.com/7qfsisz.png) |

## Limitations
* __A PC must be used to display presence, there is no way to install and use this script solely on the PS3__
* PSX and PS2 game detection depends on the name of the file
* PSX and PS2 game detection will **not** work on PSN .pkg versions because webman cannot show those games as mounted/playing.
* PS2 ISO game detection can be inconsistent, varying on degree of consistency by the value of "Refresh time."
* Using Windows 7 is not advised due to the hoops that have to be jumped through to get the script working, but the .py file *does* work (tested with Python 3.8.6 64bit)
	- If you want to use a .exe, [here](https://www.mediafire.com/file/ezzlcemhkmnmyn2/PS3RPD.exe/file) is a version that may or may not fully function (very little bug testing has been done)
* The script relies on webmanMOD, and a major change to it will break this script, please message me about updated versions of webman so that i can test the script with them

## Usage

### Requirements
* PS3 with either HFW&HEN, or CFW installed
* PS3 with [webmanMOD](https://github.com/aldostools/webMAN-MOD/releases) installed 
* PS3 and PC on the same network/internet connection
* Discord installed and open on the PC running the script
* A Python 3.9 interpreter installed on the PC if you do not wish to use the executable file

### Installation
A compiled executable (.exe) is provided for use on the windows platform.  
WARNING: This file was flagged as a virus on my computer, i do not know what causes the file to be flagged as such.

Alternatively, the PS3RPD.py file can be ran from your favourite python IDE. (you will require the external dependencies listed [here](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#remote-python-packages-required)).  
Note that this script was written with python 3.9, i cannot provide support for earlier versions.

### Installing as a Windows service (optional)
Download [NSSM](nssm.cc/release/nssm-2.24.zip) and run `nssm install <service name ie. ps3rpd>` to install PS3RPD as a Windows service.
WARNING: PS3RPD.exe must be in a location that won't change ie. C:\ps3rpd\PS3RPD.exe

### General instructions
On program start, the script will prompt the user for how to get the PS3's IP address.

If the manual option is chosen, the user can enter the PS3's IP address.

If the automatic option is chosen, the program will take the PC's local IP address, and attempt to connect to each address in range 2 - 254.

Once the script has connected to your PS3, it will generate an external config file, **"PS3RPDconfig.txt"** in the same directory as the script (more information [here](https://github.com/zorua98741/PS3-Rich-Presence-for-Discord#external-config-file)). It will automatically begin sending the game data to your Discord profile.

## Contact Me
please contact me via Discord: "zorua98741#0023".


## Additional Information

### Remote Python packages required
*These are not intended download links, they are the developers sites, please install with pip.*
* [urllib3](https://urllib3.readthedocs.io/en/stable/)
* [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/)
* [pypresence](https://github.com/qwertyquerty/pypresence)
* [requests](https://docs.python-requests.org/en/latest/)

### External config file
PS3RPD makes use of an external config file to persistently store a few variables, on creation, the default values will be:
* Your PS3's IP address 	(where the script will find your PS3 on the network)
* My Discord developer application's ID 		(where the script will send presence data to)
* A refresh time of 35 seconds 					(how often to get new data (minimum value of 15 seconds)
* To show the PS3's temperature 				(self explanatory)
* To use a shared cover for PS2&PSX games   	(self explanatory) 
* To reset the *time elapsed* whenever a new game is opened

You may change these values to suit your own tastes, an example is shown below:

IP | ID | Refresh time(seconds) | Show temperatures | Individual PS2&PSX covers | Output |
---|----|-----------------------|-------------------|---------------------------|--------|
192.168.0.13 | 780389261870235650 | 35 | True | False | ![defaults](https://i.imgur.com/E7M4yie.png) |
192.168.20.5 | 123456789012345678 | 15 | False | True | ![noTemp,indivCover](https://i.imgur.com/QHMxhnj.png) |

Please note that the external config file is sensitive to the data you input, and a change in the formatting **will** most likely break it.

Possible values for the variables:  
* __IP:__ any valid IPv4 address
* __ID:__ any valid Discord developer application ID
* __Refresh time(seconds):__ any digit in range 15-1000 	(Note: any value <15 will be set to 15 due to developer application restraints)
* __Show temperatures:__ [True, true] [False, false]
* __Individual PS2&PSX covers:__ [True, true] [False, false]
* __Reset time elapsed on game change:__ [True, true] [False, false]

### (in)Frequently asked questions
Q: Can this script be adapted for use on mobile devices?  
A: no. While the functionality of this script could certainly be adapted into a mobile app. Discord does not support rich presence from its mobile app.

Q: Can this script be used on OFW/without webmanMOD?  
A: no. The only other program i have encountered that i can scrape game info from is CCAPI, which is lesser-used, and more complicated for the user to setup than webmanMOD.

Q: Why is PS2 game detection inconsistent?  
A: this script works by scraping game data from webmanMOD. When a PS3 goes into PS2 mode, it disables all plugins including webmanMOD,
because of this the script will only detect a PS2 game if it refreshes itself and it finds a PS2 game mounted (but not open).  
There is no way of fixing this issue as far as i can tell.

Q: Can i programatically send art assets to Discord?  
A: yes, the pre-release (v1.8) of the script works to implement this using the official playstation tmdb api

Q: I want Discord to show me playing the game's name, not playing "PS3", can i do this?  
A: this is possible, however it is not yet implemented into the script

## [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/N4N87V7K5) [![pypresence](https://img.shields.io/badge/using-pypresence-00bb88.svg?style=for-the-badge&logo=discord&logoWidth=20)](https://github.com/qwertyquerty/pypresence)


### Using your own images [Not applicable to 1.8 pre-release]
If you would like to have complete control over what images are used per game, you must create your own Discord developer application over at https://discord.com/developers/applications.

Once created, copy the "APPLICATION ID" from the developer portal and paste it as to replace the current string next to "ID: " in the external config file "PS3RPDconfig.txt".
Alertnatively, if you are using the .py file, you can replace the value of "self.client_id".

You will now be able to add your own art assets in the developer portal under "Rich Presence > Art Assets". Note that the name of the art assets uploaded must be the same as whatever is output from "validate(): " when that specific game is open.

An example:  
If i want to add an image for Counter Strike: Global Offensive, I will open the game and look for the output of "validate():" from the PS3RPD script on my PC:  
![validateExample](https://i.imgur.com/7EEgUYn.png)  
As shown, i would then rename the art asset on my PC "counter_strike_global_offensive_", and upload it to my Discord developer application.

After a couple of minutes, CS:GO will go from having no image, to displaying an art asset from the developer application:
before | after |
-------|-------|
![noasset](https://i.imgur.com/8mJvYDH.png) | ![addedasset](https://i.imgur.com/XLIsIVV.png) |