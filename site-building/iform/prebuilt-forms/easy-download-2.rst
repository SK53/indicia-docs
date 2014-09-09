Easy Download 2
===============

The Easy Download 2 prebuilt form provides an alternative download page to the :doc:`easy-download` form.
The most significant difference is that it integrates with saved filters so that users can download
predefined sets of records.

iRecord's download page uses the Easy Download 2 prebuilt form. Here is the configuration required:

* **View access control** and **Permission name for view access control** - as described
  under :doc:`generic-settings`.
* **Download all users for reporting permission** - download all users
* **Download type permission - reporting** - access iform
* **Download type permission - peer review** - *not set* 
* **Download type permission - verification** - verification
* **Download type permission - data flow** - download data flow
* **Download type permission - moderation** - *not set*
* **Download format permission - CSV** - access iform
* **Download format permission - TSV** - access iform
* **Download format permission - KML** - access iform
* **Download format permission - GPX** - access iform
* **Download format permission - NBN** - access iform
* **Custom formats** - click **Edit source** then paste in the following:

  .. code-block:: javascript
    [
    {
      "title":"LEVANA British National Grid",
      "permission":"butterfly app",
      "report":"library/occurrences/filterable_occurrences_download_levana.xml",
      "format":"tsv",
      "params":"smpattrs=\noccattrs=\nsref_system=osgb\ntaxon_group_list=104"
    },
    {
      "title":"LEVANA Irish Grid",
      "permission":"butterfly app",
      "report":"library/occurrences/filterable_occurrences_download_levana.xml",
      "format":"tsv",
      "params":"smpattrs=\noccattrs=\nsref_system=osie\ntaxon_group_list=104"
    },
    {
      "title":"CSV format including unreleased records",
      "permission":"download unreleased",
      "report":"library/occurrences/filterable_occurrences_download.xml",
      "params":"smpattrs=#biotope,#all_survey_attrs\noccattrs=#det_full_name,#sex,#stage,#sex_stage_count,#all_survey_attrs\nrelease_status=A",
      "format":"csv"
    }
    ]

* **CSV download format report** - Library|Occurrences|Occurrences Download using standard filters
* **CSV additional parameters** - paste in the following::

    smpattrs=#biotope,#all_survey_attrs
    occattrs=#det_full_name,#sex,#stage,#sex_stage_count,#all_survey_attrs
  
* **TSV download format report** - Library|Occurrences|Occurrences Download using standard filters
* **TSV additional parameters** - paste in the following::

    smpattrs=#biotope,#all_survey_attrs
    occattrs=#det_full_name,#sex,#stage,#sex_stage_count,#all_survey_attrs
  
* **KML download format report** - Library|Occurrences|Occurrences Download using standard filters for GIS
* **KML additional parameters** - paste in the following::

    smpattrs=
    occattrs=
  
* **GPX download format report** - Library|Occurrences|Occurrences Download using standard filters for GIS
* **GPX additional parameters** - paste in the following::

    smpattrs=
    occattrs=
  
* **NBN download format report** - Library|Occurrences|Occurrences Download using standard filters for GIS
* **NBN additional parameters** - paste in the following::

    smpattrs=#biotope
    occattrs=#det_full_name,#sex,#stage,#sex_stage_count

Note that you need to assign the **download all users** permission to any user role that you
want to allow to download all the records, not just their own. It is assumed that verifiers 
can download the records they have rights to verify and that the permission controlling 
access to the verification page is called *verification*.

