.. _send-record:

Sending a record
----------------

When posting a record, the number of variables to be sent and the names of them depends upon how the survey has 
been configured in the warehouse. It also depends upon whether a sample is being sent with a single occurrence 
or with multiple occurrences. 

There is an option to send records without requiring user registration. This is highly discouraged as, though 
it lowers the initial barrier to recording, it results in an inferior user experience overall as a person's 
records can never be reliably accessed by them again.

The submission service endpoint is at ``mobile/submit``. 

The app must post the following basic inputs:

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
website_id              Required. The Indicia website_id of the Drupal site (23 for iRecord)
survey_id               Required. An Indicia survey_id belonging to the website_id in to which records will
                        be placed. The attributes that we post have to match those required by the survey.
                        (42 for iRecord General survey)
appname                 Required (unless anonymous). Must match the app name that was configured.
appsecret               Required. Must match the app secret set for the app name in the module configuration.
email                   Required for registered users. If not provided or not recognised then the record is 
                        submitted anonymously.
usersecret              Required for registered users and must match the value expected for the user. This is
                        returned by the registration/log in service.
======================  =====================================================================================

The sample inputs, some of which are required, are as follows:

==========================  =================================================================================
Name                        Value
==========================  =================================================================================
sample:date                 Required.
sample:entered_sref_system  
                            | Required. The system being used to submit the spatial reference. e.g.
                            | ``OSGB`` for British National Grid
                            | ``OSIE`` for Irish Grid
                            | ``4326`` for Latitude and Longitude in decimal form (WGS84 datum)
                            
sample:entered_sref         |Required. The spatial reference in the format defined by the above system e.g.
                            |``SJ70`` for a 10km OSGB grid square
                            |``SJ7404`` for a 1km OSGB grid square
                            |``SJ743047`` for a 100m OSGB grid square
                            |``SJ74350474`` for a 10m OSGB grid square
                            |``M98286465`` for a 10m OSIE grid square
                            |``51.43279N 2.57369E`` for a point using Lat/Long
                            
sample:comment              Any plain text.
==========================  =================================================================================

The occurrence inputs for a single occurrence, some of which are required, are as follows:

=============================  ==============================================================================
Name                           Value
=============================  ==============================================================================
occurrence:taxa_taxon_list_id  Required. The id of the species name within a species list.
=============================  ==============================================================================

The survey-specific custom sample attributes, which have to conform with validation rules set on the 
warehouse, have the format ``smpAttr:*N* = *value*``

