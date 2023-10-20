****
**Application Load Balancer (V2)**

* Application Load Balancer is Layer 7 (HTTP)
* Load Balancing to multiple HTTP applications across machines (target groups)
* Load balancing to multiple applications on the same machine (containers)
* Support to HTTP/2 and WebSocket
* Support redirects (from HTTP or HTTPS for example)
* Routing tables to different target groups:
    * Routing based on path in URL (example.com/users & example.com/posts)
    * Routing based on hostname in URL (one.example.com & other.example.com)
    * Routing based on Query String, Headers (example.com/users?id=123&order=false)
* ALB are a great fit for micro services & container-based application (example: Docker & Amazon ECS)
* Has a port mapping feature to redirect to a dynamic port in ECS
* In comparisson, we'd need multiple Classic Load Balancer per application
* Fixed hostname (XXX.region.elb.amazonaws.com)
* The application servers don't see the IP of the client directly
    * The true IP of the client is inserted in the header **X-Forwarded-For**
    * We can also get Port(X-Forwarded-Port) and proto (X-Forwarded-Proto)

**Target Groups**

* EC2 instances (can be managed by an Auto Scaling Group) - HTTP
* ECS tasks (managed by ECS itself) - HTTP
* Lambda functions - HTTP requests is translated into a JSON event
* IP Addresses - must be private IPs
* ALB can route to multiple target groups
* Health checks are at the target group level
* Its a good practice to only allow traffic to your instances through the security group of the Load Balancer
****