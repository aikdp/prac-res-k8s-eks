# Init Containers
* We can run init containers before main containers run. Init containers can be one or many.
* Init containers should be ready before main container runs.
* Init containers goes to completion state. (Our custom containers always running, means running containers only will push to docker hub)
* If init containers fails, main containers will not run. 
* To set configuration and check external dependency applications status, we can make use of init containers
