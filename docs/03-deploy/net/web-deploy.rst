WebDeploy
#########

Introduction
------------

WebDeploy is a tool that simplifies migration, management and deployment of IIS Web servers, Web applications and Web sites

Installation
------------

Current latest version (3.6)

`https://www.microsoft.com/en-us/download/details.aspx?id=43717 <https://www.microsoft.com/en-us/download/details.aspx?id=43717>`_

- Install Web Management Service role service
- On IIS: Enable remote connections
- Open Firewall port

.. note:: It is recommended to install it through Microsoft Web Platform Installer: Install Web Deploy 3.6 for Hosting Servers

Command line sintax
-------------------

`http://technet.microsoft.com/en-us/library/dd569106%28v=ws.10%29.aspx <http://technet.microsoft.com/en-us/library/dd569106%28v=ws.10%29.aspx>`_

Content Path Providers
----------------------

`http://technet.microsoft.com/en-us/library/dd569040(v=ws.10).aspx <http://technet.microsoft.com/en-us/library/dd569040(v=ws.10).aspx>`_

Configure Content Path Provider
-------------------------------

`http://technet.microsoft.com/en-us/library/dd569034(v=ws.10).aspx <http://technet.microsoft.com/en-us/library/dd569040(v=ws.10).aspx>`_

Database
--------

Generate a change script comparing database project schema against a database schema.

.. code-block:: bat

    msdeploy.exe –verb:sync –source:dbSqlPackage="C:\root\home\projects\my-project\src\MyProject.Database\sql\release\MyProject.dacpac" –dest:dbSqlPackage="Data Source=.;Initial Catalog=MyDataBase;user id=myprojectuser;password=password",Action=Script,OutputPath="C:\users\mario.moreno\Desktop\script.sql",BlockOnPossibleDataLoss=false

More info `http://msdn.microsoft.com/library/hh550081%28v=vs.103%29.aspx <http://msdn.microsoft.com/library/hh550081%28v=vs.103%29.aspx>`_

Examples
--------

RELEASE BUILD
^^^^^^^^^^^^^

.. code-block:: bat

    msbuild [SolutionPath]\[Solution].sln /m /nologo /p:Configuration=Release /t:rebuild

DEPLOY DATABASE
^^^^^^^^^^^^^^^

.. code-block:: bat

    msdeploy.exe -verb:sync -source:dbDacFx=[SolutionPath]\[Database.Project]\sql\release\[Database.Project].dacpac -dest:dbDacFx='Data Source=[DataSource];Database=[DatabaseName];User Id=[UserId];Password=[Password]'

GENERATE PACKAGE
^^^^^^^^^^^^^^^^

.. code-block:: bat

    msbuild [SolutionPath]\[Solution].sln /p:Configuration=Release /p:DeployOnBuild=true /p:DeployTarget=Package /p:CreatePackageOnBuild=True

DEPLOY PACKAGE
^^^^^^^^^^^^^^

.. code-block:: bat

    [SolutionPath]\[WebProjectName]\obj\Release\Package\[WebProjectName].deploy.cmd /Y /M:https://[ServerName]:8172/MSDeploy.axd /U:[Domain\UserName] /P:[Password] /A:basic -allowUntrusted  -setParamFile:[ParameterFilesPath]\[WebProjectName].SetParameters.xml

RUN SPECIFIC SQL SCRIPT
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bat

    msdeploy.exe -verb:sync -source:dbFullSql=[SQLScriptPath]\[FileName].sql -dest:dbFullSql="Data Source=[DataSource];Database=[DatabaseName];User Id=[UserId];Password=[Password]"

USING SQLCMD
^^^^^^^^^^^^

.. code-block:: bat

    sqlcmd -S [ServerName] -U [UserName] -P [Password] -i [SQLScriptPath]\[FileName] -d [DatabaseName]

DEPLOYING DIRECTLY WITHOUT PACKAGE
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bat

    msbuild /p:Configuration=[Configuration:Debug|Release|etc] /p:DeployOnBuild=True /p:DeployTarget=MsDeployPublish /p:CreatePackageOnPublish=True /p:MSDeployPublishMethod=WMSVC /p:MSDeployServiceURL=[ServerName] /p:DeployIISAppPath=[IISAppName] /p:UserName=[Domain\UserName] /p:Password=[Password] /p:AllowUntrustedCertificate=True

SYNCHRONIZE TWO FOLDERS
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bat

    msdeploy.exe -verb:sync -source:iisApp=[source-folder] -dest:iisApp=[destination-folder],computerName=[host-ip],username=[username],password=[password] -allowUntrusted

With MS Deploy Service
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bat

    msbuild /p:Configuration=Release /p:DeployOnBuild=True /p:DeployTarget=MsDeployPublish /p:CreatePackageOnPublish=True /p:MSDeployPublishMethod=WMSVC /p:MSDeployServiceURL=[server-ip] /p:DeployIISAppPath=CodeShare /p:UserName=[user-name] /p:Password=[password] /p:AllowUntrustedCertificate=True

Service Deploy
--------------

.. code-block:: bat

    msdeploy.exe -verb:sync -preSync:runCommand="C:\service.uninstall.cmd",waitInterval=30000 -source:dirPath="C:\source\bin\Release" -dest:dirPath='C:\inetpub\wwwroot\service-folder',computerName=https://host:port/msdeploy.axd?site=ServiceSiteName,username=[user],password=[password],authType=basic -allowUntrusted -postSync:runCommand="C:\install.cmd",waitInterval=30000

In order to use msdeploy to sync two folders and run pre and post sync script you must create a WebApplication on the destination server IIS and configure the folder of the application as the dest:dirPath of msdeploy

If you get a permission required error running service.deploy.cmd. You should run the following command on the destination server.

run cmd as the user account used with msdeploy

.. code-block:: bat

    sc privs wmsvc SeChangeNotifyPrivilege/SeImpersonatePrivilege/SeAssignPrimaryTokenPrivilege/SeIncreaseQuotaPrivilege
    net stop wmsvc 
    net start wmsvc

rem this script will be executed on the destination server after msdeploy sync task is executed

service.install.cmd

.. code-block:: bat

    rem for example rewrite a config file and start the service
    copy C:\[FolderOnServer]\App.exe.config C:\[AnotherFolderOnServer]\App.exe.config /Y /V
    rem net start [ServiceName]

service.uninstall.cmd

.. code-block:: bat

    rem this script will be executed on the destination server before msdeploy sync task is started
    rem for example stop the service
    rem net stop [ServiceName]

SQL
---

Define `*.publish.xml` file
Idempotent post deployment script
Migrations Idempotent Scripts: Update-Database -Script -SourceMigration:$InitialDatabase -TargetMigration:First

Windows Service
	WebDeploy Sync (the folder must be accessible by IIS (as a web application for example) )
	Installer: InstallShield Limited (very limited). Wix package (complex)
	robocopy?

SetParameters
-------------

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <parameters>
        <setParameter name="IIS Web Application Name" value="[MyWebsite]" />
        <setParameter name="ModelContext-Web.config Connection String" value="Data Source=[MyWebSiteDB];Initial Catalog=[DatabaseName];User Id=[User];Password=[Password];MultipleActiveResultSets=True" />
    </parameters>

Links
-----

`MSBuild is now part of Visual Studio <http://blogs.msdn.com/b/visualstudio/archive/2013/07/24/msbuild-is-now-part-of-visual-studio.aspx>`_