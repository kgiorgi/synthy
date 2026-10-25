# synthy

Synthy is a small 8-step synth with no microcontroller and no code. It plays a looping melody of 8 notes, and you set each note by turning its own knob. Everything runs off USB-C.

![synthy](/synthy.png)

How it works

One 555 timer ticks like a metronome. Every tick moves a 4017 counter on to the next step, so the 8 steps light up one after another and then start over.

Each step has its own knob, LED and switch. When a step is active, its knob sets how fast a second 555 timer buzzes, and that's the note you hear. The LED shows which step is playing, and the switch can turn a step off so it becomes a rest.

The sound then goes through a tone knob that goes from soft to buzzy, a volume knob, and a small LM386 amplifier that drives a speaker.

![synthy](/Screenshot2026-10-24222012.png)


How to play it

Plug in USB-C and the loop starts.

Turn the 8 step knobs to change the notes. TEMPO changes the speed. TONE makes the sound softer or buzzier, and VOLUME sets how loud it is.

Flip the small switches by the LEDs to turn steps into rests and make rhythms. The 4/8 switch picks a 4-step or 8-step loop, and RUN/STOP freezes the loop on one note so you can tune it.

Before drawing the board

I built both timers in a circuit simulator first to check the numbers. The tone timer covers about 210 Hz to 1.5 kHz, which is roughly three octaves, and the clock goes from about 1.3 to 13 steps per second. Both matched what I calculated, so I didn't need to change any part values. The simulation file is in the sim folder.

Parts

The main parts are two LMC555 timers, a 74HC4017 counter, an LM386 amplifier, 11 knobs, 9 LEDs, 8 diodes, an 8-way DIP switch, two slide switches, a USB-C socket and a small 8 ohm speaker. The full list with LCSC part numbers is in production/BOM.csv.

I bought the knobs myself on AliExpress because LCSC was out of stock. If the LMC555 sells out, two regular NE555s plus a 74HCT4017 work in the same spots.

Testing it after building

The chips go in sockets, so the board can be tested one part at a time.

With no chips in, plug in USB-C. The power LED should light, and every chip socket should have about 5 V.
Put in the clock and the counter. The step LEDs should walk from 1 to 8 and repeat, TEMPO should change the speed, and RUN/STOP should freeze it.
Put in the tone timer and the amplifier. The speaker should play the loop, each knob should change its own note, and a step with its switch off should be silent.

If something fails, only that one part of the circuit needs checking.

Files

hardware/kicad has the KiCad project. production has the gerbers and the BOM. docs/images has the render and schematic. sim has the simulator file.

What I learned

First of all measuring frequencies in circuits. A little bit niche but at least it wasn't difficult to understand unlike well, copper layers in kicad? I still can't even begin to explain what was happening towards the end but I got the intuition which is sufficient for me.
