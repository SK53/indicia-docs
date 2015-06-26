.. _send-irecord:

Sending to iRecord
==================

By way of specific example and to document the iRecord General survey, since some apps may wish to submit to this,
below is a list of the name value pairs that it accepts.

Firstly there are the basic inputs and standard sample and occurrence values.

=============================  ==============================================================================
Name                           Value
=============================  ==============================================================================
website_id                     ``23``
survey_id                      ``42``
appname                        The app name that was configured.
appsecret                      The app secret set for the app name.
email                          Email of the user submitting the record.
usersecret                     Secret of the user submitting the record.
sample:date                    E.g. ``04/12/2014``
sample:entered_sref_system     E.g. ``OSGB`` 
sample:entered_sref            E.g. ``SJ74350474``
sample:comment                 Any plain text.
occurrence:taxa_taxon_list_id  Required. The id of the species name within a species list.
=============================  ==============================================================================

.. tip::

You can grab taxa_taxon_list_id values from iRecord by examining HTML with a browser debugger.
Go to http://www.brc.ac.uk/irecord/enter-casual-record and start typing the name of the species you want to look up in the species input. The name will pop up in a list from which you can select it.
If the name does not appear then it is not in the list for some reason, e.g. incorrect spelling.
Having selected the species, inspect the HTML around the species input. You will find a hidden input like 
``<input id="occurrence:taxa_taxon_list_id" class="hidden" type="hidden" value="123169" name="occurrence:taxa_taxon_list_id">``
The value attribute holds the number you are looking for, 123169 in this case.


The sample attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
smpAttr:127             Recorder Name.
smpAttr:209             | EUNIS Habitat. A numeric value indicates a habitat as follows
                        | ``1640`` **Coast**
                        |   ``1642`` Coastal dunes and sandy shores
                        |   ``1644`` Coastal shingle
                        |   ``1646`` Rock cliffs, ledges and shores, including the splash zone
                        | ``1648`` **Inland water**
                        |   ``1650`` Standing waters
                        |   ``1652`` Running waters
                        |   ``1654`` Frequently inundated edge of inland water bodies including splash zone of waterfalls
                        | ``1656`` **Bogs and fens**
                        |   ``1658`` Raised and blanket bogs
                        |   ``1660`` Peatlands receiving water from surrounding landscape
                        |   ``1662`` Peatlands receiving calcareous or eutrophic ground water
                        |   ``1664`` Sedge and reedbeds, normally without free-standing water
                        |   ``1666`` Inland saline and brackish marshes and reedbeds
                        | ``1668`` **Grassland**
                        |   ``1670`` Dry grasslands including chalk grassland
                        |   ``1672`` Fertile grasslands including hay meadows
                        |   ``1674`` Wet grasslands such as grazing marshes, water meadows and flood meadows
                        |   ``1676`` Woodland edges, clearings and tall herb stands
                        |   ``1678`` Sparsely wooded grasslands
                        | ``1680`` **Heathland, scrub, hedgerow**
                        |   ``1682`` Scrub
                        |   ``1684`` Shrub heathland
                        |   ``1686`` Riverine and fen scrubs
                        |   ``1688`` Hedgerows
                        |   ``1690`` Shrub plantations
                        | ``1692`` **Woodland**
                        |   ``1694`` Broadleaved deciduous woodland
                        |   ``1696`` Broadleaved evergreen woodland
                        |   ``1698`` Coniferous woodland
                        |   ``1700`` Mixed deciduous and coniferous woodland
                        |   ``1702`` Lines of trees and small woodlands
                        | ``1704`` **Unvegetated or sparsely vegetated habitats**
                        |   ``1706`` Caves
                        |   ``1708`` Screes
                        |   ``1710`` Inland cliffs, rock pavements and rocky outcrops
                        |   ``1712`` Snow or ice dominated habitats
                        |   ``1714`` Inland habitats with sparse or no vegetation
                        | ``1716`` **Arable land, gardens or parks**
                        |   ``1718`` Arable and horticultural land
                        |   ``1720`` Gardens and parks
                        | ``1722`` **Industrial and urban**
                        |   ``1724`` Buildings of cities, towns and villages
                        |   ``1726`` Quarries
                        |   ``1728`` Roads and other constructed hard surfaces
                        |   ``1730`` Artifically constructed waterways and associated structures
                        |   ``1732`` Waste deposits
                        | ``1734`` **Mixed habitats**
                        |   ``1736`` Estuaries
                        |   ``1738`` Saline coastal lagoons
                        |   ``1740`` Brackish coastal lagoons
                        |   ``1742`` Snow patches
                        |   ``1744`` Crops shaded by trees
                        |   ``1746`` Intensively-farmed crops interspersed with strips of natural and/or 
                            semi-natural vegetation
                        |   ``1748`` Bottom of the water body
                        |   ``1750`` Mixed rock and sediment in the intertidal and splash zone
                        |   ``1752`` Mixed rock & sediment of shallow subtidal zone with enough light for 
                            communities of seaweeds
                        |   ``1754`` Mixed rock & sediment of subtidal zone at depths with little light and 
                            animal communities dominate
                        |   ``1756`` Coastal caves
                        | ``1758`` **Marine**
                        |   ``1760`` Rock and other hard surfaces in the intertidal and splash zone
                        |   ``1762`` Sediment (shingles, gravels, sands and muds) in the intertidal and s
                            plash zone including saltmarshes
                        |   ``1764`` Rocky or cobbled seabed in the shallow subtidal zone with enough 
                            light for communities of seaweeds
                        |   ``1766`` Rocky or cobbled seabed in the subtidal zone with little light and 
                            animal communities dominate
                        |   ``1768`` Sediments (shingles, gravels, sands and muds)  permanently covered 
                            with seawater
                        |   ``1770`` Seabed in deep water beyond the continental shelf edge
                        |   ``1772`` Water column of shallow or deep water
                        |   ``1774`` Sea ice, icebergs and other ice-associated marine habitats
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

The occurrence attributes for the iRecord General survey are as follows.

======================  =====================================================================================
Name                    Value
======================  =====================================================================================
occAttr:18              Identified By. A text value indicating who identified the specimen as this might be
                        different from both the recorder and the person submitting the record.
occAttr:54              | Certainty. A numeric value indicates the recorders certainty as follows
                        | ``859`` Certain
                        | ``860`` Likely
                        | ``861`` Uncertain
occAttr:93              Quantity. A test value indicating the number of specimens of the species that were
                        observed.
occAttr:105             | Sex. A numeric value indicates the sex of the specimen as follows
                        | ``1946`` Not recorded
                        | ``1947`` Male
                        | ``1948`` Female
                        | ``3482`` Mixed
occAttr:106             | Stage. A numeric value indicates the life stage of the specimen as follows
                        | ``1949`` Not recorded
                        | ``1950`` Adult
                        | ``1951`` Pre-adult
                        | ``1952`` Other
======================  =====================================================================================

