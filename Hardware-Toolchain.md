** WIP work in progress **

# Tools used:

* KiCAD 7.0.7
* FreeCAD 0.21.1 with KiCAD StepUp v10.19.4



# KiCad Setup
* Install KiCAD 7.0.7

# FreeCAD Setup
* Install FreeCad 0.21.1
* Install "KicadStepUp Workbench" and "dxf-library" over AddOn Manager
* Switch to KiCadStepUp Workbench (Drop-Down Box Top Left near Main Menu)
* Adjust FreeCad Settings: Import-Export => Step and DXF, kicadStepUpGui according to the [CheatSheet](https://raw.githubusercontent.com/easyw/kicadStepUpMod/master/demo/kicadStepUp-cheat-sheet.pdf) (defaults do NOT work!)
* [for now](https://github.com/easyw/kicadStepUpMod/issues/181), Import of DXF (silkscreen) does not work. Solution: Change C:\Users\xxx\AppData\Roaming\FreeCAD\Mod\dxf-library to tag 1.40 with git and disable "Automatic update" in Import-Export => DXF