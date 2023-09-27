# uPrint SE Plus
## Printer background
The Stratasys uPrint SE Plus (coined the $16,000 Paperweight by it's users) is an industrial FDM 3D printer for professional workflows, offering high part strength and fast prototyping.

The $16,000 Paperweight is the newest uPrint SE Plus in the district. The old printer was dropped by moving staff, and a replacement was ordered. It is confirmed that the $16,000 paperweight is the last uPrint SE Plus in the district.

## Printer maintenance and quirks
It's reliability is unparalled compared to it's $16,000 price tag, requiring heavy maintenance and upkeep. It will have a hot streak of printing parts reliability and quickly, and then suffer from a critical error and require creative thinking to overcome. 

### Minor errors
The minor errors it encounters are frequently non-haltable and are inherit of a bad design. The printer trusts that everything is working OK, that filament being used is not dry or extremely brittle. This frequently leads to errors it does not detect and cannot halt from.

This printer suffers from a multitude of minor errors. Some of these errors are not detectable and the printer will not halt for them, the only intervention is by an operator who observes the error and stops the print. Below is a list containing common errors.
- Minor errors caused by brittle or bad filament
  - Filament breaking in the bowden tubes in transit to the printing head, causing an LOE (Loss of Extrusion) and the part failing without halting.
  - Filament breaking in the roll and causing a filament break error. If it breaks beyond the filament runout sensor the printer will have an LOE and the part will fail.
  - Filament missing the liquefier input and curling around the drive gear, making a makeshift spring and filling the interior print head with filament.
  - Filament missing the liquefier input and grinding against the drive gear, as it lacks the force to overcome the blockage in the liquefier.
    - To clear a blockage in the liquefier, go into `Maintenance` -> `Machine` -> `Head` and wait for the head to heat up. Then press `Blower Off` and keep pressing it a few times. This allows the liquefier to heat up beyond standard operating tempreatures and melts filament inside of it. Confirm blockage is clear and return to normal operation. Refer to the [Recovering from Loss of Extrusion] section of the maintenance manual.
  - Filament partially missing the liquefier input and splitting, with one half feeding into the liquefier and the other curling around the filament motor.
- Minor errors caused by bad sclicing settings
  - Spaghettification of part caused by complex part geometry.
    - This is a pretty interesting error. Look out for too much support and material in one place; the printer toggling between the two and depositing too much in one place can cause a failure. This tends to happen on very high resolution, complex parts, with small details. Do not print the part if it fits the description provided.
  - Failure of small support structures causing deposition of support in model and spaghettification of the part.
    - On some parts, be sure to use the `SMART` support settings and the `Grow Small Supports` option under `Grow Supports`. This decreases the chance of the support failing. Supports can support themselves on the part in holes but some get knocked over very easily. This increases wear on the nozzle, but this is deemed an acceptable trade off.
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
  - >NOTE: Be sure to return control of the door servo to the controller after using the `dl` command. See the Tera Term manual for more information.
  - >There is a DIP switch that bypasses control of the door servo through the controller directly. This bypass may disable the illegal check, however it has not been tested. It is best to leave this in the Off position to recognize when the printer is about to move through door lock cues and to prevent the printer's movement during maintenance.
