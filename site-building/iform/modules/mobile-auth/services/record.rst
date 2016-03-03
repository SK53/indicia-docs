.. _send-record:

Sending a record
================

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
                            
sample:entered_sref         | Required. The spatial reference in the format defined by the above system e.g.
                            | ``SJ70`` for a 10km OSGB grid square
                            | ``SJ7404`` for a 1km OSGB grid square
                            | ``SJ743047`` for a 100m OSGB grid square
                            | ``SJ74350474`` for a 10m OSGB grid square
                            | ``M98286465`` for a 10m OSIE grid square
                            | ``51.43279N 2.57369E`` for a point using Lat/Long
sample:comment              Any plain text.
==========================  =================================================================================

The occurrence inputs for a single occurrence, some of which are required, are as follows:

=============================  ==============================================================================
Name                           Value
=============================  ==============================================================================
occurrence:taxa_taxon_list_id  Required. The id of the species name within a species list.
=============================  ==============================================================================

The survey-specific custom sample attributes, which have to conform with validation rules set on the 
warehouse, have the format smpAttr:*N* = *value*



The survey-specific custom occurrence attributes, which have to conform with validation rules set on the warehouse, 
have the format occAttr:*N* = *value* when submitting a single occurrence.



The following responses may be returned:

======  ======================  ======================================  ========================================
Status  Message                 Logged message (if enabled)             Cause
======  ======================  ======================================  ========================================
200                             [success] => *sample_id*                Record submitted successfully.
400     Bad request             Missing or incorrect shared app secret  Incorrect appname-appsecret combination.
400     Bad request             User secret incorrect                   User secret missing or incorrect.
400     Bad request             Missing or incorrect website_id         Website_id does not match that entered
                                                                        in the iFrom configuration.
400     Bad request             Missing or incorrect survey_id          Survey_id evaluates to 0 so is definitely
                                                                        incorrect. No check is made to ensure the
                                                                        survey_id is valid for the website.
407     User not activated      User not activated                      The user is disabled in Drupal, probably
                                                                        because they have not followed the 
                                                                        activation link they were emailed after
                                                                        registration.
502     *Html description of    *Description of error on warehouse*     The submission failed validation by
        error on warehouse*                                             the warehouse. E.g. required values
                                                                        missing.
======  ======================  ======================================  ========================================
                                                                        

*Authenticated record* submission adds a requirement: the record should go along with either
iRecord active *session cookie*, which would authenticate the user, or attaching to the record
user's ``usersecret`` along with its ``email``.

You should keep in mind that the recording survey, website and extra recording
fields might need to be set up in the iRecord's warehouse,
read more about that in :ref:`setting up a survey <survey-register>`.

Please check the :ref:`recording examples <send-record-example>`.

.. note:: The module will only check your app authorisation and warehouse information
  after which your request is proceeded to the Indicia's warehouse where the recording
  data is checked.

You can also send multiple occurrences in one submission by replicating the inputs from a species checklist. The pattern for adding species is sc:*grid_id-row_id*::present = *taxa_taxon_list_id*

*grid_id* is simple a unique value to distinguish multiple grids on one page.
*row_id* is a sequential number starting from 0 identifying an occurrence.
*taxa_taxon_list_id* identifies the species.

This example submits 3 occurrences::

    sc:species-0::present = 521853
    sc:species-1::present = 521867
    sc:species-2::present = 521879

Occurrence attributes can also be set for each occurrence using inputs with the pattern sc:*grid_id-row_id*::occAttr:*occurrence_attribute_id* = *value*

For example, to set an attribute with id, 230, on the three occurrences above submit the following::

    sc:species-0::occAttr:230 = adult
    sc:species-1::occAttr:230 = pupa
    sc:species-2::occAttr:230 = larva
