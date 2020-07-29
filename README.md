# ssh-jumphost

Re-work of warden/docker-jumphost which is an extended Docker image to run an SSH server.

Expected volumes:
* publickeys:/keys 

USAGE:
```
docker run --name ssh_server -d -e USER=`whoami` -v ~/.ssh/pubkeys:/keys geekinutah/ssh-jumphost
```

where:
* USER - username allowed to log in
* ~/.ssh/pubkeys/ - path containing desired public keys

The modificaitons made to warden/docker-jumphost are specifically to accomodate attaching a single user to an alternative network namespace.
For example, let's say you are using ekristen/openvpn-client to isolate a VPN connection. You can then use this ssh server to provide a jumphost into that network namespace.

```
docker run --net container:openvpn -d -e USER=`whoami` -v ~/.ssh/pubkeys/:/keys geekinutah/ssh-jumphost
```
