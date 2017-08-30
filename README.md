# Precision-Current-Source
Low-cost precision current source for calibrating multimeters, ammeters, current shunts, etc.

### Overview
The current source is based on an electronic load in which an op amp sets a known voltage drop across precision resistors. To maintain accuracy, the set-point voltage is constant and sourced by the MAX6070 low-noise, high-precision voltage reference. Different currents are selected by changing the shunt resistors with a pin header jumper. The initial accuracy without tuning (determined by detailed calculations) is <0.1% for 500mA, <0.1% for currents of 50mA to 500nA, <0.2% for 50nA, and <0.5% for 10nA. The measured accuracy was found to be within the expected values except for the nA ranges, likely due to measurement error (see the results spreadsheet file).

### Usage
To use the current source, connect the device under test (DUT) (multimeter, etc.) to the Output +/- 4mm banana connectors on the iSource. (This setup is high-side current sensing.) Put the current set and sense jumpers in the desired position; note that the bottom sense position applies to the set currents of 1.25mA and below. Connect power leads to the screw terminal block and apply power. The current set and sense jumpers can be changed while power is applied without harming the iSource.

### Design
The electronic load design is well-known amongst the electronics community. A commonly referenced design is "EEVBlog 102 – DIY Constant Current Dummy Load for Power Supply and Battery Test." In short, the op amp controls the mosfet's gate voltage to vary the voltage drop across shunt resistors between the mosfet source and ground. The voltage drop is fed to the inverting input of the op amp to provide closed-loop feedback. The set point voltage is routed to the non-inverting input of the op amp. The difference from an electronic load is that the set point voltage does not vary, instead it is constant and supplied by a precision voltage reference. To change the current, the shunt resistors are changed. The DUT is wired between Vdd and the mosfet drain.

The current ranges were chosen based on my initial desire to calibrate my 6000 count multimeter and the EEVBlog uCurrent, hence the 50, 500 and 1250 values. The ranges can be changed by using different resistor combinations. The banana jacks are spaced at the industry standard 0.75". The power input is labeled as 5V but can work down to........................ Pin headers and jumpers were used to select the current ranges since low-leakage JFETs can't handle the higher current ranges, and dip switches can't switch the higher either. Separate sense pins are used for the 50 and 500mA ranges to account for voltage drop along the tracks due to the higher current. (Voltage drop along the tracks are included in the accuracy calculations for all current ranges.) A DPAK mosfet was used in order to use a heatsink since the mosfet will dissipate a fair amount of heat at 500mA range. It is desired to take the heat away from the PCB in order to not heat the resistors, op amp and voltage reference.

The component choices typically came down to accuracy and cost. The voltage reference gives 0.04% initial accuracy and low thermal drift for $3.35 in one off quantities. The op amp has low input offset voltage (8uV), low input offset current (5pA), and low gain-bandwidth product (80kHz) to prevent the common ringing problem, all for $1.15 in one off quantities. The highest precision resistors were used for a each current range, so cost was minimized by the selection of resistor combinations.

### Accuracy
Several steps were taken to account for the current-induced voltage drop along tracks. As previously mentioned separate sense pins are used for 50 and 500mA so that separate tracks are run to the net-zero middle of the resistor pack. The op amp's ground is run to the net-zero middle of 500mA resistor ground pack since it has the greatest voltage drop. A large ground pour is used to minimuze the resistance between the ground of the op amp and rest of the current ranges' ground return.

Extensive calculations were performed to determine the maximum guaranteed tolerance for an as-built unit. (I did not want to rely on tuning each current range.) The calculations assume worst case scenario for all specifications provided in data sheets, thus the numbers ought to be maximum accuracy values. The parameters included in the accuracy calculations are:
* **Voltage reference**: initial accuracy, thermal drift, thermal hysteresis
* **Resistors**: tolerance, thermal coefficient
* **Op amp**: offset voltage, input bias current, input offset current
* **Track resistance**: 

### Results
I measured the accuracy with a Keysight 34465A 6.5 digit DMM with a 4 month old calibration. The 34465A has a low current range of 1uA with 1pA resolution. I used a single cell lithium ion battery charged to 4.2V to power the iSource. I placed the battery and iSource in a cast aluminum case to minimize EMI. The output was wired to the 34465A with an unshielded twisted pair wires. I used remote logging via PyVISA to remove myself from the measurement area. The 34465A was warmed up for 1 hour, and each current range was allowed to settle for 5 minutes before collecting data, although the currents settled within 10-30 seconds. I took 500 measurements with 10 NPLC at the lowest 34465A current range possible.

The spreadsheet shows the average value, accuracy % based on the measured average,34465A uncertainty $, and % standard deviation of the 500 measurements.

### Cost
As of June, 2017, the total build cost was $48 including the OSHPark PCB not listed in the BOM. Lower tolerance resistors may be used to significantly reduce the cost. New accuracy calculations can be performed by changing the resistor tolerance in the spreadsheet.

### License
The project is licensed as open source hardware and Creative Commons Attribution-ShareAlike 3.0 (CC BY-SA 3.0 US)
