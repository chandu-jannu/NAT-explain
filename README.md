# NAT (Network Address Translation)
 
## The problem NAT solves

Every device on the internet needs an IP address, but there aren't enough
public IPv4 addresses for every phone, laptop, and smart bulb on Earth to
have its own. NAT is the workaround: it lets many devices on a private
network share a single public IP address when they talk to the internet.

Your home Wi-Fi router does this constantly. Every device in your house
gets a **private IP** (like `192.168.1.10`), but to the outside world,
all of your traffic appears to come from **one public IP** your router's.

## Private vs. public IP ranges

Private IPs are reserved and never routed on the public internet:
 
| Range | Typical use |
|---|---|
| `10.0.0.0 – 10.255.255.255` | Large networks |
| `172.16.0.0 – 172.31.255.255` | Medium networks |
| `192.168.0.0 – 192.168.255.255` | Home networks |
