# Platform Reference Architecture for AWS EKS with CASTAI

This repo provides a configuration for AWS EKS with CASTAI, built on top of Crossplane. This configuration exposes a simple API to your internal developers for creating Kubernetes clusters. In the background, this configuration can create clusters in AWS. It automatically applies common recommended practices, such as connecting the cluster to existing Flux deployments, automating VPC setup, and creating a Flux operator in a cluster and uses CASTAI as cluster autoscaler.

This repo is a starting point for you to deliver your own Cluster-as-a-Service. Fork this repository and customize the configuration to meet your teams' needs.

Advantages of Cluster-as-a-Service:

- GitOps workflow
- Production-ready template
- Scalable architecture
- CASTAI cluster autoscaler
- Product agnostic approach

## Quickstart

To deploy in a new organization, follow the [Get Started guide](https://docs.upbound.io/quickstart/).

For deployments to an existing organization, log in to your Upbound organization
and go to **Configurations** and click **Create Configuration**.

Connect your Upbound organization to GitHub. Select the Github organization and
repository name for your cloned repo and choose the **platform-ref-aws-castai** configuration.

When your new configuration is ready, create a new control plane based on the
cloned repo you just created.

After a few minutes, your new control plane is ready!

Once authenticated and configured, your self-service Upbound console lists
available cloud resources.

### Prerequisites

- CAST AI account
- CAST AI Credentials
- AWS Credentials

### Set up ProviderConfig for CASTAI

Before we can use the reference configuration we need to configure it with CAST AI FullAccess API Access Key:
- Obtained CAST AI [API Access Key](https://docs.cast.ai/docs/authentication#obtaining-api-access-key)

```console
# Create Secret with CAST AI API Access Key
cat <<EOF | ${KUBECTL} apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: castai-creds
  namespace: upbound-system
type: Opaque
stringData:
  credentials: |
    {
      "api_token": "y0ur-t0k3n",
      "api_url": "https://api.cast.ai"
    }
EOF

# Configure the CAST AI Provider to use the secret:
kubectl apply -f examples/castai-default-provider.yaml
```

### Set up ProviderConfig for AWS
Authenticate your managed control plane with external services [here](https://docs.upbound.io/concepts/mcp/oidc)


## Using the Platform Reference Architecture for AWS EKS with CASTAI

Create the Configuration:
```console
kubectl apply -f examples/cluster.yaml
```


🎉 Congratulations. You have just installed your Platform Reference Architecture for AWS EKS with CASTAI!

## Overview

```
XCluster/platform-ref-aws-castai-8jzvs                                                True     True    Available   
├─ Usage/platform-ref-aws-castai-8jzvs-vcfhp                                          -        True    Available   
├─ Usage/platform-ref-aws-castai-8jzvs-wlkz5                                          -        True    Available   
├─ Usage/platform-ref-aws-castai-8jzvs-wsbxh                                          -        True    Available   
├─ XEKS/platform-ref-aws-castai-8jzvs-292jc                                           True     True    Available   
│  ├─ SecurityGroup/platform-ref-aws-castai-8jzvs-q6bw4                               True     True    Available   
│  ├─ Addon/platform-ref-aws-castai-8jzvs-dpvr5                                       True     True    Available   
│  ├─ Addon/platform-ref-aws-castai-8jzvs-s94g9                                       True     True    Available   
│  ├─ ClusterAuth/platform-ref-aws-castai-8jzvs-5g4w5                                 True     True    Available   
│  ├─ Cluster/platform-ref-aws-castai-8jzvs-k7bmd                                     True     True    Available   
│  ├─ NodeGroup/platform-ref-aws-castai-8jzvs-482rw                                   True     True    Available   
│  ├─ ProviderConfig/platform-ref-aws-castai                                          -        -                   
│  ├─ OpenIDConnectProvider/platform-ref-aws-castai-8jzvs-ql76z                       True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-8qrdk                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-hvqvw                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-vlwm9                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-wffcw                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-wgrjc                        True     True    Available   
│  ├─ Role/platform-ref-aws-castai-8jzvs-ldj79                                        True     True    Available   
│  ├─ Role/platform-ref-aws-castai-8jzvs-w98hp                                        True     True    Available   
│  ├─ Object/platform-ref-aws-castai-aws-auth                                         True     True    Available   
│  ├─ Object/platform-ref-aws-castai-irsa-settings                                    True     True    Available   
│  └─ ProviderConfig/platform-ref-aws-castai                                          -        -                   
├─ XNetwork/platform-ref-aws-castai-8jzvs-7d2k9                                       True     True    Available   
│  ├─ InternetGateway/platform-ref-aws-castai-8jzvs-f6tc5                             True     True    Available   
│  ├─ MainRouteTableAssociation/platform-ref-aws-castai-8jzvs-7rqtk                   True     True    Available   
│  ├─ RouteTableAssociation/platform-ref-aws-castai-8jzvs-8xwr8                       True     True    Available   
│  ├─ RouteTableAssociation/platform-ref-aws-castai-8jzvs-9xjfb                       True     True    Available   
│  ├─ RouteTableAssociation/platform-ref-aws-castai-8jzvs-ftsqm                       True     True    Available   
│  ├─ RouteTableAssociation/platform-ref-aws-castai-8jzvs-txwpq                       True     True    Available   
│  ├─ RouteTable/platform-ref-aws-castai-8jzvs-x8ghv                                  True     True    Available   
│  ├─ Route/platform-ref-aws-castai-8jzvs-7qpk9                                       True     True    Available   
│  ├─ SecurityGroupRule/platform-ref-aws-castai-8jzvs-2hjlw                           True     True    Available   
│  ├─ SecurityGroupRule/platform-ref-aws-castai-8jzvs-4tbmb                           True     True    Available   
│  ├─ SecurityGroup/platform-ref-aws-castai-8jzvs-qvwkc                               True     True    Available   
│  ├─ Subnet/platform-ref-aws-castai-8jzvs-6m2l4                                      True     True    Available   
│  ├─ Subnet/platform-ref-aws-castai-8jzvs-97d2h                                      True     True    Available   
│  ├─ Subnet/platform-ref-aws-castai-8jzvs-c4gkl                                      True     True    Available   
│  ├─ Subnet/platform-ref-aws-castai-8jzvs-tfw6g                                      True     True    Available   
│  └─ VPC/platform-ref-aws-castai-8jzvs-5p56x                                         True     True    Available   
├─ XFullAccess/platform-ref-aws-castai                                                True     True    Available   
│  ├─ XReadOnly/platform-ref-aws-castai                                               True     True    Available   
│  │  ├─ EksCluster/platform-ref-aws-castai-8jzvs-s5vhr                               True     True    Available   
│  │  └─ Release/platform-ref-aws-castai-8jzvs-6c9tv                                  True     True    Available   
│  ├─ AutoScaler/platform-ref-aws-castai-8jzvs-pltzp                                  True     True    Available   
│  ├─ EksClusterId/platform-ref-aws-castai-8jzvs-t8jzv                                True     True    Available   
│  ├─ EksUserArn/platform-ref-aws-castai-8jzvs-wb2hs                                  True     True    Available   
│  ├─ NodeConfigurationDefault/platform-ref-aws-castai-8jzvs-nsxvc                    True     True    Available   
│  ├─ NodeConfiguration/platform-ref-aws-castai-8jzvs-bpzzt                           True     True    Available   
│  ├─ NodeTemplate/platform-ref-aws-castai-8jzvs-nxktp                                True     True    Available   
│  ├─ Release/platform-ref-aws-castai-8jzvs-gckqx                                     True     True    Available   
│  ├─ Release/platform-ref-aws-castai-8jzvs-mhcvx                                     True     True    Available   
│  ├─ Release/platform-ref-aws-castai-8jzvs-pdc6p                                     True     True    Available   
│  ├─ InstanceProfile/cast-eks-platform-ref-aws-castai-8jzvs-k7bmd-instance-profile   True     True    Available   
│  ├─ Policy/cast-eks-platform-ref-aws-castai-8jzvs-k7bmd-cluster-policy              True     True    Available   
│  ├─ Policy/cast-eks-platform-ref-aws-castai-8jzvs-k7bmd-cluster-policy-restricted   True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-5zhtb                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-6wq9l                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-72bqx                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-ftrgj                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-lndxg                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-w52xn                        True     True    Available   
│  ├─ RolePolicyAttachment/platform-ref-aws-castai-8jzvs-wxklj                        True     True    Available   
│  ├─ Role/cast-eks-platform-ref-aws-castai-8jzvs-k7bmd-cluster-role                  True     True    Available   
│  └─ Role/cast-eks-platform-ref-aws-castai-8jzvs-k7bmd-instance-profile              True     True    Available   
├─ XReadOnly/platform-ref-aws-castai                                                  True     True    Available   
│  ├─ EksCluster/platform-ref-aws-castai-8jzvs-s5vhr                                  True     True    Available   
│  └─ Release/platform-ref-aws-castai-8jzvs-6c9tv                                     True     True    Available   
└─ XFlux/platform-ref-aws-castai-8jzvs-99jrm                                          True     True    Available   
   ├─ Release/platform-ref-aws-castai-8jzvs-7bqhj                                     True     True    Available   
   └─ Release/platform-ref-aws-castai-8jzvs-8nl8p                                     True     True    Available  
```

## Questions?

For any questions, thoughts and comments don't hesitate to [reach
out](https://www.upbound.io/contact) or drop by
[slack.crossplane.io](https://slack.crossplane.io), and say hi!