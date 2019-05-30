# passwordless `ssh`

```bash
ssh-copy-id remote-user@server-ip
```

# passwordless `sudo`

```bash
#!/bin/bash

if ! test -n "$1"
then echo "Usage: $0 <user>" >&2; return
fi

if ! test -n "/etc/sudoers.d/$1"
then touch "/etc/sudoers.d/$1";
fi

printf >"/etc/sudoers.d/$1" '%s    ALL= NOPASSWD: ALL\n' "$1"
```
* run this script then logout and login again to take effect


# building an example and deploy it
General steps:
* cross-build ws in Isaac dir
* run deploy script to rsync to bot
* enter app folder on bot and launch app
* run web display on ws

on ws:

```bash
bob@desktop:~/isaac$  ./engine/build/deploy.sh --remote-user ROBOTUSER -p //apps/samples/stereo_dummy:stereo_dummy-pkg -d jetpack42 -h ROBOTIP
```

to run:

on Jetson:

```bash
cd ~/deploy/boliu/stereo_dummy-pkg # paths are relative in Issac
./apps/samples/stereo_dummy/stereo_dummy
```

on ws: open browser and enter: ROBOTIP:3000/

