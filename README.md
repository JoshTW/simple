# simple
Mission modeling review for a space mission in an astroid field.

Reviewing the options for modeling a space mission, with an eye to design a mission into an astroid field. This will probably require modeling a lot of gravity fields. And space weather.

In order to meet the space apps challenge "Create Your Own Asteroid Mission" GMAT will need to be used, wether it is the primary simulator or just verfies the mission plan from a different tool. I plan to take asteroid data from http://minorplanetcenter.net/web_service and import it into GMAT. Also see how to import this data into other options. This might not be important at all because the distances are so large and gravity is so small.

A note on astroid lander design. In order to land on an astroid I am thinking that some kind of anchor/harpoon could be used. How it would work - Once the ship got into orbit of an astroid it would not be in geosycrones orbit. The smart anchor would be launched at the asteroid with a slack tether. If the anchor comes to rest on the surface, the tether is allowed to continue to deploy as the asteroid spins about it's access. Once at least one wrap of the asteroid is completed the anchor drives or flies to connect to the tether. The ship fires its engines to enter geosync orbit stabilized by the tether. This allows space elevator style landing, and launching. And the tether loop provides an anchor for surface activity.

- Check material strength and volume (per linear meter) of Carbon nanotube-based fibres invented at Rice University or a Super-Nanotube rope
- find a high density asteroid

## Space Apps Report

I spent the weekend researching simulation options and working getting data into GMAT. I placed the database from http://minorplanetcenter.net/web_service on a local mysql server. I can get a list of asteroids that have an H value from the neowise project sorted by delta v. This provides Asteroid 0228502 which is about 300 meters (plus or minus 50m) diameter and has a 5.52 km/sec delta v, an estimate of the amount of energy necessary to jump from LEO (Low Earth Orbit) to the asteroid's orbit.
I could not enter this asteroids orbit into GMAT with the help of the Horizons telnet command line interface:   telnet  ssd.jpl.nasa.gov 6775 but I was able to get a working SPK file for the 0000004 asteroid (Vesta). I think the normal tutorials will allow me to plan a simple mission to Vesta.

UPDATE

Doing a search for 0228502 in Horizons provides working SPK files. I still don't know how to generate a working SPK file from "your own osculating elements" using data from the minor planet center. I still don't have a source or method to estimate a resonable GM or Mu [km^3/sec^2] value.


## Simulation Options:
### GMAT
* Name: General Mission Analysis Tool (GMAT)
* Desc: GUI, Script, NASA
* Website: http://gmat.gsfc.nasa.gov/
* Download Location: http://sourceforge.net/projects/gmat/files/GMAT/GMAT-R2014a/
* Note: To have more gravity fields, use ..._ForceModel.CentralBody, ..._ForceModel.PrimaryBodies, ..._ForceModel.PointMasses



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
* Website: http://en.spaceengine.org/
* License: http://en.spaceengine.org/index/license/0-30

### Celestia
* Lets you explore and show objects in space
* Like eyes on the solar system
* Website: http://celestia.sourceforge.net/


### Universe Sandbox

### Mathimatical Models
* Name: Scilab, Matlab, 
* Note: Scilab with CelestLab

## Data Sources ##
http://minorplanetcenter.net/web_service
or
https://data.nasa.gov/dataset/International-Astronomical-Union-Minor-Planet-Cent/6j72-rq9c

This data set uncompresses to about a 1.8 gigabyte cvs file or a 0.9 gigabyte sql file. Contains information about 682,079 Asteroids/minor planets.

Picking an object "SELECT * FROM `properties` WHERE h_neowise IS NOT NULL ORDER BY `delta_v` ASC LIMIT 0 , 30;"

http://ssd.jpl.nasa.gov/sbdb.cg
Can search for the designation number from the mpc source by adding 2000000. eg. Vesta is designation 0000004 and it's NAIF ID is 2000004

