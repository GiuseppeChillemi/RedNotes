# TUI Notes

Notes about Red Text User Interface

[TOC]



## The "Terminal" backend



TUI is the new backend of [Red](https://github.com/red/red), our fantastic coding language. With it you can now create beautiful text intefaces to be used using window DOS console or other shells on different OS. Those interfaces where the only way to use computers in the DOS era and when BBS  run using dialup lines you access via Modem and VT100 like terminals (Link) 

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

![image-20230915025439999](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025439999_1694740315..png)



Now choose the version to download most suitable from your platform (you can use this link) [here](http://www.rebol.com/downloads.html) 

![image-20230915032041982_1694740987..png](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915032041982_1694740987..png)







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

![image-20230915025821887](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025821887_1694740328..png)

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





## Table of supported widgets (TBD add images)

|           |      |
| :-------- | ---- |
| button    |      |
| field     |      |
| progress  |      |
| rich-text |      |
| text      |      |
| text-list |      |
| base      |      |

(For an up to date list consult this [github repository directory](https://github.com/red/red/tree/TUI/modules/view/backends/terminal/widgets))

## Table of VID elemenents



| Widget  |                            | Example    | Data |      |      |      |      |      | Other |
| ------- | -------------------------- | ---------- | ---- | ---- | ---- | ---- | ---- | ---- | ----- |
| origin  |                            | origin 2z1 |      |      |      |      |      |      |       |
| panel   | 30x20                      |            |      |      |      |      |      |      |       |
| pad     | pad 1x0                    |            |      |      |      |      |      |      |       |
| return  |                            |            |      |      |      |      |      |      |       |
| button  | button 8x2 "next" [unview" |            |      |      |      |      |      |      |       |
| show    | show page-1                |            |      |      |      |      |      |      |       |
| unview  | e unview/all               |            |      |      |      |      |      |      |       |
| offset  | ;/offset facet             |            |      |      |      |      |      |      |       |
| origin  | origin 1x1                 |            |      |      |      |      |      |      |       |
| space   | space 1x2                  |            |      |      |      |      |      |      |       |
|         |                            |            |      |      |      |      |      |      |       |
| window? |                            |            |      |      |      |      |      |      |       |



## Widgets Documentation



### Characters occupied space

Normal character occupy 1x1 blocks of screen.

Emoji needs 2x1 blocks of screen. 

When you draw a `text`, if you use one or more emoji you should add 2 characters in `text` length for each emoticon used.



### Text

center  font-color            ;	

text 10x1 font-color green "Page 2" return  

text/font/color

### Base

;	base 5x4 center middle "X^/Y"<br/>;	base 5x4 wrap middle "abcdefgh" return<br/>

### Rich-Text

rich-text 40x2 transparent data [yellow "hello" u "underine" /u Strike Italic

### Progress

Supports DATA

### Buttons

button 15x1 "mouse click me" [t/text: "click"] on-dbl-click [t/text: "double click"] return

Events:

`on-key [if event/key = #"^[" [unview/all]]`



### Fields

19 hint "8888 **** **** 1234"

### text-list

;	text-list 13x3 select 2 data [<br/>;		"1 apple"<br/>;		"2 orange"<br/>;		"3 banana"<br/>;		"4 grape"<br/>;		"5 lychee"<br/>;		"6 pear"<br/>;		"7 watermelon"<br/>;	]

## Creating Styles

If you often use a particular combination of size / fonts and other parameters, you can create a STYLE to avoid repetition and data entering



```
style txt: text 10x1 font-color 255.0.127
style field: field 10x1
style b3: base black 4x3
```

### Setting and changing a face



### Draw TEXT

A `DRAW TEXT command` has been implemented in Terminal backend. 

draw [text 15x1 "~~~"]

### With

### List of facets

| Facet       | Note                | Description |      |
| ----------- | ------------------- | ----------- | ---- |
| `size`,     |                     |             |      |
| `offset`,   |                     |             |      |
| `color`,    |                     |             |      |
| `enabled?`, |                     |             |      |
| `visible?`, |                     |             |      |
| `text`,     |                     |             |      |
| `rate`,     |                     |             |      |
| `font`,     | font/color only     |             |      |
| `para`,     |                     |             |      |
| `data`      | Progress, Text-List |             |      |
| `selected`  | text-list           |             |      |
| `loose`     |                     |             |      |
| `password`  |                     |             |      |



### List of widgets supported parameters

|             |      |      |
| ----------- | ---- | ---- |
| all-over    |      |      |
| center      |      |      |
| middle      |      |      |
| hint        |      |      |
| font-color  |      |      |
| wrap        |      |      |
| data        |      |      |
| rate        |      |      |
| transparent |      |      |
|             |      |      |

### Colors palette

| Colors |
| ------ |
|        |





### Unloading the GUI

```
unview/all
```







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



### Managin events

#### On-Key

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



































