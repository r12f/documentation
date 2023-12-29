---
sidebar_position: 2
---

# Samba

Samba is a popular SMB/CIFS tool for Linux. With Samba, you can share files with many different operating systems, including Windows and Android.

1. Install samba

```
sudo apt-get update
sudo apt-get install samba
```

2. Editing the Samba Configuration File `/etc/samba/smb.conf`

```
sudo vim /etc/samba/smb.conf
```

3. Add the following configuration to the end of the file

```
[radxa]
comment = Shared from my Radxa device
path = /media/samba
available = yes
valid users = radxa
public = yes
writable = yes
```

4. Creating a shared folder

```
sudo mkdir /media/samba
sudo chmod 755 /media/samba
```

5. Create Samba user and password

```
sudo smbpasswd -a radxa
```

6. Restart the Samba service to load the updated configuration

```
sudo systemctl restart
```

7. Execute `systemctl status smbd` to check the status of samba

```
radxa@radxa-zero3:~$ systemctl status smbd
● smbd.service - Samba SMB Daemon
     Loaded: loaded (/lib/systemd/system/smbd.service; enabled; vendor preset: >
     Active: active (running) since Tue 2023-12-19 03:24:00 UTC; 14s ago
       Docs: man:smbd(8)
             man:samba(7)
             man:smb.conf(5)
    Process: 1963 ExecStartPre=/usr/share/samba/update-apparmor-samba-profile (>
   Main PID: 1964 (smbd)
     Status: "smbd: ready to serve connections..."
      Tasks: 4 (limit: 9191)
     Memory: 6.5M
        CPU: 564ms
     CGroup: /system.slice/smbd.service
             ├─1964 /usr/sbin/smbd --foreground --no-process-group
             ├─1966 /usr/sbin/smbd --foreground --no-process-group
             ├─1967 /usr/sbin/smbd --foreground --no-process-group
             └─1968 /usr/sbin/smbd --foreground --no-process-group
```
