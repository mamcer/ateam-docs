SonarQube
#########

MSBuild SonarQube Runner
------------------------

.. code-block:: bat

    MSBuild.SonarQube.Runner.exe begin /k:"[sonar-project-key]" /n:"[sonar-project-name]" /v:"[project-version]" 
    MSBuild /t:rebuild /m /p:Configuration=Debug [solution-name].sln 
    MSBuild.SonarQube.Runner.exe end

SonarQube Runner
----------------

.. code-block:: bat

    sonar-runner -D sources=. -D sonar.projectName=[my-project-name] -D sonar.projectKey=[my-project-key] -D sonar.profile=[sonar-profile-name] -D sonar.projectVersion=[project-version] -D sonar.language=[language] -D sonar.login=[sonar-user] -D sonar.password=[sonar-password] -D sonar.host.url=[sonar-url]

SonarLint
---------

SonarLint is an extension to your favorite IDE that provides on-the-fly feedback to developers on new bugs and quality issues injected into their code.

SonarLint for Visual Studio
^^^^^^^^^^^^^^^^^^^^^^^^^^^

SonarLint is a Visual Studio 2015 extension that provides on-the-fly feedback to developers on new bugs and quality issues injected into .NET code.

Download SonarLint: `https://visualstudiogallery.msdn.microsoft.com/47d1049d-bb27-454e-aab8-24566c85e548 <https://visualstudiogallery.msdn.microsoft.com/47d1049d-bb27-454e-aab8-24566c85e548>`_

Will add SonarAnalyzer.CSharp nuget package. 

[screenshots]

.. note:: At least at the moment of this write. SonarLint does not include all the SonarQube server supported rules. New rules are included in every new version

SonarQube Bamboo
----------------

.. code-block:: bat

"-Dsonar.projectKey=test-project" "-Dsonar.projectName='Test Project'" "-Dsonar.projectVersion='${bamboo.repository.revision.number}'" "-Dsonar.sources=." "-Dsonar.sourceEncoding=UTF-8" "-Dsonar.visualstudio.enable=true" "-Dsonar.dotnet.visualstudio.solution.file=habitat.sln" "-Dsonar.cs.opencover.reportsPaths=open-cover.xml" "-Dsonar.dotnet.excludeGeneratedCode=true"

