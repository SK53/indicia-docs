Standard parameters in reports
==============================

The standard parameters feature built into Indicia's reporting engine provides a flexible
set of reporting parameters that can be applied to any report that runs against the
cache_occurrences_functional table or cache_samples_functional. By having a consistent,
standard set of parameters that can run against a wide variety of reports it facilitates
developing functionality that benefits from the assumption that the  parameters it
understands will be supported. For example, the filter panel used on iRecord allows filters
to be created and saved them used for a wide variety of purposes using  different
underlying reports.

In order to support standard parameter functionality the report must:

  * include ``standard_params="occurrences"`` or ``standard_params="samples"`` in the
    attributes of the ``query`` element in the report definition.
  * include the table ``cache_occurrences_functional`` with an alias of ``o`` for
    occurrence based reports, or ``cache_samples_functional`` with an alias of ``s``
    for sample based reports.
  * include the full set of tags for sharing and filtering as shown in the template
    below::

      SELECT ...
      FROM ...
      #agreements_join#
      #joins#
      WHERE #sharing_filter#
      #idlist#
      .. more filters

The list of parameters made available for occurrence reports which support standard
parameters is described :doc:`in the next section <occurrence-standard-parameters>`.
