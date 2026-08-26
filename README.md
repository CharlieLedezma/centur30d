

A. Install Lubrication module


B. Install LinuxCNC_ArduinoConnector

	1. Copy the project with the original FOLDER NAME: 
		/LinuxCNC_ArduinoConnector
	
	2. Set the i/o, pwm outputs, analog inpust, etc

	3. Install python-serial
		$  sudo apt-get install python-serial
	4. Check arduino.py to match your arduino settings. The first line must be:
		#!/usr/bin/env python3 
	5. Make arduino-connector.py executable
		$ sudo chmod +x
	6. Copy the arduino-connector.py to /usr/bin without suffix ".py"
		$ sudo cp arduino-connector.py /usr/bin/arduino-connector
	7. Add this entry to the end of your hal file:
		loadusr arduino-connector
	8. Test arduino connector working:
		$ halrun
		$ loadusr arduino-connector
		$ show pin
