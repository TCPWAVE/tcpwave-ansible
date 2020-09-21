# tcpwave-ansible
Ansible Playbooks to interact with TCPWave IPAM.
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
