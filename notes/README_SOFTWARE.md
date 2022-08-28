<div align=center>
<h1> :skull: VETCON BADGE :skull: <br/>
SOFTWARE GUIDE </h1>
<h3> For other manuals, please view the following: </h3>
<h4>
<h4>
    <a href="./README_Engineering.md">Engineering Guide</a>
  <span> · </span>
    <a href="./README_HARDWARE.md">Hardware Guide</a>
</h4>

</div>


# :notebook_with_decorative_cover: Table of Contents
- [:notebook_with_decorative_cover: Table of Contents](#notebook_with_decorative_cover-table-of-contents)
  - [:star: About this Guide](#star-about-this-guide)
  - [:computer: Software Components](#computer-software-components)
    - [:one: Microcontroller Code](#one-microcontroller-code)
      - [:gear: Compilation](#gear-compilation)
      - [:gear: Function](#gear-function)
      - [:radio: Bluetooth](#radio-bluetooth)
    - [:two: Game 1](#two-game-1)
      - [:gear: Deployment](#gear-deployment)
      - [:gear: Interaction](#gear-interaction)
    - [:three: Game 2](#three-game-2)
      - [:gear: Compliation](#gear)
      - [:gear: Deployment](#gear-deployment-1)
      - [:gear: Interaction](#gear-interaction-1)
    - [:four: Game 3](#four-game-3)
      - [:gear: Compilation](#gear-compilation-1)
      - [:gear: Deployment](#gear-deployment-2)
      - [:gear: Interaction](#gear-interaction-2)
  - [:memo: Some Notes](#memo-some-notes)

## :star: About this Guide
<h5> THIS GUIDE IS A DETAILED OVERVIEW OF OUR PROJECT'S SOFTWARE IMPLEMENTATION AND DEPLOYMENT </h5>

## :computer: Software Components

### :one: Microcontroller Code 
<h5> <b>MSP430-FR2433 Chip Code</b> </h5>

#### :gear: Compilation
 
Compilation of the original source code (<code>EC463/src/VETCON/src/main.cpp</code>) is done through PlatformIO, a platform that interacts with the Wiring Framework to allow developers to use the Arduino format standard for any number of microcontrollers. 

Following the execution of a PlatformIO Build, a <code>firmware.elf</code> file is generated in the <code>.pio/$(PLATFORM_NAME)/ </code> folder of the project directory, which contains all of the linked firmware to be flashed to the board. 

This <code>firmware.elf</code> file is to be distributed to end users of the board, attending DEFCON, as a way to reflash their board in the situation where the board memory becomes corrupted. To reflash the board with the <code>firmware.elf</code>, one can use UniFlash, locate the board as a serial interface and then place in the location of the <code>firmware.elf</code> file, wherever the user has determined to store it.

To refer to the PlatformIO upload/debug tool, please refer to the [Quick Start Guide](./README_Engineering.md)


#### :gear: Function

The MCU (Micro Controller Unit) code controls all of the on-board hardware, including the LEDs, buttons, LCD Screen, and the Bluetooth module (discussed in the following section in detail), as well as provides the user interaction methods by way of serial communication channels. 

The board can be interfaced with by way of buttons, but not in any useful way without a serial channel being opened up between a host and the board. Be sure to use a serial communication program that has implicit line endings, as otherwise formatting will be off. 

Once a user does plug in the board and open up a serial connection, they will need to be sure to kill the UniFlash process, as it takes up the board communication channel, and  do a soft reset of the board to make sure it sends out the "WELCOME TO VETCON" message (only on the first run), as well as the main menu. The main menu contains all of the options for user interaction: 

- <code>1. Set Name Tag</code>
- <code>2. Display Name Tag</code>
- <code>3. Game Link</code>
- <code>4. Game Link 2</code>
- <code>8. Start Bluetooth</code>
- <code>0. Reset Badge</code>

The list of possible inputs can expand over time, though, with the final menu being displayed as:

- <code>1. Set Name Tag</code>
- <code>2. Display Name Tag</code>
- <code>3. Game Link</code>
- <code>4. Game Link 2</code>
- <code>5. Secret Token</code>
- <code>6. Secret Token 2</code>
- <code>7. Secret Token 3</code>
- <code>8. Start Bluetooth</code>
- <code>9. LED CNTRL Menu</code>
- <code>0. Reset Badge</code>

These new options are revealed to the user through input of the secret codes, acquired through completion of the online games (discussed later in full). 

These codes are obfuscated when presented to the user, but here they are  translated, the exact encryption and decryption method for each code will be discussed in their corresponding game. The plaintext secret codes are as follows:

- <code>Game 1: "1016"</code> 
  - <code>Unlocks: "6. Secret Token 2"</code> 
- <code>Game 2: "semperdisco"</code> 
  - <code>Unlocks: "7. Secret Token 3"</code> 
- <code>Game 3: "ilovevetcon"</code>

The process to begin inputting these secret codes is for the user to input: <code>9</code> to the initial menu. 

As the user inputs these secret codes into the device, external LEDs are lit in accordance with each unlocked secret, these are more aptly described in <code>README_HARDWARE.md</code>. 

Once all of the secrets have been unlocked, option <code>9. LED CNTRL Menu</code> is unlocked, allowing the user to choose the LED states to save power if they decide that is necessary. 

To control the LEDs, the user enters option <code>9. LED CNTRL Menu</code>, where they will be taken to the LED control menu, where they are presented with the following input options:

-   <code>1: Turn LEDs OFF</code>
    -   This places the MSP in a hibernate low-power state, which can be exited by toggling the "reset" button on the board itself
-   <code>2: LED 'WAVE'</code>
-   <code>3: LED 'BLINK'</code>
-   <code>4: LED 'ALTERNATE'</code>
-   <code>5: Back 2 Main Menu</code>

#### :radio: Bluetooth

Bluetooth functionality is relatively simple. By selecting option 8 from the main menu the user will enter the bluetooth() function. This will prompt them with the option to type 1 for communication, or type 2 to setup the parent and child connection. NOTE[The EN switch pin needs to be on for option 2, the parent/child connection to function properly. Similarliy, while it is on, option 1 for regular communication will not function properly: Please see hardware explanation for more info]
    
If two badges have already been paried, then selecting option 1 will allow the user to type data in serial [up to 15 characters]. This will then send the data to the paired badge which they can see on their menu "Data Received: "and respond back with their own message. 
    
How to pair badges: Your badge will come with your HC-05's hex address. While the EN pin is switched selecting option 2 from the menu will prompt the user to type certain commands into serial. These commands will be sent to the HC-05 through software serial which is currently in AT mode (a mode that allows for command acception). First the user can type either "AT+ROLE=0" for child or "AT+ROLE=1" for parent. If choosing child, the user is done. They can switch off the enable pin and wait for a connection. If choosing parent, the user will also have to type "AT+BIND=" and then include the hex address of the child badge they want to connect to. Once this step is complete, they can also switch off their EN pin and communicate through option 1 with the child. 
    
To exit the bluetooth menu and return, the user is always prompted to type "exitnowpls". Typing this command the software will kick them back to the main menu function. 

### :two: Game 1
<h5> Dino Run </h5>

Dino Run, at it's core, is a Phaser.IO Game that is compiled on-browser using Babel and Webpack. It leverages a ton of assets but is fairly simple at it's core. In fact, most of the game logic is located inside the [Playscene.JS](../minigames/dino_run/src/scripts/PlayScene.js) file and can be manipulated with just a few variables.

#### :gear: Compilation
- Navigate to the [dino_run](../minigames/dino_run/) folder
- Install the package dependencies via NPM ``` npm install ``` or Yarn ``` yarn install ```
- View options available via npm by typing it into your terminal ``` npm run``` or ``` yarn run```
- Run the game locally via ```npm run serve``` or ```npm run start``` or the equivalent with ``` yarn ```
- Navigate to the proper localhost port
- Play the game

#### :gear: Deployment

There are two ways to deploy this game. This step also assumes that you have run the game and built it using:
``` npm run bundle ```
``` npm run build ```

The first is to deploy it locally/on a remote server on a dedicated port that is "open".
This method assumes that you have your networking rules set up to accept incoming connections, etc.
- Navigate to the [dino_run](../minigames/dino_run/) folder
- Run the game locally via ```npm run serve```
- Take note of the port the process is running on. 

The second method involves the use of [Github Pages Deployment](https://pages.github.com/), and assumes you have the Dino Run code in it's own, separate repository:
- Create a new orphaned branch, named gh-pages, and nuke it of all files
  - ```git checkout --orphan gh-pages ```
  - ``` git rm -rf . ```
- "Save" your changes by pushing up this now-empty branch
- Switch back to main!
- Push the contents of the [dist](../minigames/dino_run/dist/) folder to the gh-pages branch
  - ``` git subtree push --prefix=dist origin gh-pages ```
- Enable the Github Pages Deployment feature, select gh-pages as your deployment branch.
- Visit your webpage at the URL provided by GH Page
[If you're getting confused about subtrees, here's a quick pointer](https://gist.github.com/cobyism/4730490)


#### :gear: Interaction
The purpose of this game is to understand how to leverage built-in Web Consoles to your advantage.

Websites are *never* bulletproof. No matter how locked down they seem to be, something can always slip through the cracks. One look at Google Chrome's [CVE](https://www.cvedetails.com/vulnerability-list/vendor_id-1224/product_id-15031/opec-1/Google-Chrome.html) list should be enough evidence to convince anyone.

As a result, Websites can be expolited in a variety of manners, with the easiest/simplest being the Web console. 

Why? Because it is one of the main debugging tools used by Web Developers to diagnose/debug web applications as they are "running". Because of this, many debug/error messages are often printed to the console.log(), and therefore we can simulatenously access the console and attempt to uncover more data than intended.

Advanced Console logging permits the use of many popular [web exploits](https://hurricanelabs.com/blog/console-wars-part-1-hacks-for-hackers/), such as:
<span> :one: </span> [SQL Injection](https://hurricanelabs.com/blog/console-wars-part-2-sql-injection/) <span> :two: </span> [Tracing Function/Stack Calls](https://developer.mozilla.org/en-US/docs/Web/API/console/trace) <span> :three: </span> [RCE with Eval ](https://medium.com/r3d-buck3t/eval-console-log-rce-warning-be68e92c3090)

To play the game, press spacebar to jump and the "down" key on your keyboard to duck. Seriously, it's Dino Run.

Once you reach score '1016', a cipher will be printed to the console log. 

1016 -- the number of the address of T. Anthony's Pizzeria on BU's Campus. 1016 Commonwealth Ave.

XOR Hashing the cipher with 'pizzatime' will give a clue as to what the plaintext secret actually is. 'pizzatimetanthony' will give the player the entire plaintext. Entering this plaintext will allow the user to advance further on the MSP.

### :three: Game 2
<h5> Coin Flip </h5>

The source for Game 2 can be found in:
- <a href="../minigames/coin_flip"> Minigames Folder </a>

Game 2 is fairly simple in construction and execution. At it's core, it is an .HTML file with some Vanilla-Javascript addons, which we will briefly describe in a moment.

The most important code snippets are the following, which are all explained in a high-level in [Interaction](#gear-interaction-1)

First, is the basic HTML syntax responsible for the "flip" animation
```
@keyframes spin-tails {
  0% {
  transform: rotateX(0);
  }

  100% {
  transform: rotateX(1980deg);
  }
}

@keyframes spin-heads {
  0% {
  transform: rotateX(0);
  }

  100% {
  transform: rotateX(2160deg);
  }
}
```
Next, are the 'set' and 'get' and 'delete' functions for cookies.

```
function getCookie(name) {
    return (name = (document.cookie + ';').match(new RegExp(name + '=.*;'))) && name[0].split(/=|;/)[1];
}

function setCookie(name, value, days) {
    if (getCookie(name)) {
        if (value = ! "") {
            return;
        }
    }
    else {
        var e = new Date;
        e.setDate(e.getDate() + (days || 365));
        document.cookie = name + "=" + value + ';expires=' + e.toUTCString() + ';path=/;domain=.' + document.domain + "; Secure";
    }
}

function deleteCookie(name) {
        setCookie(name, "", -1);
}
```

Finally, the event listener for the button presses

```
flipBtn.addEventListener("click", () => {
          let i = Math.floor(Math.random() * 2);
          coin.style.animation = "none";
          if (i) {
              setTimeout(function () {
                  coin.style.animation = "spin-heads 3s forwards";
              }, 100);
              heads++;

              if (getRandomInt(1, 2) == 1) {
                  if (!getCookie("tails")) {

                      setCookie("heads", "4315323515421424431334", 30)
                  }
              }

          }
          else {
              setTimeout(function () {
                  coin.style.animation = "spin-tails 3s forwards";
              }, 100);
              tails++;

              if (getRandomInt(1, 2) == 2) {
                  if (!getCookie("heads")) {

                      setCookie("tails", "3411323115333443242344234424521532244442453454141544431152543131111542453454", 30)
                  }
              }

          }
          setTimeout(updateStats, 3000);
          disableButton();
});
```

#### :gear: Compilation
Because .HTML is, in essence, a *markup languge* and Javascript is a *scripting language* for web pages (written in markup languages), there is no compilation in the traditional sense (aka Java, C-family languages, Rust, Go, Swift, etc.)

A full explanation of how the HTML script is converted into bytes, the creation of the Document-Object-Model (DOM), and Javascript's interaction with the DOM, can be found here (kind of optional)
  - <a href="https://blog.logrocket.com/how-browser-rendering-works-behind-scenes/"> Browser Rendering </a>

So, all in all, to "compile" our game, just have a modern browser on hand, and double click the .HTML file located in the folder. To view the source, open the file with a text editor/IDE of your choice.

#### :gear: Deployment
If you've read through the tutorial for Game 1's deployment, you should already understand how web-deployment of this app (specifically through Github Pages) works. <a href = "https://pages.github.com/"> Here's a quick Github Pages Reference </a> if you're unsure or have not seen it before. Other alternatives include hosting your webpage locally/on a fileserver using <a href = "https://www.nginx.com/">NGINX</a> or <a href = "https://httpd.apache.org/">Apache</a>

Briefly, deployment of Game 2 is as simple as the following steps:
- Create a new repository.
- Push the .HTML file to the repository, ensure it is the only file in the repository, and it is at the root of the repository.
- Enable the Github Pages Deployment feature.
- Visit your webpage at the URL provided by GH Pages

#### :gear: Interaction
The purpose of this game is to understand how to leverage cached website/web-app data (in the form of cookies) to your advantage.

Cookies are basically just strings of text that are cached locally on your browser. They're convenient pieces of data sent to your browser by websites to "cache" inputs, session logins, etc. Think of it as "persistent state" within webpages (otherwise, webpages would have a hard time knowing you visted their site and performed X actions).

The caveat here is that any sensitive/unsecured data stored in a cookie can be compromised and leveraged for potential malicious exploits. Here are some samples of popular exploits:
<span> :one: </span> [Session Hijacking](https://www.thesslstore.com/blog/the-ultimate-guide-to-session-hijacking-aka-cookie-hijacking/) <span> :two: </span> [Session Donation](https://defcon.org/images/defcon-17/dc-17-presentations/defcon-17-alek_amrani-session_donation.pdf) <span> :three: </span> [Session Fixation](https://owasp.org/www-community/attacks/Session_fixation)

With that being said, the intent behind this game is to have users "snoop around" and attempt to manually extract their session data to advance on the MSP. At some point, there will be a cookie that stores the *correct* cipher text

To play the game, you flip the coin. The coin will land on either heads or tails.

Upon first glance, it seems as though nothing happens, but further inspection of the source code says otherwise.

Basically, on each button click, there is an event listener that determines whether or not a cookie is cached locally. On each click, there is a 50% chance that a cookie is cached, meaning that it is more than possible that *no* cookies are cached upon button click.

From there, there are different cookies cached depending on the state of the coin. The cookie that is cached on "heads" is a different cookie that is cached on "tails". 

Heads stores the correct cipher. Tails stores the incorrect one.

However, due to the nature of the game, most player will not recognize this. This is because once a cookie is cached locally, no more cookies can be allocated, meaning that continued "clicks" will yield no results, convincing the player that *their* cookies is the correct one. If a player is savvy enough, they will clear their cache and attempt again.

Entry of the incorrect code on the MSP will wipe the board. Entry of the correct code will grant them access to the next challenge.

Future iterations of this game could potentially leverage the use of [Babel](https://babeljs.io/) and [Webpack](https://webpack.js.org/) to ["compile"](https://dev.to/getd/wtf-are-babel-and-webpack-explained-in-2-mins-43be) and [obfusticate](https://www.npmjs.com/package/webpack-obfuscator) the embedded JS within the HTML file. Right now, anyone clever enough can inspect the webpage and go straight to the ciphers with relative ease.

### :four: Game 3
<h5> Text-Based Adventure</h5>

The source for Game 3 can be found in the [minigames](../minigames/) folder.

There really is no "purpose" to this game. The idea behind this was to reward users for getting this far with a fun, early-90s style text-based adventure.

Running the game is another question, however. Compiled binaries for a variety of operating systems should be hosted on a remote fileserver/git repo, and players should be able to figure out which binary is compatible with their host system. Once that is all settled, they should be able to play the game with no issue.

#### :gear: Compilation

- Navigate to the [text_based](../mingames/text_based) folder
- Run the "make" bash script to trigger the CMake Build Rules ``` ./make ```
- Run the built game ``` ./game ```
- Play the game
- Cleanup when finished using the "clean" script ```./clean```

#### :gear: Interaction

The game is set up similar to old-school text based adventures. Players must juggle 4 states (money, health, grades, social) and make it through 50 days as a BU student. Options will affect stats. 

If a stat goes below 0, you fail, if it goes above 200, you also fail.

Good luck! 

## :memo: Some Notes
If you'd like to continue this project, you might want to [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) OR [duplicate](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) this repository rather than attempting to push your own commits/do a pull request. This way, you get to have as much creative freedom with the code as you desire (obviously respecting the GNU GPL v3 license).

We intend to keep this repo as-is in a "finished" state. 

If you do have any questions, or make any cool developments/improvements that you would like to let us know about! Feel free to shoot us an email with the header: [GH EC463] + your name - {subject}

Happy hunting :)
