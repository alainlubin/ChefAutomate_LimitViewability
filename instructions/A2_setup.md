### Pre-Setup:

Upgrade your Chef Automate instance to use IAM_v2
- ssh to your A2 instance: `ssh ec2-user@someIP -i your_key`
- Upgrade you Chef Automate instance to use IAM_v2: `sudo chef-automate iam upgrade-to-v2`
   <kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/ssh-automate.png" width="450" height="225"></kbd>
  
If this is a previously used A2 box, you will have to delete all `Legacy` policies.
- `Settings`>`Policies`>click on the 3 dots>`Delete Policy`   
   <kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-delete-legacy-policies.png" width="450" height="225"></kbd>  
   
#### Setup: 

Within A2:
1. Create Project:`Settings` > `Projects` > `Create Project` > name: `CISO Project` > `Create Project`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-projects.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-projects-create.png" width="380" height="190"></kbd>  
2. Create Team:`Settings`>`Teams`>`Create Team`> name: `Compliance Leadership`> Assign `CISO Project`>`Create Team`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-teams.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-teams-create.png" width="380" height="190"></kbd>    
3. Modify New Team: Access `Compliance Leadership` team >`Add Users`>`Create User`
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-teams-access-project.png" width="300" height="140"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-teams-addusers.png" width="250" height="120"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-teams-createuser.png" width="250" height="120"></kbd>    
4. Create User: name: `CISO` + password > `Create User`> Checkmark `CISO` > `Add User`
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-teams-createcisouser.png" width="280" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-teams-addcisototeam.png" width="380" height="190"></kbd>    
  
  

#### Takeaway:
- You've created a brand new team which contains a new user and is associated with you new CISO Project  
   - You could log in as the new user (CISO), but right now he has no permissions.
   - If you ever want to give more people access to this view, you simply add more users to the `Compliance Leadership` Team
   - Next we will configure the Project  
