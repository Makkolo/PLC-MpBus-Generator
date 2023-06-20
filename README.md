# PLC-MpBus-Generator
Basic command window program that generates the following:
* Global variable list
* VAV datatype
* MP-bus lines (CFC)
* VAV max program, for optimizer(ST)
* MP-bus auto addressing program(ST)
* Function for autoaddressing(ST)

Generates XML file based on the [IEC 61131-3 standard](https://plcopen.org/technical-activities/xml-exchange), and should be compatible with all IEC 61131-3 programs like for example codesys 3.5.

**Even if a program supports IEC 61131-3, alignments in cfc programs can sometimes be off. But this is purely visual and does not impact performance.**

**The wagoAppMp-bus library is used for the MP-bus programs, so they're only compatible with wago PLC's. The rest is independent**

## Generated program structure
* GVL containing all VAV's as datatypes.
  - Variable format used: GVLname.VariableName_VAVName
* Generalized DTU for VAV's.
* VAV max program that retrieves the maximum angle (0-100%) out of all VAV's, sepperated by supply and exhaust.
* One program for each MP-bus line.
* VAV MP-bus auto-addressing program for addressing.
* VAV MP-bus auto-addressing function.

## Input format
### .txt file
Currently uses a txt file as input. The txt file needs to be split with tabs and lines, like this:
| Global variable list name  | Variable name (before VAV name) |  |  |  | | | | |
| -------------------------- | ------------------------------- | ------------------------- | ------------------------- | ------------------- | ------------------- | ------------------- | ------------------- |
| VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
| next VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
| next VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
and so on...

## How to use
1. Download the last release and store it somewhere.
2. Create a .txt file in the same folder and fill it in acording to the input format. (reccomended to create the input in excel and then copy it into the .txt file)
3. Run the downloaded file, choose ipnut VAV name format used, input the name of the .txt file when asked for.
4. After succesful generation, the output .xml file is stored in the same folder and the path is copied.
5. Open the PLC program and find the import button (import PLC open xml in some programs)
6. When prompted to choose import file, CTRL + V and then enter to import the generated xml file.
7. Choose the content to import, and press import.

## Example
Input file:

<img width="522" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/6f2b59fe-525a-4701-9f4f-a167ba5c3a66">

Command window:

<img width="528" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/3c330bfb-3a21-4eec-aab1-02016eb94c83">

Import dialog in codesys 3.5:

<img width="596" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/bb96aefe-6354-4dfa-8c7f-63e7ad247b0e">

Imported items (libraries not included):

<img width="145" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/8367f551-12c2-4697-ab5f-68ad5ef2d9b4">

GVL (add retain persistent if wanted):

<img width="1278" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/4c3077db-4fd6-4d72-9398-c8b8c50bcbe1">

VAV datatype: 

<img width="423" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/bf32651d-08f0-47e0-9811-f25968cfe21d">

One MP-bus line:

<img width="894" alt="image" src="https://github.com/grisMort/PLC-MpBus-Generator/assets/115706031/d6c787cd-203a-4c76-9fa9-1b32442c6784">
