 The goal of this project was to use the Windows tracert command to:

Visualize the network path (hops) from a local system to google.com

Observe how TTL (Time To Live) expiration reveals intermediate routers

Identify latency spikes, timeouts, and potential firewalls or filtering

Understand how network segmentation or hardened infrastructure impacts visibility

**What Was Discovered:**

Hop 1 (Local Router) did not respond to ICMP-based traceroute, confirming that TTL-expired ICMP Echo Requests are filtered — a common default in consumer and ISP routers. However, a follow-up Nmap TCP-based traceroute confirmed that the router was functional and simply applying protocol-specific filtering, an important real-world security behavior.

Hops 2–6 responded reliably, though occasional jitter (e.g., Hop 5) suggested normal queuing behavior rather than performance issues. These hops reflect the ISP backbone infrastructure and regional peering points.

Hop 7 returned only one of three probes, suggesting ICMP rate-limiting or packet filtering, likely marking a firewall inspection point or hardened router.

Hops 8–10 were stable and responsive, consistent with Google’s internal edge network — indicating well-optimized cloud infrastructure.

Hop 11 was the final destination, a Google edge server in San Francisco, confirming Anycast routing and a clean path with low latency and no packet loss.

Key Takeaways:
TTL-based tools like tracert can expose a great deal about network structure, latency patterns, and filtering behaviors — even when IP hostnames are unavailable.

Different tools (ICMP vs. TCP traceroute) reveal different visibility levels, which is critical for security analysis and infrastructure testing.

IPv6 routing is widely adopted (as seen in this project), and its format, compression, and allocation are worth understanding for modern network analysis.

Concepts like jitter, rate-limiting, and backbone routing emerged naturally from the data, providing rich insight into how real-world internet routing behaves.

