# RC Rover car — Journal Export

- Exported at: 2026-06-11T07:14:01Z
- Project ID: 4030
- Entries: 11

## Entry 1
- ID: 10263
- Author: Solace
- Created At: 2026-05-29T22:26:26Z

### Content

For this project, I will be making a simple FPV RC rover car with tank tracks as wheels.
I will be using an ESP cam and my computer or phone screen to drive it with an RC remote or directly using wifi.

For the RC remote, I'm thinking of using the Howtomechatronics nRF one or maybe making my own PCB in KiCad.

For today, I started by just looking for parts availability in my country, then I started doing the wiring diagram in [Cirkit Designer](https://app.cirkitdesigner.com).
I didn't want to start doing CAD until I got the electronics ready, so I wouldn't have to make a lot of modifications later on.

The main circuit is pretty simple; it consists of two Li-on 18650 batteries (3.7V each), a rocker switch, some capacitors, an LM7805, an L293D motor driver module, an nRF24L01, an SG90 servo motor, two 6V 300RPM n20 dc motors, an ESP32 cam, and finally an ESP32 devkit 1. (This is without mentioning the howtomechatronics nrf remote)

These are our main components, other than wires and other things.

The hardest part of this project is printing a good tank track that would allow it to drive on rough terrain.
I'm not expecting much speed out of it; I just want to make a compact and simple design that will serve as an experience for me as my first RC project, especially to get more familiar with 3D printing and CAD.

![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMyNzMsInB1ciI6ImJsb2JfaWQifX0=--6f7a68489ffda8585402af3305ae7d8d8de3d9db/image.png)

I still haven't finished the wiring; I'm having a hard time with the L293D wiring.
I will be using PETG on a Bambulab A1 for the 3d printed parts. I want to try out heat-set inserts in this project, but maybe I'll do two versions so people can recreate it without them.

This project was inspired by [3D Printed FPV Rover V2.0 by markus.purtz](https://www.instructables.com/FPV-Rover-V20/) (Only the general idea; I didn't follow anything he did or even read the instructables)

![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjMyNzQsInB1ciI6ImJsb2JfaWQifX0=--96d0ca2de9d07d057f59d838308bfff280490be4/image.png)


### Recording Links

- https://lookout.hackclub.com/api/media/591a8d1b-2716-40e0-b923-24f8779984d7/video.mp4
- https://lookout.hackclub.com/api/media/ce8a7dbb-ccb2-4701-81f6-d9389462e164/video.mp4

## Entry 2
- ID: 10535
- Author: Solace
- Created At: 2026-05-30T22:55:25Z

### Content

![circuit_image(1).png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQwNDEsInB1ciI6ImJsb2JfaWQifX0=--170ff38dc1af20bf15bf8208f6072cac0a8961dd/circuit_image(1).png)
For now, I'm done with the electronic part.
The circuit is ready, and it should be all good to go.
I made some modifications to it; first of all, I switched the  L293D for a TB6612FNG Motor Driver module. It's way more compact and better for my use case, especially since I want to make a very small rover tank.
I also noticed that the buck converter I chose only had a 1.2A rating, which isn't enough for what I needed, so I switched it out for a StepDown LM2596 (which has a 3A rating) to convert the Li-Ion batteries' 7.4V to 5V.
I wanted to use the OV7670 as a camera for FPV, but it's way too weak; it only allows images and wouldn't work with the nrf and the other modules because of the esp's limited ram.
I also wanted to switch to an ESP32 C3 mini, but unfortunately it doesn't have enough pins. I wanted it because of its small form factor.
I started making the chassis design, but I have to stop here for today. I started taking parts from GrabCAD I didn't progress much.
![Capture d'écran 2026-05-30 234506.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQwNDMsInB1ciI6ImJsb2JfaWQifX0=--7b12bbea1d57c0e44823d201011f32a4ce9ee434/Capture d'écran 2026-05-30 234506.png)
I'm pretty satisfied for now with what I've done. 
Hopefully the CAD part comes out nicely. 
I also bought most parts; unfortunately, I need to change the buck converter because I bought the 1.2A one :(
I will be printing the parts in white PETG with a Bambulab A1 printer.


I will be explaining the circuit in more detail in the next journals!

### Recording Links

- https://lookout.hackclub.com/api/media/62477431-e478-49b0-a4e9-fa0aa9754e32/video.mp4

## Entry 3
- ID: 10778
- Author: Solace
- Created At: 2026-05-31T23:19:23Z

### Content

Today, after getting feedback from my friend, he pointed out that an ESP32 has some pins that I shouldn't use because they need to be set a certain way when booting, or they become unavailable when using wifi or nRF, or something like that.
Some pins have hardware-level restrictions tied to the chip's internal architecture, so I decided to avoid them to avoid boot failures and unpredictable behaviour, especially since I'm planning to solder everything, so I have no margin for error. 

Also, after a lot of talking, I decided to scrap the idea of using Howtomechatronics nrf controller. I will be making my own flight controller as a separate project but will use it to control this RC rover and all future projects.

I also added ceramic and electrolytic capacitors to the nrf so it doesn't get unstable current; I want smooth control with it and no interference.

I want to make my nrf receiver modular so I can use it in any project like a framework computer module or something (like the nintendo switch joycons for example)
 
![circuit_image(2).png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQ2MDAsInB1ciI6ImJsb2JfaWQifX0=--4913211b43b3f8cb0a6a38fb52687da3d1e9d5f5/circuit_image(2).png)

For the rover's chassis, I wanted to make something small; for now it would be 150 mm long, 130 width and 50mm height.

I first started by importing all the parts I need from [GrabCAD](https://grabcad.com/), then I started making some basic chassis shapes to get the main idea and see if everything would fit inside.
Getting everything right took a bit of time; for now I'm satisfied with how it looks, although I could've used a slotted shape from the start instead of doing a cube and filleting it.

My main difficulty is making the car's tracks. I really have no idea how to start making them, especially for 3d printing. I tried using the SolidWorks sprocket generator, but it isn't what I really need.
![Capture d'écran 2026-06-01 001655.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQ2MDQsInB1ciI6ImJsb2JfaWQifX0=--9d9bb60d05b4dc32ac47137aa297f8ad2a7eda6d/Capture d'écran 2026-06-01 001655.png)

![Capture d'écran 2026-06-01 001703.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQ2MDUsInB1ciI6ImJsb2JfaWQifX0=--4dbe9a30486b290a00499b29509414a629f09eed/Capture d'écran 2026-06-01 001703.png)
![Capture d'écran 2026-06-01 001708.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQ2MDYsInB1ciI6ImJsb2JfaWQifX0=--75a1b8ff3a8cc0acf1e9c4e162d84ea2a43c8942/Capture d'écran 2026-06-01 001708.png)
![Capture d'écran 2026-06-01 001715.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjQ2MDcsInB1ciI6ImJsb2JfaWQifX0=--f5d98cc5655cf84057bc61208c7b3ae199089677/Capture d'écran 2026-06-01 001715.png)


### Recording Links

- https://lookout.hackclub.com/api/media/6a962396-b6a3-45da-b89b-7139ba471510/video.mp4
- https://lookout.hackclub.com/api/media/fd1a5a36-7614-463a-8d57-cc8a91d72ec3/video.mp4
- https://lookout.hackclub.com/api/media/885048f0-aa66-4217-92dc-19b3768fecff/video.mp4

## Entry 4
- ID: 10988
- Author: Solace
- Created At: 2026-06-01T20:49:34Z

### Content

Today, I started making the wheel part.
I want to make a tank track as wheels so the rover can be used on any terrain (I'm having some concerns about the small N20 motors, but hopefully it should be fine)
I struggled a lot to make something good, and I'm still not done; it needs a lot of changes.

At first I wanted to use SolidWorks premade sprockets, but I scrapped that idea, and I made my own.
I have no idea how to do the tracks themselves; I also don't know if I will be attaching them using 3d printed pins or some screw.

For now, I'm pretty satisfied with this start, though a lot of things need to be remade, especially since I'm worried about printing my design and it not working at all.

Hopefully everything comes out great!




![Capture d'écran 2026-06-01 214154.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjUxNjEsInB1ciI6ImJsb2JfaWQifX0=--96c8432d6339b91759d3fdb238186b004e84f4dc/Capture d'écran 2026-06-01 214154.png)
![Capture d'écran 2026-06-01 214109.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjUxNjIsInB1ciI6ImJsb2JfaWQifX0=--ac33692d23ce25e0da519253c4b52dc362af3388/Capture d'écran 2026-06-01 214109.png)
![Capture d'écran 2026-06-01 214051.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjUxNjMsInB1ciI6ImJsb2JfaWQifX0=--364b909d178edab345c3eba0aad6b51f79b2ca6b/Capture d'écran 2026-06-01 214051.png)
(The yellow round things are 625-ZZ ball bearings)

Also, I made the main chassis in a very bad way; I might need to redo it to make it open more easily and fit the electronics better, but for now I'm sticking with it.


### Recording Links

- https://lookout.hackclub.com/api/media/780562aa-04d2-4401-ace2-5aed2d21a69c/video.mp4

## Entry 5
- ID: 11255
- Author: Solace
- Created At: 2026-06-02T22:59:05Z

### Content

Today, I found out a lot of mistakes I made, but I haven't corrected them yet.
I started doing the track, which I'm having trouble with.*

I'm still trying to figure out how to make it correctly, so a lot of changes will be made in the future, but this is what it looks like for now.

(I only have 2 minutes before midnight; sorry for the short journal. I need to keep my streak.)
![Capture d'écran 2026-06-02 231616.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MTYsInB1ciI6ImJsb2JfaWQifX0=--2abbd38d82ff6a5aea6c19308f95c0dbcf12faf2/Capture d'écran 2026-06-02 231616.png)
![Capture d'écran 2026-06-02 233151.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MTcsInB1ciI6ImJsb2JfaWQifX0=--1cf1710be97ed40d96792c9b9a99ab2b5b4d12e8/Capture d'écran 2026-06-02 233151.png)
![Capture d'écran 2026-06-02 233422.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MTgsInB1ciI6ImJsb2JfaWQifX0=--f80caeafb77b0067c427a0cba10c34544d6aec1c/Capture d'écran 2026-06-02 233422.png)
![Capture d'écran 2026-06-02 233431.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MTksInB1ciI6ImJsb2JfaWQifX0=--6bc74e89bec0a4b974be20ec2f2013be72307917/Capture d'écran 2026-06-02 233431.png)
![Capture d'écran 2026-06-02 233436.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MjAsInB1ciI6ImJsb2JfaWQifX0=--db9a6d509ccc41ff96e351b254727e30c442c492/Capture d'écran 2026-06-02 233436.png)
![Capture d'écran 2026-06-02 235536.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjU5MjEsInB1ciI6ImJsb2JfaWQifX0=--0945977f19196c31a1a28f7890d34924da0d7d21/Capture d'écran 2026-06-02 235536.png)


### Recording Links

- https://lookout.hackclub.com/api/media/ba513ec9-84bb-4f04-8dea-8b66dccd479e/video.mp4

## Entry 6
- ID: 11352
- Author: Solace
- Created At: 2026-06-03T09:58:04Z

### Content

Today, I continued working on the tracks.
It was really hard to figure out how it needs to be so it can interlock correctly with the sprockets; hopefully it works well.
I changed its dimensions and how it will hold. At first, I thought about making it connect using a strand of filament, but then I decided to use M3 cap head screws. I'm still deciding on their length; I need to see what is available locally.

I'm also still deciding whether to add a tensioner/rollers to the chain drive; I think I might print a version without them and add them if I deem it necessary. 
**Version with tensioner/rollers: **

![Capture d'écran 2026-06-03 104049.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjYxNjEsInB1ciI6ImJsb2JfaWQifX0=--4425a8295decc526d1fb3f824875c0ba6c700eec/Capture d'écran 2026-06-03 104049.png)
![Capture d'écran 2026-06-03 103819.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjYxNjMsInB1ciI6ImJsb2JfaWQifX0=--d4cb2757b1843060959c9a6d45e5568a874e24a8/Capture d'écran 2026-06-03 103819.png)

(It still needs some fixing and tweaking) 

**Version without tensioner/rollers: **
![Capture d'écran 2026-06-03 104057.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjYxNjIsInB1ciI6ImJsb2JfaWQifX0=--ab05f01be264e32a8ac91f8029e035ce735a6106/Capture d'écran 2026-06-03 104057.png)

I also got most parts for this project. When I first saw the N20 motors, I got scared because they were way smaller than I imagined.
I might change the ESP32 to another one because it kinda feels overkill for a project this small; I'm still not sure what I will use.

I also need to start working on the ESP32 cam mount for the FPV; I will be adding it to an SG90 servo so it can have a 360 view.
For now, everything is going great; hopefully the tolerances are good enough because PETG can be hard to print precisely with.

![Capture d'écran 2026-06-03 104147.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjYxNTksInB1ciI6ImJsb2JfaWQifX0=--7036348bcd1ef5d90488e7166c8cadf298af2319/Capture d'écran 2026-06-03 104147.png)




I'm a bit worried about how the track interlocks with the sprockets; I need to test it out in reality to see it better.

![Capture d'écran 2026-06-03 100001.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjYyODMsInB1ciI6ImJsb2JfaWQifX0=--edb5c745d5b702c308737d0555ddfa63ae24d5bf/Capture d'écran 2026-06-03 100001.png)

For now, each track chain will consist of 25 tracks, but I might need to add one more.

### Recording Links

- https://lookout.hackclub.com/api/media/a6762acc-ccb1-49dd-bbc3-241241b1df67/video.mp4
- https://lookout.hackclub.com/api/media/b5bd0ccb-70ed-4437-82ae-f489588d7e81/video.mp4

## Entry 7
- ID: 11707
- Author: Solace
- Created At: 2026-06-04T21:04:26Z

### Content

Today, I continued working on making the track.
It is hard to know if it will work or not in real life without first testing, but after doing some calculations, it should be good enough.

After a lot of tinkering, changing, and modifying my design, I got a somewhat satisfying result.

**But unfortunately, I encountered a big issue.**
My good friend "RoboHub" pointed out that my design was way too heavy for my n20 motors (Just the 3D-Printed parts weigh about 400 grams, so it would be about 700g total with the electronics), so it would either be very slow, or it would just stall.

I then decided to draw the robot on paper to get the real-life dimensions so I could understand what I did wrong better, and so I discovered that I made my robot way bigger than intended.

And so, the only choice was to redesign everything from scratch (I already bought the electronics, so I didn't want to just change the motor types, and from the start I wanted to make a very small rover).
Unfortunately, because of the way I designed the chassis, I just couldn't make it smaller, and everything was linked to it, so I needed to start from scratch.
And so I went about doing everything again.
It was way easier doing it a second time, especially with me knowing all that is needed for this project, from part placement to dimensions.
I also had to scrap the SG90 servo because the second prototype was way smaller and wouldn't fit it well.
I'm also a bit worried about the other electronics not fitting in the chassis, but it should be just barely enough.

I also had to switch from an esp32 devkit 1 to an esp32-c3 super mini because of its smaller form factor.
I couldn't fit the esp-cam inside the chassis, so it would just sit on top.

In the end, I didn't want to lose all the time I worked on the first prototype (the big one),  so I will finish it and submit two versions: the first a small rover without a servo motor, with N20 300 rpm motors powered by an esp32-c3, and a second one with other stronger motors (I didn't decide which type yet) and an SG9 servo for 360 fpv view and powered by an esp32 devkit 1.

Overall, I'm pretty much done with everything; I just need to triple-check everything before printing and make sure everything works.

(I can't afford to print and test both versions; I will only be doing the small one.)

### (Note to reviewer: I burnt my right hand that's why I'm working kinda slow sometimes)

![Capture d'écran 2026-06-04 133913.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzEsInB1ciI6ImJsb2JfaWQifX0=--3f6a6b6b4d1d47a8c5e593e540df0c18c8a28a1a/Capture d'écran 2026-06-04 133913.png)

![Capture d'écran 2026-06-04 133916.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzIsInB1ciI6ImJsb2JfaWQifX0=--66abf98fd41b7cbefe78f3f30e3ee7820a50bc2e/Capture d'écran 2026-06-04 133916.png)
![Capture d'écran 2026-06-04 191858.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzMsInB1ciI6ImJsb2JfaWQifX0=--ca1a3aa10aa9b6f83836587d29583c8713b31eb7/Capture d'écran 2026-06-04 191858.png)
![Capture d'écran 2026-06-04 191911.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzQsInB1ciI6ImJsb2JfaWQifX0=--77c671cb42644d7a5eaae87d419c6fd666cbcaaf/Capture d'écran 2026-06-04 191911.png)
![Capture d'écran 2026-06-04 191917.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzUsInB1ciI6ImJsb2JfaWQifX0=--763c3d4859f8aba4cfd40389834a32ac90365de2/Capture d'écran 2026-06-04 191917.png)
![Capture d'écran 2026-06-04 191926.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzYsInB1ciI6ImJsb2JfaWQifX0=--0275d853483f883d8e67831b5fd9e6c39d164cff/Capture d'écran 2026-06-04 191926.png)
![Capture d'écran 2026-06-04 205716.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyMzcsInB1ciI6ImJsb2JfaWQifX0=--721f804bd9bf2d383854b9934e00376c1149a8ce/Capture d'écran 2026-06-04 205716.png)
![Capture d'écran 2026-06-04 205721.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDAsInB1ciI6ImJsb2JfaWQifX0=--912b8290b3e86b98ece70f93aeaef496c5a2348a/Capture d'écran 2026-06-04 205721.png)
![Capture d'écran 2026-06-04 205733.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDEsInB1ciI6ImJsb2JfaWQifX0=--b2025c939ce60c561e5af3de4fd4d57e54fec1bc/Capture d'écran 2026-06-04 205733.png)
![Capture d'écran 2026-06-04 210442.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDIsInB1ciI6ImJsb2JfaWQifX0=--3950e6ef195cdce278a1f1967a6c21282eeceaaa/Capture d'écran 2026-06-04 210442.png)
![Capture d'écran 2026-06-04 211651.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDMsInB1ciI6ImJsb2JfaWQifX0=--53dd00898b7e944cc4cba99bb63b9a3c04b697cf/Capture d'écran 2026-06-04 211651.png)
![Capture d'écran 2026-06-04 211702.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDQsInB1ciI6ImJsb2JfaWQifX0=--3fd84ea0da53295f14ac4264eb55e25726fd8d66/Capture d'écran 2026-06-04 211702.png)
![Capture d'écran 2026-06-04 211708.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDUsInB1ciI6ImJsb2JfaWQifX0=--41bb90dee5dc7c24e59ed7976541fb4961c8f96e/Capture d'écran 2026-06-04 211708.png)
![Capture d'écran 2026-06-04 211728.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDYsInB1ciI6ImJsb2JfaWQifX0=--2dc903815db636b41b751f358519a6f81a54612e/Capture d'écran 2026-06-04 211728.png)
![Capture d'écran 2026-06-04 213958.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDcsInB1ciI6ImJsb2JfaWQifX0=--482b278b32938a0d1e6c8f2aef5767806f7b4933/Capture d'écran 2026-06-04 213958.png)
![Capture d'écran 2026-06-04 214007.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDgsInB1ciI6ImJsb2JfaWQifX0=--0309607fa97f1d8921c8dafbce22eb0536c3ad1d/Capture d'écran 2026-06-04 214007.png)
![Capture d'écran 2026-06-04 214015.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNDksInB1ciI6ImJsb2JfaWQifX0=--edda27e7a9b4aee9221f50aaf6de91673c395ee7/Capture d'écran 2026-06-04 214015.png)
![Capture d'écran 2026-06-04 213952.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6MjcyNTAsInB1ciI6ImJsb2JfaWQifX0=--87d6599993a6d7657b31d45dd2d6dab9858b9e2b/Capture d'écran 2026-06-04 213952.png)


### Recording Links

- https://lookout.hackclub.com/api/media/235e56b8-dafa-4b40-9fe8-8cf3a8b35f41/video.mp4
- https://lookout.hackclub.com/api/media/0e1d8db7-5334-4616-939b-e0eb82e40089/video.mp4
- https://lookout.hackclub.com/api/media/549de150-1cd0-40f9-9e05-17f9cda87b5b/video.mp4
- https://lookout.hackclub.com/api/media/7ef99313-7894-4ae6-8fea-558191b8b93a/video.mp4
- https://lookout.hackclub.com/api/media/fd485ea4-341d-4a01-89c4-3674cdb0e327/video.mp4
- https://lookout.hackclub.com/api/media/51e198a0-bfd0-452d-a73c-d6603c88dc68/video.mp4
- https://lookout.hackclub.com/api/media/9127ed97-5c92-4392-927f-2799144e561d/video.mp4

## Entry 8
- ID: 11833
- Author: Solace
- Created At: 2026-06-05T13:48:02Z

### Content

Today, I started by redesigning the electronics circuit.
First of all, I changed the LM2596 buck converter to an MP1584 one, because of its smaller form factor and better EMI-minimizing technology.
This choice was made after careful consideration, especially with only having 7x4x2 cm of room for all the electronics.
I also switched from an esp32 devkit 1 to an ESP32-C3 super mini; its pins are just enough for my project (I had to use all pins), and I added more capacitors so the nrf works without problems.

![circuit_image(5).png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MTUsInB1ciI6ImJsb2JfaWQifX0=--83c28d015b46708ade6108561fa54c2c960e00fb/circuit_image(5).png)

I will be using a 7x5 perfboard for soldering; it's a bit bigger than the space I have, so maybe I will cut a part of it.
Everything will barely fit, so it will be very hard to solder. I will try my best so as not to burn anything, as I'm not very used to soldering.

After exporting my model to BambuStudio, I noticed some problems; first of all, the walls were very thin, 1.5mm each, so I changed them to 3mm so the structure holds better.
I also made something resembling an elastic ring so the motor cog stays in place. Then I noticed how small I made it, so it wasn't printable, so I redesigned it to be thicker.
![Capture d'écran 2026-06-05 121817.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MTYsInB1ciI6ImJsb2JfaWQifX0=--4c231301ed14a713edd1c55057db1cf8022a91b9/Capture d'écran 2026-06-05 121817.png)

The second version (the small one) came out looking very good; I was very surprised, having gone down from 400 grams of filament to only about 100g. This would allow the rover to have way more speed! (and not make me go broke on one project)
Overall, everything looks good; I still need to make a few adjustments to get everything ready, but it's mostly good for printing.


![Capture d'écran 2026-06-05 122136.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MTgsInB1ciI6ImJsb2JfaWQifX0=--84c2999ff1bf6389e2d69d29ba07fe1519d58f2c/Capture d'écran 2026-06-05 122136.png)
![Capture d'écran 2026-06-05 122147.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MTksInB1ciI6ImJsb2JfaWQifX0=--311493f7555282995ba9a95cf91a94e4588353c7/Capture d'écran 2026-06-05 122147.png)

![Capture d'écran 2026-06-05 125954.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MjAsInB1ciI6ImJsb2JfaWQifX0=--3366792a7976fecd4a547f164c4ecc72cd76e4fc/Capture d'écran 2026-06-05 125954.png)
![Capture d'écran 2026-06-05 130907.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MjEsInB1ciI6ImJsb2JfaWQifX0=--32202df145fe38c149e06fd3935ffe31ee7de5d5/Capture d'écran 2026-06-05 130907.png)
![Capture d'écran 2026-06-05 131055.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc2MjIsInB1ciI6ImJsb2JfaWQifX0=--167c8cba950572cf721be86fcc78ebc3a86bff4a/Capture d'écran 2026-06-05 131055.png)

That's about it for this project; I now just need to make it in real life and continue designing the bigger versions, which I wouldn't be building; it's just missing the SG90 servo and some little tweaking nothing hard to do.

### Recording Links

- https://lookout.hackclub.com/api/media/c9845de6-3ed3-48db-88e8-d535bfb88e23/video.mp4
- https://lookout.hackclub.com/api/media/476d0407-bc86-4ba1-b52a-6c4f6237e107/video.mp4

## Entry 9
- ID: 11930
- Author: Solace
- Created At: 2026-06-05T20:24:56Z

### Content

![Capture d'écran 2026-06-05 190009.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDIsInB1ciI6ImJsb2JfaWQifX0=--103694a0cb3962c0e11c2a435c757e8078d1b780/Capture d'écran 2026-06-05 190009.png)
![Capture d'écran 2026-06-05 190013.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDMsInB1ciI6ImJsb2JfaWQifX0=--8f58df3fc0f84bf2285a355bfe652ba7336e36f8/Capture d'écran 2026-06-05 190013.png)

While trying to make an assembly using all the electronic components after adding all the screws and heat-set inserts, I remembered that I had to place the batteries somewhere, which, in my case, I unfortunately have no place for inside the chassis.

![2026_06_05 9_13 PM Office Lens (6).jpg](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDYsInB1ciI6ImJsb2JfaWQifX0=--8983efd78e13ae6ceb199284382f7cfe6cefffcc/2026_06_05 9_13 PM Office Lens (6).jpg)
(I still didn't buy the MP1584 module)
I was very mad at myself for forgetting such an important thing, and so my only choice was to make space for it on top.
First, I put a 7x5 cm perfboard; it didn't fit, so I made more space for it.
![Capture d'écran 2026-06-05 211930.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDgsInB1ciI6ImJsb2JfaWQifX0=--d6cc25f669855dbef460fcda73ad769e38a7eb94/Capture d'écran 2026-06-05 211930.png)
![Capture d'écran 2026-06-05 193112.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDksInB1ciI6ImJsb2JfaWQifX0=--536a8b500e42541562d8666ea6d76efef69c8887/Capture d'écran 2026-06-05 193112.png)
![Capture d'écran 2026-06-05 191839.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MTAsInB1ciI6ImJsb2JfaWQifX0=--819c7098c288e724b7847d58549634cda6d01d18/Capture d'écran 2026-06-05 191839.png)

And so I had to move the esp32-cam and the rocker switch because the battery holder is as big as the chassis length. I decided to make a holder for them on top of the batteries, which would come and clamp on the batteries. This was the only way I could think of for the moment, but I will try to make it better.
Also, the esp32-cam isn't held by anything, so I need to find a solution for it too.
All of this is very unfortunate because I was happy to finally complete the designing part of this project, but now I'm realizing a lot of mistakes I need to fix.

![Capture d'écran 2026-06-05 211332.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MTEsInB1ciI6ImJsb2JfaWQifX0=--0cc40191c3d6d136970cbd6df4fdd20bb1cac83a/Capture d'écran 2026-06-05 211332.png)
![Capture d'écran 2026-06-05 211841.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjc5MDcsInB1ciI6ImJsb2JfaWQifX0=--1502f0a6e3f3fb771994bbe7110d949b181811ea/Capture d'écran 2026-06-05 211841.png)

For now, I need to find solutions to all these problems because I want to make something clean and reliable, and I'm very worried about the soldering part; I don't want to solder everything then find out that nothing fits.



### Recording Links

- https://lookout.hackclub.com/api/media/7812c391-a6fa-43d8-9ba2-1e97117b93eb/video.mp4

## Entry 10
- ID: 12145
- Author: Solace
- Created At: 2026-06-06T22:02:33Z

### Content

Today, after thinking a lot about how to reduce space and make my rover smaller, without the need to add batteries on top, etc. I found some ggn-751723 180mah 3.7v batteries 0.67wh lying around from an old drone I had, and so I thought about using them instead of the Li-on batteries, as they are way smaller. Unfortunately, I will be losing maximum use time, as their capacity is way smaller, going from 2550mAh to only 180mAh, but it should be enough to last about 30 minutes to maybe one hour.
The biggest problem is that I will need to use 3 of themù to get the result I want.

I will be using two in series to get 7.4V (3.7V each) for powering the ESP-C3 super mini and the n20 motors, coupled with an MP1584 buck converter to have 5V required. 
I will also need to use a step-up booster to get 5V to the ESP32-CAM; I chose the MT3608 for its small size.

I'm not really happy with all this; I would've preferred using a small lipo battery that had 7.4 V and more mAh, but this is the best I can do with what is available to me.
Honestly, the best choice is to make my own PCB, but there are no PCB-making services locally, and I can't acquire any from abroad without requesting a grant, so maybe I will design one so others recreating this project could have something cleaner.

I also made the ESP-cam holder separately, so you can choose not to use it and just drive around without FPV, as it is easily removable.

I changed where the perfboard would be held inside the chassis; I had to elevate it because of the nrf pins (other components I could solder directly with wires on top without pins poking on the bottom)
![Capture d'écran 2026-06-06 174002.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MTcsInB1ciI6ImJsb2JfaWQifX0=--b0f8bc5ebeda4ae98819964bbcf3fdd5ba9b1196/Capture d'écran 2026-06-06 174002.png)
![Capture d'écran 2026-06-06 173958.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MTgsInB1ciI6ImJsb2JfaWQifX0=--59e5a77f3e1845e0ecf67a8245a6706d2c38f876/Capture d'écran 2026-06-06 173958.png)

I also finished making the version with all the electronics; I'm just missing the bearing and the capacitors.

I also remade the circuit to accommodate the new changes and added two ceramic capacitors to the motors to filter noise so they don't interfere with the nrf.
![circuit_image (4).png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjEsInB1ciI6ImJsb2JfaWQifX0=--d072c93d0949127a3551e9220f070215048735c7/circuit_image (4).png)

The two batteries will sit at the bottom with the perf board on top of them; this way I should have enough space for all the wires and stuff.
![Capture d'écran 2026-06-06 225540.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjQsInB1ciI6ImJsb2JfaWQifX0=--7c0cd843efc4c65ca2e14727007a2587f6cdcdd5/Capture d'écran 2026-06-06 225540.png)
![Capture d'écran 2026-06-06 225546.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjUsInB1ciI6ImJsb2JfaWQifX0=--fb174c8211a57c44cfbb62a76f7c6bdeef12b7af/Capture d'écran 2026-06-06 225546.png)
![Capture d'écran 2026-06-06 225553.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjYsInB1ciI6ImJsb2JfaWQifX0=--9834799bb56919e3a3e9f3ab32fcd0e566ff641a/Capture d'écran 2026-06-06 225553.png)
![Capture d'écran 2026-06-06 225557.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjcsInB1ciI6ImJsb2JfaWQifX0=--4243534808c079138454162c1dec459b6883feb4/Capture d'écran 2026-06-06 225557.png)
![Capture d'écran 2026-06-06 225702.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjgsInB1ciI6ImJsb2JfaWQifX0=--d4712e52f0f66c6d739673da352202dbf866dda3/Capture d'écran 2026-06-06 225702.png)
![Capture d'écran 2026-06-06 225710.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MjksInB1ciI6ImJsb2JfaWQifX0=--06925e643d969bc53edb13c65d43acc3928ce15a/Capture d'écran 2026-06-06 225710.png)
![Capture d'écran 2026-06-06 225721.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjg1MzAsInB1ciI6ImJsb2JfaWQifX0=--b9fc2054fe41a2035e58c070cb4cda3c457daea7/Capture d'écran 2026-06-06 225721.png)

Honestly, I don't really like the ESP32 holder; I would've rather used another FPV cam, but this is the only one I have available. I will try to make it a bit better looking.

Now I just need to double-check some things and get to printing it out.

### Recording Links

- https://lookout.hackclub.com/api/media/ed50c784-ef8c-4144-a292-ac1743188180/video.mp4
- https://lookout.hackclub.com/api/media/9b3deef1-3067-4f13-9d51-700070668c98/video.mp4

## Entry 11
- ID: 12573
- Author: Solace
- Created At: 2026-06-08T19:45:53Z

### Content

Today I didn't really manage to do much; I went to buy other parts I was missing, fixed the esp32-cam holder, and wanted to render something for a zine, but Blender and my pc just crashed nonstop.

I also sliced and sent my files for printing (Forgot to record)
![image.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjk1NzcsInB1ciI6ImJsb2JfaWQifX0=--739c6a574b2922e7f14ede2dc04072618f3841ca/image.png)
![Capture d'écran 2026-06-08 204336.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjk1NzksInB1ciI6ImJsb2JfaWQifX0=--3806047c7440ee63241b7a9872138ce104cff348/Capture d'écran 2026-06-08 204336.png)

I will be printing in white PETG (the only color available for PETG)
I chose PETG because it's less brittle than PLA and tougher, with greater resistance to higher temperatures.

I'm really excited to start the building part of the project!
![Capture d'écran 2026-06-08 125944.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjk1NzQsInB1ciI6ImJsb2JfaWQifX0=--9f5666ef5461158b468e6917d50cf99c5afc4d8a/Capture d'écran 2026-06-08 125944.png)
![Capture d'écran 2026-06-08 140209.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjk1NzUsInB1ciI6ImJsb2JfaWQifX0=--7fb579caabac4bcf9029ba78821888eae9af6f7b/Capture d'écran 2026-06-08 140209.png)
![Capture d'écran 2026-06-08 140214.png](/user-attachments/blobs/redirect/eyJfcmFpbHMiOnsiZGF0YSI6Mjk1NzYsInB1ciI6ImJsb2JfaWQifX0=--12153d4a923eb3705d5b65014dcbebcd769f1f52/Capture d'écran 2026-06-08 140214.png)


### Recording Links

- https://lookout.hackclub.com/api/media/0f01b49e-87db-4814-94f5-23fb974ab592/video.mp4
