___
## Installing Docker Engine:
___
	Uninstall conflicting packages:
		for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
	Install using apt repository:
		sudo apt-get update
		sudo apt-get install ca-certificates curl
		sudo install -m 0755 -d /etc/apt/keyrings
		sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
		sudo chmod a+r /etc/apt/keyrings/docker.asc
___
		echo \ 
		"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
		$(. /etc/os-release && echo "$UBUNTU_CODENAME") stable" | \
		sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

>[!NOTE]
>I used UBUNTU_CODENAME because I used a ubuntu distribution, you may have to use VERSION_CODENAME if not

___
	Install Docker packages:
		sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
	and verify installation:
		sudo docker run hello-world
		*if there was an output, then installation has been successfully verified*

## Setting up WordPress
___
>[!NOTE]
>I used the instructions provided by the GitHub page found at this [link](https://github.com/docker/awesome-compose/blob/master/official-documentation-samples/wordpress/README.md)

___
	Create an empty directory:
		mkdir *directory_name*
	Enter the new directory:
		cd *directory_name*
	Create a new docker-compose.yml file:
		nano docker-compose.yml
	*Copy the file contents for the .yml file found at the link, make sure to change the appropriate MYSQL and WORDPRESS_DB fields*
___
	Build the Project:
		docker compose up -d
	Access the container at http://<ip#>:<port#> if you made these containers while in a vm, such as VirtualBox like I was. Otherwise, just use localhost. From there, simply follow the instructions as given to you on the website and fill out the applicable fields.
___
	Shutting down containers:
		docker compose down --volume
		*This also removes the database*
	To preserve the database:
		docker compose down

>[!NOTE]
>I did not use sudo for most of the commands for building the containers or for much of setting up WordPress, use sudo otherwise there will be a lot of errors and the setup will not complete

