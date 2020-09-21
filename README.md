# TCPWave-Ansible Integration
You can automate TCPWave IP Address Management System (TIMS) using Ansible playbooks using the
secure and powerful REST APIsthat are used by TIMS GUI and CLI interfaces, and for integration into cloud
orchestration layers. The TIMS REST APIs are designed to be secure and allow only encrypted access to
the system without the need for any plain text user ID or password.
TIMS supports two mechanisms for handling REST API Authentication

## Session Token Based Authentication:
A long-lived session token is generated in TIMS. This session
token is associated with a given admin user and inherits all the permissions of that user. The
session token is also associated with a source IP and can be used only from that IP. The life of the
session token is set as per the global policy “Maximum Concurrent Sessions per Admin”. The
session token can be revoked or extended at any time. This token is set on the request header as
the TIMS-Session-Token parameter. All the API calls with this token are subjected to the same
permission checks as the associated user and are audited against that user.

## Certificate-Based Authentication:
In this protocol, access to TIMS is provided using a certificate
signed by a trusted authority. The certificate-based mechanism provides a stateless interface that
can be leveraged by automation clients that interact with more than one system. User certificates
can be imported to TIMS and associated with a particular admin. All the service calls made using
that certificate are authorized and audited against the associated admin



# Playbook Commands
  $ ansible-playbook create_object.yaml
  
  $ ansible-playbook delete_object.yaml
  
  $ ansible-playbook create_object_rr_atype.yaml
  
  $ ansible-playbook create_object_rr_cname.yaml
  
  $ ansible-playbook create_object_rr_mx.yaml
  
  $ ansible-playbook create_object_rr_txt.yaml
  
  $ ansible-playbook create_object_rr_srv.yaml
  
  $ ansible-playbook create_object_rr_naptr.yaml
  
  $ ansible-playbook create_zone.yaml
  
  $ ansible-playbook create_zone_rr_Atype.yaml
  
  $ ansible-playbook create_zone_rr_cname.yaml
  
  $ ansible-playbook create_zone_rr_mx.yaml
  
  $ ansible-playbook create_zone_rr_txt.yaml
  
  $ ansible-playbook create_zone_rr_aaaa.yaml
  
  $ ansible-playbook create_zone_rr_srv.yaml
  
  $ ansible-playbook create_zone_rr_naptr.yaml
  
  $ ansible-playbook create_next_available_subnet.yaml
  
  $ ansible-playbook create_dhcp_scopes.yaml
  
  $ ansible-playbook object_workflow.yaml --extra-vars "host_name=ansible-obj object_type=Laptop“
  
  $ ansible-playbook delete_object.yaml --extra-vars "ip_address=10.1.10.11"
  
# Steps to create and use certificates in TCPWave IPAM and Playbooks
## Create root CA cert:
$ openssl  genrsa -des3 -out rootCA.key 4096

$ openssl  req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt

## Create user Cert for cert based REST API:
$ openssl genrsa -out ansible.key 2048

$ openssl req -new -key ansible.key -out ansible.csr

$ openssl x509 -req -in ansible.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out ansible.crt -days 500 -sha256
