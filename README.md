# Heat

The OpenStack Orchestration Service

## Terminology
### Stack
A stack is the collection of objects—or resources—that will be created by Heat. This might include instances (VMs), networks, subnets, routers, ports, router interfaces, security groups, security group rules, auto-scaling rules, etc.

### Template
Heat uses the idea of a template to define a stack. If you wanted to have a stack that created two instances connected by a private network, then your template would contain the definitions for two instances, a network, a subnet, and two network ports. Since templates are central to how Heat operates, I’ll show you examples of templates in this post.

### Parameters
A Heat template has three major sections, and one of those sections defines the template’s parameters. These are tidbits of information—like a specific image ID, or a particular network ID—that are passed to the Heat template by the user. This allows users to create more generic templates that could potentially use different resources.

### Resources
Resources are the specific objects that Heat will create and/or modify as part of its operation, and the second of the three major sections in a Heat template.

### Output
The third and last major section of a Heat template is the output, which is information that is passed to the user, either via OpenStack Dashboard or via the heat stack-list and heat stack-show commands.

### HOT
Short for Heat Orchestration Template, HOT is one of two template formats used by Heat. HOT is not backwards-compatible with AWS CloudFormation templates and can only be used with OpenStack. Templates in HOT format are typically—but not necessarily required to be—expressed as YAML (more information on YAML here). (I’ll do my best to avoid saying “HOT template,” as that would be redundant, wouldn’t it?)

### CFN
Short for AWS CloudFormation, this is the second template format that is supported by Heat. CFN-formatted templates are typically expressed in JSON (see here and see my non-programmer’s introduction to JSON for more information on JSON specifically).

## Architecture
### Heat API
The heat-api component implements an OpenStack-native RESTful API. This components processes API requests by sending them to the Heat engine via AMQP.
### Heat API CFN
The heat-api-cfn component provides an API compatible with AWS CloudFormation, and also forwards API requests to the Heat engine over AMQP.
### Heat Engine
The heat-engine component provides the main orchestration functionality.
