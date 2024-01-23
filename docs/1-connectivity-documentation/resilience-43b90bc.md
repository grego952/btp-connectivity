<!-- loio43b90bc61fa043068cb2bae5ed89f09e -->

# Resilience

Improve resilience of the transparent proxy for Kubernetes.

Even though the transparent proxy is not a cloud service, it offers options to improve resilience and robustness of the whole system benefiting from the transparent proxy functionality.

The software architecture of the transparent proxy in terms of HTTP and TCP proxies is loosely decoupled, meaning that if there are failures in one of them it would not affect the other. Thus they are independent of each other and errors regarding for example the transparent HTTP proxy should not affect the work of the transparent TCP proxy instances.

To achieve additional resilience, see [High Availability](high-availability-fb92ab6.md).

