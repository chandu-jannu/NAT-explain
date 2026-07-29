# NAT (Network Address Translation)
 
## The problem NAT solves

Every device on the internet needs an IP address, but there aren't enough
public IPv4 addresses for every phone, laptop, and smart bulb on Earth to
have its own. NAT is the workaround: it lets many devices on a private
network share a single public IP address when they talk to the internet.

Your home Wi-Fi router does this constantly. Every device in your house
gets a **private IP** (like `192.168.1.10`), but to the outside world,
all of your traffic appears to come from **one public IP** your router's
