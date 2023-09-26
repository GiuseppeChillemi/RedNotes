# TUI Notes

Notes about Red Text User Interface



## The "Terminal" backend



TUI is the new backend of [Red](https://github.com/red/red), our fantastic coding language. With it you can now create beautiful text intefaces to be used on Window or a Linux console or other shells on different OS. Those interfaces where the only way to use computers in the [DOS](https://en.wikipedia.org/wiki/DOS) and [Unix](https://en.wikipedia.org/wiki/Unix) era. Also, text interfaces were the foundation of the first interconnected devices, when [BBS](https://en.wikipedia.org/wiki/Bulletin_board_system)  run on dialup lines and you access via modem and [VT100](https://en.wikipedia.org/wiki/VT100) like terminals but all system still supports them.



Here are some examples of textual intefaces from TUI



![image-20230915025049476](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025049476_1694740249..png)



![iAvEIaHuUt](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/iAvEIaHuUt_1694740678..png)



![7EoEBXoJDF](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/7EoEBXoJDF_1694740299..png)

You can even create games with it!

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025338827_1694740308..png" alt="image-20230915025338827" style="zoom: 50%;" />

And show images with a single command

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230917172117933.png" alt="image-20230917172117933" style="zoom:67%;" />



## Prerequisites before continuing

You should know 

[Red](https://www.red-lang.org/), a fantastic programming language

[VID](https://github.com/red/docs/blob/master/en/gui.adoc), the Visual Inteface Dialect, which red uses to build visual interfaces

### Installing and running Red TUI

To use TUI you must first download Red TUI branch from GitHub using this [link](https://github.com/red/red/tree/TUI), as this branch has not been merged at the moment

You need compile Red using [Rebol,](http://www.rebol.com) the ancestor of Red. Download it from the site www.rebol.com . Then click on *Get-It*

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025439999_1694740315..png" alt="image-20230915025439999" style="zoom: 67%;" />



Now choose the version to download most suitable from your platform. 

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916025433761.png" alt="image-20230916025433761" style="zoom: 67%;" />







Once downloaded, store Rebol in the same directory where the Red one is located (but not inside of it!)



![image-20230916144344021](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916144344021.png)

Before continuing you need to modify the header of the file `console.red` in the Red folder. (This until TUI will be officially merged into Red Master)



![image-20230916144546394](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916144546394.png)

`red/environment/console/cli/console.red`

You can use Notepad on windows to change `console.red` from this

```
Red [
	Title:	"Red console"
	Author: ["Nenad Rakocevic" "Kaj de Vos"]
	File: 	%console.red
	Tabs: 	4
	Needs:	[JSON CSV]
	Rights: "Copyright (C) 2012-2018 Red Foundation. All rights reserved."
	License: {
		Distributed under the Boost Software License, Version 1.0.
		See https://github.com/red/red/blob/master/BSL-License.txt
	}
]

```

to this:

```
Red [
	Title:	"Red console"
	Author: ["Nenad Rakocevic" "Kaj de Vos"]
	File: 	%console.red
	Tabs: 	4
	Needs:	[JSON CSV VIEW]  ;<<<<----------------
	Config: [GUI-engine: 'terminal]  ;<<<<---------------
	Rights: "Copyright (C) 2012-2018 Red Foundation. All rights reserved."
	License: {
		Distributed under the Boost Software License, Version 1.0.
		See https://github.com/red/red/blob/master/BSL-License.txt
	}
]
```

Note the `Config:` line and the adding of `VIEW` to `Needs:` 

(Remove the arrows and the semicolon `;` in the saved file, they are here as comments to show the correct position but they are unuseful in the final file.

### Compiling

Now you are ready to compile TUI !


Run Rebol and enter this command in the console: 

`do/args %red/red.r "-r -t MSDOS %red/environment/console/cli/console.red"`

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025821887_1694740328..png" alt="image-20230915025821887" style="zoom:67%;" />

If everything has been done properly, you will find the file `console.exe` (an executable) in the same directory where Rebol il located

![image-20230916145215199](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916145215199.png)

Now you are ready to go! Open the red console and run your first commands.

This guide presumes you are familiar with Red language, if you are not, learn it, you won't regreet.

## Running the examples

If you are familiar with Red, skip this section.

For new users, Red code can be written in the console when short



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916150039485.png" alt="image-20230916150039485" style="zoom: 67%;" />



 Otherwise you need an editor like Notepad (build in in windows), Notepad+, VScode, UltraEdit. The first examples are concise and can be written in the console without using them but longer needs to be written with a good coding instrument and stored in a file.



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916150334662.png" alt="image-20230916150334662" style="zoom:80%;" />

Modern editors provide syntax highlighting of the code so it is easier to read (even for 2 decades we have lived without this!). If you want to use them, store in directory named `scripts` or `code` (or anything you want) and run the test as follow:



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916150702596.png" alt="image-20230916150702596" style="zoom: 80%;" />



## Using Tui

### For new users

If you have never used VID, it is a GUI description language (a dialect of Red). With few words you are able to build complete interfaces using natural sounding sequence of commands.  Each visual elements is built on top of an inner structure called `face` that is created when you ask VIEW to interpret you textual description. 

### For experienced users

If you know View and VID, using TUI a breeze as the same concept applies. Widgets, are just textual but each one is a `face` as usual, have `facets` and `events. ` A subset of the VID keywords are available for TUI:  like `TEXT`, `BUTTON`, `TEXT-LIST`, `PANEL...`(full list ahead)

The output is arranged in columns so `face/offset` returns `integer` and not `float!`

The origin of the screen are `0x0` (X, Y)  

### Now we can start

Lets create our first Textual GUI, run the console and write:

```
View/tight [
	Text "Hello TUI!" 10x1 font-color green
]
```

The you will see this:

![image-20230915030028965](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030028965_1694740335..png)

This is your first textual interface. You have asked Red to `VIEW` a GUI made of  the `TEXT` "Hello TUI!" display it on `1` line of `10` caracters with `10x1` (HxV `PAIR!`) with a ``green` `font-color`. Easy, isn't it!?



You can even set a different background writing 

```
View/tight [
	Text "Hello TUI!" 10x1 red font-color green
]
```

![image-20230915030139337](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030139337_1694740393..png)

Now lets try to see what happens if you don't express the size of the text removing `10x1`

```
View/tight [
	Text "Hello TUI!" red font-color green
]
```

...The backgroud color will fill all the surrounding area up to the default size the VID creator has hardcoded into the language, so it is important to set a size as `HxV` pair if you don't want to fill the whole GUI with you choosen color!

 

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030217359_1694740404..png" alt="image-20230915030217359" style="zoom: 50%;" />

### Giving the GUI elements a name

As written before, every GUI element you have created is build on top of a `face` 

The `face` word can be used to access the inner values of the widget like `face/size` or `face/text` but you can do this only from the inner block of code following each widget definition.

Otherwise, if you need to access another face from the inside of a widget you must ask to the `VID` engine to assign a name. This is needed if you want to later view or modify things.

To do this, simply add the name you want to give to the `face` object before its description as follow:

```
View/tight [
	txt: Text "Hello TUI!" red font-color green
]
```

Do you see  `TXT:` ? Now if you want to access this GUI element you can do this from everywhere. If you need to change the text, simply write:  `TXT/text: "My new text"`

  

### Adding buttons

Having 2 clickable text buttons is as simple as writing `Button "Press Me"` inside the description block.

Let's add 2 buttons under the "Hello TUI!" text:

![image-20230915030913239](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030913239_1694740426..png)

We have used the previous script to do this, adding some parts. `return` and `pad` and `[unview]`will be explained later, you just need to concentrate on the `button` lines 

```
View/tight [
	txt: Text "Hello TUI!" 10x1 red font-color green
	return
	pad 0x2
	Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
	pad 10x0
	Button "Quit" 8x1 [unview]   
]
```

If after a description of a GUI element you add a block `[<code here>]`, it is executed when the default event associated with it is triggered. In this case, if the end user hits `enter` on the keyboard, the code is run if it exists.

In TUI you move from a gui element to another pressing `TAB` and you click the button hitting `ENTER`

**Let's try it!**

Now run the code and use TAB to alternate between "Press Me" and "Quit". Choose "Press Me" and hit return to see what happens.... 

... Have you seen a change on "Hello TUI?" If so, it's perfect! Everything is working as expected

If you press `Quit` the `UNVIEW` command is executed and the last open text "window" is closed



Feel free to experiment with above code changing the text, color or adding another button

### VIEW

To display the GUI, everything you need is the command `VIEW` followed by a block

`VIEW` has a new keyword: `tight` , it is used to instruct the GUI system to have no margins.

```
VIEW/Tight [
   >GUI here<
]
```

If you don't need to display the GUI immediately and select later from a set of GUIs PAGES you need to use LAYOUT for this.

### Creating the GUI: Layout

VIEW is a command that displays a group of GUI objects. It calls the `layout` command that creates them. You can multiple of such object by hand and display them on screen on request.

 ```
 page-1: layout/tight [
 	Button "Turn On Light" 10x1 green font-color yellow [<Do something here>]
 ]
 
 page-0: layout/tight [
 	Text "Another screen" 20x1
 	Button "Switch off Light" 10x1 red font-color yellow [<Do something here>]
 ]
 
 View page-0
 ```



The `layout` command processes the block and creates a graphical object with all the GUI elements of both screens. As seen for faces, you can give a name to the layouts writing `page-0:` or `page-1:`. You can later choose which one to display using `view screen1` or `view screen2` (without colon)



### Panels and positioning

VID let you use rectangular containers to group gui elements. Each container has its own life inside a window and moving it you move all the elements inside of it. To create a container is as simple as writing `panel [>gui elements here< ]`

You can even better express a dimension:

`panel 30x20 [>gui elements here< ]`

Here is an example:

```
View/tight [
	
	panel 30x20 [
		txt: Text "Panel One!" 14x1 red font-color green
        return
        pad 0x2
        Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
        pad 10x0
        Button "Quit" 8x1 [unview]   
	]
	
	;return
	
	panel 30x20 [
		txt: Text "Another PANEL!" 14x1 red font-color blue
        return
        pad 0x2
        Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
        pad 10x0
        Button "Quit" 8x1 [unview]   
	]
	
]
```

Try it and keep an eyer to the `return` keyword.

This is the result.  Press TAB to navigate and ENTER to select someting

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916173648281.png" alt="image-20230916173648281" style="zoom:67%;" />

Red VID has created 2 rectangular panels and each element is drawn relative to it. You only need to uncomment the `return` command to change everything. Just remove the `semicolon` tun the code again.

 

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916173813107.png" alt="image-20230916173813107" style="zoom:67%;" />

By default, Red adds GUI elements from left to right, when it encounters `return` as a word processor (in 1980 I would have used the term "typewriter!") , it continues in a newline and resets its position continuing from the far left. If the previous elements have a maximum eight of 20 lines, then it starts drawing from line 21 (if there is no `PAD`ing or margins) (TBD: verify this affirmation)

This working is regulated by the word `ACROSS` which you don't see but it is implicit when the GUI is built.

You have the same effect starting the description of the interface in this way:

```
View/tight [

	across
	
	panel 30x20 [
		txt: Text "Panel One!" 14x1 red font-color green
		...
		...
```



The other available mode is BELOW. It acts in the opposite way: you draw from TOP to BOTTOM: 

Try it by yourself:



```
View/tight [

	below; <<<<<---- Note this difference
	
	panel 30x20 [
		txt: Text "Panel One!" 14x1 red font-color green
        return
        pad 0x2
        Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
        pad 10x0
        Button "Quit" 8x1 [unview]   
	]
	
	;return
	
	panel 30x20 [
		txt: Text "Another PANEL!" 14x1 red font-color blue
        return
        pad 0x2
        Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
        pad 10x0
        Button "Quit" 8x1 [unview]   
	]
	
]
```





The result is the same as using `ACROSSS` and `RETURN`



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916173813107.png" alt="image-20230916173813107" style="zoom:67%;" />



Now uncomment  `return` in the middle:



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916173648281.png" alt="image-20230916173648281" style="zoom:67%;" />

And you have the same result of the first code written for panels!



### Table of supported widgets (TBD add images)

This is a list all the widgets implemented in RED TUI (as of 16/09/2023 (DD/MM/YYYY))

| Widget name | Description                                                  |
| :---------- | ------------------------------------------------------------ |
| button      | A cliccable button on screen                                 |
| field       | A rectangle that can be used to enter text                   |
| progress    | Progress bar                                                 |
| rich-text   | Draw text with different colors and styles                   |
| text        | Simple text on screen                                        |
| text-list   | List of of elements you can navigate with cursors and choose |
| base        | a rectangle with wrappable text inside                       |
| Panel       | a container for all the above elements                       |
|             |                                                              |
|             |                                                              |

(For an up to date list consult this [github repository directory](https://github.com/red/red/tree/TUI/modules/view/backends/terminal/widgets))

### The coordinate system

The `VIEW` engine has a coordinate system that range from `0x0` to infinite. They rapresents horizontal lines and columns. They are expressed as `HxY` pair. This origin corresponds to the upper left angle of the console, where is printed the first character if you don't change this.





<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916180550535.png" alt="image-20230916180550535" style="zoom: 67%;" />

(TBD: View if you can change the origin)

#### Characters size

Normal character occupy `1x1` blocks of screen.

Emoji needs `2x1` blocks of screen. 

When you draw a `text`, if you use one or more emoji you should add 2 characters in `text` length for each emoticon used.

#### VID Positioning keywords

To govern the positioning of GUI elements, other commands  are available in VID. You have already encountered `return` but there are a lot more.



| Widget     | Arguments | Description                             |
| ---------- | --------- | --------------------------------------- |
| origin     |           | Set the origin of the coordinate system |
| pad        | 1x0       |                                         |
|            |           |                                         |
| origin     | 1x2       | TBD: `/origin facet`                    |
| space  (?) | 1x2       |                                         |
| return     |           |                                         |
| window?    |           |                                         |

TBD: test if `offset` exists

### Events

When you display a GUI, a lot of events happens, either internally or caused by the user. As an example, when you show a button, the system start waiting for someone pressing `ENTER` on the text button. When such input is received, the default event is triggered. Look at thhe "Hello TUI" code:



```
View/tight [
	txt: Text "Hello TUI!" 10x1 red font-color green
	return
	pad 0x2
	Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
	pad 10x0
	Button "Quit" 8x1 [unview]   
]
```



The line that describes the button ends with code inside square brackets.

```
Button "Press Me" 8x1 blue [txt/text: "Pressed!" Txt/font/color: white]
```

This is the code executed when the user hits `enter`

`Button` has another event you can use: `on-dbl-click` . This is triggered when the user hits 2 times consecutively the button when it has focus. To configure it add its name after the first code block and then the code to execute



```
Button "Press Me" 8x1 blue [
		txt/text: "Pressed!" Txt/font/color: white
	] on-dbl-click [
		txt/text: "2 Times!" Txt/font/color: white	
	]
```

(TBD: review indenting stule)

Inner events are those triggered by something from the inside of Red interpreter or the OS. For example, if you add the keyword `RATE` to a widget followed by a `number`, the `on-time` event will execute your code `number` of times per second. Think about a text which changes its color 2 times a second. You just need to write only 

```
view/tight [
	text "Rainbow" font-color red 10x1 rate 10 on-time [
		face/font/color: random white ;Here you set the color
		face/text: "Rainbow"	;here you rewrite the text with the new color
	]
] 
```

A lot more events are available

| Event           |      |                                      |
| --------------- | ---- | ------------------------------------ |
| on-event        |      |                                      |
| on-over         |      | event/offset <br />event/flags       |
| on-down         |      | event/offset                         |
| on-up           |      | event/offset                         |
| on-mid-down     |      | event/offset                         |
| on-mid-up       |      | event/offset                         |
| on-alt-down     |      | event/offset                         |
| on-alt-up       |      | event/offset                         |
| on-wheel        |      | mold event/picked <br />event/offset |
| on-dbl-click    |      |                                      |
|                 |      |                                      |
| `on-time`(?)    |      |                                      |
| `on-create`(?)  |      |                                      |
| `on-created`(?) |      |                                      |

### Facets

Each `face` has a set of attributes. When you describe the GUI and VID interprets it, each face created is an object and each object has a set attributes with their value.

To analyze how a face is composed you need to create the GUI but you should not display it. To do this you must use the command `layout` instead of `view`. View calls layout and then display the GUI, `layout` just create the faces as described from the VID block. 

Let's create a simple `text` widget called TXT.  Enter the following code in the console.

```
layout/tight [
	txt: text "Hello" green 10x1
]
```

Once you create it, you still have the cursor control. As we have given the name `TXT` to the `face`, we can display the its content in the console writing `probe txt`



![image-20230917005644829](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230917005644829.png) 



It will appear the printout of an object with all its members and values. Those members are called FACETS and their content depends from the parameters used to describe it and from the engine itself.

I have omitted the contant of `parent` and `pane` facets for readability. They will be addressed later.

```
make object! [
    type: 'text
    offset: 0x0
    size: 10x1
    text: "Hello"
    image: none
    color: 0.255.0
    menu: none
    data: none
    enabled?: true
    visible?: true
    selected: none
    flags: none
    options: [style: text vid-align: top at-offset: none]
    parent: make object! [>omitted<]
    pane: none
    state: none
    rate: none
    edge: none
    para: none
    font: none
    actors: none
    extra: none
    draw: none
]
```

Some facets are used to connect faces, other reflects the value you have entered in the description.

Take a look at `text` facets. It contains the  `"Hello"` string; the `size` is set to `10x1` and color 0.255.0 is the value of full GREEN. (Triplette is RGB 8 bit) .

Important mention to `parent` which has a backlink to the father object and `pane` that contain a links to the children the current object composed or is the container (a `panel` is such kind of face, it contains other faces in `pane` facet). They  are structural facets, they are needed to glue all the GUI parts.



We will go deeper later. Actually is important to note that in this backend, only the following non structural ones have been implemented.

| Facet      | Note                | Description                                                  |
| ---------- | ------------------- | ------------------------------------------------------------ |
| `size`     |                     | The size of widget as `integer`, `pair` or `point2d!`        |
| `offset`   |                     |                                                              |
| `color`    |                     |                                                              |
| `enabled?` |                     |                                                              |
| `visible?` |                     |                                                              |
| `text`     |                     |                                                              |
| `rate`     |                     | The number of times the on-time-event is triggered each second |
| `font`     | font/color only     |                                                              |
| `para`     |                     |                                                              |
| `data`     | progress, text-list |                                                              |
| `selected` | only text-list      | The line of the selected text                                |
| `draw`     | only TEXT           |                                                              |
|            |                     |                                                              |

Those not mentioned in the previous table are USER definible and they are result of internal VID operations and reflects internal states, flags...

### The DATA facet

Faces store their visible values in 2 containers: `text` and `data`. The latter is managed only on `progress` and `text-list` widget. (TBD: look for field...)

If you build a `text-list` with

```
layout/tight [mylist: text-list 10x5 data [blue mangenta yellow red brown blue]]
```

The `data` facet will contain that block of values.

Run the code and `probe` it

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230917012058089.png" alt="image-20230917012058089" style="zoom:67%;" />



### With

This is a special keyword. It must be followed by a `block` with a list of all the attributes you want to set and the code to generate the value. It can be a simple one or a complex computation.

```
layout/tight [
	mylist: text-list 10x5 with [data: load %alist.txt]
]
```

Instead of expressing the content of the `data` facet directly you `load` the content from a file. 

Not only data but many other user dependent facet can set inside the `with` block.

Note: when `with` block is executed, has not been set so you can't access it. 

(TBD: verify if previous faces are available)



## Widget documentation

### Text

Print a simple text on screen

```
view/tight [
	origin 3x3
	text "This is a simple text!" 25x1 font-color green 
]
```

![image-20230916020305663](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916020305663.png)



Special facet:

`text/font/color`

### Base

Display an area of text which can be automatically wrapped on the next line

```
view/tight [
	origin 3x3
	base 10x4 wrap middle "This is a text to show how base works" blue font-color white
]
```

![image-20230916021642869](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916021642869.png)

### Image

Red is capable of displaying images in the console.  It is sufficient to write a code like this:

```
view/tight [
	origin 3x3
	text 20x1 font-color green "A fantastic sunset" return
	image 60x30 %sunset.png
]
```



<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230917173257816.png" alt="image-20230917173257816" style="zoom:67%;" />

### Rich-Text

Display text with various colors or styles

```
view/tight [
	origin 3x3
	rich-text 40x2 transparent data [yellow "hello " green u "underline" /u ]
]
```

![image-20230916022056537](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916022056537.png)



You may use any of the following styles

| Activate          | Deactivate           | Description                                |
| ----------------- | -------------------- | ------------------------------------------ |
| b , bold , <b>    | /b, /bold, </b>      | **Bold** text                              |
| i, italic, <i>    | /i, /italic, </i>    | *Italic* text                              |
| u, underline, <u> | /u, /underline, </u> | <ins>underline</ins>                       |
| s, strike, <s>    | /s, /strike, </s>    | ~~strike~~                                 |
| f, font, <font>   | /f, /font, <font>    | TBD: ask                                   |
| bg, <bg>          | /bg, </bg>           | Example:<br />bg yellow<br /> TBD: to test |
|                   |                      | TBD: Ho to set Foreground one?             |

Example:

```
rich-text [>TBD:<]
```



### Progress

```

view/tight [
	origin 3x3
	text "Progress bars: " 25x1 font-color green return
	pad 0x1
	Progress 20x1 80% red return
	pad 0x1
	Progress 20x1 20% blue
]

```

![image-20230916020605989](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916020605989.png)

### Buttons

Display rectangular button. You can navigate from one to another using TAB. To press the button hit ENTER

```
view/tight [
	origin 3x3
	text "Hit a button: " 25x1 font-color green return
	pad 0x1
	button "click me" 20x1 [face/text: "Thank you"] 
	button "or click here" 20x1 [face/text: "Thank you again!"] 
]
```



![image-20230916025733616](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916025733616.png)



Special events:

```
on-dbl-click [face/text: "double click"] 
```



### Fields

Display an Horizontal rectangle you can use to enter text

```
view/tight [
	origin 3x3
	Text "Enter Text:" 10x1
	pad 2x0 
	Field 15x1  hint "xxxx xxxx xxxxx xxxx" red
]
```

![image-20230916020000100](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916020000100.png)

### text-list

Display a list of choices you can navigate with UP and DOWN cursor buttons, mouse wheel or click with your mouse or ENTER



```
view/tight [
	origin 3x3
	text "Please, select a color " 25x1 font-color green return
	pad 0x1
	text-list 13x5 select 2 data [
		"1 apple"
	    "2 orange"
	    "3 banana"
	    "4 grape"
	    "5 lychee"
	    "6 pear"
	    "7 watermelon"
	]
]
```

![image-20230916021332123](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916021332123.png)



### Draw TEXT

The terminal backend imprementing only the  `DRAW TEXT` command 

```
draw [text 15x1 "This is a test" ]
```



## Creating Styles

If you often use a particular combination of size / fonts and other parameters, you can create a STYLE to avoid repetition and data entering

Examples:

```
style txt: text 10x1 font-color 255.0.127
```

Create a style called `TXT` , whose size is predefined to 10x1 and font color 255.0.123. So you can use it in code in this way:

```
TXT "Hello"
```



Other examples:

```
style field: field 10x1
```

```
style b3: base black 4x3
```



A style when used accepts missing parameters or the predefined onse



### Setting and changing the widget content using code

Now you know that below the visible part of each widget, there is a face: a Red object created from VID which interpreted your instructions. 

Each object can be accessed using the `face` words from the code inside of its actors. If you create a text, you can change the face content randomly using the following code

```
view/tight [
	text "Hello" 15x10 font-color red on-time 10 [face/text: random/omly ["World!" "Hello" "People!"]]
]
```

You could also change the element of another `text` field but to do this you must give it a name.

```
mytext: Text "Hello" 10x1 font-color red
```

Using the name `mytext` you access it from everywhere.

This names are globals, so use a good naming structure to avoid collision with other elements. 

````
mytext\text "World!"
````



You can change any other visible or invisible element setting a facet of the face in the same way.

## Reactivity





### List of widgets supported parameters

| Paramenter    | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| `all-over`    |                                                              |
| `center`      |                                                              |
| `middle`      |                                                              |
| `hint`        | Used in `field`, show an guide text in the widget that suggests the kind of input to enter |
| `font-color`  | Set the color used for drawing the font                      |
| `wrap`        | If the text is longer than the number of columns, then it goes to the next line |
| `data`        | Some widgets have additional data like `text-list` where each element of a block is a line of the `text-list` |
| `rate`        | Followed by a number, generates an `on-time` event number of times per seconds |
| `transparent` | set the background color to the one of the base face (verify) |
| `loose`       |                                                              |
| `password`    |                                                              |
|               |                                                              |



### List of facets

| Facet      | Note                | Description                                                  |
| ---------- | ------------------- | ------------------------------------------------------------ |
| `size`     |                     | The size of widget as `integer`, `pair` or `point2d!`        |
| `offset`   |                     |                                                              |
| `color`    |                     |                                                              |
| `enabled?` |                     |                                                              |
| `visible?` |                     |                                                              |
| `text`     |                     |                                                              |
| `rate`     |                     | The number of times the on-time-event is triggered each second |
| `font`     | font/color only     |                                                              |
| `para`     |                     |                                                              |
| `data`     | progress, text-list |                                                              |
| `selected` | only text-list      | The line of the selected text                                |
| `draw`     | only TEXT           |                                                              |
|            |                     |                                                              |





### Colors palette

| Colors        |
| ------------- |
| To be written |

## Viewing the GUI

(to be written)

### Unloading the GUI

These commands can be used to close you GUI

| Command       | Parameter |                             |
| ------------- | --------- | --------------------------- |
| `unview`      | none      | Closes the current window   |
| `unview/all`  | none      | Closes all windows          |
| `unview/only` | object    | Closes the specified object |



## List of supported actors



| Event           |      |                                      |
| --------------- | ---- | ------------------------------------ |
| on-event        |      |                                      |
| on-over         |      | event/offset <br />event/flags       |
| on-down         |      | event/offset                         |
| on-up           |      | event/offset                         |
| on-mid-down     |      | event/offset                         |
| on-mid-up       |      | event/offset                         |
| on-alt-down     |      | event/offset                         |
| on-alt-up       |      | event/offset                         |
| on-wheel        |      | mold event/picked <br />event/offset |
| on-dbl-click    |      |                                      |
|                 |      |                                      |
| `on-time`(?)    |      |                                      |
| `on-create`(?)  |      |                                      |
| `on-created`(?) |      |                                      |



### Managing events

(To be written)

### Managin input

#### On-Key

(Explain how to associate to window)

event/key

```
on-key [if event/key = #"^[" [unview/all]]
```



 	on-key [
 		switch event/key [
 			left	[cat/offset: cat/offset - 1x0]
 			right	[cat/offset: cat/offset + 1x0]
 			up 		[cat/offset: cat/offset - 0x1]
 			down	[cat/offset: cat/offset + 0x1]
 		]
 	]

[table of KEY events]

### Manage mouse events

### Events processed

To activate mouse processing:

`system/view/platform/mouse-event?: yes`

`base 30x5 all-over center middle "moving mouse on here"`

### Timers

If you specify a timer as parameter in a face like

`text "Hello TUI" 10x1 color Red rate 10 on-time [>code here<]`

The `on-time` event will start happening the `N` times per second and the code after the word `on-time` will be excuted.

Be sure to not your code does not spend more than `1/n` times per second to be executed.

(TBD: talk about multitaskin)

### Focus Chain

(TBD: Draft)

Each time you press `TAB` the current active widget changes. The next element is determined by the Focus CHAIN..... you can control it via....

You can use `set-focus` inside your events to...





## Advanced Operations





### Writing a new layer

You can also use a child base face. Sets the `face/offset` to the place you want. Sets `face/visible?: no` to hide it.

### Redrawing the screen

### Clearing the Screen

### Clearing an area



## Advanced topics

## Ansi 

### Ansi Characters



### Ansi Graphic



## Telenet and BBS

Introduction

### Opening an listening port



## Resources

### Examples and locations

TUI Folder

Red Master

Giuseppe Chillemi Test

Other

### Links

Branch

Ansi Resources

ANSI Tables

ASCII Tables

ANSI/Ascii Editors



### Other documentation

Red Documentation

...

### 

## Appendix

### Colors palette

### Standards

### Source Tables and pointers



	PIXEL_BOLD
	PIXEL_FAINT
	PIXEL_ITALIC
	PIXEL_UNDERLINE
	PIXEL_BLINK
	0
	PIXEL_INVERTED
	PIXEL_HIDDEN
	PIXEL_STRIKE

Color16 TAble

### Active Keys

(Vedi Fields)



### Character Tables


### Notes

### Palette (TBD: to test)

Here is the palette of colors you can use with its name and the corresponding value

(TBD: ask if it is right)

| Color                | Value       |
| -------------------- | ----------- |
| aqua                 | 40.100.130  |
| beige                | 255.228.196 |
| black                | 0.0.0       |
| blue                 | 0.0.255     |
| brick                | 178.34.34   |
| brown                | 139.69.19   |
| coal                 | 64.64.64    |
| coffee               | 76.26.0     |
| crimson              | 220.20.60   |
| cyan                 | 0.255.255   |
| forest               | 0.48.0      |
| gold                 | 255.205.40  |
| gray                 | 128.128.128 |
| green                | 0.255.0     |
| ivory                | 255.255.240 |
| khaki                | 179.179.126 |
| leaf                 | 0.128.0     |
| linen                | 250.240.230 |
| magenta              | 255.0.255   |
| maroon               | 128.0.0     |
| mint                 | 100.136.116 |
| navy                 | 0.0.128     |
| oldrab               | 72.72.16    |
| olive                | 128.128.0   |
| orange               | 255.150.10  |
| papaya               | 255.80.37   |
| pewter               | 170.170.170 |
| pink                 | 255.164.200 |
| purple               | 128.0.128   |
| reblue               | 38.58.108   |
| rebolor              | 142.128.110 |
| red                  | 255.0.0     |
| sienna               | 160.82.45   |
| silver               | 192.192.192 |
| sky                  | 164.200.255 |
| snow                 | 240.240.240 |
| teal                 | 0.128.128   |
| violet               | 72.0.90     |
| water                | 80.108.142  |
| wheat                | 245.222.129 |
| white                | 255.255.255 |
| yello                | 255.240.120 |
| yellow               | 255.255.0   |
|                      |             |
| glass , transparent: | 0.0.0.255   |



## Go deeper with:



|                                                              |      |      |
| ------------------------------------------------------------ | ---- | ---- |
| #"^H"  ???                                                   |      |      |
| #"^-" TAB                                                    |      |      |
| ^/ in strings                                                |      |      |
| "^M^[[%dA^[[0J"                                              |      |      |
|                                                              |      |      |
| screen/redraw                                                |      |      |
| screen/remove-window                                         |      |      |
| Adding mouse events<br />https://github.com/red/red/commit/1725a930289bc429dc29c20a58d87685280db3fc |      |      |
| screen.red render-widget                                     |      |      |
| screen/hover-widget                                          |      |      |
| build/includes.r                                             |      |      |
| modules/view/backends/platform.red                           |      |      |
| tests/source/units/regression-test-red.red                   |      |      |
| ANSI-Parser                                                  |      |      |
| KEY-Definition                                               |      |      |
| make-ui                                                      |      |      |
| guis                                                         |      |      |
| /widgets                                                     |      |      |
| modules/view/backends/terminal/definitions.reds              |      |      |
| modules/view/backends/terminal/gui.reds                      |      |      |
| #define MAKE_COLOR_16(idx) [palette-16 << 24 or idx]<br/>#define MAKE_COLOR_256(idx) [palette-256 << 24 or idx]<br/>#define MAKE_TRUE_COLOR(idx) [true-color << 24 or idx]<br /> |      |      |
| What is a comnining table? in [runtime/wcwidth.reds](https://github.com/red/red/commit/2a41f20862c97f5977428584571d6898cd5d1505#diff-9ee561bcdc4ba8eaa36bacdba5b92f3f272a2c05a2838e6f2f109ea6b6e996de) |      |      |
| UTF-16 Codepoints                                            |      |      |
| screen/buffer                                                |      |      |
| font-color 255.0.127                                         |      |      |
| Events/Flags                                                 |      |      |
| https://github.com/red/red/commit/ccdc3c8f3729e4ce10a5d234c88d0b7ef49ef0aa#diff-b7ad1bfe02e11568ef15555b731401d13addb11100ffc9ce5ea0425644c0eacc |      |      |
|                                                              |      |      |



Widgets.red

	#enum ansi-erase-mode! [
		ERASE_DOWN
		ERASE_UP
		ERASE_SCREEN
		ERASE_LINE
		ERASE_LINE_END
		ERASE_LINE_START
	]





		sym = button 	[init-button widget]
		sym = progress	[init-progress widget]
		sym = text-list [init-text-list widget]
		sym = rich-text [init-rich-text widget]
		true			[0]
	]



```
make object! [
    type: 'text
    offset: 0x0
    size: 10x1
    text: "Hello"
    image: none
    color: 0.255.0
    menu: none
    data: none
    enabled?: true
    visible?: true
    selected: none
    flags: none
    options: [style: text vid-align: top at-offset: none]
    parent: make object! [
        type: 'window
        offset: none
        size: 10x1
        text: none
        image: none
        color: none
        menu: none
        data: none
        enabled?: true
        visible?: true
        selected: none
        flags: none
        options: none
        parent: make object! [
            type: 'screen
            offset: 0x0
            size: 120x30
            text: none
            image: none
            color: none
            menu: none
            data: none
            enabled?: true
            visible?: true
            selected: none
            flags: none
            options: none
            parent: none
            pane: []
            state: [handle! 0 none [1]]
            rate: none
            edge: none
            para: none
            font: none
            actors: none
            extra: none
            draw: none
        ]
        pane: [make object! [...]]
        state: none
        rate: none
        edge: none
        para: none
        font: none
        actors: none
        extra: none
        draw: none
    ]
    pane: none
    state: none
    rate: none
    edge: none
    para: none
    font: none
    actors: none
    extra: none
    draw: none
]
```









