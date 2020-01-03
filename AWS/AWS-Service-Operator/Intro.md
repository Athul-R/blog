# AWS-Service-Operator
#### [TL;DR](#foo) Too Long Didn't Read. 

The AWS-Service-Operator is an open source project aimed at managing AWS resources from the kubernetes.


Usually it requires a [HashiCorp Terraform](https://www.terraform.io/) or 
[AWS CloudFormation](https://aws.amazon.com/cloudformation/) templates to create AWS resources in the AWS Cloud.
Though maintaining the CloudFormation templates are easy but the creation and the management of the resources can be 
hectic at times. Especially when you use Kubernetes where services use AWS resources and services. 

The separation between Kubernetes platform, AWS CloudFormation and the AWS resources makes it laborious to maintain the 
existing resources' lifecycle and to create new ones. 

The AWS-Service-Operator bridges the gap between them. It uses Kubernetes API to create, manage and delete the AWS resources
using CloudFormation templates. ---- Okay.. this is a lot to break down, which I would do in the below paragraphs.

### Prerequisites
The [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) uses a controllers to manage the applications lifecycle. 
The Kubernetes uses a central state manager (etcd) (which has all the cluster data  (configurations of all applications)) to update the applications.


