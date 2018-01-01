## Issues to solve to run with ROS

* Fix ROS 
  * Due to the update of cmake to install glog, we lost some dependencies the best would be to update all basics and reinstall the distribution \(Jade\) to start again with something clean and up to date. A new distribution could be tested but nothing insure that it will work on the pelican \(may require lot of work to fix everything\). 
  * **Do not upgrade ubuntu, jade only works on 14.0**
  * Note that the pelican and the firefly use the same motherboard, an image of a working system could be useful.
* Compile the package

  * Add mav\_comm to your src and install glog 

* To run the package
  * Transfert the modified firmware to the HLP 
  * Launch the HL\_interface via : rosrun asctec\_hl\_interface your-topic



**Note :** the bios battery have to be changed, it's not problematic but lead to issues when you just power on and boot. 

