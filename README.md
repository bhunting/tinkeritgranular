# tinkeritgranular
Granular Synth for Arduino
Original code by Peter Knight at tinker.it




From the site https://code.google.com/archive/p/tinkerit/wikis/Auduino.wiki


Introduction
The Auduino is a sound synthesiser based on the Arduino platform. It works on all Arduinos running at 16MHz - everything from the original Arduino serial to the Arduino Mega. It uses granular synthesis techniques to generate a distinctive filter-sweep sound that had much more character than boring square waves.
Have a look and a listen
	• The first Auduino
	• Aiden's Auduino
	• xndr77's beautifully cased Auduino
	• Medaispoca
	• Berit Greinke
	• Adam Franchino's Ant Farm

Synthesis model

Sound is generated by playing the same noise ('grain') repeatedly at very high speed. This merges into a tone that is an audible hybrid of the repetition rate and the original grain. It sounds quite similar to an oscillator with two resonating bandpass filters, although the different architecture means there are lots of additional interesting noises at parameter extremes.
The grain consists of two triangular waves of adjustable frequency, and adjustable decay rate. This is based on FOF synthesis model, but using triangle waves instead of sine and using a rectangular window.
The repetition rate is set by another control.

Programming the Arduino

Download the source code from the the Tinker.it Google Code site. Load it into the Arduino environment, set up your board type and serial port, then hit the Upload button. Done. If you've never used Arduino before, you'll need to download the development software from the Arduino site.

Construction



Auduino uses 5 controls. You can use anything that generates a 0-5V analogue signal, but the prototype uses five 4.7Kohm linear potentiometers. 
	• Connect one side of each potentiometer to GND. 
	• Connect the other side to the 5V pin on Arduino. 
	• Connect the middle (wiper) pins to Analog inputs 0 to 4 on the Arduino.

The audio comes out of Digital pin 3 (or pin 11 on ATmega8 Arduinos). The prototype uses a 1/4" jack socket, with the tip connected to pin 3 (or 11 on ATmega8's) and the shield connected to GND. Plug the other end into an audio amplifier, and you're good to go.

The Arduino can drive a small piezo, speaker or headphones directly. Strictly speaking it outputs at 5V rather than the 1V line level, but most amplifiers don't seem to mind.

Auduino community
We now have a group on Google Groups. Show off your hacks, or get help with your Auduino projects.

Auduino controller hacks
The Auduino can take any analogue signal and make it audible. Add a Light Dependent Resistor, you have an instant theremin. Add a linear softpot, instant keyboard or ribbon controller. The Arduino Playground is a great place to get new ideas.

Auduino software hacks
Have a look at the loop() function. The controllers are mapped to the synthesiser parameters there. You can really customise the controllers there - adding different musical scales, vibrato, envelopes - whatever takes your fancy.

Start by playing with the pitch mapping. Three mappings are available to start with. Uncomment the one you prefer: 
	• // Smooth frequency mapping 
		○ // syncPhaseInc = mapPhaseInc(analogRead(SYNC_CONTROL)) / 4;
	• // Stepped mapping to MIDI notes: C, Db, D, Eb, E, F... 
		○ // syncPhaseInc = mapMidi(analogRead(SYNC_CONTROL));
	• // Stepped pentatonic mapping: D, E, G, A, B
		○ // syncPhaseInc = mapPentatonic(analogRead(SYNC_CONTROL)); 

syncPhaseInc is proportional to frequency, so the /4 above drops the pitch to a quarter, or two octaves.

Auduino hardcore hacking
If you're really into algorithmic synthesis, have a poke around in the interrupt routine at the bottom of the source code. You'll have to be careful to keep the routine fast, but there is plenty of spare CPU to implement other synthesis techniques.

From <https://code.google.com/archive/p/tinkerit/wikis/Auduino.wiki> 


