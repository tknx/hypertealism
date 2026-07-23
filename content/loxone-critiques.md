---
title: "Loxone critiques"
craft_id: 45EE4645-62C8-435C-96C5-BE7EA0B93A2B
date: 2026-04-18T17:23:56.073Z
lastmod: 2026-07-23T19:13:44.710Z
---

Ongoing list, updated whenever

Interface

  - Saving should not default to project.loxone but whatever file name was opened first. 
  - There is no clear communication when you connect if it is going to download over your file or not - the workflow is a flat out disaster
  - Backups are primitive and not very well done - honestly just make every save a version and let me flag key ones
  - Blocks should not be able to go off the borders
  - I'd like meaninful room hierarchy (e.g., Whole House > Floors > Combined Areas > Specific Rooms) that also add up the underlying sq footage and let me order rooms according to floor then alpha versus just alpha
  - Room Types are a bit confusing and not sure what they are used for

Config Blocks

- Schedule Blocks
  - All schedule blocks should have Everyday as default and you can add Weekdays, Weekends, or individual days of the week as options
  - Main schedule block should be fully HVAC enabled to allow combining different IRCs into one. (But see HVAC section)
- Analog values
  - Analog values and text are second citizens to pulses - most blocks should be trimodal (digital, analog, text) ; analog memory is a conceptually annoying workaround
  - Gating Blocks are needed - pass through if allowed, otherwise block (not 0, no signal) (for digital, analog, and text - any data flows)
- Logging
  - Should be able to push syslog to remote server instead of wearing down the SD card
  - /dev/syslog does not comply with RFC5424.
  - Many blocks are terrible loggers, every input, every output value, every parameter change and initial setting should be logged *at the minimum*; many log nothing
- Irrigation
  - Module should support more sophisticated models using Eto, water tension meters, soil moisture meteres, lux by zone (at least match rainbird and HA smart irrigation plugin but realistically should be FAO56)
- Shading Logic
  - Needs to accommodate nonlinear curtain motor movement (ramp up speeds, slight changes as roll unwinds, delay in command - realistically a formula would be best)
  - When using DCT; open, close, and hold might be three different relays, not two; so should be three independent VQs and outputs on the shading block
- HVAC
  - Different zones should not mean different schedules. I add a damper to modulate the air to get the temperature to be consistent, not to have wildly different temps. How many times do you want me to adjust the temp?
  - Mode has multiple overlapping meanings across blocks because Loxone fails to distinguish between functional operating mode (e.g. a minisplit has heat, cool, dry, fan) and user operating modees (heat, cool, auto, heat to setpoint but don't cool)
  - On top of that modes are keyed to different numbers across blocks so you can't slave one to another without blocks
  - Overshooting is ridiculously common, there is a PID block, It should be integrated
  - Tooltips are in C even when my miniserver is set to F
- Ventilation (RVC and TVC blocks)
  - While HVAC is opaque and not well designed, ventilation is outright stupid
  - Is completely missing the Pto block of lighting. Total oversight. (Also why is musics exact same thing called Ti?); so you turn off the light manually with a button press and it instantly turns back on because your arm is moving - dumb
  - Should have an On pin and Tr pin like, you know, every other control?
  - Should have a humidity rise trigger built in (take a min moving value and compare to current and trigger)

Hardware

- Where is a good mmWave sensor? - Everything Presence Pro is a much better sensor than all of the Loxone sensors and cheaper
- Needs Apple Wallet support for the NFC reader
- In fact, fingerprint or facial recognition would be better than any of these

Integrations

- Loxone needs to be a full Matter coordinator and client both
- Supporting only 16 MQTT feeds is a sick joke

User Management

- Permissions are unions not intersections, so I can't say you get lighting and shading across these specific rooms unless I do it device by device 

Education

- 
- There is no UI/XML cross-reference available
- Descriptions are abstract and often difficult to follow; every single one should have:
  - is it a pulse or sustained
  - what values it intakes or outputs
  - which pins are dominant and subordinate to it
  - a concrete example or two of how it will work connected to other blocks with a nice narrative story of what happens
- There should never be hidden settings (e.g. CO2 sensor has a -9 hysteresis to turn off on RVC)
