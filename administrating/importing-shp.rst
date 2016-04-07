*****************************
Importing Location Boundaries
*****************************

The Indicia Warehouse allows you to upload a list of locations from an ESRI Shape File (.shp) which is a widely available GIS file 
format. This includes setting the boundaries of those locations and it can either create new locations or update existing ones.

Import Steps
============

1. First you need a suitable SHP file. The SHP file must contain a list of objects to be imported as locations in Indicia, as well as at least one attribute for the name of each location. You will therefore have a file called _myfile_.shp and also a file called _myfile_.dbf containing the attribute values.
2. Zip these 2 files into a single zip file with the same name, ready for upload.
3. Log into the Warehouse.
4. Select Lookup Lists > Locations from the menu.
5. Click the Browse button next to the input at the bottom called "Upload a Zipped up SHP fileset into this list" and select your _myfile_.zip file. Click the Upload Zip File button.
6. On the next page are various options for specifying how the upload is handled. You can choose the following things:

    a. Whether to import the polygon into the location's centroid or boundary geometry.
    b. Whether the locations have a parent location.
    c. Which spatial reference projection is used in the SHP file (SRID). 
    d. Which website the locations are being imported for.
    e. A prefix for the name field.
    f. Which field in the list of attributes is to be used to obtain the location's name, and which is used for the location's parent if the list of objects is hierarchical.

Note, if there are existing locations with the same name and website, then they are updated rather than new locations created.

When you are ready to import, click the Upload Data button.
