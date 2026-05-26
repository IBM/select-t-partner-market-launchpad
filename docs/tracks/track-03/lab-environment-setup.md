# Lab Environment Setup — Maximo

Provision and validate all lab environments **at least 24 hours before** the session. Never leave this to the morning of.

## Configuring Maximo Application Suite

Use the Suite administration Configurations page to access and manage the IBM® Maximo® Application Suite configuration settings for your environment.

When you deploy and activate a Maximo Application Suite application, you must provide the required settings for the application and for any supporting tools. You can preconfigure these settings to require no further input during deployment.

The following sections describe the Maximo Application Suite configurations and the required parameters. Any configurations that require pod downtime can result in system or application outages for users.

### Configuration Scopes

Maximo Application Suite configurations are set at a defined scope, such as system or application:

- **System scope**: The configuration is set for and can be used across the whole suite. Example: A JDBC configuration that can be used by all applications in the suite.

- **Workspace scope**: The configuration is set for and can be used in the default workspace. Example: The JDBC connection that can be used by all applications in the suite.

- **Application scope**: The configuration is set for and can be used by a single application. Example: The JDBC connection that is used by the application.

- **Workspace-application scope**: The configuration is set for and can be used by a single application in the default workspace. Example: The JDBC connection that is used by the application in the default workspace.

### Key Configuration Areas

#### 1. [Setting up IBM Maximo Application Suite](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/install/setup.html)
After you install IBM Maximo Application Suite, the setup program guides you through the initial configuration.

#### 2. [Storing Configuration Values as Secrets](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/manage_config_secrets.html)
Maximo Application Suite uses Red Hat® OpenShift® for managing digital authentication credentials (secrets).

#### 3. [Configuring the Global Image Pull Secret](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/install/configure_pull_secret.html)
Configure the global image pull secret so that you can pull image sources from the IBM Entitled Registry.

#### 4. [Certificate Management](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/c_ctr_cert_mgt.html)
Maximo Application Suite uses IBM Certificate Manager service to automatically manage SSL/TLS certificates for your apps and services and ensure that certificates are valid and up to date. Alternatively, you can also enable manual certificate management to upload your public transport layer security (TLS) certificates.

#### 5. [Storage](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/manage_config_storage.html)
The storage configurations control Maximo Application Suite storage options at the system and application scope.

#### 6. [User Authentication](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/c_ctr_user_auth.html)
Users authentication is managed by using:
- Local user authentication
- Lightweight Directory Access Protocol (LDAP) authentication
- Security Assertion Markup Language (SAML) authentication
- OpenID Connect (OIDC) authentication

After you set up identity providers, you can configure them to provide multiple login options that users can authenticate to when they log in. You can also specify a default identity provider to be the primary login option and enable seamless login for SAML.

#### 7. [User Synchronization](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/c_ctr_user_reg_sync.html)
User registry synchronization simplifies Maximo Application Suite user management by synchronizing users and groups with an LDAP server. By using user registry synchronization, you can automate your user management by synchronizing users and groups between an LDAP server and your local user registry.

#### 8. [Setting up System Event Email Notifications](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_ctr_setup_emails.html)
You can enable email notifications for Maximo Application Suite system events such as new user welcome emails and password reset communication. Starting in Maximo Application Suite 9.0.3, 8.11.15 or 8.10.18, you can configure how transactional emails are used by creating custom templates, changing the language of emails, and disabling emails.

#### 9. [Configuring External Launchers](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/manage_config_other.html)
External launchers are products that are managed outside of Maximo Application Suite. By configuring an external launcher, you enable product for use with Maximo Application Suite and add a tile in the Suite navigator.

#### 10. [Configuring the Minimum Password Length](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_password_length_cr.html)
You can change the default minimum password length in Maximo Application Suite by creating a secret.

#### 11. [Changing Privacy Access for Obtaining User Data](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_config_privacy_user_data.html)
If you use APIs to retrieve user data, you can view that data. However, you can configure the Suite custom resource (CR) file to control whether that information is available to all users.

#### 12. [Enabling Special Characters for User ID and Username](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_enable_sp_characters.html)
User IDs and username can typically contain only alphanumeric characters and some special characters. However, you can enable Maximo Application Suite the use of all special characters by updating the custom resource file in Red Hat OpenShift Container Platform.

#### 13. [Customizing Workloads](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/c_ctr_cust_workload.html)
As an administrator, you can manually configure workloads so that IBM Maximo Application Suite can scale them to match demand. You can modify pod specifications, such as replicas, container resources, affinity, anti-affinity, and tolerations.

#### 14. [Configuring the User Interface](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_ctr_user_interface.html)
You can change the appearance of the user interface by adding notifications to the login page, including your own branding and custom visual style, or hiding guided tours.

#### 15. [Configuring Cross-Origin Resource Sharing (CORS)](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/admin/t_config_cors.html)
Cross-origin resource sharing (CORS) in Maximo Application Suite enables secure access for communication between various resources from different domains. You can implement CORS in Maximo Application Suite by updating the custom resource file in Red Hat OpenShift Container Platform.

#### 16. [Using Single-Node Red Hat OpenShift Clusters](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/sno/c_using_single_node_rhos_clusters.html)
A single-node cluster in Red Hat OpenShift consists of a single control plane node that is configured to run workloads. This configuration offers both control node and worker node functions, so you can deploy a smaller Red Hat OpenShift environment with or without dependence on a centralized management cluster. A single-node cluster can run autonomously when needed, which is useful for resource-constrained environments, demos, proofs of concept, or on-premises deployments.

#### 17. [Message Processing](https://www.ibm.com/docs/en/masv-and-l/cd?topic=appsuite/c_show_ID.html)
The JMSQSEQCONSUMER cron task reads from a continuous queue that already has an active Message Driven Bean. This setup can lead to duplicate message processing, messages being processed hours or days after initial processing, and confusing and misleading entries in the Message Tracking application.

---

## Reference
For more detailed information, visit: [IBM Maximo Application Suite Configuration Documentation](https://www.ibm.com/docs/en/masv-and-l/cd?topic=configuring)
