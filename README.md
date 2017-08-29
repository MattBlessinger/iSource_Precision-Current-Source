# Precision-Current-Source
Precision current source for calibrating multimeters, ammeters, current shunts, etc.

Overview: 
The current source is based on an electronic load in which an op amp sets a known voltage drop across precision resistors by controlling the mosfet's gate voltage. To maintain accuracy, the set-point voltage is constant and sourced by the MAX6070 low-noise, high-precision voltage reference. Different currents are selected by changing the shunt resistors with a pin header jumper. The designed tolerance without tuning (determined by detailed calculations) is <0.1% for currents of 500mA to 500nA, <0.15% for 50nA, and <0.5% for 10nA.

Usage:
To use the current source, connect the DUT (multimeter, etc.) to the DUT + & - 4mm banana connectors on the iSource. (This setup is high-side current sensing.) Put the current set and sense jumpers in the desired position; note that the bottom sense position applies to set current of 1.25mA and less. Connect power leads to the screw terminal block and apply power. The current set and sense jumpers can be changed while power is applied without harming the unit.

Design:


Accuracy:


Results:

