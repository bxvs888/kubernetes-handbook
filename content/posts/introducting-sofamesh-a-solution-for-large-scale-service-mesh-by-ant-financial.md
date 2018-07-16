---
title: "Introducing SOFAMesh - A Solution for Large Scale Service Mesh based on Istio"
subtitle: "Open sourced by Ant Financial"
description: "SOFAMesh is an solution for large-scale Service Mesh based on Istio open-sourced by Ant Financial. At the same time it is also as one of components in SOFA(Scalable Open Financial Architecture)  which is open sourced by Ant Financial."
date: 2018-07-16T12:02:17+08:00
bigimg: [{src: "https://ws1.sinaimg.cn/large/006tKfTcly1ftbkn25cm5j31kw0pyu0z.jpg", desc: "Naval fleet|From Wikipedia|Jul 16,2018"}]
draft: false
tags: ["istio","SOFAMesh","MOSN","Ant Financial","service mesh"]
categories: ["service mesh"]
---

[SOFAMesh](https://github.com/alipay/sofa-mesh) is an solution for large-scale Service Mesh based on [Istio](https://istio.io) open-sourced by [Ant Financial](http://antfin.com). At the same time it is also as one of components in SOFA(Scalable Open Financial Architecture)  which is open sourced by [Ant Financial](http://www.antfin.com). On the basis of inheriting the powerful functions and rich features of Istio, in order to meet the performance requirements under large-scale deployment and to deal with the actual situation in the practice, the following improvements have been made:

1. Replace [Envoy](https://github.com/envoyproxy/envoy) with [MOSN](https://github.com/alipay/mosn) written in Golang.
2. Merge Mixer to the data plane to resolve performance bottlenecks/
3. Enhance Pilot for a more flexible service discovery mechanism.
4. Increase support for [SOFA RPC](https://github.com/alipay/sofa-rpc), [Dubbo](https://dubbo.incubator.apache.org/), etc.

You can find them on GitHub:

- SOFAMesh: https://github.com/alipay/sofa-mesh
- MOSN: https://github.com/alipay/mosn

Our goal is to create a more pragmatic Istio version!

## Architecture

SOFAMesh is logically split into a **data plane** and a **control plane** which is the same as Istio, but it has made some adjustments based on the compatibility of Istio’s overall architecture and protocols:

- **Data plane:** We developed a new Sidecar using Golang instead of Envoy.
- **Control plane:** In order to avoid the performance bottleneck caused by Mixer, we merged the Mixer part into the Sidecar. We also have greatly expanded and enhanced the Pilot and Auth modules.

The following diagram shows the different components that make up each plane:

![SOFAMesh architecture](https://ws3.sinaimg.cn/large/006tKfTcgy1ft798kjr0mj31kw1biagi.jpg)

### MOSN

MOSN(Modular Observable Smart Net-stub) is a sidecar written in Golang. The short-term goal of MOSN is to implement Envoy’s functionality, compatible with Envoy’s API, and integrate with Istio.

In addition, we will increase support for other protocols such as SOFA RPC, Dubbo and HSF to better cater to Chinese users, including our own actual needs.

![SOFAMesh MOSN](https://ws1.sinaimg.cn/large/006tKfTcgy1ft75ot24lzj31ec18479s.jpg)

Because of Sidecar is a relatively independent modular, and we also expect to have a separate scenario to use MOSN, we have made a independent repository from SOFAMesh for it, you can find it on https://github.com/alipay/mosn. Welcome everyone to use, asks for requirements and feedbacks.

### Pilot

We will greatly expand and enhance the Pilot module in Istio:

- Add SOFA Registry Adapter to provide solutions for hyper-scale service registration and discovery.
- A data synchronization module is added to enable data exchange between multiple service registration centers.
- Add Open Service Registry APIs to provide standardized service registration.

![SOFAMesh Pilot架构图](https://ws1.sinaimg.cn/large/006tKfTcgy1ft75pq8rplj31kw19sn5q.jpg)

## Future

Together with Pilot, MOSN will provide the ability to allow traditional intrusive frameworks (such as Spring Cloud, Dubbo, SOFA RPC, etc) and Service Mesh products to communicate with each another, in order to smoothly evolve and transition to Service Mesh products.

We put the Pilot, Mixer, Auth and other Istio modules in the same code repository forked from Istio. We will keep update and consistency with the latest code of Istio in the future.

## Furthermore

- MOSN: https://github.com/alipay/mosn
- SOFAMesh: https://github.com/alipay/sofa-mesh
- SOFA official website: http://www.sofastack.tech