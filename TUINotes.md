# TUI Notes

Notes about Red Text User Interface





## The "Terminal" backend



TUI is the new backend of [Red](https://github.com/red/red), our fantastic coding language. With it you can now create beautiful text intefaces to be used using window DOS console or other shells on different OS. Those interfaces where the only way to use computers in the DOS era and when BBS  run using dialup lines you access via Modem and VT100 like terminals (Link) 

Here are some examples:



![image-20230915025049476](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025049476_1694740249..png)



![iAvEIaHuUt](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/iAvEIaHuUt_1694740678..png)



![7EoEBXoJDF](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/7EoEBXoJDF_1694740299..png)

You can even create games with it!

![image-20230915025338827](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915025338827_1694740308..png)

## Prerequisites before continuing

You should know 

RED

VID

### Installing and running Red TUI

To use TUI you must first download it from GitHub using this [link](https://github.com/red/red/tree/TUI), as this branch has not been merged at the moment

You need compile it using [Rebol,](http://www.rebol.com) the ancestor of Red. Download it from the site www.rebol.com . Then click on *Get-It*

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



If everything has been done properly, you will see the file `console.red` in the same directory of Rebol

Now you are ready to go.

This guide presumes you are familiar with Red language, if you are not, learn it, it is a fantastic language.

## Using Tui



If you are familiar with View and VID, using TUI is a breeze.

A subset of the VID keywords are available for TUI: `TEXT`, `BUTTON`, `TEXT-LIST`, `PANEL`

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

...The backgroud color will fill all the surrounding area upto ....

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030217359_1694740404..png" alt="image-20230915030217359" style="zoom: 50%;" />



Instead of XxY you may express just the horizontal lenght using an integer

```
View/tight [
	Text "Hello TUI!" 15 red font-color green
]
```

<img src="https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030338048_1694740420..png" alt="image-20230915030338048" style="zoom:67%;" />



#### A GUI with buttons

Now, let's add 2 buttons under the text:

![image-20230915030913239](https://raw.githubusercontent.com/GiuseppeChillemi/_Images/main/image-20230915030913239_1694740426..png)

Run this script

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



And use TAB to alternate between "Press Me" and "Quit". Choose "Press Me" and hit return to see what happens....

Have you seen a change on "Hello TUI?"

Perfect! Everything is working as expected

Feel free to experiment with above code



## Table of supported styles (Put images!)



| Widget       |                                                              |            |            |      |      |      | Data |                                                              | Other           |
| ------------ | ------------------------------------------------------------ | ---------- | ---------- | ---- | ---- | ---- | ---- | ------------------------------------------------------------ | --------------- |
| text         | center                                                       | font-color |            |      |      |      |      | ;	text 10x1 font-color green "Page 2" return              | text/font/color |
| base         |                                                              |            |            |      |      |      |      |                                                              |                 |
| origin       |                                                              |            |            |      |      |      |      |                                                              | origin 2z1      |
| progress     | rate 20                                                      |            | on-time [] |      |      |      | yes  |                                                              |                 |
| panel        | 30x20                                                        |            |            |      |      |      |      |                                                              |                 |
| pad          | pad 1x0                                                      |            |            |      |      |      |      |                                                              |                 |
| rich-text    |                                                              |            |            |      |      |      |      | rich-text 40x2 transparent data [yellow "hello" u "underine" /u Strike Italic |                 |
| return       |                                                              |            |            |      |      |      |      |                                                              |                 |
| button       | button 8x2 "next" [unview"                                   |            |            |      |      |      |      |                                                              |                 |
| show         | show page-1                                                  |            |            |      |      |      |      |                                                              |                 |
| unview       | e unview/all                                                 |            |            |      |      |      |      |                                                              |                 |
| layout/tight |                                                              |            |            |      |      |      |      |                                                              |                 |
| offset       | ;/offset facet                                               |            |            |      |      |      |      |                                                              |                 |
| base         | ;	base 5x4 center middle "X^/Y"<br/>;	base 5x4 wrap middle "abcdefgh" return<br/> |            |            |      |      |      |      |                                                              |                 |
| origin       | origin 1x1                                                   |            |            |      |      |      |      |                                                              |                 |
| text-list    |                                                              |            |            |      |      |      | Yes  | ;	text-list 13x3 select 2 data [<br/>;		"1 apple"<br/>;		"2 orange"<br/>;		"3 banana"<br/>;		"4 grape"<br/>;		"5 lychee"<br/>;		"6 pear"<br/>;		"7 watermelon"<br/>;	] |                 |
| space        | space 1x2                                                    |            |            |      |      |      |      |                                                              |                 |
| field        | 19 hint "8888 **** **** 1234"                                |            |            |      |      |      |      |                                                              |                 |
|              |                                                              |            |            |      |      |      |      |                                                              |                 |
|              |                                                              |            |            |      |      |      |      |                                                              |                 |
|              |                                                              |            |            |      |      |      |      |                                                              |                 |

yellow

### Characters occupied space

### Draw

### Writing a new layer

### Redrawing the screen

### Clearing the Screen

### Clearing an area

### Changing an area content

### Rich-Text

### Progress

### Buttons

### Fields

### table-list



### Unloading the GUI

```
unview/all
```

### Panels and positioning



### Setting the content



### With







### Events processed

To activate mouse processing:

`system/view/platform/mouse-event?: yes`

`base 30x5 all-over center middle "moving mouse on here"`



##### Buttons

;	button 15x1 "mouse click me" [t/text: "click"] on-dbl-click [t/text: "double click"] return



Events:

`on-key [if event/key = #"^[" [unview/all]]`



| Event       |      |                                      |
| ----------- | ---- | ------------------------------------ |
| on-event    |      |                                      |
| on-over     |      | event/offset <br />event/flags       |
| on-down     |      | event/offset                         |
| on-up       |      | event/offset                         |
| on-mid-down |      | event/offset                         |
| on-mid-up   |      | event/offset                         |
| on-alt-down |      | event/offset                         |
| on-alt-up   |      | event/offset                         |
| on-wheel    |      | mold event/picked <br />event/offset |
|             |      |                                      |
|             |      |                                      |
|             |      |                                      |
| on-create?  |      |                                      |
| on-created? |      |                                      |



| Facet       | Note                | Description |      |
| ----------- | ------------------- | ----------- | ---- |
| `size`,     |                     |             |      |
| `offset`,   |                     |             |      |
| `color`,    |                     |             |      |
| `enable?`,  |                     |             |      |
| `visible?`, |                     |             |      |
| `text`,     |                     |             |      |
| `rate`,     |                     |             |      |
| `font`,     | font/color only     |             |      |
| `para`,     |                     |             |      |
| `data`      | Progress, Text-List |             |      |
| `selected`  | text-list           |             |      |
|             |                     |             |      |
|             |                     |             |      |

`draw`. `text` command only



## Ansi



Resources



### Other documentation

Red Documentation

...

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

## Telenet and BBS

Introduction

### Opening an listening port




### Notes



on-key [if event/key = #"^[" [unview/all]]

;	style txt: text 10x1 font-color 255.0.127
;	style field: field 10x1
;	style b3: base black 4x3



;	panel 20x9 [
;		base 20x5 red wrap "I can eat glass, it does not hurt me^/^/我能吞下玻璃而不伤身体" return
;		base 20x4 transparent draw [text 15x1 "~~~"]
;		field 19 hint "8888 **** **** 1234"
;		b3 blue left "😀" b3 center "😆" b3 green right "🙂" return
;		txt 8 "EXP" txt 3 "CVV" return
;		field 5 hint "MM/YY" pad 3x0 field 3 hint "999"

