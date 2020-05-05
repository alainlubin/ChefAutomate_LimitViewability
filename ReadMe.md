### Summary: Modify the A2 default view to only allow for specific information
 - For this exercise, we will limit viewability to only see Compliance (CISO-only view), but it provides the lay of the land on how to customize whatever you want.

### This exercise runs through the following objectives:
  - Become Familiarized with Chef Automate
  - Learn about the new IAM/RBAC capabilities within A2
  - Interact with API requests using Postman 

### Pre-Setup:

Upgrade your Chef Automate instance to use IAM_v2
- ssh to your A2 instance: `ssh ec2-user@someIP -i your_key`
- Upgrade you Chef Automate instance to use IAM_v2: `sudo chef-automate iam upgrade-to-v2`
   <img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/ssh-automate.png" width="450" height="225">
  
If this is a previously used A2 box, you will have to delete all `Legacy` policies.
- `Settings`>`Policies`>click on the 3 dots>`Delete Policy`   
   <img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-delete-legacy-policies.png" width="450" height="225">  
   
#### Setup 

Within A2:
- Create Project:`Settings` > `Projects` > `Create Project` > name: `CISO Project` > `Create Project`  
<img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-projects.png" width="380" height="190">  <img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-projects-create.png" width="380" height="190">    
- Create Team:`Settings`>`Teams`>`Create Team`> name: `Compliance Leadership`> Assign `CISO Project`>`Create Team`  
<img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-teams.png" width="380" height="190">  <img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-settings-teams-create.png" width="380" height="190">    
- Create a new user: `ciso`
- Add user `ciso` to team `leadership`

In order to modify the Roles and Policies via API, we need to create a token:
- Within `Settings`, go to `API tokens` -> `Create` -> Give it an [API_NAME], I'm calling `api-token` for now.
    - Click on the 3 dots to the right of you [API_NAME], and click on `Copy Token`
- Within `Settings`, go to `Policies` -> `Administrator` 
    - `Add Members` -> `Add Members Expressions`:
    - `By Token`, then type the token-id (in my case `api-token`)


Using Postman (or your preferred API Dev tool):
- Download postman: https://www.postman.com/downloads/
- If you are using a local A2 Instance, then go to `Settings` -> `General` -> `uncheck ssl verification`
- In Postman, go to `Headers`, name header `api-token`, and paste the content of the token in `blank`.

Creating a Custom Role:
- `POST` the following to this URL: `https://aut-automate-server/apis/iam/v2/roles`
```
{
  "actions": [
    "compliance:*:get",
    "compliance:*:list"
  ],
  "id": "limited-view",
  "name": "Limited View"
}
```

Creating a Custom Policy:
- `POST` the following to this URL: `https://aut-automate-server/apis/iam/v2/policies`
```
{
  "id": "limited-viewer-policy",
  "name": "Limited View Policy",
  "projects": ["ciso"],
  "statements": [
    {
      "effect": "ALLOW",
      "role": "limited-view",
      "projects": [
        "ciso"
      ]
    }
  ]
}
```

Notice that the Role was called `limited-view` and we are using that role within the new `limited-viewer-policy`

- In Automate, go to policies and select your new policy `limited view`
- `Add members` -> `leadership`

- Edit `ciso` project to limit view

for more information: 
- https://automate.chef.io/docs/iam-v2-guide/
- https://automate.chef.io/docs/api/#operation/UpdateRole