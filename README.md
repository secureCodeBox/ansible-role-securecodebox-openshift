Ansible secureCodeBox OpenShift Role
=========

An ansible role to deploy a secureCodeBox stack on a OpenShift environment.

Requirements
------------

A fully fletched OpenShift environment.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

None

Example Playbook
----------------

Note additionally to the following configuration you'll need to store some confidential values securely between deployments. (e.g. The password to the camunda database). We recommend storing these in encrypted form via ansible vault. These can then be imported using the include vars syntax.

```yml
---
- hosts: localhost ansible_connection=local
  remote_user: root
  pre_tasks:
  - name: secret config
    include_vars: secrets.yml
  roles:
    - role: ansible-role-securecodebox-openshift
      vars:
        oc_project_id: secure-code-box
        oc_project_name: secureCodeBox
        oc_project_description: "Passion for IT Security - Continuous Security out-of-the-box."
        # URL to your OpenShift Cluster Console
        oc_cluster_url: https://localhost:8443
        # Login credentials used for oc login
        oc_username: MY-USERNAME
        oc_token: MY-TOKEN

        # This will create routes like engine.foobar.com
        oc_route_base_url: .foobar.com

        # Deletes the existing project (with the "oc_project_id") if 'true', otherwise 'false'
        development: false
        #
        # Project Members
        # Possible Roles: https://docs.openshift.org/latest/architecture/additional_concepts/authorization.html#roles
        #
        oc_project_members:
          - name: foo_bar
            role: admin
          - name: max_musterman
            role: edit
        #
        # IP-Whitelist
        # Block any Requests coming from other IP-Address Ranges
        #
        oc_enable_ip_whitelisting: false
        # Can be mutiple address ranges separeted by a space.
        # e.g. "12.34.56.78/24 98.76.54.32/8"
        oc_ip_whitelist: ""
        #
        # Persistence / Volume Configuration
        # Configuration to enable a fully persistent stack (engine & elasticsearch)
        #

        # if set to false no volume wil be specified or mounted to the pods
        # setting this to false will mean that all other persistence option will not have any effect
        oc_persistence_enabled: true

        # if set to false you have to specify the names of the pre existing volumes to use!
        # if set to true new volume claims will be created
        # More on prebinding: https://docs.openshift.org/latest/dev_guide/persistent_volumes.html#persistent-volumes-volumes-and-claim-prebinding
        oc_create_volumes: true
```

Example (decrypted) `secret.yml`

```yml
mysql_password: eQZfqKybEgLwKkrisFs]WgmMFe6%dEw{qKEAG2tLCR89tG3G
scanner_user: scanner-technical-user
scanner_password: CDaFqCjWokwkeFwhMdi7HEe7sTv3cLTB.w{n9L7hNNkHWZ;V
```

License
-------

Apache-2.0

Author Information
------------------

secureCodeBox - iteratec GmbH
[secureCodeBox.io](https://www.securecodebox.io/)
[iteratec.de](https://www.iteratec.de/)
[secureCodeBox Github](https://github.com/secureCodeBox/secureCodeBox)
