## Intro

_What's a distributed system?_

- A group of nodes working together communicating over message links in order to achieve a task.
  _Why do we need distributed systems?_
- Some applications are inherently distributed. Such as the web.
- Build fault tolerance. If 1 node fails then we can have another or multiple be there to handle the failure.
- Horizontal Scaling. An application/service may have an enormous amount of computation to do and a single node can't be enough to handle it. We would need multiple.

  ## 1.4 Resiliency

  - When a system can continue to serve it's function even when failure occurs.
  - The more components and operations of a system, the higher the chances of failure to occur.
  - If a component fails and it's not well isolated, then the probability of another one crashing increases.
  - **System availability**: _The percentage of the time the system is available for use_.
    - Measured by: uptime / total time (uptime + downtime)

- Availability is _described by nines_: 90% (one nine), 99%(two nines), 99.9%(three nines),... with 3 nines being acceptable and 4+ being highly available.
  **Takeaway:** _Systems will fail and if they don't have any sort of resiliency to handle said fails, the availability will decrease._

## 1.5 Maintainability

- Most of the cost of software after it's it's initial development goes to maintenance (Fixing bugs, adding new features, operation, etc..)
- Because of this we want to make our systems easy to extend and work with.
- Any change could be a incident and so we want to make sure our system's changes don't negatively effect availability.
  - We can accomplish this by testing.
- We also need to monitor the system for any decrease in performance and possibly fix with changes.

## 1.6 Anatomy of a distributed system 
