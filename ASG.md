# ASG

- Link: https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/13528102#overview

## ASG Atrribute
- A Launch Template(Older "Launch COnfigurations are deprecated)
- Min Size/ Max Size/ Initial Capacity
- Using with **CloudWatch Alarm**

## Scaling Policies
- https://nab.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26148326#overview

- Dynamic Scaling
  - Target tracking policies(Create alarm for us)
- Schedule Scaling
- Predictable Scaling -> Machine Learning
## Scaling Cooldows

## Suspend-resume processes
- Types of processes
    + **ReplaceUnhealthy** – Terminates instances that are marked as unhealthy and then creates new instances to replace them. For more information, see Health checks for instances in an Auto Scaling group.

    + **ScheduledActions** – Performs the scheduled scaling actions that you create or that are created for you when you create an AWS Auto Scaling scaling plan and turn on predictive scaling. For more information, see Scheduled scaling for Amazon EC2 Auto Scaling.

