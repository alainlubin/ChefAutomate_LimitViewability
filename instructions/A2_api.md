In order to give custom access to the `Compliance Leadership` team, we need to modify Roles and Policies.  
This requires to be done through the A2 API.  

For this portion, I will be using postman. That said, you can use whatever your preferred API Dev Tool is.  

### Create and Copy Chef Automate Token
1. Create A2 Token: `Settings`>`API Tokens`>`Create Token`>  
                    `name: Limit View`+`policies: Administrator`+`projects: (unassigned)`>`Create Token`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-createtoken.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-createtoken2.png" width="380" height="190"></kbd>   
2. Copy Token: Next to `Limit View` click on the 3 dots > `Copy Token`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-copytoken.png" width="600" height="200"></kbd>  
  
  
  
### Creating Roles and Policies through the A2 API + Postman:
0. Optional: 
  - Checkout A2 API docs:  
  - If you are using a local A2 box, then in Postman:`Settings`>`General`>`uncheck SSL cert verification`  
1. Test Connectivity:   
    - Set Request: `Request: GET` > `URL: your_a2_url/api/iam/v2/roles`  
    - Set Headers: `Headers`>`key=api-token`>`value=paste_your_token_here`  
    - Press `Send`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/postman-testconnection.png" width="600" height="200"></kbd>  
    - You should get a `Response` that looks similar to:  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/postman-getresponse.png" width="400" height="200"></kbd>  

2. Create Role:  
    - Set Request to `POST` > `URL: your_a2_url/apis/iam/v2/roles`  
    - Set your changes: `Body` > `raw` > Paste the following: (Get more info on API: https://automate.chef.io/docs/api/)
    ```
    {
      "actions": [
        "compliance:*:get",
        "compliance:*:list"
      ],
      "id": "limited-view-role",
      "name": "Limited View Role"
    }
    ```
    - Press `Send`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/postman-api-createrole.png" width="480" height="210"></kbd>  

3. Create Policies:  
    - Set Request to `POST` > `URL: your_a2_url/apis/iam/v2/policies`  
    - Set your changes: `Body` > `raw` > Paste the following: (Get more info on API: https://automate.chef.io/docs/api/)
    ```
    {
      "id": "limited-viewer-policy",
      "name": "Limited View Policy",
      "projects": ["ciso-project"],
      "statements": [
        {
          "effect": "ALLOW",
          "role": "limited-view-role",
          "projects": [
            "ciso-project"
          ]
        }
      ]
    }
    ```
    - Press `Send`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/postman-api-createpolicy.png" width="400" height="225"></kbd>  

- Note: we use `limited-view-role` and reference the `ciso-project` we created earlier in the new Policy
- You can see these now appear within A2





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