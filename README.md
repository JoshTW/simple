# simple
Mission modeling review for a space mission in an astroid field.

Reviewing the options for modeling a space mission, with an eye to design a mission into an astroid field. This will probably require modeling a lot of gravity fields. And space weather.

In order to meet the space apps challenge "Create Your Own Asteroid Mission" GMAT will need to be used, wether it is the primary simulator or just verfies the mission plan from a different tool. I plan to take asteroid data from http://minorplanetcenter.net/web_service and import it into GMAT. Also see how to import this data into other options. This might not be important at all because the distances are so large and gravity is so small.

A note on astroid lander design. In order to land on an astroid I am thinking that some kind of anchor/harpoon could be used. How it would work - Once the ship got into orbit of an astroid it would not be in geosycrones orbit. The smart anchor would be launched at the asteroid with a slack tether. If the anchor comes to rest on the surface, the tether is allowed to continue to deploy as the asteroid spins about it's access. Once at least one wrap of the asteroid is completed the anchor drives or flies to connect to the tether. The ship fires its engines to enter geosync orbit stabilized by the tether. This allows space elevator style landing, and launching. And the tether loop provides an anchor for surface activity.

- Check material strength and volume (per linear meter) of Carbon nanotube-based fibres invented at Rice University or a Super-Nanotube rope
- find a high density asteroid


## Simulation Options:
### GMAT
* Name: General Mission Analysis Tool (GMAT)
* Desc: GUI, Script, NASA
* Website: http://gmat.gsfc.nasa.gov/
* Download Location: http://sourceforge.net/projects/gmat/files/GMAT/GMAT-R2014a/
* Note: To have more gravity fields, use ..._ForceModel.CentralBody, ..._ForceModel.PrimaryBodies, ..._ForceModel.PointMasses

GMAT DefaultProp_ForceModel.CentralBody = Earth;
GMAT DefaultProp_ForceModel.PrimaryBodies = {Earth};
GMAT DefaultProp_ForceModel.PointMasses = {Luna, Sun};

GMAT DefaultProp_ForceModel.GravityField.Earth.Degree = 10;
GMAT DefaultProp_ForceModel.GravityField.Earth.Order = 10;
GMAT DefaultProp_ForceModel.GravityField.Earth.PotentialFile = 'JGM2.cof';
GMAT DefaultProp_ForceModel.GravityField.Earth.EarthTideModel = 'None';

### Kerbal Space Program
* Name: Kerbal Space Program
* Desc: GUI, Game, requires mods to have real world physics, models not verified by other software.
* Website: https://kerbalspaceprogram.com/
* Download: http://store.steampowered.com/app/220200/
* Download (other): http://www.curse.com/ksp-mods/kerbal
* Note: Need to verify simulation in another program

### Orbiter
* Name: Orbiter 2010
* Desc: Simulator
* Website: http://orbit.medphys.ucl.ac.uk/
* Download: http://orbit.medphys.ucl.ac.uk/download.html

### Game Engines
* Name: Unity, Blender, Unreal, ...
* Desc: GUI, 

### Space Engine
* Lets you explore and show objects in space. No space ships
* Like eyes on the solar system

### Celestia
* Lets you explore and show objects in space
* Like eyes on the solar system


### Universe Sandbox

### Mathimatical Models
* Name: Scilab, Matlab, 
* Note: Scilab with CelestLab

## Data Sources ##
http://minorplanetcenter.net/web_service

This data set uncompresses to about a 1.8 gigabyte cvs file or a 0.9 gigabyte sql file. Contains information about 682,079 Asteroids/minor planets.

Picking an object "SELECT * FROM `properties` WHERE h_neowise IS NOT NULL ORDER BY `delta_v` ASC LIMIT 0 , 30;"

4 Vesta seems cool
Mass=2.590x10^20 kg
Rotation Period=5.342h