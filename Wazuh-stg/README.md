+++
Credits to Wazuh for the awesome project of Wazuh and their template for K8s, although it has been modified deeply to fit certain needs.


```markdown
### THIS IS THE **STAGING** VERSION!!!!
```

---


![Wazuh Logo](https://electrotuto.com/wp-content/uploads/2022/02/wazuh_img.png)


---




This guide outlines the steps to deploy a hardened, production-ready Wazuh cluster on Kubernetes, adhering to Kubernetes security best practices. It allows in-depth configuration of your Wazuh cluster for an enterprise environment.

### Future Plans for Wauzh is as follows

- OpenZiti for Making services Dark in a cluster to the endpoint.
- Add Rules and Plugins instead of a vanilla install Ruleset with Wazuh.

## Configuration Overview

### Wazuh Components

- **Dashboard**: Visualize and manage your security data.
- **API**: Interface for interaction with the Wazuh ecosystem.
- **Filebeat**: Facilitates log data forwarding to the Wazuh manager.
- **Local Options**: Customize agent configurations and behaviors.



### OpenSearch Components

- **Dashboard**: A powerful visualization platform for data indexed in OpenSearch.
- **Internal Users**: Manage user access and privileges. *(Note: Coordination required for access provisioning.)*
- **RBAC**: Define roles and map them to users or groups to enforce security policies.
- **SSO**: Implement Single Sign-On to streamline authentication processes with Microsoft Entra ID



### Kubernetes Cluster Security

- **Node Up-to-date**: Ensure all cluster nodes are regularly updated.
- **Firewall Setup**: Configure firewalls to protect cluster nodes.
- **Secure Etcd**: Encrypt and restrict access to Etcd.
- **Image Scanning**: Regularly scan container images for vulnerabilities.
- **Auditing and Logging**: Implement mechanisms to audit and log activities.
- **Backup & Restore Policies**: Define and automate backup and restore procedures.



### Production Deployment

1. Ensure your Kubernetes cluster is version 1.25 or higher.
2. Rancher Longhorn is configured for StorageClass, PersistentVolume, and PersistentVolumeClaim
3. Securely manage secrets, considering external secret managers like Vault by HashiCorp / AuthentiK 
4. Review and adapt network policies to secure service access.
5. Fine-tune resource requests/limits based on load testing.
6. Apply role-based access control (RBAC) configurations.

### Common Steps

- Clone the provided repository.
- Generate or provide certificates, adjusting as necessary within the `certs` and `opensearch.yml` files.
- Amend secrets within the `secrets` directory.
- Deploy using Kustomize: `kubectl apply -k .`.

### Accessing the Dashboard

- Establish a secure method to access the dashboard, such as setting up a reverse proxy, HAProxy, or API Gateway or OpenZiti
- For testing, you can also use port forwarding: `kubectl -n wazuh port-forward service/wazuh-dashboard 5601:5601`.
- OpenZiti will be implemented for accessing the dashboard and other services down the line.



