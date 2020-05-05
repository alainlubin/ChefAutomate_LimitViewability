### Summary: Modify the A2 default view to only allow for specific information

This exercise runs through a couple objectives:
  - Become Familiarized with Chef Automate
  - Learn about the new IAM/RBAC capabilities within A2
  - Interact with API requests using Postman 

### Warm up:

Upgrade your Chef Automate instance to use IAM_v2
- ssh to your A2 instance: `ssh ec2-user@someIP -i your_key`
- Upgrade you Chef Automate instance to use IAM_v2: `sudo chef-automate iam upgrade-to-v2`
![SSH into A2](/images/ssh-automate.png)
<img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/ssh-automate.png" wdith="200" hight=""400>

Within the A2 Dashboard:
- Go to `Settings` -> `Policies` -> Manually delete all Legacy policies

Setting up the project and view within A2 (For this example we are creating a Compliance only - CISO view):
- Go to `Settings` -> `Project` -> Create a new project called `CISO project`
- Within `Settings` -> `Teams` -> Create a new team: `leadership` and attach the `CISO project` to it.
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