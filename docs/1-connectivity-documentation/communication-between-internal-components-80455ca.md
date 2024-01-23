<!-- loio80455cab3d024991b649963187ec2e17 -->

# Communication between Internal Components

Configure secure internal communication between transparent proxy components.

Internal communication between transparent proxy components can be made secure by setting the Helm property `.Values.config.security.communication.internal.encryptionEnabled` to true. By default, `.Values.config.security.communication.internal.encryptionEnabled` is true, and this is recommended for all productive scenarios.

If `.Values.config.security.communication.internal.encryptionEnabled` is true, `.Values.config.security.communication.internal.certmanager.issuerRef.name` is required.

The certificate management types *cert-manager.io* \([https://cert-manager.io/docs/](https://cert-manager.io/docs/)\) and *cert.gardener.cloud* \([https://github.com/gardener/cert-management](https://github.com/gardener/cert-management)\) are currently supported.

-   When using *cert-manager.io*, you should specify `.Values.config.security.communication.internal.certManager.issuerRef.kind` and `.Values.config.security.communication.internal.certManager.issuerRef.Name`.
-   When using *cert.gardener.cloud*, you should specify `.Values.config.security.communication.internal.certManager.issuerRef.namespace` and `.Values.config.security.communication.internal.certManager.issuerRef.Name`.

