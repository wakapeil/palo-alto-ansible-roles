# What this is for
This role will automate creating VPN tunnels for Palo Alto firewalls. Specifically, it will configure the following items:
- IKE crypto profiles
- IPSec crypto profiles
- IKE gateways
- Tunnel interfaces
- IPSec tunnels, and optionally proxy-IDs
- Static routes

This role is not intended to be a "one size fits all" solution; it's a baseline that can (and should) be customized to meet your specific needs. Refer to the `examples` folder to understand how it can be used, and feel free to make any modifications you want. 


# Usage Instructions
This role uses Ansible Collections, and as such requires version 2.9 or higher. 

You will also need to install the panos ansible-galaxy collection using: 

```bash
ansible-galaxy collection install paloaltonetworks.panos
```

# Notes
 This role is meant to be used with other tasks/roles. It shouldn't be too difficult to integrate it into workflows that also create address objects and security policies for the VPN. 

 Tested on PanOS 8.1, 9.0, and 9.1

Using the `--check` flag will fail when creating proxy-IDs if the VPN tunnel does not exist. It's still pretty safe to run the playbook as long as the `vpn_commit_config` flag is set to 'false'. 
 
# List of Configurable Variables
Below is a list of configurable variables, along with some examples of the values they accept. 
You can find additional module-specific details [here](https://ansible-pan.readthedocs.io/en/latest/modules/index.html)


Some default values have already been set in `/defaults/main.yml`, but those can be changes at any time.

## Required Settings  
vpn_panos_provider:
vpn_name:  
vpn_state: `[present | absent]`  
vpn_local_peer_ip:  
vpn_remote_peer_ip:  
vpn_preshared_key:  
vpn_local_subnet:  
vpn_remote_subnet:  

## Phase 1 Crypto Settings
vpn_ike_version: 
vpn_phase1_authentication: `['md5','sha1','sha256','sha384','sha512']`  
vpn_phase1_encryption: `['des','3des','aes-128-cbc','aes-192-cbc','aes-256-cbc']`  
vpn_phase1_dhgroup:  `['group1','group2','group5','group14','group19','group20']`  
vpn_phase1_lifetime_hours:

## Phase 2 Crypto Settings
vpn_phase2_authentication: `['md5','sha1','sha256','sha384','sha512']`  
vpn_phase2_encryption: `['des','3des','aes-128-cbc','aes-192-cbc','aes-256-cbc']`  
vpn_phase2_dhgroup: `['no-pfs','group1','group2','group5','group14','group19','group20']`  
vpn_phase2_lifetime_hours: 

## IKE Gateway Settings
vpn_ike_gateway_interface:
vpn_local_id_type: `['ipaddr','fwdn','ufqdn','keyid','dn']`  
vpn_local_id_value:
vpn_peer_id_type: `['ipaddr', 'fwdn', 'ufqdn', 'keyid', 'dn']`  
vpn_peer_id_value: 

## Tunnel Interface Settings:
vpn_tunnel_zone:  
vpn_tunnel_interface_number:  
vpn_virtual_router:  
vpn_tunnel_interface_ip:  

## Object Names
vpn_phase1_profile_name:  
vpn_phase2_profile_name:  
vpn_ike_gateway_name:  
vpn_ipsec_tunnel_name:  
vpn_proxy_id_name:  
vpn_static_route_name:  

## Boolean Options
vpn_configure_proxy_id:  
vpn_enable_nat_traversal:   
vpn_enable_passive_mode:  
vpn_is_disabled:  
vpn_commit_config:   
vpn_enable_dpd:  
