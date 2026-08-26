
A. Install Lubrication module (work for trajectory)
	1. Download the lube_component.zip inside /linuxcnc/components
	2. Compile component lube.comp
		$ sudo halcompile --install lube.comp 
	3. Into de .hal
		loadrt lube
		addf lube.0 servo-thread
	 
		net machine-is-enabled lube.0.mrun
		setp lube.0.xpath 3000	#(mm, travel distance)
		setp lube.0.zpath 3000	#(mm, travel distance)
		setp lube.0.lubetime 3	#(seconds, pump ON)
		net lubevel_x <= joint.0.vel-cmd => lube.0.xvel
		net lubevel_z <= joint.1.vel-cmd => lube.0.zvel
		net lube-sig <= lube.0.out => parport.0.pin-04-out

B. Install Lubrication module (DOESN'T WORK)
	1. Clone the project:
		$ git@github.com:AlexmagToast/LinuxCNC-LubeDude.git
	2. Put the module lubedude.py inside:
		/linuxcnc/components
	3. Become the modulo executable with:
		sudo chmod +x lubedude.py
	4. Copy the lubedube.py to /usr/bin without suffix ".py"
		$ sudo cp lubedude.py /usr/bin/lubedude
	5. Add this entry to the end of your hal file:
		loadusr lubedude
	6. Test arduino connector working:
		$ halrun
		$ loadusr lubedude
		$ show pin
		

C. Install LinuxCNC_ArduinoConnector

	1. Clone the project:
		git@github.com:AlexmagToast/LinuxCNC_ArduinoConnector.git
	2. Copy the project with the original FOLDER NAME: 
		Set the folder name: linuxcnc/arduino/
	
	3. Set the i/o, pwm outputs, analog inpust, etc. Inside the source:
		LinuxCNC_ArduinoConnector.ino
	4. Check if python-serial is installed:
		$ python3 -c "import serial; print(serial.__version__)"
		-> If installed: It will print the version number (e.g., 3.5).
	5. Install python-serial if necessary
		$  sudo apt-get install python-serial
	6. Check arduino.py to match your arduino settings. The first line must be:
		#!/usr/bin/env python3 
	7. Make arduino-connector.py executable
		$ sudo chmod +x
	8. Copy the arduino-connector.py to /usr/bin without suffix ".py"
		$ sudo cp arduino-connector.py /usr/bin/arduino-connector
	9. Add this entry to the end of your hal file:
		loadusr arduino-connector
	10. Test arduino connector working:
		$ halrun
		$ loadusr arduino-connector
		$ show pin
