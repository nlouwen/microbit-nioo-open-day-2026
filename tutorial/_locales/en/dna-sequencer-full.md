# NIOO Open day Micro:bit tutorial

## {Introduction @unplugged}

In this tutorial, you will learn to code our micro:bit "sequencer" yourself!

## {Step 2}

In the workspace below, you can see we have added some "blocks" to start. 
These blocks tell the micro:bit what to do.<br>
In this case: when button **A** is pressed, all blocks inside are activated from top to bottom.
It writes the color sensor's RGB values (Red, Green, Blue) to the computer.

## {Step 3}

During this tutorial, you will build your own "sequencer" by adding more blocks.
To add a block, click and drag the chosen block from the toolbox on the left into 
the workspace. Some blocks can fit into each other by dragging one on top of another. 
When the shapes match, the blocks will snap into place like puzzle pieces.
To delete a block, click and drag it back into the toolbox. 

## {Step 4}

Let's try to detect which color was scanned by the color scanner. Click on
``||logic:Logic||`` in the toolbox and drag an ``||logic:if true then||`` block
onto the workspace. Drop it after the ``||basic:pause||`` block.
The ``||logic:if true then||`` block you just added checks if something is 
true or false.<br>
*If you need any hints, check the lightbulb!*


```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (true)})

```

## {Step 5}

Let's check if the scanned color was red. From the color sensor ``||TCS34725:TCS34725||``
in the toolbox, drag an ``||TCS34725:is color||`` block to replace **true** in
the ``||logic:if true then||`` block. Fill in the values R=160, G=70, B=60.

```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (TCS34725.isColor(
    160,
    70,
    60,
    20
    )) {}
})
```

## {Step 6}

Now we can add what happens when red is detected. In our "sequencer", a red
color means the nucleotide base "A". From ``||basic:Basic||``, drag a ``||basic:show string||``
block into the workspace. The ``||basic:show string||`` block you just added can 
change what is shown on the micro:bit display.
Drag it into the empty slot of the ``||logic:if||`` block. 
Change the shown string to **A**.

```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (TCS34725.isColor(
    160,
    70,
    60,
    20
    )) {basic.showString("A")}
```

## {Step 7}

We also need to communicate to the computer which nucleotide base was scanned.
Look for ``||serial:Serial||`` in the toolbox, this will be located under
``||advanced:Advanced||``. Drop a ``||serial:serial write string||`` into the
same ``||logic:if||`` block and change the text to **DNA: A**. 
Also add an empty ``||serial:serial write line||``.

```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (TCS34725.isColor(
    160,
    70,
    60,
    20
    )) {
    basic.showString("A")
    serial.writeString("DNA: A")
    serial.writeLine("")
    }
})
```

## {Step 8}

Let's also add what happens when the color is **not** red. Click on the 
**plus** icon on the bottom of the ``||logic:if||`` block. Now an **else** appears.
From ``||basic:Basic||``, drag an ``||basic:show leds||`` block into the
**else** slot. Draw a "?" (or anything you'd like) to show that the color was not recognized.

```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (TCS34725.isColor(
    160,
    70,
    60,
    20
    )) {
    basic.showString("A")
    serial.writeString("DNA: A")
    serial.writeLine("")
    } else {
    basic.showLeds(`
            . # # # .
            # . . . #
            . . # # .
            . . . . .
            . . # . .
            `)
    }
```

## {Step 9}

Of course, red is not the only color we see. You can skip this step, but 
if you want to complete the three other colors, you can click on
the ``||logic:if||`` **plus** icon again and add more ``||TCS34725:is color||`` checks.
Use RGB=70,130,75 for green and write **T**, 
RGB=105,110,50 for yellow and write **G**, 
RGB=60,105,110 for blue and write **C**.

```blocks
input.onButtonPressed(Button.A, function () {
    serial.writeString("")
    basic.pause(1000)
    // Check for RED
    if (TCS34725.isColor(
    160,
    70,
    60,
    20
    )) {
        basic.showString("A")
        serial.writeString("DNA: A")
        serial.writeLine("")
    } else if (TCS34725.isColor(
    70,
    130,
    75,
    20
    )) {
        basic.showString("T")
        serial.writeString("DNA: T")
        serial.writeLine("")
    } else if (TCS34725.isColor(
    105,
    110,
    50,
    20
    )) {
        basic.showString("G")
        serial.writeString("DNA: G")
        serial.writeLine("")
    } else if (TCS34725.isColor(
    60,
    105,
    110,
    20
    )) {
        basic.showString("C")
        serial.writeString("DNA: C")
        serial.writeLine("")
    } else {
        basic.showString("?")
    }
})
```


## {Step 10}

The micro:bit has many other customizable features! For example, let's play
a sound whenever the **A** button on the micro:bit is pressed. 
From ``||music:Music||``, drag a ``||music:play||`` block into the workspace.
You can adjust the tone and duration. Drag the ``||music:play||`` block inside the 
``||input:on button pressed||`` block all the way on top.
Now press the **A** button on the micro:bit in the left panel!

```blocks
input.onButtonPressed(Button.A, function () {
    music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    serial.writeString("")
    basic.pause(1000)
})
```

## {Step 11}

Congratulations - you have made a micro:bit DNA sequencer! 

Now download your code onto your micro:bit. 
Press the download button in the bottom left and follow the instructions.

## @showdialog 

This is the end of this tutorial. Once you click next, you will have access to all
available blocks. There is much more to try out!

```template
input.onButtonPressed(Button.A, function () {
    serial.writeString("RGB:")
    serial.writeString("" + TCS34725.red())
    serial.writeString(",")
    serial.writeString("" + TCS34725.green())
    serial.writeString(",")
    serial.writeString("" + TCS34725.blue())
    serial.writeLine("")
    basic.pause(1000)})
})

```

```package
tcs34725=github:sweig/pxt-tcs34725-fixed
```
