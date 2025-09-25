
# What Happens When You Type `https://www.google.com` and Press Enter

> A step-by-step look at what really happens behind the scenes—from your browser to Google's servers.

---

## 1. DNS Lookup

Your browser first needs to get the IP address of `www.google.com`.

1. **Browser cache**  
   It checks if it already knows the IP.

2. **OS cache**  
   If not, the system cache is checked.

3. **DNS Resolver**  
   If still not found, your computer asks a DNS server (from your ISP or like `8.8.8.8`).

4. **Root > TLD > Authoritative**  
   The DNS request goes up to the root server, then to `.com`, then to Google's DNS server.  
   It returns an IP address like `142.250.72.196`.

---

## 2. TCP/IP Connection

Once the IP is known, the browser starts a connection.

1. **TCP handshake**  
   - Your browser sends a `SYN`.  
   - Google replies with `SYN-ACK`.  
   - Your browser responds with `ACK`.

2. **IP Routing**  
   The packets travel through routers, from your computer to Google.

---

## 3. Firewalls

Firewalls check the traffic.

- **Local firewall** on your device.  
- **Network firewall** on your router.  
- **ISP firewall** in between.  

They block bad traffic but let safe packets through.

---

## 4. HTTPS and SSL/TLS

The connection becomes secure using **TLS**.

1. **ClientHello**  
   The browser says: "Here are my TLS settings."

2. **ServerHello + Certificate**  
   Google sends back a certificate.

3. **Verification**  
   Your browser checks if the certificate is valid and trusted.

4. **Key exchange**  
   Both sides create a shared key.  
   All future communication is now encrypted.

---

## 5. Load Balancer

Google has many servers worldwide.

1. The **load balancer** picks the closest and best server.  
2. It also spreads traffic across machines to avoid overload.  
3. It decrypts TLS, so backend servers work with plain HTTP.

---

## 6. Web Server

The request hits Google’s web server.

- It reads the HTTP request.  
- If it's asking for a static file (like an image), it can return it directly.  
- If it’s a search, it forwards the request to an application server.

---

## 7. Application Server

This is where your search gets processed.

- It cleans up the query.  
- It may correct typos or suggest similar terms.  
- It sends the query to Google’s search engine backend.  
- It gathers results, ads, and other info.

---

## 8. Database and Index

The app server talks to big databases.

- **Bigtable** stores structured data.  
- **Spanner** handles relational data globally.  
- **Colossus** stores Google’s huge index of the web.

These systems return search results, which are assembled into an HTML page.

---

## 9. Response and Rendering

1. Google sends back the response over HTTP/2 or QUIC.  
2. Your browser receives HTML and builds the page.  
3. It fetches images, JavaScript, and CSS.  
4. The page is displayed.

---

## Conclusion

When you type a URL and hit Enter:

- **DNS** gets the IP.  
- **TCP/IP** opens the connection.  
- **Firewalls** protect the flow.  
- **TLS** secures it.  
- **Load balancers** pick a server.  
- **Web and app servers** handle the request.  
- **Databases** provide the data.  
- **Browser** shows the result.

