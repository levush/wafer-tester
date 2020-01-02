# wafer-tester
for libresilicon: a simple and cheap to build silicon tester to measure test wafers in order to extract spice parameters. 

Wafer testers are extremely expensive as they have to be precise in mechanical and electrical domain. One wants to measure
the exact behavior of integrated electronics. So if one does a home brew silicon approach using only minimal clean room 
instruments, one wishes to have a wafer tester. Cheap and easy to build. So also universities in poor countries can afford
to build a wafer tester by its students.

The tester consists of a mechanical part and the measurement electronics which uses d/a converters and a/d converters as 
well as scaling amplifiers and pin drivers.

MECHANICS:
The mechanical part will use old hard disks:
A hard disk (best is 5.25 inch as the machanical components are stronger) is disassembled, 
the heads are removed and the 1 to 3 top platters are removed depending on thickness of the glass disk to be installed. 

Now we have the spindle motor which is a very preceise 3 phase AC motor and the arm with the voice coil.
The Spindle motor now gets a thick glas board made from float glass which is equipped with a round hole so it fits on the 
remaining lower platters of the spindle motor and is held in place by the remaining distance rings of the spindle motors.
The assembly looks like a record player while the glass disk resembles the record. The only difference is that the 
glass disk is thicker and the remaining platters and distance rings are adjusted in order to level the glass disk so the 
glass disk is a bit (e.g. 3mm) higher than the spindle motor, while the glass disk is e.g. 6 or 10mm thick.
The glass disk has to be strong enough not to bend. One might use parts of old armoured glass windows, or just thick glass plates
that came with a glass table or a glass floor used in modern architecture. We need a wafer scale disk while the roundness
of the disk is not that critical as it will only rotate at low speeds.
The disk is rotated using the 3 phase AC-Motor which is now driven by 3 class-d audio amps controlled digitaly by I2S or,
if not available using a 16bit dac with differential pair output and differential pair input at the class-d amp, as we need a 
precise "analog quality" control whithout switching noise. Fortunately the mechanics are a good low pass filter for high 
frequencies in the range of 80kHz.
The position of the disk is defined by the resulting force vector of magnetism as the rotating magnet assembly in the disk
motor will be moved by it. So every position of the rotating disk will be defined by 3 currents through the coils. 
Here we will use a more static current for positioning and a decaying higher freqency signal in the range of about 
300Hz to 5kHz added to it in order to vibrate the spindle motor in order to overcome bearing friction so the position is 
preceise and reproduceable.
The waver is put directly on the glass disk while an interposer material may be good to distribute force that is produced by
the needle assembly. Here one can experiment with plain water with dish washing detergent added in order to get a thin film on
the disk that holds the wafer using the cohesive forces of water molecules. The technique would be like the soap water trick
used by advertizing technicans who stick big stickers on window panes without bubbles.
So we now can place the the waver on the disk and spin it to the desired position at low speeds while beeing able to reproduce
the movements.

The Testhead-Assembly 
--------------------
The test head assembly is mounted on the voice coil drive that was used to position the heads of the hard disk on the platters.
With the heads removed the voice coil motor now gets a relatively thick aluminium plate of 3mm thickness that is small but big 
enough to hold the needle assembly.
The needle assembly will try to use normal needles used for sewing which are fine positioned using the piezo or voice coil based
actuators found in cd-rom dives. These actuators are very preceise as they need to control the positon of the laser head in the range
of the wave length of light.
With the tester we should have a precision of at least 10um, which is 0.01mm. T

Position Feedback
------------------
Position feedback will be generated from feducials and structures found on the waver as the test points will be arranged in a
fractal manner so a microscope can measure the distances and patterns of the test pads and the control software will find where the
waver is positioned. Also the needles will be seen by the camera.
Camera:
--------
Using a board *like* a raspi pi4 or something better, having a camera input and a decent frame grabber, we can use a cheap
camera of a mobile phone and use it in a tube together with a microscope lens in order to build a small and cheap microscope.
The microscope will be attached to the moving Testhead-Assembly, so the camera an see the needles and the positoon of the
test head assembly. Fine positioning commands can be generated by image analysis for the spindle motor and the voice coil drive of
the hard disk that positiones the Testhead-Assembly.

We want to have at least 4 and in the best case 8 needles that can be positioned relatively to the Test-Head assembly.
Also the test head assembly will in the best case have to carry at least the pin drivers in order to get good signal integrity
by short wires. But today there are very small packages, so we have a chance to build something small and light. Sorry, no 2.54mm
pinheaders :-)

Electronics:
=============
Measurement Electronics:
------------------------
In order to be cheap and easy the tester will not be that preceise but it is a design goal to get at least *true* preceise 
16bit resolution upto 1MHz we will see what precision we get :-)

So for now the goal is to test +/- 60V upto +/- 0.1A this is nice for analog circuity and basics like transistors, diodes,
resistors and capacitors. The circuity will be inspired by oscilloscope frontends.

For "high speed" digital logic another test amp will be build with less resolution and smaller voltage and current ranges,
but lets see.
A least the pin drivers are to be build into the test head assembly in order to get good signal integrity
by short wires. But today there are very small packages, so we have a chance to build something small and light. Sorry, no 2.54mm
pinheaders :-)
The analog parts of the measurement electronics will also get distributed power mosfet transistors with temperature sensors and
op-Amps in order to keep a pre-set temperature of e.g. 50C in the whole circuit board so that changes in environment temperature
will not affect the measurements.
The electronics will be shielded and use differential amplifiers and be build strictly symmetrical to get a good dynamic range and
noise immunity.


Drive Electronics:
-------------------
The drive will use class-d amplifieres and d/a converters to control them. Ideally a complete digital audio solution will be used,
if it is linear and able to produce dc at different current levels.
We use current feedback instead of voltage feedback as the current relates to the force of the drive. While the software needs to
calculate the force and direction of the force in realtime in order to position the spindle with the glass table to hold the wafer.
Also the voice coil driven arm of that positiones the test head assembly is positioned by a current sent into the voice coil resembling
a force to move the test head assembly on a bow over the waver.


These are the ideas how the wafer-tester will be created. Any help is appeciated.

levush, 02jan2020
