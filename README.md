<p align="center"><img width="300" src="./thunderhead.png" alt="thunderhead logo"></p>

<p align="center">Thunderously productive CloudFormation</p>

## What is this supposed to be?
Well, it's nothing yet. If I have the inclination to finish it, it might be pretty cool. So far all this repository is are some design ideas and Golang learning!

I have used CloudFormation for probably 6-7 years now, but I have never really loved writing the templates. The part that seems really tedious to me is when you have to create all the VPC and IAM resources to wire things together. Even though it takes them hours of work, people usually don't get them right anyway and then they have a nice insecure infrastructure to build their application on. :)

The idea of this tool is to be a sort of preprocessor for CloudFormation. Here's a rough feature set:

* Provide a simple dependency syntax to allow you to wire resources together, automatically creating all the security bits for you
* Provide support in automatically wiring event sources between AWS services that support them
* Provide a plugin system so that very-high-level resource types can be provided (i.e. a load-balanced ECS Fargate service)
* Output regular vanilla CloudFormation. You aren't tied into this tool, and you can use as much or as little of it as you like.

Many ideas I have for this tool are a continuation of ideas formulated while working on the [Handel](https://handel.readthedocs.io/en/latest/) tool that I worked on while employed at BYU. That tool had somewhat different goals than I have for this tool, but there are also many similarities.

## Usage
1. Build from source using the Go toolchain
2. Run `thunderhead`
3. Realize that so far the program just outputs 'Hello'. Proceed to :cry:
