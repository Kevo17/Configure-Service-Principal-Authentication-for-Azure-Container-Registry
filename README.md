<h1>Configure Service Principal Authentication for Azure Container Registry</h1>


<h2>Description</h2>
Azure Container Registry provides the functionality to store and share private container images. Within this hands-on lab, we’ll review the permissions for a service principal to access Azure Container Registry. This is helpful in scenarios where you have apps/scripts that need some form of automated access to push/pull images to/from your registry. We'll push and pull some images from the registry and run a container image.
<br />

<h2>Environments Used </h2>

- <b>Azure</b>
- <b>Windows 11</b>
- <b>Power Shell</b>
  
<h2>Program walk-through:</h2>

<h3>Confirm Service Principal Access to Push/Pull Container Images</h3>


- From the Azure portal, select Access control (IAM) in the left menu.
- Click the Role assignments tab to check for our Service Principal


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Push/Pull and Run Container Images Using the Service Principal</h3>

1. Navigate back to the resource group.
2. Click the provisioned container registry to open it.
3. Beneath Essentials, copy the login server for later use.



<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Connect to the virtual machine using the credentials provided for Lab-VM on the lab page.
2. Once connected, click the Windows Start menu and select Windows PowerShell.
3. In PowerShell, log in to the container registry using the service principal application client ID and secret provided on the lab page and the registry login server name previously copied:
```
docker login -u <SP_USERNAME> -p <SP_PASSWORD> <REGISTRY_LOGIN_SERVER>
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Pull an image of a sample ASP.NET application from Microsoft's public repository:
```
docker pull mcr.microsoft.com/dotnet/samples:aspnetapp
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Tag the image with your container registry's name, replacing <REGISTRY_LOGIN_SERVER> with your login server name:
```
docker tag mcr.microsoft.com/dotnet/samples:aspnetapp <REGISTRY_LOGIN_SERVER>/aspnetapp
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Push the image to your container registry:
```
docker push <REGISTRY_LOGIN_SERVER>/aspnetapp
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Verify that the aspnetapp image is pushed into the repository by navigating to the Container Registry, then to Repositories

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- List the locally stored images:
```
docker image ls
```


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Remove the local Microsoft image, replacing <IMAGE_ID> with the image ID of your local image:
```
docker image rm <IMAGE_ID> -f
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Pull the Microsoft image from your container registry:
```
docker pull <REGISTRY_LOGIN_SERVER>/aspnetapp
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Run the image:
```
docker run -p 8080:80 -d <REGISTRY_LOGIN_SERVER>/aspnetapp:latest
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- To verify the container is running, launch Internet Explorer and navigate to http://localhost:8080.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />
