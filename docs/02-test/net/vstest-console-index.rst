Summary
#######

VSTest.Console.exe is optimized for performance and is used in place of MSTest.exe since Visual Studio 2012.

Run from system Path
--------------------

VSTest.Console is configured in the Path environment variable on every Windows Agent. You can for example call it from a script task:

.. code-block:: bat

    vstest.console.exe  MyProject.Web.Test.dll MyProject.Service.Test.dll /Logger:trx

.. note:: A complete list of parameters can be found in the `official documentation at MSDN <https://msdn.microsoft.com/en-us/library/jj155796.aspx>`_

Run using Bamboo Command
------------------------

Discussed with details in a different article [Link]