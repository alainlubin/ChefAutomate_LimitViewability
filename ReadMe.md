####Warm up:

Upgrade your Chef Automate instance to use IAM_v2
- ssh to your A2 instance: `ssh ec2-user@someIP -i your_key`
- Upgrade you Chef Automate instance to use IAM_v2: `sudo chef-automate iam upgrade-to-v2`

Within the A2 Dashboard:
- Go to Settings -> Policies -> Manually delete all Legacy policies


- Create a project called `CISO project`
- Create a new team: `leadership`, that is attached to `CISO project`
- Create a new user: `ciso`
- Add user `ciso` to team `leadership`
- Create a new API token
- Add that API token to the `Administrator` policy. 
    - click on Administrator
    - `Add Members`
    - `Add Members Expressions`
    - By `token`, then type the token-id

In the EMEA Windows Machine
- Download postman 
- uncheck ssl verification on settings
- Add your api-token, to the header

- Create Role. POST the code below to the following URL: `https://aut-automate-server/apis/iam/v2/roles`
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
- Create Policy:POST the code below to the following URL: `https://aut-automate-server/apis/iam/v2/policies`
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

- In Automate, go to policies and select your new policy `limited view`
- `Add members` -> `leadership`

- Edit `ciso` project to limit view

for more information: 
- https://automate.chef.io/docs/iam-v2-guide/
- https://automate.chef.io/docs/api/#operation/UpdateRole