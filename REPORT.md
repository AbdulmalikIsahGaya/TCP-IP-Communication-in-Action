# TCP/IP Communication in Action: Opening a Secure Website

## 1. Introduction

This report explains how a user’s request to open a secure website such as `https://example.com` travels through the TCP/IP communication model. It highlights the roles of key protocols, network devices, addresses, and security mechanisms involved in establishing a secure connection and retrieving a web page.

The report focuses on how data moves from a client device to a web server and back, demonstrating the process of encapsulation, routing, addressing, and secure transmission. The study also explains how network layers cooperate to ensure communication is reliable, secure, and efficient.

---

## 2. Background and Scenario

The scenario involves a user on a laptop opening a secure website. When a user types a URL, the browser initiates a series of steps that include:

- DNS resolution to map the domain name to an IP address
- TCP connection setup
- TLS negotiation for secure communication
- HTTP request transfer
- Response delivery from the web server

This communication passes through several devices, including:

- Client laptop
- Access point or switch
- Router
- Internet transit
- Firewall
- Web server

The main idea is that even a single page load touches multiple layers of the network stack.

---

## 3. The TCP/IP Model

The TCP/IP model is a four-layer architecture used for communication across networks. It is closely related to the OSI model, but it groups functions differently.

### 3.1 Application Layer
This layer handles user-facing services and data generation. Examples include:

- HTTP (web browsing)
- DNS (domain name resolution)
- TLS (security and encryption)

At this layer, data is treated as a message.

### 3.2 Transport Layer
This layer is responsible for end-to-end communication and data reliability. It includes:

- TCP: reliable, connection-oriented, ordered
- UDP: faster, connectionless, best-effort

At this layer, data is called a segment.

### 3.3 Internet Layer
This layer handles logical addressing and routing. The main protocol is:

- IP (Internet Protocol)

At this layer, data is called a packet.

### 3.4 Network Access Layer
This layer manages physical network delivery and local communication. It includes:

- Ethernet
- Wi-Fi
- ARP

At this layer, data is called a frame.

---

## 4. Encapsulation and Decapsulation

A major principle in the TCP/IP model is encapsulation. Each layer adds its own header to the data before it is transmitted.

### Client Side
When the browser requests a page, the data is created at the Application Layer and then moved downward through the stack:

1. HTTP request is created
2. TLS adds encryption and authentication information
3. TCP adds source and destination ports
4. IP adds source and destination IP addresses
5. Ethernet adds MAC addresses and frame trailer
6. Data is converted to bits and sent over Wi-Fi or Ethernet

### Server Side
At the server, the reverse process occurs:

- Ethernet header is removed
- IP header is removed
- TCP header is removed
- TLS is decrypted
- HTTP content is delivered to the web server
- Response is generated, typically `200 OK`

This process is known as decapsulation.

---

## 5. Addressing in TCP/IP Communication

A packet travels from the client to the server using several types of addresses:

### 5.1 IP Address
The IP address provides logical addressing. For example:

- Client: `192.168.1.10`
- Web server: `93.184.216.34`

The IP address helps packets move across different networks.

### 5.2 MAC Address
The MAC address is a physical address used for local network delivery. It changes at each network hop within the local segment. For example, the packet may be delivered to the default gateway using the router’s MAC address.

### 5.3 Port Number
Ports identify the specific application or service:

- Source port: `54321`
- Destination port: `443` for HTTPS

This allows the receiving host to know which application should receive the data.

### 5.4 Domain Name / URL
The user enters a URL such as `https://example.com`. Before communication can occur, the domain must be translated into an IP address using DNS.

---

## 6. DNS Resolution

Before a browser can communicate with a web server, it must resolve the domain name into an IP address.

### Process
1. The user enters `https://example.com`
2. The browser sends a DNS query
3. The DNS server responds with the IP address
4. The browser connects to the server using that IP

DNS is essential because users work with names, while machines work with IP addresses.

---

## 7. Secure Communication Using TLS

Once the IP address is known, the client establishes a secure connection using TLS (Transport Layer Security), especially in HTTPS.

### TLS Functions
- Encryption of data
- Authentication of the server
- Integrity protection

During TLS handshake, the client and server exchange messages such as:

- Client Hello
- Server certificate
- Key exchange
- Secure session establishment

This ensures that the communication cannot be easily intercepted or altered by attackers.

---

## 8. TCP vs UDP

The choice between TCP and UDP is important for different network services.

### TCP
TCP is reliable and connection-oriented. It provides:

- Connection setup using a three-way handshake
- Ordered delivery
- Retransmission of lost data

Example:
- HTTPS on port 443
- SMTP on port 587
- FTP on port 21

### UDP
UDP is fast and connectionless. It provides:

- Minimal overhead
- No guarantee of delivery
- No retransmission

Example:
- DNS on port 53
- DHCP
- Voice and video streaming

For a secure website, TCP is required because it ensures that the page content is delivered reliably and in order.

---

## 9. Packet Journey from Client to Server

The request travels from the client device to the destination server through a series of network devices.

### Request Path
- Client laptop initiates HTTPS request
- Access point or switch forwards the traffic
- Router routes the packet toward the internet
- Internet transit moves the packet across networks
- Firewall may inspect or filter the traffic
- Web server receives the request

### Response Path
The server processes the request and sends the response back along the reverse path to the client. This is the return journey of the same communication process.

---

## 10. Security Considerations

A secure website requires more than just a valid address. Several security features work together:

- TLS encryption
- Firewall filtering
- IP routing
- Port-based service identification
- Authentication and integrity checks

Security is therefore part of the communication process rather than a separate add-on.

---

## 11. Troubleshooting DNS Failures

A common problem is a DNS failure, which prevents the browser from resolving the server name.

Example error:
`DNS_PROBE_FINISHED_NXDOMAIN`

### Troubleshooting Approach
A systematic method is to check the problem from the bottom of the network stack upward:

1. Check physical connectivity
   - Ensure the Wi-Fi or Ethernet connection is active
2. Check connectivity to the internet
   - Use `ping 8.8.8.8`
3. Check DNS resolution
   - Use `nslookup example.com`
4. Check IP reachability
   - Use `ping 93.184.216.34`
5. Check firewall rules
   - Ensure port 53 is not blocked
6. Flush and reset DNS settings
   - Use `ipconfig /flushdns`
   - Change DNS server to `1.1.1.1` or `8.8.8.8`
   - Restart DNS client service

This process helps isolate whether the issue is physical, routing, DNS, or firewall-related.

---

## 12. Conclusion

Opening a secure website is a complex but well-structured process that relies on multiple layers of the TCP/IP model. From DNS resolution to TLS handshakes and HTTP requests, each protocol contributes to the successful transfer of data between client and server.

The communication process depends on:

- Correct addressing
- Reliable transport
- Encrypted communication
- Proper routing
- Security controls

Understanding this process is essential for network administration, cybersecurity, and general computer networking. It demonstrates that even a simple web page request uses a coordinated sequence of technologies working together seamlessly.

---

## 13. References

- RFC 791: Internet Protocol
- RFC 793: Transmission Control Protocol
- RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3
- Cisco Networking documentation
- Cloudflare learning resources
- IETF Internet standards

---

If you want, I can also turn this into:
1. a shorter academic report version,
2. a formal project report with abstract and table of contents,
3. a GitHub-ready `README.md` version, or
4. a slide-by-slide report matching your presentation exactly.
