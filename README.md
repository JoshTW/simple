# simple
Mission modeling review

Reviewing the options for modeling a space mission, with an eye to design a mission into an astroid field. This will probably require modeling a lot of gravity fields. And space weather.


## Simulation Options:
### GMAT
Name: General Mission Analysis Tool (GMAT)
Desc: GUI, Script, NASA
Website: http://gmat.gsfc.nasa.gov/
Download Location: http://sourceforge.net/projects/gmat/files/GMAT/GMAT-R2014a/
Note: To have more gravity fields, use ..._ForceModel.CentralBody, ..._ForceModel.PrimaryBodies, ..._ForceModel.PointMasses

GMAT DefaultProp_ForceModel.CentralBody = Earth;
GMAT DefaultProp_ForceModel.PrimaryBodies = {Earth};
GMAT DefaultProp_ForceModel.PointMasses = {Luna, Sun};

GMAT DefaultProp_ForceModel.GravityField.Earth.Degree = 10;
GMAT DefaultProp_ForceModel.GravityField.Earth.Order = 10;
GMAT DefaultProp_ForceModel.GravityField.Earth.PotentialFile = 'JGM2.cof';
GMAT DefaultProp_ForceModel.GravityField.Earth.EarthTideModel = 'None';



### Kerbal Space Program
Name: Kerbal Space Program
Desc: GUI, Game, requires mods to have real world physics, models not verified by other software.
Website: https://kerbalspaceprogram.com/
Download: http://store.steampowered.com/app/220200/
Download (other): http://www.curse.com/ksp-mods/kerbal
Note: Need to verify simulation in another program

### Game Engines
Name: Unity, Blender, Unreal, ...
Desc: GUI, 



