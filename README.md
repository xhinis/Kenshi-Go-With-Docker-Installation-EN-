# Kenshi-Go-With-Docker-Installation


> [!NOTE]
>  This repo is for Ubuntu only.
> Kenshi recently stated that they will work with GOLang instead of TypeScript and started testing it. It is a repo created for those who want to test it.
<br>
If you are ready to test the Kenshi Go version with Docker, let's get started.
<br>

## Server Update and Docker Installation
```
# First, let's make our updates and upgrades on the server.
sudo apt update -y && sudo apt upgrade -y

# Then, let's enter the codes below in order to avoid problems with the source we will download via HTTPS to our server and to avoid problems when unzipping the zip file we downloaded from the link.
sudo apt install apt-transport-https ca-certificates curl software-properties-common wget unzip

# Let's add the Docker GPG key to our server
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Let's add Docker to our resources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Let's update it again so that the source we added is recognized
sudo apt update

# Let's ensure that we will install Ubuntu via Docker
apt-cache policy docker-ce

```
> [!WARNING]
> The last code we wrote will give us a screen output. Let's make sure that the output here is Installed: (none).
```
docker-ce:
  Installed: (none)
  ...
  ...
  5:20.10.14~3-0~ubuntu-focal 500
  500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
  5:20.10.13~3-0~ubuntu-focal 500
  500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
  ...
  ...

## And then let's install Docker
sudo apt install docker-ce

## Let's run the code below to make sure Docker is installed.
sudo systemctl status docker
```
> [!WARNING]
> The last code we wrote should give us an output like the following.
```
Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     ...
     ...
     ...
```
<br>

## Kenshi Unchained Go Version Installation

```
# Download the new release with wget
wget https://github.com/KenshiTech/unchained/releases/download/v0.11.0-alpha.5/unchained-v0.11.0-alpha.5-docker.zip

# Unzip the downloaded file
unzip unchained-v0.11.0-alpha.5-docker.zip

# Navigate into the extracted directory
cd unchained-v0.11.0-alpha.5-docker/conf

# Edit the copied configuration file using nano
nano secrets.worker.yaml

nano conf.worker.yaml

```

> [!WARNING]
> When we enter Nano, the first part we need to change is the "name" part. If you are running Typescript, please enter the same name and be sure to add the secretKey and publicKey in your typescript at the end of the file.<br><br>
> If you are running Kenshi for the first time, you can generate it with TypeScript and get the secretKey, since the Kenshi Go Docker version does not have the generate feature yet. <br><br>
> After editing the required fields, you can exit the editor by pressing CTRL + X, Y and Enter respectively.

```
# If we have completed the above steps, now let's give execution permission to our file.
chmod +x unchained.sh

# We are now ready to run! Let's run it with the code below.
./unchained.sh worker up -d
```

> [!TIP]
> You can check your logs with the ./unchained.sh worker logs -f code.<br><br>
> If there is no problem, your screenshot should be as follows.<br><br>

![Screenshot_6](https://github.com/Dtractus/Kenshi-Go-Docker-Kurulumu/assets/55835876/9060921b-9e56-401e-bba1-9c0ba4b290fa)