The sample attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
smpAttr:127             Recorder Name.
smpAttr:209             |EUNIS Habitat. A numeric value indicates a habitat term as follows
                        |``1640`` Coast
                        |  ``1642`` Coastal dunes and sandy shores
                        |``1644`` Coastal shingle
                        |  ``1646`` Rock cliffs, ledges and shores, including the splash zone
                        |``1648`` Inland water
                        |  ``1650`` Standing waters
                        |  ``1652`` Running waters
                        |  ``1654`` Frequently inundated edge of inland water bodies including splash zone of waterfalls
                        |``1656`` Bogs and fens
                        |  ``1658`` Raised and blanket bogs
                        |  ``1660`` Peatlands receiving water from surrounding landscape
                        |  ``1662`` Peatlands receiving calcareous or eutrophic ground water
                        |  ``1664`` Sedge and reedbeds, normally without free-standing water
                        |  ``1666`` Inland saline and brackish marshes and reedbeds
                        |``1668`` Grassland
                        |  ``1670`` Dry grasslands including chalk grassland
                        |  ``1672`` Fertile grasslands including hay meadows
                        |  ``1674`` Wet grasslands such as grazing marshes, water meadows and flood meadows
                        |  ``1676`` Woodland edges, clearings and tall herb stands
                        |  ``1678`` Sparsely wooded grasslands
                        |``1680`` Heathland, scrub, hedgerow
                        |  ``1682`` Scrub
                        |  ``1684`` Shrub heathland
                        |  ``1686`` Riverine and fen scrubs
                        |  ``1688`` Hedgerows
                        |  ``1690`` Shrub plantations
                        |``1692`` Woodland
                        |  ``1694`` Broadleaved deciduous woodland
                        |  ``1696`` Broadleaved evergreen woodland
                        |  ``1698`` Coniferous woodland
                        |  ``1700`` Mixed deciduous and coniferous woodland
                        |  ``1702`` Lines of trees and small woodlands
                        |``1704`` Unvegetated or sparsely vegetated habitats
                        |  ``1706`` Caves
                        |  ``1708`` Screes
                        |  ``1710`` Inland cliffs, rock pavements and rocky outcrops
                        |  ``1712`` Snow or ice dominated habitats
                        |  ``1714`` Inland habitats with sparse or no vegetation
                        |``1716`` Arable land, gardens or parks
                        |  ``1718`` Arable and horticultural land
                        |  ``1720`` Gardens and parks
                        |``1722`` Industrial and urban
                        |  ``1724`` Buildings of cities, towns and villages
                        |  ``1726`` Quarries
                        |  ``1728`` Roads and other constructed hard surfaces
                        |  ``1730`` Artifically constructed waterways and associated structures
                        |  ``1732`` Waste deposits
                        |``1734`` Mixed habitats
                        |  ``1736`` Estuaries
                        |  ``1738`` Saline coastal lagoons
                        |  ``1740`` Brackish coastal lagoons
                        |  ``1742`` Snow patches
                        |  ``1744`` Crops shaded by trees
                        |  ``1746`` Intensively-farmed crops interspersed with strips of natural and/or 
                        semi-natural vegetation
                        |  ``1748`` Bottom of the water body
                        |  ``1750`` Mixed rock and sediment in the intertidal and splash zone
                        |  ``1752`` Mixed rock & sediment of shallow subtidal zone with enough light for 
                        communities of seaweeds
                        |  ``1754`` Mixed rock & sediment of subtidal zone at depths with little light and 
                        animal communities dominate
                        |  ``1756`` Coastal caves
                        |``1758`` Marine
                        |  ``1760`` Rock and other hard surfaces in the intertidal and splash zone
                        |  ``1762`` Sediment (shingles, gravels, sands and muds) in the intertidal and s
                        plash zone including saltmarshes
                        |  ``1764`` Rocky or cobbled seabed in the shallow subtidal zone with enough 
                        light for communities of seaweeds
                        |  ``1766`` Rocky or cobbled seabed in the subtidal zone with little light and 
                        animal communities dominate
                        |  ``1768`` Sediments (shingles, gravels, sands and muds)  permanently covered 
                        with seawater
                        |  ``1770`` Seabed in deep water beyond the continental shelf edge
                        |  ``1772`` Water column of shallow or deep water
                        |  ``1774`` Sea ice, icebergs and other ice-associated marine habitats
======================  =====================================================================================

There are five other sample attributes which exist for historic reasons and are now largely redundant because
the Indicia User Id is saved with each record. For completeness, these are

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
smpAttr:8               Email. Submit a value of ``[email]`` and the email address of the logged in user will 
                        be substituted.
smpAttr:21              CMS User ID. Submit a value of ``[userid]`` and the Drupal user id of the logged in
                        user will be substituted.
smpAttr:22              CMS Username. Submit a value of ``[username]`` and the Drupal username of the logged 
                        in user will be substituted.
smpAttr:36              First Name.  Submit a value of ``[firstname]`` and the first name of the logged 
                        in user will be substituted.
smpAttr:58              Last Name. Submit a value of ``[surname]`` and the last name of the logged 
                        in user will be substituted.
======================  =====================================================================================

The survey-specific custom occurrence attributes, which have to conform with validation rules set on the warehouse, 
have the format ``occAttr:*N* = *value*`` when submitting a single occurrence.

The occurrence attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
======================  =====================================================================================


The following responses may be returned:

======  ======================  ======================================  ========================================
Status  Message                 Logged message (if enabled)             Cause
======  ======================  ======================================  ========================================
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Bad request             User secret incorrect                   User secret missing or incorrect.
407     User not activated      User not activated                      The user is disabled in Drupal, probably
                                                                        because they have not followed the 
                                                                        activation link they were emailed after
                                                                        registration.
======  ======================  ======================================  ========================================
                                                                        

*Authenticated record* submission adds a requirement: the record should go along with either
iRecord active *session cookie*, which would authenticate the user, or attaching to the record
user's ``usersecret`` along with its ``email``.

You should keep in mind that the recording survey, website and extra recording
fields might need to be set up in the iRecord's warehouse,
read more about that in :ref:`setting up a survey <survey-register>`.

Please check the :ref:`recording examples <send-record-example>`.

.. note:: To module will only check your app authorisation and warehouse information
  after which your request is proceeded to the Indicia's warehouse where the recording
  data is checked.

