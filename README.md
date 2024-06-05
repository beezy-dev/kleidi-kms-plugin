# kleidi KMS provider plugin for Kubernetes

## Why? 
The traditional credentials handling practices enforce a clear separation of concerns between application and infrastructure teams.   
However, Kubernetes centralized credentials through the ```secret``` and ```configmap``` API objects within ```etcd``` with an encryption layer. 

More here [Security](docs/security.md) or with [Kubernetes Secrets Handbook](https://www.amazon.com/Kubernetes-Secrets-Handbook-production-grade-management/dp/180512322X)

## How?
Kubernetes introduces a KMS plugin framework to support access to an external security (hardware or software) module and enable an envelope encryption practice. 
The Kubernetes API server will encrypt plaintext data with a data key, request kleidi to encrypt the data key with a third-party key, and store all the encrypted payload in ```etcd```. 
Reading the payload will require access to the third-party provider via Kleidi.

## Current state
* KMSv2 with Kubernetes 1.29 and onwards.
* PKCS#11 interface to [SoftHSM](https://www.opendnssec.org/softhsm/) deployed on the control plane nodes.   
* HashiCorp Vault Community/Enterprise integration
More here [Implementation](docs/architecture.md)

# Deployments

* [HashiCorp Vault Implementation](docs/vault.md)
* [SoftHSM Implementation](docs/softhsm.md)

## Future state  
* (v)TPM integration (see R&D)
* AWS/Azure Key Vault integration
* Delinea/Thycotic integration 

## Why 1.29 or later?
***Stability!***   

Any prior release marked KMSv2 as non-stable. Here is the extract from the [Kubernetes documentation](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/#before-you-begin):  
*The version of Kubernetes that you need depends on which KMS API version you have selected. Kubernetes recommends using KMS v2.*   
* *If you selected KMS API v2, you should use Kubernetes v1.29 (if you are running a different version of Kubernetes that also supports the v2 KMS API, switch to the documentation for that version of Kubernetes).*
* *If you selected KMS API v1 to support clusters before version v1.27 or if you have a legacy KMS plugin that only supports KMS v1, any supported Kubernetes version will work. This API is deprecated as of Kubernetes v1.28. Kubernetes does not recommend the use of this API.*

## Origin of kleidi
<img align="right" src="https://beezy.dev/images/DALL-E-kleid%C3%AD_comic_strip.png" width="25%">

Initially, [romdalf](https://github.com/romdalf) founded [Trousseau](https://trousseau.io) in 2019 and released a production-grade KMSv1 provider plugin during his tenure at Ondat.  

With the Kubernetes project moving to KMSv2 stable at 1.29 and KMSv1 being deprecated since 1.27, a decision needed to be made regarding rewriting the plugin, leading to the creation of kleidi.

The origin is Greek, and the meaning is "key". (Source: [Wikipedia](https://en.wiktionary.org/wiki/%CE%BA%CE%BB%CE%B5%CE%B9%CE%B4%CE%AF))

<br clear="left"/>
<br clear="left"/>
