Occurrence Associations module
------------------------------

This module enables an extra table in the Indicia database called occurrence_associations, 
which allows 2 records to be linked together where there is an interaction or some other 
association. This allows everything from predator-prey relationships or parasite-host 
relationships through to ecological networks to be recorded. 

Once the module is enabled there are several ways to use the module. Before data can be 
stored for an occurrence association, it is necessary to prepare term lists with terms 
that allow the metadata about the association to be defined. Because the terms available 
for recording association metadata (such as the interaction type or the part of the 
organism interacted with) are highly specific to each discipline, the module allows you 
to define your own lists of terms to pick from for each attribute. The following 
lists of terms should be created:

**Association type** - e.g. ‘preys upon’, ‘parasitises’. Generally these terms should be 
written assuming that the actor in the relationship could be written to the left of the 
term and the acted upon organism to the right - lion preys upon impala, rather than 
impala is preyed upon by lion.

**Association position** - optional, e.g. ‘on’, ‘under’, ‘beside’. Position of interaction 
such as whether a fungus is under, in or on the tree.

**Association parts** -optional, part of the acted upon organism that is interacted with. 
E.g. leaf, trunk, intestine etc.

**Association impact** - impact that the association is causing to the acted upon 
organism. Could be ‘leaf spot’, ‘death’, ‘rot’ etc. 

To capture associations, one method is to use the **dynamic_sample_occurrence** prebuilt 
form to build a form. This form can refer to a special extension control in it’s user 
interface - ``[associations.input_associations_list]``. The form will need 2 species_checklist
controls, one for the "from" and one for the "to" species lists. Use the ``@gridIdAttributeId``
option of the grids to specify a text custom occurrence attribute that can be used to tag which
grid the records are associated with. You might also need to use the @extraParams filter of 
each grid to control the species list or taxon groups that are available for selection in each
grid.

An example configuration of this control might be::

  [species]
  @id=fungi
  @gridIdAttributeId=100
  @extraParams={"query":"\in\":[\"taxon_group_id\",[493,494]]}"}
  [species]
  @id=associations
  @gridIdAttributeId=100
  [associations.input_associations_list]
  @from_grid_id=fungi
  @to_grid_id=hosts
  @association_type_termlist=My association types
  @position_termlist=My association positions
  @part_termlist=My association parts
  @impact_termlist=My association impacts
  
  
