node-batch-aerender
===================

Batch rendering lots of compositions in After Effects really gets progressively slow... if I used AfterEffect's batch render to render 40 3 minute long animations. it would take 756 hours... um what? 

The time it takes to render frames goes from 0-1s per frame to 30s per frame..... and progressively upwards to the 40s/frame mark.

I set out to test if I can hack a work around solution to be able to do hands off batch rendering the way it was ment to be... fast and seemless.

Essentially this will kill the render process after every composition is rendered and create a new process, which I think will somehow prevent the inevitable bogging down of my machine by After Effects batch render.


###Update - 11-7-2014
Successss! I was able to keep batch render time down to 0-1s per frame using a synchronous program. Which worked perfectly for rendering one composition after another. 

But...I got greedy and rewrote the code to use node's cluster module to run multiple renders in parallel using half of the cpus available... Essentially I was able to render 4 videos at once in about 8 minutes time. But his somehow kept the aerendercore process alive, which caused the next round of videos to start bogging down because that process was still kept alive. 

I plan on fixing that and making sure the associated aerendercore process truly gets killed for a clean slate and keep the parallel times down to 0-1s per frame, FTW!

The goal is to be able to create a mini batch render farm on one pc, spreading the renders across a portion of your computers CPUs.


### Additional Observations
* An additional aerendercore will float around, causing the other aerendercore processess to slow down.
* When the aerendercore process time reaches > 60 minutes, the process starts slowing down.
