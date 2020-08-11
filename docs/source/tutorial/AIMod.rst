Changing AI Priorities
-----------------------

In this tutorial, the AI priorities of mudraptors will be changed.

The files used are available `separately <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/tree/master/docs/source/_code/tutorial/AIMod/AIMod>`_ or `zipped <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/tree/master/docs/source/_code/tutorial/AIMod/AIMod.zip>`_.
You can see the output `here <https://github.com/Jlobblet/Barotrauma-Mod-Generator-Docs/tree/master/docs/source/_code/tutorial/AIMod/AIMod_generated>`_.

First, we'll need to build the folder for the Mod Generator to use as input.
Make new files and folders until you have the following:

::

    AIMod
    ├── filelist.xml
    └── Content
        └── Characters
            └── Mudraptor
                └── Mudraptor.xml

Since we're only changing the AI priorities here, we don't need to include the ragdoll or any of the assets.

Now populate ``filelist.xml`` with the mod files:

.. literalinclude :: /_code/tutorial/AIMod/AIMod/filelist.xml
    :language: XML

We can begin writing our diff (``Mudraptor.xml``) now.
Let's start by taking a look at the vanilla mudraptor's XML.

.. literalinclude :: /_code/tutorial/AIMod/AIMod_partial/.Mudraptor.xml
    :language: XML

Some of the file has been omitted to make reading the relevant parts easier.

We can edit the priority of an existing ``target`` with a simple patch operation:

.. code-block :: XML

    <replace sel="/Character/ai/target[@tag='door']/@priority">90</replace>

Working out what each part of this xpath is straightforward: ``/Character/ai`` select the mudraptor's ``ai`` element, then ``target[@tag='door']`` finds the ``target`` element with ``tag`` attribute ``door``, and finally ``@priority`` selects the ``priority`` attribute of that element.

It's also possible to use a more concise xpath:

.. code-block :: XML

    <replace sel="//target[@tag='door']/@priority">90</replace>

Here, the ``//`` selects *any* element in the entire tree that meets the conditions - in this case, its ``tag`` attribute must be ``door``.

Whichever of these you use is down to preference - in a small file like ``Mudraptor.xml``, it's easy to check that there's no other elements that are accidentally edited, however in larger files (such as files with items) using ``//`` can cause unwanted edits.
If you're unsure, just check the output of the Mod Generator to confirm.

This same method can also be used to change what action the mudraptor should take:

.. code-block :: XML

    <replace sel="//target[@tag='stronger']/@state">Attack</replace>


Removing a target from the list is also easy:

.. code-block :: XML

    <remove sel="//target[@tag='turret']"/>

Note here how the element has no value.
That's because ``remove`` operations just need to know the selection of the element(s) to remove.

Finally, adding a target is also fairly trivial:

.. code-block :: XML

    <add sel="//ai">
        <target tag="leucocyte" state="Avoid" priority="50" reactdistance="2000"/>
    </add>

Combining all these changes into one diff, we get:

.. literalinclude :: /_code/tutorial/AIMod/AIMod/Characters/Mudraptor/Mudraptor.xml
    :language: XML

Since we're editing a character file, we have to override the root element.
Furthermore, ``cleanup`` is false since we don't want to delete the rest of the mudraptor's character file.

Here's the output in full:

.. literalinclude :: /_code/tutorial/AIMod/AIMod_generated/Characters/Mudraptor/Mudraptor.xml
    :language: XML
    :emphasize-lines: 45,51,54

As you can see, the ``turret`` target is also gone.

This concludes the AI Priorities tutorial.
