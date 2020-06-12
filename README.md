# ansible-role-sp-reg-app
Ansible role for installing application for registration SPs

## Requirements

## Role variables

### Must be filled
* spreg_email_address - Email address
* spreg_server_name - Server name (without http or https)
* spreg_available_languages - Available languages
* spreg_db_name - Database name (will be created)
* spreg_db_username - Database username (will be created)
* spreg_db_password - Database password
* spreg_yubikey_id - Yubikey id (Generate at https://upgrade.yubico.com/getapikey/)
* spreg_yubikey_key - Yubikey key (Generate at https://upgrade.yubico.com/getapikey/)
* spreg_yubikey_lognames - List of login names to use from the yubikey_users hash, default is empty
* spreg_sudo_root_lognames - Llist of lognames that can sudo to root, default is empty
* spreg_yubikey_users - List of users with their ssh key and yubikey id
    * Example of structure:
    ```yaml
    tesla:
        name: Nikola Tesla
        yubikeys:
          - ccccccefghij
        sshkeys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDe9Rb2N5aq5qYAi8OCeQKlpOBJi/Ll2tlxqiD7Gan7wJrFBbrZIj8a5tOpHKTm61ldihxG7hnXkyEvbAX5vx/6lLagKaLFL3ysh3iH3ZxiXFYXfLklqrrCK2kuwdCIasMF4kJYzS/goLEGeqBkeJN8SvTj2THvzWcvsTZXIgXygzqiiSKlJao2v62EZv3Pi0eP8KhLrdYW2EcePBOKclLGYxdAX0k9KMJHJRecQhS2BtDLDL1rGoCCrw3Pd8689xovzYKC/ATnTZ89slA9HlrKyQjkjVeBX7WbRsjrgYKEDeqWZbdzjT9Nhg/Ftewbqh2V6p8OFQTftKUOmmPXlwAr
    ```
* spreg_mariadb_root_password - Password for root user
* spreg_certs_dir - Path to cert dir
* spreg_idp_entity_id - Entity Id of identity provider
* spreg_shibboleth_template_metadata_url - Url to metadata of identity provider
* spreg_apache_template_ssl_certificate_file_path - Path to SSL certificate
* spreg_apache_template_ssl_certificate_key_path - Path to SSL key
* spreg_apache_template_ssl_certificate_chain_path - Path to SSL chain
* spreg_template_appconfig_admins - List of admin's userIds
* spreg_template_appconfig_oidc_enabled - Url to metadata of identity provider
* spreg_template_appconfig_languages - List of available languages
* spreg_template_appconfig_host_url - Host url
* spreg_template_appconfig_secret - the secret (the random string which will be used for generating codes)
* spreg_template_appconfig_proxyidentifier_attrname - Perun attribute name proxyIdentifier
* spreg_template_appconfig_masterproxyidentifier_attrname - Perun attribute name masterProxyIdentifier
* spreg_template_appconfig_testsp_attrname - Perun attribute name isTestSp
* spreg_template_appconfig_issamlsp_attrname - Perun attribute name isSamlSp
* spreg_template_appconfig_isoidcsp_attrname - Perun attribute name isOidcSp
* spreg_template_appconfig_showonservicelist_attrname - Perun attribute name showOnServiceList
* spreg_template_appconfig_admincontact_attrname - Perun attribute name administrationContact
* spreg_template_appconfig_usermail_attrname - Perun attribute name preferredMail
 * spreg_template_appconfig_entityid_attrname - Perun attribute name entityId
* spreg_template_appconfig_oidcclientid_attrname - Perun attribute name oidc clientId
* spreg_template_appconfig_oidcclientid_attrname - Perun attribute name oidc clientSecret
* spreg_template_appconfig_approval_allowspecifymails - False if user is not given an option to fill emails of persons who should sign the approval
* spreg_template_appconfig_approval_defaultauthorities - List of emails that should be used when user does not fill the emails for approval
* spreg_template_appconfig_footer_html - Application custom footer
* spreg_template_appconfig_header_html - Application custom header (in HTML)
* spreg_template_appconfig_header_title Application title
* spreg_template_appconfig_header_logo - Logo rul
* spreg_template_appconfig_perunrpc_url - Perun RPC url
* spreg_template_appconfig_perunrpc_username - Perun RPC username
* spreg_template_appconfig_perunrpc_password - Perun RPC user password
* spreg_template_mail_emails - List of application administrator emails
* spreg_template_mail_smtphost - SMTP host for sending mails
* spreg_template_mail_from - Message FROM field
* spreg_template_mail_footer - Foter of the messages
* spreg_template_mail_create_user_subject - Subject of message when notification is sent to user about created request
* spreg_template_mail_create_user_message - Message body when notification is sent to user about created request
* spreg_template_mail_create_admin_subject - Subject of message when notification is sent to admin about created request
* spreg_template_mail_create_admin_message - Message body when notification is sent to admin about created request
* spreg_template_mail_update_user_subject - Subject of message when notification is sent to user about updated request
* spreg_template_mail_update_user_message - Message body when notification is sent to user about updated request
* spreg_template_mail_update_admin_subject - Subject of message when notification is sent to admin about updated request
* spreg_template_mail_update_admin_message - Message body when notification is sent to admin about created request
* spreg_template_mail_status_updated_subject - Subject of message when notification is sent to user about updated request
* spreg_template_mail_status_updated_message - Message body when notification is sent to user about updated request
* spreg_template_mail_signed_user_subject - Subject of message when notification is sent to user about signed request to move SP to production
* spreg_template_mail_signed_user_message - Message body of message when notification is sent to user about signed request to move SP to production
* spreg_template_mail_signed_admin_subject - Subject of message when notification is sent to admin about signed request to move SP to production
* spreg_template_mail_signed_admin_message - Message body of message when notification is sent to admin about signed request to move SP to production
* spreg_template_mail_production_authorities_subject - Subject of message when notification is sent to authority when moving to production has been requested
* spreg_template_mail_production_authorities_message - Message body when notification is sent to authority when moving to production has been requested
* spreg_template_mail_admins_add_subject - Subject of message when notification is sent to user when asked to become service administrator
* spreg_template_mail_admins_add_message - Message body when notification is sent to user when asked to become service administrator
* spreg_template_prod_transfer_authorities_mails - Configuration for mails for transferring to production
* spreg_template_all_attrs - All attributes definition
    * Example of structure:
    ```yaml
    attributeId:  # AttributeIdentifier - REQUIRED
     attrName: # Perun attribute identifier - REQUIRED
     name: # REQUIRED
       cs: # Name in CS lang
       en: # Name in EN lang
     description: # REQUIRED
       cs: # Description in CS lang
       en: # Description in EN lang
     allowed_keys: # List of keys - REQUIRED ONLY ON ATTRIBUTES WITH TYPE MAP
       - cs
       - en
     allowed_values: # List of available values - OPTIONAL
     regex: "a" # Regular expresison which will be applied on input - OPTIONAL
     displayed: true # Specify if input will be displayed - OPTIONAL - Default value is true
     editable: true # Specify if input will be editable - OPTIONAL - Default value is true
     required: true # Specify if attribute is required - OPTIONAL - Default value is true
    attributeId2:  # AttributeIdentifier - REQUIRED
     attrName: # Perun attribute identifier - REQUIRED
     name: # REQUIRED
       cs: # Name in CS lang
       en: # Name in EN lang
     description: # REQUIRED
       cs: # Description in CS lang
       en: # Description in EN lang
   ```
* spreg_template_attrs_access_control_inputs - List of attributes Ids of attributes defined in accessControl.properties
* spreg_template_attrs_oidc_inputs - List of attributes Ids of attributes defined in oidc.properties
* spreg_template_attrs_organization_inputs - List of attributes Ids of attributes defined in organization.properties
* spreg_template_attrs_saml_inputs - List of attributes Ids of attributes defined in saml.properties
* spreg_template_attrs_service_inputs - List of attributes Ids of attributes defined in service.properties

### Optional params

:information_source: Default values are stored [here](defaults/main.yml).

* spreg_firewall_open_ssh_ports - Firewall settings for ssh
    * Example of structure:
    ```yaml
    - { port: "ssh", ipv4: "x.x.x.x/16", comment: "accept ssh from X" }
    ```
* spreg_firewall_open_tcp_ports - Firewall settings
    * Example of structure:
    ```yaml
    - { port: 80, comment: "Allow http" }
    - { port: 443, comment: "Allow https" }
    ```
* spreg_unattended_upgrades_origin_patterns - Repositories to use for automatic updates
    * Example value: 
    ```yaml
    |2
    "origin=Debian,codename=${distro_codename}";
    "origin=Debian,codename=${distro_codename}-updates";
    "origin=meta@cesnet.cz,a=stable";
    ```
* spreg_unattended_upgrades_blacklist - Blacklist for unattended upgrades
* spreg_unattended_upgrades_mail_address - Mail address for unattended upgrades
* spreg_monitoring_check_mk_packages - List of packages to install for monitoring
* spreg_monitoring_check_mk_local_scripts_by_template - List of files which will be copied to /usr/lib/check_mk_agent/local/
* spreg_monitoring_check_mk_local_scripts_file - List of templates for files in /usr/lib/check_mk_agent/local/
* spreg_monitoring_check_mk_plugins_by_template - List of files which will be copied to /usr/lib/check_mk_agent/plugins/
* spreg_monitoring_check_mk_plugins_file - List of templates for files in /usr/lib/check_mk_agent/plugins/
* monitoring_template_service_running_check_services - List of monitoring services
    * This option is only for 'service_running.sh.j2' template
* spreg_sendmail_relays - List of relays which will be defined in sendmail
* spreg_mariadb_databases_to_create - List of databases which will be created
* spreg_mariadb_scripts - Structure of script's which will be run on database
    * Example of structure:
    ```yaml
    - script: script1
     database: dbname1
    - script: script2
     database: dbname1
    ```
* spreg_mariadb_users_to_create - Structure of user's login and password
    * Example of structure:
    ```yaml
    spreg_mariadb_users_to_create:
      - login: user1
        password: password1
      - login: user2
        password: password2
    ```
* spreg_mariadb_users_privileges - Structure od user's login and list of privileges
    * Example of structure:
    ```yaml
    spreg_mariadb_users_privileges:
      - login: user1
        privileges:
          - "dbname1.*:ALL"
          - "dbname2.*:ALL"
      - login: user2
        privileges:
          - "dbname1.*:ALL"
    ```
* spreg_shibboleth_sp_entity_id - Shibboleth SP entityId
* spreg_shibboleth_template_attribute_map_allow_urn_oid_attributes - If True, urn:oid attributes will be uncommented in attribute-map 
* spreg_shibboleth_template_attribute_map_allow_urn_mace_attributes - If True, urn:mace attributes will be uncommented in attribute-map 
* spreg_shibboleth_template_attribute_map_allow_schac_attributes - If True, schac attributes will be uncommented in attribute-map 
* spreg_shibboleth_template_attribute_map_custom_attributes - Structure of custom attributes for 
    * Exemple structure:
    ```yaml
    - id: epuid
    name: urn:oid:1.3.6.1.4.1.5923.1.1.1.13
    comment: eduPersonUniqueId
    decoder:
      type: ScopedAttributeDecoder
    ```
* spreg_shibboleth_template_remote_users - List of shibboleth Remote user values()
* spreg_shibboleth_template_attribute_prefix - Shibboleth attribute prefix
* spreg_shibboleth_template_idp_entity_id - Shibboleth IdP ntityId
* spreg_apache_packages - List of packages which will be installed
* spreg_apache_modules - List of apache2 modules which will be enabled (Must include suffix '.load' or '.conf')
* spreg_apache_remove_sites - List of apache2 sites for remove
* spreg_apache_create_sites - List of sites which will be copied from templates (Must start with 'sites-available/')
* spreg_apache_enable_sites - List of sites which will be enabled
* spreg_apache_template_document_root - Path to Apache2 document root
* spreg_repository_URL - Git repository URL
* spreg_source_code_dest - Path to destination directory where will be cloned git repository
* spreg_source_code_version - Branch / Tag which will be used as source
* spreg_config_destination - Path to directory, where will be every configuration file for spreg application
* spreg_template_appconfig_confirmperiod_days - Confirmation limit in days
* spreg_template_appconfig_confirmperiod_hours - Confirmation limit in hours
* spreg_template_appconfig_jdbc_driver - JDBC driver
* spreg_template_appconfig_jdbc_url - JDBC URL
* spreg_template_appconfig_jdbc_username - Username
* spreg_template_appconfig_jdbc_password - Password
* spreg_template_appconfig_entityid - EntityId of Identity provider
* spreg_template_appconfig_masterproxyidentifier_attrvalue - Master identifier of proxy
* spreg_template_appconfig_proxyidentifier_attrvalue - Identifier of Proxy

---
 
## Available tags
* install - Install all necessary packages
* configuration - Reconfigured application
* upgrade - Upgrade SPReg application
* scheme - Change database scheme
* start - Start all services
* stop - Stop all services


## Example playbook
```
- hosts: all
  remote_user: root
  vars:
    spreg_email_address: "proxyidp@cesnet.cz"
    spreg_server_name: "spreg.aai.example.com"
    spreg_available_languages: ['en']
    spreg_db_name: "spreg_db_name"
    spreg_db_username: "spreg_user"
    spreg_db_password: "spreg_passwd"
    spreg_yubikey_id: "48695"
    spreg_yubikey_key: "jGAqANjXDwthsKp0dnboFGmZ5ag="
    spreg_yubikey_lognames: [ 'tesla', 'einstein' ]
    spreg_sudo_root_lognames: [ 'tesla' ]
    spreg_yubikey_users:
      tesla:
        name: Nikola Tesla
        yubikeys:
          - ccccccefghij
        sshkeys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDe9Rb2N5aq5qYAi8OCeQKlpOBJi/Ll2tlxqiD7Gan7wJrFBbrZIj8a5tOpHKTm61ldihxG7hnXkyEvbAX5vx/6lLagKaLFL3ysh3iH3ZxiXFYXfLklqrrCK2kuwdCIasMF4kJYzS/goLEGeqBkeJN8SvTj2THvzWcvsTZXIgXygzqiiSKlJao2v62EZv3Pi0eP8KhLrdYW2EcePBOKclLGYxdAX0k9KMJHJRecQhS2BtDLDL1rGoCCrw3Pd8689xovzYKC/ATnTZ89slA9HlrKyQjkjVeBX7WbRsjrgYKEDeqWZbdzjT9Nhg/Ftewbqh2V6p8OFQTftKUOmmPXlwAr
      einstein:
        name: Albert Einstein
        yubikeys:
          - ccccccghijkl
        sshkeys:
          - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDQiusTXxPGdXXzhHyU9wEb1i5PAdN/qBX8lVw90/yZo6LKBl+fO2QuRTQUxxRgk05puXYwWMF4IheoVBmWFzwClyH/Ox88Yq+WM4nGxIpzvoyUZQ0rRM7a0LfaLvDsJpkoMOr53LFfQtdTY7ZiKXsaTI1EmhHXVmfgFXDTu4IE2EBGUrKPj28+yD/5UuyybA/TfZJ6wW51M0QAaQy3n2xWY+K+aFfTJv2vQin2cIjIPMWfUoUCR2eYNbtZ/uHwXgJxK1W3PeeJhLjW8RXdfLiSOA3+8X5NCHGBs5BLdvieQjB0SYb0NqCc7scAlJV14MGlWdBYuczV2gvn2mnT4q3F
    spreg_mariadb_root_password: "root_passwd"
    spreg_certs_dir: "/etc/ssl/certs"
    spreg_idp_entity_id: "https://idp.example.com/idp"
    spreg_shibboleth_template_metadata_url: "http://federation.org/federation-metadata.xml"
    spreg_apache_template_ssl_certificate_file_path: ""
    spreg_apache_template_ssl_certificate_key_path: ""
    spreg_apache_template_ssl_certificate_chain_path: ""
    spreg_template_appconfig_admins: []
    spreg_template_appconfig_oidc_enabled: true
    spreg_template_appconfig_host_url: ""
    spreg_template_appconfig_secret: ""
    spreg_template_appconfig_proxyidentifier_attrname: ""
    spreg_template_appconfig_masterproxyidentifier_attrname: ""
    spreg_template_appconfig_testsp_attrname: ""
    spreg_template_appconfig_issamlsp_attrname: ""                 
    spreg_template_appconfig_isoidcsp_attrname: ""
    spreg_template_appconfig_showonservicelist_attrname: ""
    spreg_template_appconfig_admincontact_attrname: ""
    spreg_template_appconfig_usermail_attrname: ""
    spreg_template_appconfig_entityid_attrname: ""
    spreg_template_appconfig_oidcclientid_attrname: ""
    spreg_template_appconfig_oidcclientsecret_attrname: ""
    spreg_template_appconfig_approval_allowspecifymails: true/false
    spreg_template_appconfig_approval_defaultauthorities: []
    spreg_template_appconfig_footer_html: ""
    spreg_template_appconfig_header_html: ""
    spreg_template_appconfig_header_title: "Service provider registration"
    spreg_template_appconfig_header_logo: ""
    spreg_template_appconfig_perunrpc_url: ""
    spreg_template_appconfig_perunrpc_username: ""
    spreg_template_appconfig_perunrpc_password: ""
    spreg_template_prod_transfer_authorities_mails: []
    spreg_template_attrs_access_control_inputs: []
    spreg_template_all_attrs: []
    spreg_template_attrs_oidc_inputs: []
    spreg_template_attrs_organization_inputs: []
    spreg_template_attrs_saml_inputs: []
    spreg_template_attrs_service_inputs: []
  roles:
    - cesnet.spreg
```

## How to install SP registration app
1. Create a new playbook from example playbook
2. Add `perun-ansible-roles` as a submodule for your playbook
    ```git
    git submodule add https://github.com/CESNET/perun-ansible-roles.git cesnet_roles 
    git submodule update --init --recursive    
    ```
3. Set correct `roles_path in your ansible.cfg`
    ```bash
    echo "roles_path=cesnet_roles" >>ansible.cfg
    ```
4. Run your playbook