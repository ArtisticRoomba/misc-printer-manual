# uPrint SE Plus
## Printer background
The uPrint SE Plus by Stratasys (coined the $16,000 Paperweight by it's operators) is an industrial FDM 3D printer for professional workflows, offering high part strength and fast prototyping. This is because the extruder maintains a toasty 300°C and as such allows very nice layer adhesion.

>It is theorized that the unique high temperature requirements of the proprietary ABS that the printer uses can be used in other printers capable of achieving hotend temperatures of 300°C. Preliminary testing of the filament in other printers capable of yielding these tempreatures show good part quality and acceptable strength. More testing is advised.

>The $16,000 Paperweight is the newest uPrint SE Plus in the district. The old printer was dropped by moving staff, and a replacement was ordered. It is confirmed that the $16,000 paperweight is the last uPrint SE Plus in the district.
## Getting started
### Downloading printer software
Proprietary printer software is required. You can also download maintenance software and server software.
- Download GrabCAD Print (admin rights required, per machine installer)
- Download GrabCAD Print Server
  - Allows remote sending of parts and monitoring over the internet when on a different network. Offers notifications for print status and completions.
- Download TeraTerm
  - Allows direct communication to the printer's mainboard. **WARNING: This can damage the printer if you do not know what you are doing.**
- Download MacaraEX
  - Basic troubleshooting and telmetery monitoring software
### Installing and setting up GrabCAD Print
GrabCAD Print is Stratasys' proprietary slicer for all of their printers. While it is partially restrictive, it is not as bad as some other slicers as it at least preforms well.
- Install GrabCAD Print (requires admin rights)
- Sign in to your account. Contact the operator of the printer to be invited to the printer's Company (currently BOOMBA EXPLOSIVE CLEANING SOLUTIONS INCORPORATED).
- >NOTE: Any person can print to the printer if they know the printer's IP address on the LAN. However, this requires direct interaction with the printer.
### Using GrabCAD
GrabCAD is the proprietary slicing software Stratasys uses for all of their machines.

[Continue later]
### Installing and setting up TeraTerm
TeraTerm is a console emulator that we will use to communicate and send commands to the printer's main control board via the diagnostic serial interface on the back of the printer.
- Install TeraTerm
- Acquire a serial to USB cable and connect the two devices together.
- Open a new connection on the USB cable (usually `COM4`)
- Open the serial port connection and change the link rate to `38500`.
- Send a `gp` or `help` command to verify a connection with the printer has been made. The printer should respond with it's last post summary.
>If the printer is responding with absolute gibberish, there is a link error. Reseat the USB and serial connector. Make sure to fully screw in the retaining screws on the serial connector. Keep reseating the connector if the TeraTerm console keeps reporting jibberish.

>The printer will automatically send POST information when it turns on, and exception logs when it encounters a reportable error.

### Using TeraTerm
Basic commands include:
- `help` for the command list, arguments, and minimal descriptions.
- `dl <x>` for controlling the door solenoid.
- `le` for the printer's exception log (error log).
- `gp` for getting the printer's recent POST information.

You can use TeraTerm to submit axis movement commands and to control head and chamber temps. Check the brief [TeraTerm Manual] as well as the `help` command for more info.

**WARNING: While using axis move commands, the printer has no safeguards in place to prevent damage when moving the axises. Blind movements may cause the toolhead to collide with the frame, breaking fragile parts such as the head toggle bar or leveling sensor.**

**WARNING: While using temperature commands, going beyond safe limits (77°C for chamber, 310°C for liquefier) will damage the printer.**

## Printer maintenance and quirks
It's reliability is unparalled compared to it's $16,000 price tag, requiring heavy maintenance and upkeep. It will have a hot streak of printing parts reliability and quickly, and then suffer from a critical error and require creative thinking to overcome. 

### Minor errors
The minor errors it encounters are frequently non-haltable. The printer trusts that everything is working OK, that filament being used is not dry or extremely brittle. This frequently leads to errors it does not detect and cannot halt from.

This printer suffers from a multitude of minor errors. Some of these errors are not detectable and the printer will not halt for them, the only intervention is by an operator who observes the error and stops the print. Below is a list containing common errors.
- Minor errors caused by brittle or bad filament
  - Filament breaking in the bowden tubes in transit to the printing head, causing an LOE (Loss of Extrusion) and the part failing without halting.
  - Filament breaking in the roll and causing a filament break error. If it breaks beyond the filament runout sensor the printer will have an LOE and the part will fail.
  - Filament missing the liquefier input and curling around the drive gear, making a makeshift spring and filling the interior print head with filament.
  - Filament missing the liquefier input and grinding against the drive gear, as it lacks the force to overcome the blockage in the liquefier.
    - To clear a blockage in the liquefier, go into `Maintenance` -> `Machine` -> `Head` and wait for the head to heat up. Then press `Blower Off` and keep pressing it a few times. This allows the liquefier to heat up beyond standard operating tempreatures and melts filament inside of it. Confirm blockage is clear and return to normal operation. Refer to the [Recovering from Loss of Extrusion] section of the maintenance manual.
  - Filament so wet and ruined that it cannot heat up in the liquefier fast enough, clogging the liquefier, causing a LOE. This is only caused by a completely trashed filament roll, and it is advisable to dispose of the roll.
    - >The printer can detect blockages in the liquefier channel and pause printing. Printing can be resumed after clearing the blockage.
  - Filament partially missing the liquefier input and splitting, with one half feeding into the liquefier and the other curling around the filament motor.
- Minor errors caused by bad sclicing settings
  - Spaghettification of part caused by complex part geometry.
    - This is a pretty interesting error. Look out for too much support and material in one place; the printer toggling between the two and depositing too much in one place can cause a failure. This tends to happen on very high resolution, complex parts, with small details. Do not print the part if it fits the description provided.
  - Failure of small support structures causing deposition of support in model and spaghettification of the part.
    - On some parts, be sure to use the `SMART` support settings and the `Grow Small Supports` option under `Grow Supports`. This decreases the chance of the support failing. Supports can support themselves on the part in holes but some get knocked over very easily. This increases wear and support filament usage, however this option may be required on supports that have a high chance of being knocked over.
    - >NOTE: You cannot turn off supports, you can only decrease the angle at which the slicer will place supports. Turning down the support angle all the way is perfectly fine except on some parts.
You can consult the Service Manual of this printer for more information on failure events and what to do during a Loss of Extrusion (LOE).
### Major errors
Major errors are errors that cause an exception in the printer's main control board and subsequently abort printing. These errors are non-recoverable and require a manual `Continue` input issued on the control panel before the printer fully reboots. It is recommended to take note of the error code displayed `(xx, xx)` and look it up in the Printer Manual. You can also type `le` into Teraterm to review the printer's error and exception log. This is useful for troubleshooting persistent errors.

Examples of major errors include:
- `(14, 08)` Unexpected contact with Y axis EOT sensor
  - This error is caused by the Y axis end of travel sensor tripping during operation when the printer did not expect the Y axis sensor to trip during the move.
  - This can be caused by a faulty Y axis sensor. This sensor can fail over time and start generating false positives. Clean the sensor using a q-tip and reseat the sensor cables as well as the main control board cables. If this does not work, replace the sensor.
- `(14, 11)` Door opened while axis in motion
  - This error is caused while the machine detects that the door is open while an axis move is being preformed. Access to the insides of the printer during operation is considered illegal. Using the `dl` command to exeuctively control the door servo does not disable the illegal check.
  - >NOTE: Be sure to return control of the door servo to the controller after using the `dl` command. See the TeraTerm manual for more information.
  - >There is a DIP switch on the controller that bypasses control of the door servo through the controller directly. This bypass may disable the illegal check, however it has not been tested. It is best to leave this in the Off position, as door open/close conflicts are useful to prevent the printer from moving.
