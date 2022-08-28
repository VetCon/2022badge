<div align=center>
<h1> :skull: VETCON BADGE :skull: <br/>
:stopwatch:  Quick Start Guide :athletic_shoe:</h1>
<h3> For the full manuals, please view the following: </h3>
<h4>
<h4>
    <a href="./README_HARDWARE.md">Hardware Guide</a>
  <span> · </span>
    <a href="./README_SOFTWARE.md">Software Guide</a>
</h4>

</div>


# :notebook_with_decorative_cover: Table of Contents
- [:notebook_with_decorative_cover: Table of Contents](#notebook_with_decorative_cover-table-of-contents)
  - [:star: About this Guide](#star-about-this-guide)
  - [:gear: Prerequisites](#gear-prerequisites)
  - [:computer: Software Components](#computer-software-components)
    - [:one: Microcontroller Code](#one-microcontroller-code)
    - [:two: Game 1](#two-game-1)
    - [:three: Game 2](#three-game-2)
    - [:four: Game 3](#four-game-3)
  - [:hammer: Hardware Components](#hammer-hardware-components)
    - [:one: PCB Schematics](#one-pcb-schematics)
    - [:two: Fabrication Files](#two-fabrication-files)
  - [:memo: Some Notes](#memo-some-notes)

## :star: About this Guide
<h5> THIS GUIDE IS INTENDED TO BE PURELY A 'QUICK START' GUIDE TO GET YOU UP AND RUNNING </h5>
<h5> PLEASE USE THE INCLUDED MANUALS AS A 'FULL' REFERENCE FOR DEPLOYMENTS, BUILDS, ETC.</h5>

## :gear: Prerequisites
1. Have a working [MSP-EXP430FR2433](https://www.ti.com/tool/MSP-EXP430FR2433) development board (complete with MicroUSB to USB-A cable).
a. Alternatively, have a [Wiring Framework](http://wiring.org.co/) compatible board that is listed on [PlatformIO's supported board list](https://registry.platformio.org/search?t=platform&f=arduino&p=1) and is cross-compile compatible with the [Arduino](https://www.arduino.cc/en/software) or [Energia](https://energia.nu/) IDEs.
2. Download and install the [PlatformIO Toolchain](https://platformio.org/platformio-ide) via VSCode Extension (recommended).
   1. It would be wise to read up on some of the documentation and get your own "Hello World" going to faciltate the rest of this guide!
3. Have this repo cloned ```git clone https://github.com/derekbarbosa/EC463```
   1. This repo houses everything you need for all components of the project. If you don't have it locally on your machine, now would be a good time to have it downloaded.
4. If on Windows or any other non **nix*-based OS, have PuTTY (or your terminal emulator of choice) installed and ready to connect via serial (9600-ish baud). 
5. Download and Install [KiCad](https://www.kicad.org/download/) (recommended) or any eCAD software of your choice.
## :computer: Software Components

### :one: Microcontroller Code 
<h5> i.e. The stuff that runs on the board</h5>

- Connect your MSP (or whatever board you have) to the computer where you will building the code from
- Ensure you are able to communicate with your USB-connected device via serial (baud 9600)
  - [Helpful Resource](https://learn.sparkfun.com/tutorials/terminal-basics/connecting-to-your-device)
- Open a VSCode Window, if you have the PlatformIO plugin you should be able to see it on the left navigation bar
  - Click the Icon, it should take you to the PlatformIO splash screen, also known as "PIO HOME"
- Select the "Open a Project" option
- Navigate to the root of the downloaded Github repo
  - Select the platformIO folder, then select the VETCON folder
  - Click "open" to finalize your selection
- Click the extension icon again
- Select the "Build and Monitor" option on the left navigation bar of the PlatformIO extension
- Follow the provided prompts
  
:star2: SUCCESS! :star2:
You have now succesfully built the MCU code and are now monitoring your dev board via serial!
Interact with the "Shell" and navigate the program


### :two: Game 1
<h5> Dino Run </h5>

- Navigate to the [dino_run](../minigames/dino_run/) folder
- Install the package dependencies via NPM ``` npm install ``` or Yarn ``` yarn install ```
- View options available via npm by typing it into your terminal ``` npm run``` or ``` yarn run```
- Run the game locally via ```npm run serve``` or ```npm run start``` or the equivalent with ``` yarn ```
- Navigate to the proper localhost port
- Play the game :)

:star2: SUCCESS! :star2:
You have now succesfully built the dino run code!

### :three: Game 2
<h5> Coin Flip </h5>

- Navigate to the [coin_flip](../minigames/coin_flip) folder
- Launch the .HTML file
- Voila!

:star2: SUCCESS! :star2:
You have now succesfully built the coin flip code!

### :four: Game 3
<h5> Text-based Adventure</h5>

- Navigate to the [text_based](../mingames/text_based) folder
- Run the "make" bash script to trigger the CMake Build Rules ``` ./make ```
- Run the built game ``` ./game ```
- Play the game
- Cleanup when finished using the "clean" script ```./clean```

:star2: SUCCESS! :star2:
You have now succesfully built the text based code!

## :hammer: Hardware Components

### :one: PCB Schematics
- Navigate to the [pcb](../pcb/) folder in the root of the repository
- Open the .PRO file with KiCad
- Select from any of the options presented (PCB Viewer, Schematic Viewer, Footprint Viewer, etc.)

### :two: Fabrication Files
- Within the pcb folder, navigate to the [fab_files](../pcb/fab_files/) folder
- View/Open the Gerber (.gbr) or Drill (.drl) files with your eCAD software of choice


## :memo: Some Notes
If you'd like to continue this project, you might want to [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) OR [duplicate](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) this repository rather than attempting to push your own commits/do a pull request. This way, you get to have as much creative freedom with the code as you desire (obviously respecting the GNU GPL v3 license).

We intend to keep this repo as-is in a "finished" state. 

If you do have any questions, or make any cool developments/improvements that you would like to let us know about! Feel free to shoot us an email with the header: [GH EC463] + your name - {subject}

Happy hunting :)