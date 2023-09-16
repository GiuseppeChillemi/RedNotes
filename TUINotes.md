# TUI Notes

Notes about Red Text User Interface



## The "Terminal" backend



TUI is the new backend of [Red](https://github.com/red/red), our fantastic coding language. With it you can now create beautiful text intefaces to be used on Window or a Linux console or other shells on different OS. Those interfaces where the only way to use computers in the DOS era and when BBS  run using dialup lines you access via Modem and VT100 like terminals (Link) but all system still supports them.

Here are some examples:



![image-20230915025049476](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025049476_1694740249..png)



![iAvEIaHuUt](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/iAvEIaHuUt_1694740678..png)



![7EoEBXoJDF](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/7EoEBXoJDF_1694740299..png)

You can even create games with it!

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025338827_1694740308..png" alt="image-20230915025338827" style="zoom: 50%;" />

## Prerequisites before continuing

You should know 

[Red](https://www.red-lang.org/), a fantastic programming language

VID, the Visual Inteface Dialect, which red uses to build visual interfaces

### Installing and running Red TUI

To use TUI you must first download Red TUI branch from GitHub using this [link](https://github.com/red/red/tree/TUI), as this branch has not been merged at the moment

You need compile Red using [Rebol,](http://www.rebol.com) the ancestor of Red. Download it from the site www.rebol.com . Then click on *Get-It*

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025439999_1694740315..png" alt="image-20230915025439999" style="zoom: 67%;" />



Now choose the version to download most suitable from your platform (you can use this link) [here](http://www.rebol.com/downloads.html) 

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916025433761.png" alt="image-20230916025433761" style="zoom: 67%;" />







Once downloaded, put Rebol in the same directory where the Red one is located (but not inside of it!)

Before continuing you need to modify the header of the file `console.red` in the Red folder:

`red/environment/console/cli/console.red`

You can use Notepad on windows to change console.red from this

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

Note the `Config:` line and the adding of `VIEW` to `Needs` 

(Remove the arrows and the semicolon)

### Compiling

Now you are ready to compile TUI !


Run Rebol and enter this command in the console: 

`do/args %red/red.r "-r -t MSDOS %red/environment/console/cli/console.red"`

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025821887_1694740328..png" alt="image-20230915025821887" style="zoom:67%;" />

If everything has been done properly, you will fine the file `console.red` in the same directory where Rebol il located

Now you are ready to go!

This guide presumes you are familiar with Red language, if you are not, learn it, you won't regreet.

## Using Tui



If you are familiar with View and VID, using TUI is a breeze.

A subset of the VID keywords are available for TUI:  like `TEXT`, `BUTTON`, `TEXT-LIST`, `PANEL...`(full list ahead)

The output is arranged in columns so `face/offset` returns `integer` and not `float!`

The origin of the screen are `0x0` (X, Y)  

Lets create our first Textual GUI

```
View/tight [
	Text "Hello TUI!" 10x1 font-color green
]
```

The you will see this:

![image-20230915030028965](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030028965_1694740335..png)





You can even set a different background writing 

```
View/tight [
	Text "Hello TUI!" 10x1 red font-color green
]
```

![image-20230915030139337](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030139337_1694740393..png)



If you don't express the size of the text...

```
View/tight [
	Text "Hello TUI!" red font-color green
]
```

...The backgroud color will fill all the surrounding area upto, so it is important to set a size as `XxY` pair

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030217359_1694740404..png" alt="image-20230915030217359" style="zoom: 50%;" />



#### A GUI with buttons

Having 2 cliccable text button is as simple as writing `Button "Press Me"` inside the description block.

Let's add 2 buttons under the "Hello TUI!" text:

![image-20230915030913239](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030913239_1694740426..png)

We have completed previus script adding 2 buttons

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

As usual with VID, `Button ..` is followed by a code block, it is executed once clicked.

In TUI you move from a gui element to another pressing `TAB` and you click the button hitting `ENTER`

Now use TAB to alternate between "Press Me" and "Quit". Choose "Press Me" and hit return to see what happens.... Have you seen a change on "Hello TUI?" If so, it's perfect! Everything is working as expected

If you press `Quit` the `UNVIEW` command is executed and the last open text "window" is closed



Feel free to experiment with above code!



## Layout

VIEW is a command that displays a group of GUI objects. It calls the `layout` command that creates them. You can multiple of such object by hand and display them on screen on request.

 ```
 screen1: layout/tight [
 	Button "Turn On Light" 10x1 green font-color yellow [<Do something here>]
 ]
 
 screen2: layout/tight [
 	Text "Another screen" 20x1
 	Button "Switch off Light" 10x1 red font-color yellow [<Do something here>]
 ]
 
 View screen1
 ```



The `layout` command processes the block and creates a graphical object with all the GUI elements of both screens. You can later choose which one to display using `view screen1` or `view screen2`

Note that `VID` has a new keyword: `tight` , it is used to instruct the GUI system to have no margins.



## Panels and positioning

(to be written)



## Table of supported widgets (TBD add images)

| Windget name | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| button       | A cliccable button on screen                                 |
| field        | A rectangle that can be used to enter text                   |
| progress     | Progress bar                                                 |
| rich-text    | Draw text with different colors and styles                   |
| text         | Simple text on screen                                        |
| text-list    | List of of elements you can navigate with cursors and choose |
| base         | a rectangle with wrappable text inside                       |
| Panel        | a container for all the above elements                       |
|              |                                                              |
|              |                                                              |

(For an up to date list consult this [github repository directory](https://github.com/red/red/tree/TUI/modules/view/backends/terminal/widgets))

## Other VID elements



| Widget     | Description | Example        |
| ---------- | ----------- | -------------- |
| origin     |             |                |
| panel      |             | 30x20          |
| pad        |             | pad 1x0        |
| return     |             |                |
| offset     |             | ;/offset facet |
| origin     |             | origin 1x1     |
| space  (?) |             | space 1x2      |
|            |             |                |
| window?    |             |                |



### Characters size

Normal character occupy `1x1` blocks of screen.

Emoji needs `2x1` blocks of screen. 

When you draw a `text`, if you use one or more emoji you should add 2 characters in `text` length for each emoticon used.

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

### Rich-Text

Display text with various colors or styles

```
view/tight [
	origin 3x3
	rich-text 40x2 transparent data [yellow "hello " green u "underline" /u ]
]
```

![image-20230916022056537](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916022056537.png)

Supported text attributes:



underline `u` Text `/u`

Strike `s` `/s`

Italic `i` `/i`

bold `b`  `/b`

Color like `yellow`, `blue`

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
	text "Hit one button: " 25x1 font-color green return
	pad 0x1
	button "click me" 20x1 [face/text: "Thank you"] 
	button "or click here" 20x1 [face/text: "Thank you again!"] 
]
```

![image-20230916021100316](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230916021100316.png)

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



### Setting and changing a face

If you define a text widget using:

```
mytext: Text "Hello" 10x1 font-color red
```

You can change its content using the defined name 

````
mytext\text "World!"
````



You can change any other visible or invisible element setting a facet of the face in the same way.



### Draw TEXT

The terminal backend imprementing only the  `DRAW TEXT` command 

```
draw [text 15x1 "This is a test" ]
```



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

| Facet       | Note                | Description                                                  |
| ----------- | ------------------- | ------------------------------------------------------------ |
| `size`,     |                     | The size of widget as `integer`, `pair` or `point2d!`        |
| `offset`,   |                     |                                                              |
| `color`,    |                     |                                                              |
| `enabled?`, |                     |                                                              |
| `visible?`, |                     |                                                              |
| `text`,     |                     |                                                              |
| `rate`,     |                     | The number of times the on-time-event is triggered each second |
| `font`,     | font/color only     |                                                              |
| `para`,     |                     |                                                              |
| `data`      | progress, text-list |                                                              |
| `selected`  | only text-list      | The line of the selected text                                |
| `draw`      | only TEXT           |                                                              |
|             |                     |                                                              |

### With

(to be written)

### Colors palette

| Colors        |
| ------------- |
| To be written |

## Viewing the GUI

(to be written)

### Unloading the GUI

These commands can be used to close you GUI

`unview`

`unview/all`



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

#### Timers

Rate

on-time



#### Events processed

To activate mouse processing:

`system/view/platform/mouse-event?: yes`

`base 30x5 all-over center middle "moving mouse on here"`

### Focus Chain

## Advanced Operations

### Writing a new layer

You can also use a child base face. Sets the `face/offset` to the place you want. Sets `face/visible?: no` to hide it.

### Redrawing the screen

### Clearing the Screen

### Clearing an area

### Changing an area content



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

### List of colors



### Active Keys

(Vedi Fields)



### Character Tables


### Notes



## To investigate



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



































