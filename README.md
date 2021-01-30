## Linux development tools installation
A shell script file for installing dev tools. It would be very useful for quick start on development without much worrying about dev tools setup and in other case if you have a crazy habit of changing debian/ubuntu distros like me ;-)

# Install snap store
```sh
echo "Installing snap store.."
sudo apt-get install snapd
echo "Snap store installed successfully"
```

# Install Java
```sh
echo "Installing Java...."
sudo apt-get update
sudo apt-get install openjdk-11-jdk
sudo update-alternatives --config java
java -version
echo "Java installed successfully"
```

# Install visual studio code
> [VS code linux package installation docs](https://code.visualstudio.com/docs/setup/linux)  | [Snap store docs for vscode](https://snapcraft.io/install/code/mint)
```sh
echo "Installing visual studio code"
sudo snap install --classic code
echo "VScode IDE installed successfully"
```

# Install Pycharm community
[snapstore installation docs for Pycharm](https://snapcraft.io/install/pycharm-community/mint)
```sh
echo "Installing pycharm"
sudo snap install pycharm-community --classic
echo "PyCharm IDE installed successfully"
```

# Install intellij-idea-community
[snapstore installation docs for Intellij Idea](https://snapcraft.io/install/intellij-idea-community/mint)
```sh
echo "Installing Intellij idea - community"
sudo snap install intellij-idea-community --classic
echo "Intellij Idea IDE installed successfully"
```
# Installing scala sbt
```sh
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
sudo apt-get update
sudo apt-get install sbt
echo "Scala installed successfully"
```

# pip install
```sh
echo "Installing pip"
sudo apt-get install python-pip
sudo pip install --upgrade pip setuptools
echo "pip installed successfully"
```
# set pip.config
```sh
mkdir ~/.pip
touch ~/.pip/pip.conf
PIPCONFIG="~/.pip/pip.conf"

/bin/cat <<EOM >$PIPCONFIG
[global]
index-url = <index-url>
EOM
```
> replace <index-url> with actual URL

# Install nvm
```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
source ~/.nvm/nvm.sh
source ~/.profile
source ~/.bashrc
```

# Install node version
```sh
nvm install 13.7.0
nvm list
```
> You can any node version using `nvm install` and you can check list of node versions with `nvm list`

# set artifactory .npmrc
```sh
touch ~/.npmrc
npm config set registry <npm-regisry-url>
```
> registry url should be accurate if it's intranet otherwise npm login doesn't work. Prevalidation, it would be better to verify npm login with corp credentials.

# login to npm (No need if you are using public registry i.e. )
```sh
echo "Login to npm using your corp credentials"
npm login
```

# Install docker
```sh
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo apt-key fingerprint 0EBFCD88
#https://github.com/typora/typora-issues/issues/2065
sudo add-apt-repository "deb https://download.docker.com/linux/ubuntu bionic stable"

sudo apt-get update
sudo apt-get -y install docker-ce
sudo usermod -aG docker $USER
```

# Create deamon.json file for docker registry
```sh
sudo touch /etc/docker/daemon.json
sudo tee -a /etc/docker/daemon.json > /dev/null <<EOT
{
    "dns": ["<dns_ip1>", "<dns_ip2>"],
    "insecure-registries": ["registry1", "registry2"]
}
EOT
```
> replace *dns_ip1* *dns_ip2* with intranet IP addresses, the same way for insecure regisries
