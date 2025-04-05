# ipi-yaml-generator - Automated YAML generation for OpenShift IPI install method

OpenShift Installer Provisioned Installation (IPI) follows a fully automated, opinionated approach where the OpenShift installer manages the entire infrastructure.
This installation program uses each cluster host’s baseboard management controller (BMC) for cluster provisioning. 
The install-config.yaml file, required to initiate an Installer-Provisioned Infrastructure (IPI) installation, contains essential details about the cluster, infrastructure, and nodes. The attempt to auto-generate the "install-config.yaml" file leverages Intersight APIs and Ansible, offering several advantages:

•	Speed up deployment – Automates cluster setup, reducing provisioning time. 

•	Improve reliability – Ensures consistent configurations across multiple clusters.

•	Enable repeatable deployments – Facilitates consistent deployments for testing, validation, and production environments.

•	Minimize human errors – Reduces manual intervention, preventing misconfigurations and improving stability.

•	Support dynamic provisioning – Leverages Intersight APIs to dynamically fetch infrastructure settings based on the target platform. 

# Simple block diagram showing YAML generation for OpenShift IPI installation process

<img width="948" alt="image" src="https://github.com/user-attachments/assets/495c7b8a-c23c-47cd-aded-4f59ebc7f462" />

The diagram above shows the various pieces addressed in the YAML file. Cluster, infra and node details are fetched using Intersight APIs. The user input variables for:

•	Cluster and infra are captured in the inventory.ini file within the folder inventory

•	Each of the node details are captured in the host vars folder within inventory

<img width="452" alt="image" src="https://github.com/user-attachments/assets/5d827c5e-1148-4c36-9d1d-aae7559b8efa" />

The auto-generated YAML file follows Jinja template to render install-config.yaml file. The generated YAML file will be available in the outputs folder.

<img width="452" alt="image" src="https://github.com/user-attachments/assets/fe194eb4-e84f-4608-9194-fd6e90bfd439" />

# Prerequisites:

1.	Use ansible-playbook to create pools, policies, and profiles. Apply profiles to the baremetal servers. 
Note – Infrastructure provisioning using Ansible using Intersight API is available in Ansible Galaxy: https://docs.ansible.com/ansible/devel/collections/cisco/intersight/ 
2.	DNS, DHCP, client machine is configured and ready to use.
3.	In this example code, static IP assignment is opted to suit the lab protocol. However, DHCP server can be referenced within the playbook for dynamic OS IP assignment.
To use this code base to auto-generate install-config.yaml for bringing up OpenShift cluster using IPI install methods, follow these steps:
1.	Git clone the respository.
2.	Install Cisco Intersight Ansible by running the command: 
ansible-galaxy collection install 
Note: You can refer to the Cisco Intersight Ansible Collections documentation for setup information: cisco.intersighthttps://galaxy.ansible.com/ui/repo/published/cisco/intersight/
3.	Provide user inputs for cluster, infra and hosts by following the example.
4.	Generate API key and Secret for your Intersight account.
5.	Provide the Intersight API key and Secret in the inventory > inventory.ini
6.	Run the command- ansible-playbook -i inventory/inventory.ini server.yml
7.	Access your auto-generated install-config.yaml file in the output folder.

# YAML generation workflow using Ansible

<img width="696" alt="image" src="https://github.com/user-attachments/assets/5c0d7310-e32f-443d-aaac-2f91567a29e1" />






