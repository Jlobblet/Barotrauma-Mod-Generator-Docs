Changing the Prices of Items
------------------------------

Here, the price of multiple several items will be changed to demonstrate an example structure for the mod.

The files used are available `separately <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/tree/master/docs/source/_code/tutorial/ItemPriceMod/ItemPriceMod>`_ or `zipped <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/blob/master/docs/source/_code/tutorial/ItemPriceMod/ItemPriceMod.zip>`_.
You can see the output `here <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/tree/master/docs/source/_code/tutorial/ItemPriceMod/ItemPriceMod_generated>`_.

First, we'll need to build the folder for the Mod Generator to use as input.
Make new files and folders until you have the following:

::

    ItemPriceMod
    ├── filelist.xml
    └── Content
        └── Items
            ├── Misc
            |   └── misc.xml
            └── Weapons
                └── weapons.xml

Here, ``filelist.xml`` will be copied over and ``misc.xml`` and ``weapons.xml`` will be diff files instructing the Generator to change certain files.
The same structure as vanilla's Content directory is used, but this is down to preference.
Keeping the same vanilla structure makes it easier to tell what each file modifies.

Now, edit ``filelist.xml`` to contain the relevant information.

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod/filelist.xml
    :language: XML

With ``filelist.xml`` in place, we can now edit the diff files.
Starting with ``misc.xml``, define a basic diff element:

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod_partial/Content/Items/Misc/.misc1.xml
    :language: XML

Now add elements that change the properties of that file.
Reading the vanilla file, we see:

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod_partial/Content/Items/Misc/.vanillamisc.xml
    :language: XML

The rest of the file has been left out for clarity.

To change the price of an item, we need to edit the ``baseprice`` attribute of the ``Price`` element, and the ``multiplier`` on each of the ``locationtypes``.
Since we're changing values that are already present, we use the ``replace`` element.

Let's increase the guitar's baseprice, and make it cheaper at cities.
Update our ``misc.xml`` diff to be:

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod/Content/Items/Misc/misc.xml
    :language: XML

Now we can run the Mod Generator to check the output.

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod_generated/Content/Items/Misc/misc.xml
    :language: XML
    :emphasize-lines: 7,9

This method will work for any number of items in the same file.
One diff per file is required, but one file could also have multiple diffs to make some things clearer (such as editing multiple items in it in complex ways).

Here's our ``weapons.xml`` diff:

.. literalinclude :: /_code/tutorial/ItemPriceMod/ItemPriceMod/Content/Items/Weapons/weapons.xml
    :language: XML

Running the Mod Generator on the input directory (zipped) will produce the same result as the pre-generated version.

This concludes the Item Price tutorial.
