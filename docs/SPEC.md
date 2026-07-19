

Following modern (2026) consumer mop robot design, OOMWOO One requires

View [BOM.md](https://github.com/makerspet/oomwoo/blob/main/BOM.md).

- one right front side brush (not two), with an extendable arm (swings out to the side to clean under cabinets)
- mop is 2-disk rotary (not roller for now); the right mop is extendable (swings out to the side to clean under cabinets); the left mop is fixed
- mop disks land into the dock tray (for mop washing, drying)
- having charging contacts on the *rear vertical face*
  - charging contacts cannot be on the robot's underside because this is where the mop wash tray sits
- vacuum *backing* into the (wash) dock (not driving in front-first)
- robot's dock homing sensor must be on the *rear vertical face* between the charging contacts
- robot's charging contacts are "dumb" (not spring-loaded), use an nickel-plated steel strip
  - nickel-plated steel strips resist corrosion, scratching
- charging contacts on the dock have to be spring loaded, with gold-plated pogo pins, 4A 20.1V to provide 65W
- TODO bagless or not
- LiDAR must be inset 10+cm from vacuum's enclosure edges
  - because LiDAR sensor has a ~10cm dead zone around it
- need to lift mops (when traveling over carpet) 12mm
- need a [carpet sensor](https://makerspet.com/blog/how-to-source-bom-for-oomwoo-open-source-vacuum-robot/#carpet-sensor) (ultrasonic ~300kHz) placed in front of main brush; carpet detect causes mops to lift, stop spinning, main brush to spin appropriately for carpet
  - carpet sensor detects carpet ahead of time as the vacuum travels forward, so the mop is always lifted over carpet
- need 2 side wall sensors (left, right)
  - wall sensors detect dock presence (by receiving IR signal from the dock) and act as a crude wall following (intensity based) sensor
  - wall sensor has to be a small custom PCB
- drving wheels should be centered, wide apart
  - let's try reusing [Roborock S5 Max assembly](https://makerspet.com/blog/how-to-source-bom-for-oomwoo-open-source-vacuum-robot/#driving-wheels) because it is abundant in the aftermarket
  - each wheel comes with a wheel drop sensor (a microswitch)
  - FYI some vacuums don't center driving wheels exactly
- robot-to-floor gap is largely defined by the drive wheels
- caster wheel - front center
  - let's try reusing the abundant [iRobot Roomba](https://makerspet.com/blog/how-to-source-bom-for-oomwoo-open-source-vacuum-robot/#caster-wheel)
- I/O board and compute module - front center top, shape TBD
  - board has pushbuttons
- battery pack - reuse abundant standard [Roborock battery pack](https://makerspet.com/blog/how-to-source-bom-for-oomwoo-open-source-vacuum-robot/#battery-pack)
  - place battery pack on the vacuum bottom, with an access door with screws, roughly under the I/O board or slightly behind, roughly centered to equalize pressure on both wheels and mops
  - TODO check if battery should be close to mops for cleaning pressure

## Dock

- use an external certified 24 V DC brick (~200–350 W)
  - the dock only sees 24V
  - inherit the brick's UL/CE certification
  - reuse 25.2 V stick-vac motors, e.g. Dreame M10-E-4 (25.2 V, 310 W) handheld motor, use for auto-empty
- dock contains USB PD sink, converts power to ~20-24V charger contacts
  - dock charger contacts check for robot's presence (resistance), enable power only when robot is present
- skip hot air dry, use a regular fan
  - Hot air dries the mop in ~2–3 h instead of ~6. But the robot sits docked for hours anyway.
  - Dropping the heater removes your biggest power draw and biggest thermal-safety risk.
- bagless
  - No consumable lock-in. The bin is a printed part.
  - Downside: emptying a dusty bin by hand. The dock bin is far larger than the robot's, so you empty it ~monthly instead of every run. Design a wide opening + lid to limit the dust puff.
  - Bagged is significantly easier to engineer — the bag is the container and the filter, so there's no cyclone to design.
  - Bagless needs real separation (a working cyclone + washable filter), and the cyclone is the main engineering risk of this choice — a poor one sends fines straight to the filter, it clogs, and suction dies.
  - Maybe prototype the auto-empty tier bagged to de-risk the port/sealing/motor work, then move to bagless once you've validated a cyclone geometry. Ship bagless.
- bottom extraction auto-empty
  - why? proven, Roborock style; gravity helps dust fall/evacuate vs non-bagless rise; only one, simple robot-side port, one flap - no sealed opening in the robot's dust bin needed; robot-to-dock flat plate-to-plate gasketed mating is relatively simple vs bagged nozzle-into-the-port mating; frees us space in the robot's rear
- safety
  - Mains stays outside (certified brick) — non-negotiable.
  - Physically separate the wet section from the electronics; drip loops, drainage, a dam/lip toward the contacts.
  - Presence-detect the robot, energize charge contacts only when the robot is docked
  - If you ever add the heater: redundant thermal cutoff (thermistor + independent thermal fuse), never fan-less.
  - Document this tier honestly as the advanced build.
