# Makerbot Sketch
## Printer background
The Makerbot Sketch is a light PLA FDM 3D printer by MakerBot. It's capable of slow, basic part printing, with higher complexity parts facing difficulty in printing.

## Getting started / Using Makerbot CloudPrint
The Makerbot Sketch's software is unique in that it's slicing software is entirely hosted on the cloud. This is nice because you can login from anywhere on any machine, however the preformance of the slicer and available settings are limited.

- Login to [Makerbot CloudPrint](https://cloudprint.makerbot.com/)
- Be invited to Jmtritch_makerbot's workspace.
- Visit the Print Preparation tab of the interface.

The cloud slicer is actually pretty useful given basic job control can be done through the cloud. With the slicer, you can:
- Start, stop, pause, and transfer jobs between printers.
- Slice and queue parts to be printed.
- Re-print parts from part history (You cannot change the settings the parts were sliced with).
- Monitor prints remotely through a camera.

### Advisories
Take care to read this section to it's fullest. It contains useful info in operating the printer.

#### The CloudPrint Slicer
- MakerBot's default settings are garbage. Download and import the tuned printing profile included in this repo.
  - Using default settings results in the part fusing to the raft.
  - Using default settings may cause the raft to seperate from the build plate.
- Using a raft is required. The printer loses it's accuracy in determining the build plate's position quite easily, making it unable to print without a raft.
- Do not print objects with large overhangs, small details, or parts with complex geometries.
- Do not use supports in large volume on the printer. The support is very difficult to remove and leaves extreme surface scarring.
- Only use hexagonal infill. It's the best infill setting that you can use.
- Don't go below 0.1mm layer height, or part quality will suffer as a result.
- Don't go slower than the recommended speeds. The filament will heat up too much and cause part defects as a result.

#### The printer itself
- The printer is not very airtight. Filament goes bad after a week when sitting in the filament recepticle.
- It's advisable to calibrate the Z axis offset every so often (once a week).
- The printer rails lose their lubricant a little fast (especially the z axis). It's advisable to try to lubricate these once every few months to keep noise down.
- The filament intake on the extrusion head has a little lip where new filament can get caught on. This can lead to a jam and the filament motor grinding on the filament.
- Filament jams often happen in the extruder. Preheat the extruder to it's highest temp, undo the bowden tube at the extruder end, pull the filament out (you can use as much force as you can) and use a metal stick to purge the rest of the clogged filament through the rest of the nozzle.
- The printer can sometimes encounter network errors. Rebooting the machine often clears them.
