

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

 
    
