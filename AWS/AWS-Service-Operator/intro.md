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
By changing the controller behaviour you can change the way your applications are managed. Hence, the controller pattern 
allows us to create decoupled experiences and not have to worry about how other components are integrated.
You can read about Kubernetes Controllers over [here](https://kubernetes.io/docs/concepts/overview/components/) and in 
detail over [here](https://kubernetes.io/docs/concepts/architecture/controller/).

In Kubernetes all applications, volumes, processes are objects. It also gives you the flexibility to define you own custom
objects which it refers by the name [`CustomResourceDefintions`](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/).
AWS Service Operator defines custom resource definitions for each of the AWS Cloud Service in Kubernetes.
This makes it easy to manage your AWS Cloud resource like any other Kubernetes object all at one place.

Let me explain it with an example. Say you want to create an S3Bucket. Instead of creating it using CloudFormation, you wll now
use an S3 CRD in Kubernetes to create your S3 Bucket in AWS. The CRD (CustomResourceDefintions) of S3 In Kubernetes would point 
to the bucket in the cloud.

### Getting Started

1) The first step of using AWS Service Operator is to give your Kubernetes Namespace or the whole cluster itself, the 
necessary IAM Role and Permissions. There are multiple ways to provide the IAM Role. 
    - Through [Kube2IAM](https://github.com/uswitch/kiam)
    - [Role Based Access Control](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) (RBAC) which uses the 
    Kubernetes Service Account Object to attach it with an IAM role and 
    annotates the IAM Role with the Kubernetes Service Account.  
    
Depending on your use-case you can use either of them.

2) Once you are done granting permissions to the namespace or Kubernetes Cluster you can then deploy the AWS-Service-Operator. 
It can be deployed using [helm](https://github.com/amazon-archives/aws-service-operator/tree/master/charts/aws-service-operator)
 or using `kubectl apply -f aws-service-operator.yaml` 

3) Upon successful deployment you would have your AWS Cloud Resources created and corresponding Kubernetes Custom Resource Definitions.
You can get your Kube CRDs and it would show something like this
```.bash
kubectl get customresourcedefinitions
```
```.text
NAME                                   CREATED AT
cloudformationtemplates.operator.aws   2018-09-27T21:30:10Z
dynamodbs.operator.aws                 2018-09-27T21:30:10Z
ecrrepositories.operator.aws           2018-09-27T21:30:10Z
s3buckets.operator.aws                 2018-09-27T21:30:10Z
snssubscriptions.operator.aws          2018-09-27T21:30:10Z
snstopics.operator.aws                 2018-09-27T21:30:10Z
sqsqueues.operator.aws                 2018-09-27T21:30:10Z
```

4) As of 2020 Jan, The AWS Service Operator exposes a way to manage DynamoDB Tables, S3 Buckets, Amazon Elastic Container
 Registry (Amazon ECR) Repositories, SNS Topics, SQS Queues, and SNS Subscriptions.
 If you wanna use some other AWS resource then you might have to do something like this as shown [here](https://github.com/amazon-archives/aws-service-operator/issues/99)
 and define your corresponding CRD like the ones given [here](https://github.com/amazon-archives/aws-service-operator/blob/master/charts/aws-service-operator/templates/crd.yaml)
 
