# Hostname Header

## Add server hostname headers to your app in one module

This module determines the servers internal host name, and then creates a response header for you.

This module is ideal for clustered setups, or docker swarms, where the code could be running on one of many servers. In Docker, can you search for this hostname in portainer or via the CLI, making debugging much easier

## How does it work?

### Response Header

The module sets a header called `x-server-hostname`.

### When does it run?

The module listens to the onRequestCapture ColdBox interception point.

With Errors, this function might not run... if that interception point is not announced. You might need to add to your Application.cfc directly if errors occur before the ColdBox framework loads.

### How does it determine the hostname?

This module looks for the hostname a few different ways.

- First, it looks for the hostname in /etc/hostname file.
- If that does not work, it uses java to get the hostname.

```
var inet = CreateObject("java", "java.net.InetAddress");
var hostname = inet.getLocalHost().getHostName();
```
* Note - Java errors when trying to return a hostname that does not resolve to an IP, so in docker, this hashed hostname will not resolve, unless you add it dynamically to the /etc/hosts file.


