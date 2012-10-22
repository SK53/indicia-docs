About Warehouse Modules
=======================

The Kohana framework provides useful support for extensibility via the concept
of modules, which allow the provision of additional models, views and 
controllers as well as the overriding of existing code from the main 
application. Indicia's warehouse extends this idea by allowing modules to hook
into various bits of core functionality. For example, Indicia allows a module
to provide additional items to add to the main menu or new tabs for an existing
page.

In addition to the **application** and **system** folders, Kohana supports a 
**modules** folder in the root of the installation folder which allows optional 
extra code files to be provided. Each module is held within a single folder 
inside the modules folder and provides a specific extension to core 
functionality. Modules typically declare additional models, views and 
controllers but can also declare other types of files, such as helpers used to 
perform spatial reference notation translations. Within the module folder, the 
path structure is the same as for core files within the application folder, so 
for example a module called *specimens* would declare controller classes in the 
folder *modules/specimens/controllers*, view code in *modules/specimens/views*
and model classes in *modules/specimens/models*.

The module controllers provide public methods and therefore additional URLs 
available within the warehouse, such as the URL paths which support the web 
services or installation procedures. However, although the modules folder can be 
used to create URL paths for separate functionality within the warehouse, there 
is a need to allow these URL paths to be accessed from the existing core 
warehouse screens. For example you might want to add a URL path to the main 
menu, or to add a tab to an existing edit screen. Furthermore if you use a 
module to declare additional database entities, you need to be able to declare 
how those entities relate to the existing entities in the model. Although your 
module's model classes can declare the other models that they relate to, you 
cannot simply edit the core model to declare the inverse relationship since a 
module cannot depend on changes to the core code. Indicia includes a method of 
defining modules which act as plugins, hooking their functionality into the 
existing Warehouse in a seamless way. Currently the plugin architecture supports 
the following integration functionality:

#. modification of the main menu, e.g. to add a new page
#. the insertion of a new tab onto an existing view page
#. declare additional data entities that can be exposed via the data services
#. declare how new data entities are related to other entities.