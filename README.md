# The electrostatic magic wand
## What it is
If you have seen Electroboom's video about creating a Harry Potter magic wand, this is my attemt to recreate it. 
This is a hand held battery operated device that generates around 50kV DC on the tip with very low maximum current in order for it to be somewhat safe.

## What to expect from this repository
All my files, documentation and links usful for creating an electroboom-style electrostatic magic wand.
This circuitry will work with standard components, in fact I built it mostly from stuff I had laying around.
If you try to build one youself, don't expect it to work on the first try. You will have to experiment a bit yourself. But that is the fun part in my oppinion.


## Supplies that might be useful
- Soldering iron and solder
- Multimeter to measure voltage and current
- Heat gun if you decide to pot the high voltage part in wax
- 3D Printer for printing the handle, button and the tip
- Oscilloscope for debugging the circuit
- Electrical tape for to keep parts from touching and make a battery pack

## How to build it
### Step 1: Aquire parts
#### Low voltage components
|name|rating|amount|link|
|---|---|---|---|
|MOSFET Q1, Q2|GS<sub>th</sub> < 3.5V, V<sub>ds</sub> > 50V, V<sub>gs</sub> > 15V, I<sub>D</sub> > 4A, R<sub>DS(on)</sub> < 100mΩ or Heatsink |2 pcs| any MOSFET with ratings better than the described minimum requirements. I used a small piece of copper foil as a heatsink as I used SMD MOSFETs. Buy: https://www.conrad.at/de/p/infineon-technologies-irlu3110zpbf-mosfet-1-n-kanal-140-w-to-251-3-564201.html|
|diodes D1, D2|50V, 1A Peak|2 pcs|any that fit this requirement e.g. https://www.conrad.at/de/p/vishay-schottky-diode-gleichrichter-mbr160-do-204al-60-v-einzeln-163687.html|
|diodes D5, D6|15V, 1A, preferrably low forward voltage drop|2pcs|any that fit this requirement e.g. https://www.conrad.at/de/p/vishay-schottky-diode-gleichrichter-mbr160-do-204al-60-v-einzeln-163687.html|
|zener diode|V<sub>Z</sub> 12V|2 pcs|any that fit this requirement e.g. https://www.conrad.at/de/p/diotec-z-diode-zy12-gehaeuseart-halbleiter-do-41-zener-spannung-12-v-leistung-max-p-tot-2-w-sperrspannung-u-r-7-v-2811697.html|
|resistors R1, R2|100Ω, 1W|2 pcs|any that fit this requirement or multiple in paralell / series to reach the desired resistance and power e.g. https://www.conrad.at/de/p/te-connectivity-1-1625885-2-metallschicht-widerstand-100-axial-bedrahtet-1-w-5-1-st-1677271.html|
|resistor R3|10kΩ|1 pc|any that fit this requirement, Power rating does not matter, this is a bleed resistor e.g. https://www.conrad.at/de/p/tru-components-1557259-kohleschicht-widerstand-10-k-axial-bedrahtet-0204-0-1-w-5-1-st-1557259.html|
|button SW1|12V|1 pc|using a standard small pushbutton soldered on a small pcb should fits inside the housing e.g. https://www.conrad.at/de/p/weltron-t602-t602-drucktaster-24-v-dc-0-05-a-1-x-aus-ein-tastend-l-x-b-x-h-6-x-6-x-5-0-mm-1-st-700460.html|
|on/off switch SW2|12V 5A|1 pc|make sure there are tabs to mount it in the case like this one: https://www.conrad.at/de/p/tru-components-6351072-tc-r13-603c-05-schiebeschalter-250-v-ac-3-a-1-x-ein-ein-1-st-1587768.html|
|power inductors L1, L2|3A average|2 pcs|sorry I can't measure inductance... I used one with a ferrite ring core, like this one: https://www.conrad.at/de/p/534455-drossel-ringkern-radial-bedrahtet-rastermass-10-mm-1000-h-16-a-1-st-534455.html|
|power capacitor C1|4µF, 100V, 10A, low ESR!|1 pc|I prefer multiple smaller capacitors in paralell for better heat dissipation like 4*1µF: https://www.conrad.at/de/p/suntan-ts02002e105ksb0f0r-1-st-folienkondensator-1-f-250-v-10-20-mm-l-x-b-8-5-mm-x-24-mm-3014375.html|
|battery connector J1|4 Pin, 5A|1 female per battery pack, 2 male| I used JST SMP connectors from a set like this: https://www.amazon.com/dp/B0C8N8JBDC/|
|lacker coated primary coil copper wire for T1|0.1mm, 100V|3m|I created my own litz wire by folding it multiple times until I have about 16 wires paralell, twisted them together and removed the coating from the ends. Wire like this: https://www.conrad.at/de/p/block-kupferlackdraht-aussen-durchmesser-ohne-isolierlack-0-15-mm-609-m-0-10-kg-605053.html|
|18650 battery BT1-4|Li-Ion 4A discharge|4 per battery pack|I used some from an old laptop battery. Buy new ones: e.g. https://www.conrad.at/de/p/voltcraft-vc-li-3-7-2000-spezial-akku-18650-li-ion-3-7-v-2000-mah-2749811.html|
#### High Voltage components
|name|rating|amount|link|
|---|---|---|---|
|High voltage capacitor|~1nF (102), 20kV|20 pcs|https://de.aliexpress.com/item/1005006355663702.html|
|High voltage diodes, fast recovery if possible|20kV|20 pcs|I used 4 5kV Diodes in series each https://www.conrad.at/de/p/tru-components-schnelle-si-hochspannungs-gleichrichterdiode-tc-hv5-do-15-5000-v-200-ma-1582088.html, but 2 of these each should work too: https://www.conrad.at/de/p/diotec-si-hochspannungs-gleichrichterdiode-2cl72a-d2-5x12-10000-v-1-a-2806788.html
|High voltage transformer|5kV, potted, ~9 windings primary|1 pc|I rewound the primary of this transformer using lacker coated wire (20 in paralell to handle the current) with 9 windings. This is important because of the skin effect! https://de.aliexpress.com/item/4001091321165.html |
#### Miscellaneous
|name|purpose|properties|amount|source|
|---|---|---|---|---|
|wax|coating the high voltage part and the gap in the transformer to avoid corona discharge in the gap between the transformer and the secondary winding|not brittle at room temperature (arcs can jump through cracks)|depends on the size of your circuit, ~150ml should be enough |candle wax idealy mixed with some sort of soft wax like bees wax, I used wax collected from the shell of cheese|
### Step 2: Assemble the circuit
### Step 3: Test the circuit and ajust frequency and power of the oscillator
### Step 4: Pot the high voltage parts
### Step 5: Ajust the 3d models to fit your build
### Step 6: Final Assembly
### Step 7: Make the battery pack
### Step 8: Make the charger
