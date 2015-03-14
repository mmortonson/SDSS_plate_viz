## Interactive visualization of an SDSS plate and spectra

http://mmortonson.github.io/SDSS_plate_viz/

The gray circle shown on the site above represents an aluminum ["plug plate"]
used by the Sloan Digital Sky Survey (SDSS) to direct light from distant 
galaxies onto optical fibers that carry the light to spectrographs.

The colored dots represent the relative positions of 
holes drilled in the plate to observe galaxies (red) and quasars (blue).
Clicking on any of these dots will bring up the spectrum that SDSS
observed for the corresponding galaxy or quasar.
(The dots are not to scale relative to the plate; the size has been
increased to make it easier to click on them.)

The visualization currently uses a fixed plate chosen at random from
the thousands of plates used to cover the survey area. The data
for this plate were obtained using the following query in the 
SDSS SkyServer [SQL search]:
```
SELECT
    plateX.plate, plateX.ra, plateX.dec, PhotoObj.ObjID,
    specObj.mjd, specObj.fiberID, specObj.run2d, 
    PhotoObj.ra, PhotoObj.dec, specObj.z, 
    PhotoObj.modelMag_u, PhotoObj.modelMag_g, 
    PhotoObj.modelMag_r, PhotoObj.modelMag_i, 
    PhotoObj.modelMag_z, specObj.class
FROM
    PhotoObj, specObj, plateX
WHERE
    specObj.bestObjid = PhotoObj.ObjID
    AND plateX.plateID = specObj.plateID
    AND (specObj.class = 'galaxy' OR specObj.class = 'qso')
    AND plateX.plate = 3586
    AND specObj.zWarning = 0
```

Spectra for the objects on this plate are accessed using the public
[SDSS API].


[SQL search]: http://skyserver.sdss.org/dr12/en/tools/search/sql.aspx
[SDSS API]: http://api.sdss3.org/
["plug plate"]: http://classic.sdss.org/tour/plug_house.html
