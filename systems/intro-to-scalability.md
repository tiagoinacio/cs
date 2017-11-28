# How to scale a website to handle more users

## Vertical scaling

Buy more CPU's, more disk space and more Ram. But it is not a full solution because either going to be out of budget or we will not always be at the state of the art.

## Horizontal scalling

Not use the state of the art hardware, but use more and cheaper hardware. Instead of one or two good machines, we have a bunch of servers not so good.

With horizontal scalling we need load balancers to distribute HTTP requests to our servers.
Now, DNS instead of return the IP Address of each box, it now returns the IP of the load balancer. And the load balancer distributes the traffic through each box. Each box is private, are not accessible from the public world.

## Load Balancer

How can a loader balancer decide how to route the traffic?

Based on the actual load: who is the busiest server. (better solution)
Round robin: one box at a time. The load balancer forwards to the first server, then the second, then the third and so forth. The problem is that one server could be getting all the expensive computation.

Operating system and the browser tipically caches the DNS response, which means it stores the IP address of the server. But the load balancer has only one adress, and it redirects the traffic based on round robin, randomness, load of each server, etc.

But what about sessions? Are now broken, because sessions are saved as a text file in /tmp directory. Because we are reaching different servers, that don't have the session saved.

We could have one server per feature. A PHP server for example to store those sessions. But again, if we need to scale we have the same problem.

We could have a file server, which is connected to all of the servers, where we could store state.

Weakness in our network topology. What if that machine breaks? We loose all our information.

Solved the problem of shared state but sacrifice some robustness, some redundancy. How do we fix this?

With RAID.

Raid assumes that we have multiple hard drives.

Raid 0 is good for performance, every time the operating system wants to write, we write some to one disk and to another, and so on.

Raid 1 writes the same data for multiple hard drives. If some hard drive fails, we still have the other.

Raid 10, is the combination of the previous one. We use 4 drives.

Raid 5

