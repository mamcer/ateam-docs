OpenCover.MSTest cmd
####################

OpenCover.MSTest is a custom Windows batch file (cmd) configured as a command in Bamboo. It basically look for test assemblies recursively and executes a code coverage analysis with [OpenCover](https://github.com/OpenCover/opencover)

MSTest
------

Internally it uses MSTest to run the tests and assume tests are written with MS MSTest Framework.

File Pattern
------------

When it look for test assemblies it basically look for files that match the following pattern:

.. code-block:: bat

    \**\bin\Debug\*.Tests.dll
    \**\bin\Debug\*.Test.dll

Examples of matching assemblies:

.. code-block:: bat

     MyProject.Application.Tests.dll
     MyProject.Web.Test.dll 

Configuration
-------------

The only parameter needed is a directory. The starting point where the script will recursively start to look for test assemblies. In most cases the default directory is the Bamboo working directory then you can configure it with the `${bamboo.build.working.directory}` Bamboo environment variable.

.. image:: _static/opencover.mstest/01-command-configuration.png  

Output
------

The output of the analysis is an xml file with the coverage results. The file is created at the directory level configured in the previous step. The name of the file is `open-cover.xml` and you can expose it through an artifact for example.

.. image:: _static/opencover.mstest/02-artifact-edition.png    

Source code
-----------

You can find the source code in GitHub.