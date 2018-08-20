7zip
####

7zip is an open source file archiver with a high compression ratio.

7zip as a Bamboo Command
------------------------

7zip is available in Bamboo as a command. Then you can for example create a zip file with the output of a build making it available to following stages.

.. image:: _static/7zip/01-command-configuration.png

.. code-block:: bat

    a -r -y -xr!.svn -xr!obj build-output.zip

.. note:: In the example we are adding to an archive, recursively, assumming yes to all queries and excluding the .svn and obj directories

Delete previous zip file
------------------------

Unless we are forcing a clean checkout in every build (it takes longer so usually it's avoided) then we can be in the situation were a zip file from a previous build exists. In that case the `-a` (add content) option will update the file with the new content, situation that usually is not what we are looking for. In that case is recommended to add a script task before the 7zip task to delete any previous zip file

An example in a Windows environment:

.. code-block:: bat

    IF NOT EXIST build-output.zip GOTO NoZip
    erase build-output.zip
    :NoZip 

Unzip file
----------

.. image:: _static/7zip/02-unzip-content.png

.. code-block:: bat

    x -y build-output.zip
