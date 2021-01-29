# DRAFT UNDER TEST: Network UPS Tools (K)Ubuntu 20.04 Shutdown With 3024 Protocol Tripp Lite UPS For A. Lizard

* Note 1: Testing this process with a specific user! If you are not that user, please disregard this process and contact me! (@DavidZomaya on Twitter)
* Note 2: Security and passwords are not optimal here. Modify as needed.

1. Process assumes this is your initial configuration: https://askubuntu.com/a/1249758

2. Use the below /etc/nut/upsmon.conf or a similar version : https://github.com/dzomaya/TestingConfigs/blob/main/upsmon.conf
	* The key additions are: 
  ```
  MONITOR myups@localhost 1 upsmon pass master
  ```
  ```
	MINSUPPLIES 1
  ```
		

3. Make sure there is a matching user in /etc/nut/upsd.users like what is here: https://github.com/dzomaya/TestingConfigs/blob/main/upsd.users

4. Because it is easier to do Network UPS Tools shutdown with Low Battery than with "Time On Battery", make these two modifications to /etc/nut/ups.conf
  ```	
  # Ignore default Low Battery 

	ignorelb
  ```
  ```	
  # Set a Low Battery Warning Level. Use a level that makes sense for your application, 

	# e.g. 50 percent to shut down at 50 percent battery charge

	override.battery.charge.low = 88
  ```
	
Example here: 
https://github.com/dzomaya/TestingConfigs/blob/main/ups.conf

5. Reboot or restart the driver (upsdrvctl start) & upsmon (upsmon -c reload)

6. Test the new configuration! Using Network UPS Tool's fsd (see: https://networkupstools.org/docs/man/upsmon.html) can help, but for end to end testing you probably want to:
Safely place the UPS on battery and confirm the Operating System and then UPS, gracefully shut down. 
