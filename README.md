# Set up tunneling server

You can either self-host tunneling server on any machine accessible from lab client/server or use Oracle Cloud Free Tier to host tunneling server for free.

## Self-hosted tunneling server

Run:
```
docker run -it --init --rm --network host -p 7835:7835 -p 8991:8991 ekzhang/bore server
```

## Hosting tunneling server using Oracle Cloud Free Tier

* Signup [here](https://signup.cloud.oracle.com/)
* Create VM instance
* ssh into created VM instance
* [Install Docker](https://www.atlantic.net/dedicated-server-hosting/how-to-install-docker-and-docker-compose-on-oracle-linux/)
* Open ports and allow traffic on 7835 and 8991
* Run ```docker run --name bore -d --init --network host -p 7835:7835 -p 8991:8991 ekzhang/bore server```

# Set up lab server

* [Install Arduino Create Agent](https://support.arduino.cc/hc/en-us/articles/360014869820-Install-the-Arduino-Create-Agent)
* [Install bore](https://github.com/ekzhang/bore)
* Run ```bore local 8991 --to <tunneling server address> --port 8991```
* Connect Arduino board

# Set up lab client

Run:
```
netsh interface portproxy add v4tov4 listenport=8991 connectport=8991 connectaddress=<tunneling server address>
```

... or:

* [Install bore](https://github.com/ekzhang/bore)
* Run ```bore server```
* Run ```bore local 8991 --local-host <tunneling server address> --to 127.0.0.1 --port 8991```
* [Log in the Arduino Web Editor](http://create.arduino.cc/editor)
