# AWS Fundamentals: Elastic Load Balancing and Autoscaling Groups

## Scalability
Applications ability to handle greater loads by adapting.

---

## Vertical Scaling
- Increasing the size of the resource
- ie. t2.micro --> t2.large
- Common for non-distributed systems like a database
- RDS, ElasiCache are services that can scale vertically
- Limit to how much you can vertically scale

---

## Horizontal Scaling

- increasing the number of instances in application
- implies creating a distributed system
- common for web, modern apps
- cloud makes it easy to horizontally scale

---

## High Availability
- running application in at least 2 data centers
- if one goes down, the application is still up and running
- scaling horizontally goes hand in hand with high availability

- Can be
  - passive
  - active

---

## Scalability and High Availability for EC2

Vertical Scaling
- scale Up / Down
- increase size of instance
- from t2.nano (smallest) --> u-12tb1.metal (largest)

Horizontal Scaling
- Scale in / out
- increase number of instances
- Auto Scaling Group
- Load Balancer

High Availability
- Run instances across many AZs
- Auto Scaling Group multi AZ
- Load Balancer multi AZ

---

## Elastic Load Balancing

Load Balancer
- server that forwards traffic to multiple downstream servers
- balances the traffic load
- Exposes a single point of access to your application
 
### Why use a Load Balancer

- Spread traffic evenly across many instances
- gracefully handle failure of downstream instances
- Can do regular health checks for instances
- Can provide SSL termination (HTTPS) to website
- Enforce stickiness with cookies
- Allows for high availability
- separate public traffic from private traffic

---

### Elastic Load Balancer

- AWS's managed load balancer
- AWS
  - guarantees it to work
  - manages upgrades, maintainance
  - provides only a few configuration knobs

- Much easier than setting up your own load balancer

- Integrates with many AWS offerings

---

### Health Checks








