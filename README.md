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

Because these ranges are reused inside millions of separate private
networks, a packet with a private source address can't be routed across the internet-routers have no idea which of the millions of `192.168.1.10`s. NAT exists to translate that private address into something globally unique before the packet leaves the network.

## How the translation actually works
 
imagine your laptop (`192.168.1.10`) sends a request to a web server
(`93.184.216.34`) on port 80. Your laptop uses a random local port for
this connection - say `51000`.

1. **Outbound**: the packet leaves your laptop with
   `src = 192.168.1.10:51000`, `dst = 93.184.216.34:80`


2. **At the router**: NAT rewrites the source to the router's public IP
   and picks a public port to represent this specific connection:
   `src = 203.0.113.5:40001`, `dst = 93.184.216.34:80`

3. **The router remembers this** in a **NAT table** — a row that maps
   `192.168.1.10:51000 ↔ 203.0.113.5:40001`

4. **The server replies** to what it believes is the sender:
   `src = 93.184.216.34:80`, `dst = 203.0.113.5:40001`

5. **At the router**: it looks up port `40001` in its NAT table, finds
   your laptop's private address, and rewrites the destination back:
   `dst = 192.168.1.10:51000`

6. **Your laptop receives the reply** as if the router weren't even
   there.

The **port number is the key** it lets one public IP represent many simultaneous private devices. this specific technique is called as **PAT(port address translation)** it translates on ports, not just addresses.

## 3 Types of NAT
 
| Type | What happens | Common use |
|---|---|---|
| **Static NAT** | One private IP always maps to one fixed public IP | Hosting a server behind NAT |
| **Dynamic NAT** | Private IPs are mapped to public IPs from a shared pool, one-to-one | ISPs with a small public IP pool |
| **PAT** (most common) | Many private IPs share **one** public IP, distinguished by port | Home and office routers |



