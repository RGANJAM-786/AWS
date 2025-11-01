What is AWS Route 53?

Route 53 provides DNS as a service on AWS. The core function of DNS is to map easy-to-remember domain names (like amazon.com) to hard-to-remember IP addresses (like 3.6.10.171) [04:07]. This is essential because:

Readability: Domain names are much easier for users to remember than IP addresses [06:33].

Stability: IP addresses can change (especially if you restart a service or instance). The domain name remains constant, and Route 53 updates the mapping to the new IP address [07:15].

How Route 53 Works in an AWS Architecture
Route 53 acts as the initial interceptor for user requests [10:46].

A user attempts to access an application using a domain name (e.g., amazon.com).

Route 53 is the first service to intercept this request.

Route 53 checks its DNS records (which are stored in a Hosted Zone) [11:19].

It resolves the domain name to the IP address of the target, which is typically an AWS Load Balancer (ELB) in the public subnet.

The request is then forwarded to the Load Balancer, and the traffic continues through the VPC components (like the private subnet) to reach the final application [10:53].

Key Components of Route 53
Route 53 offers three main capabilities [13:28]:

Domain Registration: Users can purchase new domain names directly through AWS Route 53 (similar to GoDaddy) or integrate domains purchased from external registrars [11:41].

Hosted Zones:

This is the container where all your DNS records are stored [12:13].

The records map your domain name to the target IP address or resource (like a Load Balancer) [13:53].

Hosted Zones can be either Public (for internet-facing applications) or Private (for internal applications within your VPC) [13:06].

Health Checks:

Route 53 can perform checks on your web servers (e.g., every one or five minutes) to confirm they are active and healthy [14:45].

This capability is crucial for advanced routing policies where Route 53 might balance traffic between multiple active web servers or redirect traffic away from an unhealthy one [15:02].
