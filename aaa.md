RCBenchmark

Installation procedure

This is a tutorial on how to install the[ RCBenchmark 1580](https://www.rcbenchmark.com/wp-content/uploads/2016/01/2016-02-04-RCbenchmark-1580-datasheet.pdf) in the laboratory.

1. Download the software for the [RCBenchmarkGUI](https://rcbenchmark.gitlab.io/docs/en/dynamometer/software/dynamometer-software-download.html).
2. Follow the tutorial for the installation of the hardware in the [RCBenchmark manual](https://www.rcbenchmark.com/wp-content/uploads/2016/03/Manual_Series_1580_1_12.pdf) \(step 1 to 6\).

3. Download the drivers located [here](https://rcbenchmark.gitlab.io/docs/en/dynamometer/software/troubleshooting-driver-issues.html). Run the .ex file as administrator.

4. Follow the instructions for the installation of the software in the [RCBenchmark manual](https://www.rcbenchmark.com/wp-content/uploads/2016/03/Manual_Series_1580_1_12.pdf) \(step 7 to 12\) BUT do not use the chrome app. Use the software downloaded at step 1. The chrome app seems to yield inferior results \(poor sample rate\) and has problems recognizing the USB port of the RCBenchmark.

5. When the Benchmark is installed \(not bolted yet\), the Thrust and Torque Calibration can be performed in the Utilities menu. Afterward, the Load Cells can be tared to obtain maximum precision. After these calibrations, the setup can be bolted. 

6. Use the Manual Control menu to directly send commands to the ESC or the motor. 

Other information:

* Always wear security glasses when using the TestBench. The motors can go to speeds of 10 000 RPM and the vibrations caused by the setup at high intensity can unscrew the bolts of the propeller. 

* The signal sent by the software to the ESC is a PWM signal of frequency 50Hz and duty-cycle between 1/20 \(No throttle\) and 1/10 \(max throttle\). This signal has a tension between 0 and 5V. The maximum and minimum value for the duty-cycle of the PWM can be changed in the section Utilities-&gt;Outputs limits.
* Be sure to not firmly bolt the Benchmark before having completed the Thrust Calibration because this procedure needs to be done with the setup placed vertically \(with a C-Grip\). 
* Stiff security cutoffs are in place on the GUI, which limits the value of current, RPM, vibrations and other critical value on the Testbench. Their value can be modified in the menu Safety Cutoffs. 

* The sample rate of the Testbench is dependent on the performance of the computer connected to the Testbench. Maximum 50Hz with a good computer. 

* 

Usefuls links:

* [Short guide on the installation of the RCBenchmark 1580 ](https://rcbenchmark.gitlab.io/docs/en/dynamometer/series-1580/series-1580-setup-guide.html)

* [Main site of RCBenchmark 1580](https://www.rcbenchmark.com/dynamometer-series-1580/)

By Karim Bouzid, If you have any questions, contact me at karim.bouzid.1@ulaval.ca

