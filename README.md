#### Readme

   ```flow
   st=>start: Start AWX Provisioning
   c_tower_up=>condition: Wait till AWX is up
   o_tower_conf=>operation: Configure AWX connection settings
   o_create_project=>operation: Create project zo-devops-ansible
   o_create_inventory=>operation: Create inventory for this stack
   o_create_jt=>operation: Create job_template(s) for each role
   o_update_tags=>operation: Update status tag on Instance
   o_c_inv_script=>subroutine: Create inventory script based on zoaws.py
   o_c_inv_sc=>subroutine: Attach inventory script to inventory
   sns=>operation: Send Notifications
   e=>end: End
   
   st(right)->c_tower_up
   c_tower_up(yes,right)->o_tower_conf
   o_tower_conf->o_create_project
   o_create_project->o_create_inventory
   o_create_inventory->o_create_jt
   o_create_inventory->o_c_inv_script
   o_c_inv_script->o_create_jt(left)->o_update_tags
   o_update_tags->e
   c_tower_up(no)->sns(bottom)
   sns(bottom)->o_update_tags
   
   
   
   ```

- Client instance(s) (linux, windows, ?) 

  ```bash
  sudo apt update -y
  sudo apt install -y curl vim git python jq python-pip
  pip install awscli boto3 ec2_metdata ansible-tower-cli tenacity 
  
  #Bootstrap script
  ```

