Repository hooks
################

SVN
---

In the repository update the `hooks/post-commit` file adding the following line:

.. code-block:: bash

    /opt/bambo/bin/postCommitBuildTrigger.sh [bamboo-url] [ProjectKey]-[PlanKey]

The `postCommitBuildTrigger.sh` content is: 

.. code-block:: bash

	#!/bin/bash

	# the base url of the bamboo server
	baseurl="$1/updateAndBuild.action?buildKey="

	#
	# Use the REST API to trigger a build
	#

	# Moves to the 2nd param (first is URL)
	shift
	# Loop for each build key
	while (( "$#" )); do

	   #
	   # Invoke the trigger
	   #
	   remoteCall=$baseurl$1
	   echo "Detected last directory that was committed ... triggering $remoteCall"
	   /usr/bin/wget --quiet --timeout=10 -t1 $remoteCall -O /dev/null
	   shift
	done

	exit 0

Git
---

The same process as SVN but instead of `hooks/post-commit` we have to update `hooks/post-receive`
