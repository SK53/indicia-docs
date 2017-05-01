Images and maps
---------------

Including photos in report grids
================================

As well as output of textual information into the grid columns, report output  can include
photos which the report grid control will automatically display as  thumbnails with links
to the full size image. Simply include a column containing  the image file name (relative
to the upload path on the warehouse) - you can  include multiple images in the column by
comma separating the file names.  Handily the **cache_occurrences_nonfunctional** table
includes a column called **media**  which uses exactly that format. Also, you must declare
the column with an  attribute called ``img`` set to true for the column to behave as an
image. Try adding the following to the `<columns>` section of your report:

.. code-block:: xml

  <column name="images" display="Images" sql="onf.media" img="true" />

You also need to add a join to cache_occurrences_nonfunctional in the `<query>` element.
Your report should now look like the following:

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
  <report title="Tutorial"
          description="Display some records for the report writing tutorial">
    <query website_filter_field="o.website_id" standard_params="occurrences">
      select #columns#
      from cache_occurrences_functional o
      join cache_occurrences_nonfunctional onf on onf.id=o.id
      join cache_samples_nonfunctional snf on snf.id=o.sample_Id
      join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
      #agreements_join#
      #joins#
      where #sharing_filter#
      #idlist#
    </query>
    <params>
      <param name="smpattrs" display="Sample attribute list" default=""
             description="Comma separated list of sample attribute IDs to include"
             datatype="smpattrs" />
      <param name="occattrs" display="Occurrence attribute list" default=""
             description="Comma separated list of occurrence attribute IDs to include"
             datatype="occattrs" />
    </params>
    <columns>
      <column name="id" sql="o.id" visible="false" datatype="integer"/>
      <column name="public_entered_sref" sql="snf.public_entered_sref"
              display="Grid Ref" datatype="text"/>
      <column name="preferred_taxon" sql="cttl.preferred_taxon"
              display="Species" datatype="text"/>
      <column name="default_common_name" sql="cttl.default_common_name"
              display="Common Name" datatype="text"/>
      <column name="date_start" sql="o.date_start" visible="false"/>
      <column name="date_end" sql="o.date_end" visible="false"/>
      <column name="date_type" sql="o.date_type" visible="false"/>
      <column name="date" display="Date" datatype="date"/>
      <column name="images" display="Images" sql="onf.media" img="true" />
    </columns>
  </report>

.. tip::

  When you add a new column to a report definition, it may not appear immediately in the
  reporting pages you've created in Drupal, because the code caches metadata about the
  report which only changes infrequently rather than request it fresh everytime you load
  the page. To ensure your page loads the new column clear the Indicia cache by visiting
  **Configuration** > **Iform Admin Tasks** on the admin menu then click the **Clear
  Indicia cache** button.

Outputting your records onto a map
==================================

If you use the Report Map prebuilt form (also in the Reporting category) you can output a
map of the records in your report. So, set up a new prebuilt form for a Report Map, give it
a title and add it to the primary links menu as before. Configure it to use the report you
have been creating by setting the **Report Name** option under **Report Settings**. Now, go
to the **Base Map Layers** section and select the Google Satellite layer. There are other
options, in particular those under **Report Map Settings** but the defaults are fine for
now. Save the page and view the results. You should see the map, but with a message output
at the top::

  The report's configuration does not output any mappable data

Ok, so we need to extend our report to include a column which includes mappable
information. PostGIS (the spatial database extension for PostgreSQL which we use
to store the locality of the records) stores grid references or other boundary
and point data internally using a binary format which Indicia cannot use
directly, so we need to pass the geometry binary data for each record through
PostGIS's ``st_astext`` function. Don't worry if this does not make sense you
can just copy this technique to make other reports mappable! So, add the
following column definition to the report, noting the use of the **mappable**
attribute to tell Indicia that it contains mapping data.

.. code-block:: xml

  <column name="geom" visible="false" mappable="true" sql="st_astext(o.public_geom)" />

Save that and try reloading the Drupal Report Map page you created. You should
see the dots now appear on the map. For reference, here is the entire report XML
document you should have created:

.. code-block:: xml

  <?xml version="1.0" encoding="UTF-8"?>
    <report title="Tutorial"
          description="Display some records for the report writing tutorial">
    <query website_filter_field="o.website_id" standard_params="occurrences">
      select #columns#
      from cache_occurrences_functional o
      join cache_occurrences_nonfunctional onf on onf.id=o.id
      join cache_samples_nonfunctional snf on snf.id=o.sample_Id
      join cache_taxa_taxon_lists cttl on cttl.id=o.taxa_taxon_list_id
      #agreements_join#
      #joins#
      where #sharing_filter#
      #idlist#
    </query>
    <params>
      <param name="smpattrs" display="Sample attribute list" default=""
             description="Comma separated list of sample attribute IDs to include"
             datatype="smpattrs" />
      <param name="occattrs" display="Occurrence attribute list" default=""
             description="Comma separated list of occurrence attribute IDs to include"
             datatype="occattrs" />
    </params>
    <columns>
      <column name="id" sql="o.id" visible="false" datatype="integer"/>
      <column name="public_entered_sref" sql="snf.public_entered_sref"
              display="Grid Ref" datatype="text"/>
      <column name="preferred_taxon" sql="cttl.preferred_taxon"
              display="Species" datatype="text"/>
      <column name="default_common_name" sql="cttl.default_common_name"
              display="Common Name" datatype="text"/>
      <column name="date_start" sql="o.date_start" visible="false"/>
      <column name="date_end" sql="o.date_end" visible="false"/>
      <column name="date_type" sql="o.date_type" visible="false"/>
      <column name="date" display="Date" datatype="date"/>
      <column name="images" display="Images" sql="onf.media" img="true" />
      <column name="geom" visible="false" mappable="true" sql="st_astext(o.public_geom)" />
    </columns>
  </report>

.. tip::

  If you are coding using PHP directly instead of prebuilt forms in Drupal, you
  can achieve the same mapping output from your report data using the
  report_helper::report_map control.

Rather than have a separate report grid page and map page you can combine the two on the
same page. Edit the page you created earlier which has the filter bar and report grid on it
then change the following settings:

  * **Base Map Layers** - tick **OpenStreetMap** under **Preset Base Layers**.
  * **User Interface** - under **Form Structure**, add the following to the existing
    content inbetween the [standard params] and [reportgrid] controls::

      [map]
      @dataSource=<path to my report, excluding .xml suffix>

  * You can also add the option `@rowId=id` to the [reportgrid] control if you want to
    enable clicking on a grid row to highlight the correct point on the map.

The options you've covered for building this report file are not exhaustive but
hopefully you now have a good taste for what can be achieved.
