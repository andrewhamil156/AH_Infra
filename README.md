# AH_Infra - README
Ansible playbooks to install/configure various resources

## GIT
cd ${BaseDir}

git clone https://github.com/ahamilto156/AH_Infra.git

## Requirements
For any required Ansible roles, review:
[requirements.yml](requirements.yml)

## Hosts file
###NOTE: Must be done first or the yml's won't run
cd  .../AH_Infra
cp hosts_template.yml hosts
vim hosts 
###-> Fill out between the lines


## DNS files
cd  .../AH_Infra/templates
vim fwd.LAN.Net.Fwd.j2 rvs.LAN.Net.Fwd.j2     ###for resolution addresses

##  Variables
[vars/main.yml](vars/main.yml)
vim ../vars/main.yml                        ###for variables as used in ALL playbooks

## Download roles
cd  .../AH_Infra
./initialiseRepo.sh

## Execution
ansible-playbook -kK --limit "${CommaDelimitedHOSTS}” ${PLAYBOOK}.yml

### e.g.s
#### Hardening
ansible-playbook -kK --limit ${server} hardening.yml
#### Configure Squid Proxy
ansible-playbook -kK --limit ${proxy_svr1},${proxy_svr2} proxy_squid.yml
#### Configure basic IdM/IPA
ansible-playbook -kK --limit ${ipa_svr} ipa.yml
#### Configure DNS server
ansible-playbook -kK --limit ${dns1},${dns2} dns.yml

### NOTES:
1/ You do not need a comma at the end of ${CommaDelimitedHOSTS}

2/ proxy_squid.yml does NOT do HA nor load balancing ATM

## License
Free

# Author Information
Andrew Hamilton MEngSc. (Elec.), Grad Dip. PM, BE (Comp.)

Senior Consultant
Red Hat

A: L11, 40 Marcus Clarke Street,
    Canberra City, ACT, 2601, Australia

E: andrew.hamilton@redhat.com  

M: +61-477-242-645-[+61-477-ahamil]

F: +61-2-6247-4380    

# Acknowledgements
- Firstly:
      I would like to thank Geoff Gatward [GG] who patiently taught me much of what I know about Ansible and directed
      me to his playbooks https://github.com/ggatward/GG_Infra.git that I have based these playbooks on [sometimes plagiarised]
- Secondly:
      I would like to thank everyone that created roles that I utilise. These roles are listed in [roles/requirements.yml](roles/requirements.yml) 

# To Do
- Clean up vars: currently in vars/main.yml, vars/proxy_squid.yml AND hosts. i.e. put hosts variables in vars/main.yml