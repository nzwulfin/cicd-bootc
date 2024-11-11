# cicd-bootc
Demo repo for Github Actions based builds of bootc images

For RHEL, this example uses an activation key to get access to a subscription and a service account to get access to the terms based registry images. These are set up as secrets and variables scoped to the repo.You can easily change the names of these in the repo and the workflow file to suit your own standards.

## Accessing a subscription during build
To use packages from the RHEL repositories, the builder will need to have subscription information available. This workflow will register the container, execute the build, and then unregister as a 
final step. You will only be using the subscription for the duration of the build. To use subscription-manager in a pipieline like this, it's easiest to use an activation key. If you don't have a subscription already, the [No-cost RHEL for developers subscription](https://developers.redhat.com/products/rhel/download) is a good option.

If you aren't familiar with actionvation keys, from the docs:
> An activation key is a preshared authentication token that enables authorized users to register and auto-configure systems. Running a registration command with an activation key and organization  ID combination, instead of a username and password combination, increases security and facilitates automation.

[Creating an activation key in the console](https://docs.redhat.com/en/documentation/subscription_central/1-latest/html/getting_started_with_activation_keys_on_the_hybrid_cloud_console/assembly-creating-managing-activation-keys#proc-creating-act-keys-console_)

Create 2 secrets in the repo

Organization ID as *RHT_ORGID*

Activation key as *RHT_ACT_KEY*

## Getting access to the base image
Ublike UBI, the bootc base image does require an account to access since this is a full RHEL host. To log into the registry during a pipeline build or other automation, you can [create a regitry service account}(https://access.redhat.com/RegistryAuthentication#registry-service-accounts-for-shared-environments-4) in tne customer portal.

### Token Information
Create 1 var and 1 secret in the repo

Token username as *RHT_REG_SVCUSER* (has a "|" character in the name)

Password as *RHT_REG_SVCPASS*

### Crrent build status
[![Fedora 40 bootc image workflow](https://github.com/nzwulfin/cicd-bootc/actions/workflows/build_fedora_bootc.yml/badge.svg)](https://github.com/nzwulfin/cicd-bootc/actions/workflows/build_fedora_bootc.yml)
[![RHEL 9 bootc image workflow](https://github.com/nzwulfin/cicd-bootc/actions/workflows/build_rhel_bootc.yml/badge.svg)](https://github.com/nzwulfin/cicd-bootc/actions/workflows/build_rhel_bootc.yml)
