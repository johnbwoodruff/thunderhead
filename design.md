# AWS Service Resolvers
Need a more descriptive name for these.
Each service (i.e.) can *optionally* have a service resolver created for it in Thunderhead.
This service is a preprocessor that reads dependencies in it. For each dependency
    The service gets the outputs from that service resolver
    It adds it to the relevant list of resources it is creating (i.e. SGs ingress/egress, IAM policies, environment variables, scripts)


# Thunderhead Resources
These are high-level resource concepts under a different namespace (e.g. "Thunderhead::Fargate")
    They expand to form their own collection of one or more AWS resources
You don't need to use these, but they can be much more concise for some tasks
** These resources can also have dependencies (e.g. a Fargate service that consumes an S3 bucket)

# Dependency output types
The following output types can be produced by a resource:

* Security group partial ingress rules (i.e. "add an )
* IAM policies
* Environment variables
* Scripts

What about resource-based policies? Those essentially go in the other direction

** In some cases the dependent service needs to perform an action to wire up to its dependency:
    IAM Policies
    Environment variables
    Scripts (not now, future)
   In other cases the dependency needs to perform an action to *allow* the dependent service to wire:
    Resource-based policies
    Security group ingress rules

# Wiring Procedures
## IAM policy
Using example: Lambda consuming S3

1. S3 creates bucket, exports policy for consumers
2. Lambda creates function and IAM role/policy. The exported policies go in the policy, referencing the bucket

## Environment Variables
Using example: Lambda consuming S3

1. S3 creates bucket, exports environment variables of bucket name and URL
2. Lambda creates function and adds exported variables in its "environment variables section"

## Resource based policy:
Using example: Lambda consuming SQS with resource based policy

1. Lambda creates function
2. SQS creates queue, along with resource policy that references the Lambda

## Security group ingress rules
Using example: Lambda consuming RDS

1. Lambda creates function and security group 1
2. RDS creates database and security group 2
3. RDS adds ingress rule from security group 1 on security group 2

## Lifecycle
Calculate dependency graph for dependencies
From top to bottom for each provisioner:
    Call createSecurityGroup() - Takes ingress rules from lower levels (if any)

From bottom to top for each provisioner:
    Call createResources() - Takes in environment variables and policies (if any)

From top to bottom for each provisioner:
    Call createResources
    

# Event Handling
What about events? These were their own concept in Handel because they basically go the other way.

Event handling often has actions required by *both* the producer and consumer (e.g. SNS producing events to Lambda)

# VPC Handling
VPCs are special because they can be created in the template or passed in outside. Somehow the created resources need to understand which VPC and subnets to use