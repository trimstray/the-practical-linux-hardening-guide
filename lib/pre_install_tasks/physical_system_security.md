## Pre install tasks

### Physical system security

#### :information_source: Introduction

The primary goal of physical security is to stop physical attacks whenever possible, and, failing that, to slow them down so that hopefully someone will notice the presence of the attacker in a restricted area, preventing any tampering with the system. Weak physical security often invalidates any other security measure, and thus should be prioritized.

#### :eight_pointed_black_star: Secure rooms

For secure rooms make sure that the walls go beyond the false ceiling, and below the raised floor, large vents should also be covered with bars if possible.

###### Useful resources

- [Establishing Server Room Security](https://www.getkisi.com/guides/server-room-security)
- [How to secure your server room](https://www.hpe.com/us/en/insights/articles/how-to-secure-your-server-room-1809.html)

#### :eight_pointed_black_star: Monitoring

Monitoring the room with CCTV or wired cameras is a great way to provide security for your server room or data center. As well as providing video footage of events which may occur - door open events, motion detection or any other sensor event, they also act as a visual deterrent to would be criminals.

Solution for remotely monitoring the temperature ensue proactively notify you when the temperature goes above or below pre-defined thresholds, potentially allowing you to take corrective measures before encountering costly downtime.

###### Useful resources

[Monitoring Physical Security for your Server Room](https://www.enviromon.net/monitoring-physical-security-server-room/)

#### :eight_pointed_black_star: Air conditioning

Computer equipment generates heat, and is sensitive to heat, humidity, and dust, but also the need for very high resilience and failover requirements. Maintaining a stable temperature and humidity within tight tolerances is critical to IT system reliability.

Air conditioning designs for most computer or server rooms will vary depending on various design considerations, but they are generally one of two types: "up-flow" and "down-flow" configurations.

###### Useful resources

[How to Monitor Server Room Temperature and Environmental Conditions](https://www.enviromon.net/how-to-monitor-server-room-temperature/)

#### :eight_pointed_black_star: Fire protection

The fire protection system's main goal should be to detect and alert of fire in the early stages, then bring fire under control without disrupting the flow of business and without threatening the personnel in the facility. Server room fire suppression technology has been around for as long as there have been server rooms.

There are a series of things you need in a fire suppression system:

- an emergency power off function
- gas-based suppression system
- fire detection sensors

###### Useful resources

[What Type of Suppression System Works Best for Computer Room Fires?](https://www.controlfiresystems.com/news/what-type-of-suppression-system-works-best-for-computer-room-fires/)

#### :eight_pointed_black_star: Locked racks

All systems should be securely fastened to something with a cable system, or locked in an equipment cage if possible. Case locks should be used when possible to slow attackers down.

###### Useful resources

[Securing the Physical Safety of Data with Rack-Level Access Control](https://securitytoday.com/blogs/reaction/2018/02/Securing-the-Physical-Safety-of-Data-with-Rack-Level-Access-Control.aspx)

#### :eight_pointed_black_star: Console security

With physical access to most machines you can simply reboot the system and ask it nicely to launch into single user mode, or tell it to use `/bin/sh` for init.

###### Useful resources

[Physical Security](https://www.tldp.org/HOWTO/Security-HOWTO/physical-security.html)

#### :eight_pointed_black_star: BIOS protection

In the program itself to edit the BIOS settings:

- only boot from specific drive
- disable the unused controllers
- disable the booting from external media devices (USB/CD/DVD)
- enable BIOS password

You need to protect the BIOS of the host with a password so the end-user won’t be able to change and override the security settings in the BIOS.

Main reasons for password protecting the BIOS:

- preventing changes to BIOS settings
- preventing system booting

Because the methods for setting a BIOS password vary between computer manufacturers, consult the computer's manual for specific instructions.

  > For this reason, it is good practice to lock the computer case if possible. However, consult the manual for the computer or motherboard before attempting to disconnect the CMOS battery.

###### Useful resources

[BIOS Protection Guidelines for Servers (Draft)](https://csrc.nist.gov/csrc/media/publications/sp/800-147b/final/documents/draft-sp800-147b_july2012.pdf)

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Physically secure machine (also outside of a server room) | :black_square_button: | :black_square_button: |
| Monitoring server rooms with CCTV or wired cameras | :black_square_button: | :black_square_button: |
| Remotely monitoring the temperature | :black_square_button: | :black_square_button: |
| Efficient air conditioning solution | :black_square_button: | :black_square_button: |
| Efficient fire protection system | :black_square_button: | :black_square_button: |
| Locked cage (server case) | :black_square_button: | :black_square_button: |
| Physical access to server console | :black_square_button: | :black_square_button: |
| Password on the BIOS | :black_square_button: | :black_square_button: |
| Disable external media devices | :black_square_button: | :black_square_button: |
| Periodic physical inspections | :black_square_button: | :black_square_button: |
