# OpenWeatherMap Exporter for Prometheus
!This documentation is not finish and tested!

This is a Prometheus exporter for [OpenWeatherMap](https://openweathermap.org/).

## Requirements
### API Key
You need an API key from [OpenWeatherMap](https://openweathermap.org/price).

### Python
**Python 3.9.18** is recommended and tested. You need also following modules:
- pyyaml
- requests
There is also a requirements file for Pip that you can use to install the required modules:
```bash
pip3 install -r requirements.txt
```

## Installation
### Installation from source
#### Create User (optional but recommended)
You should not run this program as root user or with your own user. Instead you should create an user for this program:
```bash
sudo useradd \
--home-dir /opt/owm_exporter \
--create-home \
--system \
owm_exporter
```
#### Download and place files
You can download the files with git or with wget:
##### git
```bash
git clone https://github.com/ppixel/owm_exporter.git /opt/owm_exporter/
```

##### wget
```bash
wget -O /opt/owm_exporter/ TODO(url)
```
#### Create configuration file
You need the configuration file "owm_exporter.yml" at the location of the binary "owm_exporter". Without it the program will not work!
```bash
cp /opt/owm_exporter/samples/owm_exporter.yml.sample /opt/owm_exporter/owm_exporter.yml
```
After creation you must set the parameters in this file!

#### Change HTTP server configuration (optional)
If you want to change the configuration for the HTTP server, then you have to create the file "web_config.yml" at the location of the binary "owm_exporter".
```bash
cp /opt/owm_exporter/samples/web_config.yml.sample /opt/owm_exporter/web_config.yml
```
After creation you must set the parameters in this file!

#### Test program
Now you can try to run the program by executing the binary:
```bash
/opt/owm_exporter/owm_exporter
```
If you dont see any error, all is fine and you can go one. Otherwise you should solve the errors. A small collection of solutions you can find under "Trouble shooting" or with Google.

Now test the exporter by open a connection:
```bash
curl -vvv http://localhost:9200/metrics
```
Or open a browser and go to http://ip_address:9200/metrics

You leave the test connection by pressing "CTRL" + "C" and you will get back you prompt.

#### Create Systemd service
Because you dont want to let open a tty the hole time, you should create a service. Here is an example how to create a Systemd service:

Create a service file unter `/etc/systemd/system/owm_exporter.service` with following content:
```
[Unit]
Description=OpenWeaterMap Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=owm_exporter
Group=owm_exporter
Type=simple
ExecStart=/opt/owm_exporter/owm_exporter

[Install]
WantedBy=multi-user.target
```
After creation you have to reload the configuration of Systemd:
```bash
systemctl daemon-reload
```

#### Start service
Now you can start the service and you should also enable it, so after a reboot it will start automaticly:
```bash
systemctl start owm_exporter.service
systemctl enable owm_exporter.service

# Make sure it is running:
systemctl status owm_exporter.service
```

### Installation from package
Is planned.
### Installation with Ansible
Is planned.
### Installation with Docker
Is planned.

## Add Exporter to Prometheus
TODO(add it)

## Code Snippets
In the file "samples/vscode_snippets.md" you can find some code snippets that I used to write this program. I dont know why you need them to run this program. But I like to share them, so perhaps you can use them for your own projects.