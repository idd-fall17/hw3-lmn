# Photo-theremin (Musical instrument)

## Demo and images

[![Video demo](https://raw.githubusercontent.com/idd-fall17/hw3-lmn/master/media/demo-thumb.JPG) Watch video demo](https://youtu.be/CjBjLMEMnmk)

![Hardware top view](https://raw.githubusercontent.com/idd-fall17/hw3-lmn/master/media/hardware_top.jpg)
_Top view of the instrument_

## Team members L-M-N

Rachel Lee: Hardware

Kartikye Mittal: Microcontroller programming

Lily Nguyen: Sound synthesizer programming

## The control scheme

The photo-theremin uses a photocell, two potentiometers, and one momentary switch as inputs.
It is similar to a [theremin](https://www.youtube.com/watch?v=ajM4vYCZMZk) in that the left hand controls pitch by hover distance to the board (via blocking light out from the photocell).
The right hand controls volume by turning a potentiometer knob (~200 degrees range).
It can also turn another potentiometre knob for changing the timbre.
The momentary switch REC enables or disables the midi serial data transfer. It is disabled on program start.
By dextrously turning the volume knob and controlling pitch with the left hand, the user should be able to play a tune. 

## Implementation

### Hardware

The enclosure is made out of 1/8" thick birch plywood cut by the laser cutter.
The inputs needed by the hardware was determined in a group meeting before any fabrication.
Then, we decided to use the photocell and potentiometers and one switch.
After putting the input devices into the enclosure, it was soldered into place and the ribbon wire was attached as well.

![Schematic-fritzing](https://raw.githubusercontent.com/idd-fall17/hw3-lmn/master/media/schematic-fritzing.png)
_The schematic (using GPIOs for both analog and digital inputs on a Raspberry Pi 3 instead of Pico Pro model)_

### Software

We used a custom MIDI output written in Javascript. We read data from the serial port on a Node server, then stream that to a webpage using websockets. We then use that MIDI output to control an oscillator, using [timbre.js](https://github.com/mohayonao/timbre.js/).

For an added audiovisual experience, we used THREE.js to render a cat on the screen, which changes size, position, and color depending on user input.

## Reflection

The hardware was not particularly hard to make.
It used similar skills as making the keyboard text entry device.
The software on the microcontroller was also straightforward with the sample code, sending MIDI encoded messages from 
serial to USB.
The sound synthesizer was the hardest to make. The biggest challenge we came across was playing a MIDI sound on the browser. There are many libraries that deal with MIDI, but most are old and unmaintained.
We consider the creation of our pieces to be successful.

However, we did face issues with scaling using the photocell. Most of the change of value (resistance) occurred when the hand was mostly right on top of the photocell. Ideally the movement of the hand would be linearly related to the pitch of the sound.

# Using this codebase

## Cloning the repo

The webserver lives in a git submodule. If you want to get that code, run `git clone` with the `--recursive` flag:

```
git clone git@github.com:idd-fall17/hw3-lmn.git --recursive
```

## Pre-requisites

- Android Things compatible board
- Android Studio 2.2+


## Build and install

On Android Studio, click on the "Run" button.

If you prefer to run on the command line, type

```bash
./gradlew installDebug
adb shell am start com.example.androidthings.myproject/.MainActivity
```

## License

Copyright 2016 The Android Open Source Project, Inc.

Licensed to the Apache Software Foundation (ASF) under one or more contributor
license agreements.  See the NOTICE file distributed with this work for
additional information regarding copyright ownership.  The ASF licenses this
file to you under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License.  You may obtain a copy of
the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
License for the specific language governing permissions and limitations under
the License.