### 4 Vesta seems cool
* Mass=2.590x10^20 kg (from Eyes on the Solar System)
* Rotation Period=5.342h (from Eyes on the Solar System)
* Diameter of 550km x 462km elliptical profile (from Wikipedia from [Povenmire, H. (September 2001). "The January 4, 1991 Occultation of SAO 93228 by Asteroid (4) Vesta". Meteoritics & Planetary Science 36 (Supplement): A165. Bibcode:2001M&PSA..36Q.165P])
* Probably not a very good candidate for the lasso landing method descriped above.

Data from the minor planet center (mpc) database. 
SELECT * FROM `properties` WHERE properties.name LIKE 'Vesta'
delta_v = 9.39 km/sec (Low Earth Orbit to asteroid's Orbit)

### Creating a SPICE file for GMAT
Horizons WWW interface: http://ssd.jpl.nasa.gov/x/spk.html, 
Horizons telnet command line interface:   telnet  ssd.jpl.nasa.gov 6775
  An example script is available at:  ftp://ssd.jpl.nasa.gov/pub/ssd/smb_spk

Entering custom data:
EPOCH= epoch_jd
EC= eccentricity
QR= perihelion_distance
TP= perihelion_date_jd
OM= ascending_node
W= argument of perihelion
IN= inclination

0228502
EPOCH= 2456600.5  EC= 0.196640824  QR= 0.870321442  TP= 2456526.2612306  OM= 171.1889368  W= 35.8312024  IN= 7.6236264  H= 20 RAD= 0.3
-> wld10395.15 (binary)


4 Vesta
EPOCH= 2456800.5  EC= 0.088612126  QR= 2.152206144  TP= 2456923.7240618  OM= 103.8513349  W= 151.2171118  IN= 7.1404949 RAD= 262.7
-> wld361.15 (binary)
-> wld2309.15 (ASCII)

Using existing Vesta data -> wld2309.15 (binary)

The existing Vesta data works in GMAT but the generated data isn't working. Using both the telnet and the web gui results in an "Utility Exception: Error getting state for body "2228502". Message received from CSPICE is: [Insufficient ephemeris data has been loaded to compute the state of 2228502 relative to 399 (EARTH) at the ephemeris epoch 2015 JUN 01 12:00:35.184.]"

Values for existing data
<code>
*******************************************************************************
JPL/HORIZONS                       4 Vesta                 2015-Apr-12 15:45:24
Rec #:     4 (+COV)   Soln.date: 2013-Jul-16_08:46:23   # obs: 7107 (1827-2013)

FK5/J2000.0 helio. ecliptic osc. elements (au, days, deg., period=Julian yrs):

  EPOCH=  2451544.5 ! 2000-Jan-01.00 (CT)          Residual RMS= .30082
   EC= .09002258422539088  QR= 2.148943570760723   TP= 2451614.8711416456
   OM= 103.9514346862076   W=  149.5867755441192   IN= 7.133936541718016
   A= 2.361535059561293    MA= 340.8879587395919   ADIST= 2.574126548361863
   PER= 3.62911            N= .271589181           ANGMOM= .026327626
   DAN= 2.53956            DDN= 2.17365            L= 253.7322376
   B= 3.6044855            MOID= 1.13629997        TP= 2000-Mar-11.3711416456

Asteroid physical parameters (km, seconds, rotational period in hours):
   GM= 17.8                RAD= 265.               ROTPER= 5.342
   H= 3.2                  G= .320                 B-V= .782
                           ALBEDO= .4228           STYP= V

ASTEROID comments:
1: soln ref.= JPL#33, OCC=0
2: source=ORB
*******************************************************************************
</code>

So I might need to add "A= MA= ADIST= PER= N= ANGMOM= DAN= DDN= L= B= MOID= TP= " to my custom osculating elements except that the telnet interface indicates not to add some of these values.

A= semimajor_axis
MA= mean_anomaly

Making Asteroid 0228502 a space craft in GMAT seems to require changing it's location into Earth based coordinates.
