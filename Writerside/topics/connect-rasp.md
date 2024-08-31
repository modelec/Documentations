# Connect To Raspberry

## Connect to the raspberry with ssh without knowing its IP

Usage of tailscale to connect to the raspberry without knowing its IP.

### Installation

[Download the tailscale client](https://tailscale.com/kb/1347/installation)

### Usage

1. Create an account on tailscale
2. Register your device
3. Install the tailscale client on your device
4. Run this following commands

```Bash
sudo tailscale login
```

Now ask an admin to give you the access to the raspberry

```Bash
sudo tailscale status
```

With `tailscale status` you have the IP of the raspberry.

```Bash
ssh modelec@<IP>
```

The password must be the famous one.