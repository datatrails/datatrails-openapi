.. _intro_locations:

Locations
---------

Assets in Jitsuin Archivist are arranged into *locations*, which allows 
logical assets (eg digital twins) to be grouped together in a physical 
context (eg a single plant location). 

This enables users of the system to quickly identify the answers to 
questions such as *"how many PLCs in the Greyslake plant need to be 
updated?"*, or *"who was the last person to touch any device in the 
Cape Town facility?"*.  It is not *required* for assets to be 
associated with a location, but it is a useful way to group assets in 
the same physical location without inventing your own link values in 
``extended_attributes``.

Resolution
==========
Locations have full 6-digit decimal latitude and longitude components 
allowing high-precision placement on any map renderer or GIS software 
you wish to link them to.  While the primary intention of locations is 
to provide a way of grouping a number of assets together into a single 
plant or facility, it is possible to create and manage a location for 
each individual asset if that is more suitable.

Data members
============
As with all Jitsuin Archivist data types, locations support extended 
attributes which can be defined and used for any purpose by the user. 
This enables storage of a mailing address, phone number, or contact 
details of the site manager, for example.  

Natively, the data structure contains and requires only the basic 
identification and latitude/longitude information to plot and display 
in a GIS framework such as Google Maps.  

For further details, see :ref:`locations_creation`. 
