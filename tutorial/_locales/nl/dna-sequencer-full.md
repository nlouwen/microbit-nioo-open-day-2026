# NIOO Open dag Micro:bit tutorial

## {Introductie @unplugged}

In deze tutorial leer je zelf onze micro:bit-"sequencer" programmeren!

## {Step 2}

In het werkgebied hieronder zie je dat we alvast enkele 'blokken' hebben toegevoegd.
Deze blokken vertellen de micro:bit wat hij moet doen.<br>
In dit geval: wanneer knop **A** wordt ingedrukt, worden alle blokken erin van boven naar beneden geactiveerd.
De RGB-waarden (Red/Rood, Green/Groen, Blue/Blauw) van de kleurensensor worden naar de computer geschreven via **serieel schrijf**.

## {Step 3}

Tijdens deze tutorial bouw je je eigen 'sequencer' door meer blokken toe te voegen.
Je kan een blok toevoegen door het vanuit de gereedschapskist aan de linkerkant 
naar het werkgebied te slepen. Sommige blokken sluiten op elkaar aan.
Als de vormen op elkaar aansluiten, klikken de blokken vast als puzzelstukjes.
Als je een ​​blok wilt verwijderen, klik en sleep je het terug naar de gereedschapskist.

## {Step 4}

Laten we proberen te detecteren welke kleur door de kleurensensor is gezien. 
Klik op ``||logic:Logisch||`` in de gereedschapskist en sleep een ``||logic:als waar dan||``-blok
naar het werkgebied. Plaats deze onder het ``||basic:pauzeer||``-blok.
Het ``||logic:als waar dan||``-blok dat je zojuist hebt toegevoegd, controleert of iets
waar of onwaar is.<br>
*Heb je een hint nodig? Klik dan op het lampje!*

```blocks
input.onButtonPressed(Button.A, function () {
serial.writeString("")
basic.pause(1000)
if (true)})

```

## {Step 5}

Laten we testen of de gescande kleur rood was. Sleep vanuit de categorie ``||TCS34725:TCS34725||``
in de gereedschapskist een ``||TCS34725:is color||``-blok naar de plek van **waar** in
het ``||logic:als waar dan||``-blok. Vul de waarden R=160, G=70, B=60 in.

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

Nu kunnen we bepalen wat er gebeurt als rood wordt gedetecteerd. 
In onze "sequencer" staat de kleur rood voor de nucleotidebase "A". 
Sleep vanuit ``||basic:Basis||`` een ``||basic:toon tekens||``-blok 
naar het werkgebied. Met het ``||basic:toon tekens||``-blok dat je 
zojuist hebt toegevoegd, kun je aanpassen wat er op het display van 
de micro:bit wordt weergegeven.
Sleep het naar de lege plek in het ``||logic:als||``-blok.
Verander de tekens naar **A**.

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

We moeten de computer ook laten weten welke nucleotidebase er is gescand.
Zoek naar ``||serial:Serieel||`` in de gereedschapskist; dit vind je onder
``||advanced:Geavanceerd||``. Sleep een ``||serial:serieel schrijf tekenreeks||`` naar
hetzelfde ``||logic:als||``-blok en verander de tekst naar **DNA: A**.
Voeg ook een lege ``||serial:serieel schrijf regel||`` toe.

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

Laten we ook toevoegen wat er gebeurt als de kleur **niet** rood is. Klik op het 
**plus**-icoon onderaan het ``||logic:als||``-blok. Er verschijnt nu een **anders**.
Sleep vanuit ``||basic:Basis||`` een ``||basic:toon lichtjes||``-blok naar de
**anders**-opening. Teken een "?" (of iets anders naar keuze) om aan te geven dat de kleur niet werd herkend.


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

Natuurlijk is rood niet de enige kleur die we kunnen zien. 
Je kunt deze stap overslaan, maar als je de drie andere kleuren wilt toevoegen, 
kun je opnieuw op het **plus**-icoon van ``||logic:als||`` klikken 
en meer ``||TCS34725:is color||``-controles toevoegen.<br>
Gebruik RGB=70,130,75 voor groen en schrijf **T**,<br>
RGB=105,110,50 voor geel en schrijf **G**,<br>
RGB=60,105,110 voor blauw en schrijf **C**.

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

De micro:bit heeft nog veel meer aanpasbare functies! Laten we bijvoorbeeld
een geluid afspelen wanneer er op de **A**-knop van de micro:bit wordt gedrukt.
Sleep vanuit ``||music:Muziek||`` een ``||music:speel||``-blok naar het werkgebied.
Je kunt de toon en de lengte aanpassen. Sleep het ``||music:speel||``-blok in het
``||input:wanneer knop wordt ingedrukt||``-blok, helemaal bovenaan.
Druk nu op de **A**-knop van de micro:bit in het linkerpaneel!

```blocks
input.onButtonPressed(Button.A, function () {
    music.play(music.tonePlayable(262, music.beat(BeatFraction.Whole)), music.PlaybackMode.UntilDone)
    serial.writeString("")
    basic.pause(1000)
})
```

## {Step 11}

Gefeliciteerd – je hebt een micro:bit-DNA-sequencer gemaakt!

Zet nu je code op je micro:bit.
Klik op de downloadknop linksonder en volg de instructies.

## @showdialog 

Dit is het einde van deze tutorial. Zodra je op 'Klaar' klikt, krijg je toegang tot alle
beschikbare blokken. Er valt nog veel meer uit te proberen!

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
