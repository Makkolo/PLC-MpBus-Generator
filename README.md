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
| Global variable list name  | Variable name (before VAV name) |  |  | | | | |
| -------------------------- | ------------------------------- | ------------------------- | ------------------------- | ------------------- | ------------------- | ------------------- | ------------------- |
| VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
| next VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
| next VAV  name  | MP-bus line/card  | Line address | VAV code/serial nr. | Minimum air sp | Normal air sp | Maximum air SP | VAV size (airflow) |
and so on...
