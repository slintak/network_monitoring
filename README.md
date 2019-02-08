RPi Network Monitoring
======================

This is simple network monitoring I use in my home network.

My network is quite simple -- one router Mikrotik RB2011 with IP address
`10.0.0.1` and one WiFi AP Mikrotik RBmAPL with IP address `10.0.0.2`.

Note: if you have diferent network settings, you should change SNMP inputs in
`./etc/telegraf.conf` file.

Mikrotik setup
--------------

Enable SNMP on all Mikrotik device you want to monitor:

```
/snmp community set [ find default=yes ] name=telegraf
/snmp set enabled=yes
```

Raspberry setup
---------------

Install Docker on Raspberry Pi:

```
$ curl -sSL https://get.docker.com | sh
# Note: Previous command can be a little dangerous. If you dont like to
# Note: pipe "unknown" script directly to shell, you can run it manually:
# $ curl -sSL https://get.docker.com > docker.sh
# $ sh docker.sh

# Add `pi` user to `docker` group, so you don't have to use `sudo docker`.
$ sudo usermod -aG docker pi

# Install `docker-compose`
$ sudo apt-get install docker-compose
```

After this you should be able to start InfluxDB, Telegraf and Grafana containers:

```
$ git clone https://github.com/slintak/network_monitoring.git
$ cd network_monitoring
$ docker-compose up -d
```

Grafana setup
-------------

![Grafana Dashboard](imgs/grafana_dashboard.png?raw=true "Grafana Dashboard")
