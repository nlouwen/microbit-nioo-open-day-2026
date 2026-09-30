# NIOO Open day Micro:bit tutorial

## {Introduction @unplugged}

In this tutorial, you will learn to code our micro:bit "sequencer" yourself!

## {Step 1}

In the workspace below, you can see we have added some "blocks" to start. 
These blocks tell the micro-bit what to do.<br>
In this case it writes the color sensor's RGB values (Red, Green, Blue) 
to the computer every second.

## {Step 2}

Let's try to detect which color was scanned by the color scanner. Click on
``||logic:Logic||`` in the toolbox and drag an ``||logic:if true then||`` block
onto the workspace. Drop it after the ``||basic:pause||`` block.
The ``||logic:if true then||`` block checks if something is true or false.

```blocks
basic.forever(function () {
basic.pause(1000)
if (true)})

```

## {Step 3}

Let's check if the scanned color was red. From the color sensor ``||TCS34725:TCS34725||``
in the toolbox, drag an ``||TCS34725:is color||`` block to replace **true** in
the ``||logic:if true then||`` block. Fill in the values R=170, G=70, B=55.

```blocks
basic.forever(function () {
basic.pause(1000)
if (TCS34725.isColor(
    170,
    70,
    55,
    20
    )) {}
```

## {Step 4}

Now we can add what happens when red is detected. In our "sequencer", a red
color means the nucleotide base "A". From ``||basic:Basic||``, drag a ``||basic:show string||``
block into the ``||logic:if||`` block. Change the shown string to **A**.

```blocks
basic.forever(function () {
basic.pause(1000)
if (TCS34725.isColor(
    170,
    70,
    55,
    20
    )) {basic.showString("A")}
```

## {Step 5}

Let's also add what happens when the color is **not** red. Click on the 
**plus** icon in the ``||logic:if||`` block. Now an **else** appears.
From ``||basic:Basic||``, drag an ``||basic:show leds||`` block into the
**else** slot. Draw a "?" (or anything you'd like) to show that the color was not recognized.

```blocks
basic.forever(function () {
basic.pause(1000)
if (TCS34725.isColor(
    170,
    70,
    55,
    20
    )) {
    basic.showString("A")
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

## {Step 6}

Of course, red is not the only color we see. You can skip this step, but 
if you want to complete the three other colors, you can click on
the ``||logic:if||`` **plus** icon again and add more ``||TCS34725:is color||`` checks.
Use RGB=75,120,80 for green, RGB=110,105,45 for yellow, RGB=80,100,110 for blue.

```blocks
basic.forever(function () {
    basic.pause(1000)
    // Check for RED
    if (TCS34725.isColor(
    170,
    70,
    55,
    20
    )) {
        basic.showString("A")
    } else if (TCS34725.isColor(
    75,
    120,
    80,
    20
    )) {
        basic.showString("T")
    } else if (TCS34725.isColor(
    110,
    105,
    45,
    20
    )) {
        basic.showString("G")
    } else if (TCS34725.isColor(
    80,
    100,
    110,
    20
    )) {
        basic.showString("C")
    } else {
        basic.showString("?")
    }
})
```


## {Step 7}

The micro:bit has many other customizable features! For example, let's play
a sound whenever one of the buttons on the micro:bit is pressed. From
``||input:Input||``, drag a ``||input:on button pressed||`` block onto the workspace.

```blocks
input.onButtonPressed(Button.A, function () {
```

## {Step 8}

From ``||music:Music||``, drag a ``||music:play||`` block into the ``||input:on button pressed||`` 
slot. You can adjust the tone and duration. Now press the **A** button on the 
micro:bit displayed in the left panel!

```blocks
input.onButtonPressed(Button.A, function () {
    music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
}
```

## {Step 9}

This is the end of this tutorial. Once you click next, you will have access to all
available blocks. There is much more to try out!

```template
basic.forever(function () {
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
