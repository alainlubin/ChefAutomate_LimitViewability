The road so far:
- We have upgraded Chef Automate to API_v2
- We have created a new team, a new user, and a project
    - The `compliance-leadership` team gets the `ciso-project` view
    - The `ciso` user is part of `compliance-leadership` team
    - If a new a user needs this view, then we can just add them to the same team.
- We have used Postman to interact with the A2 API 
    - Familiarized ourselves w/ API Dev tools
    - Utilzied API token for GET and POST requests
    - Created custom Policies and custom Roles


### Attaching the Team to your new Policy
1. Access your new policy: `Settings`>`Policies`>`Limited View Policy`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-newpolicies.png" width="450" height="225"></kbd>   
2. Add a team to the policy: `Members`>`Add Members`>`checkmark: compliance-leadership`>`Add Member`
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-newpolicy-member.png" width="250" height="120"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-newpolicy-addmember.png" width="250" height="120"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-members-addcompliance.png" width="250" height="120"></kbd>  


### Let's checkout our final view:
- Login to A2 as `ciso`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-ciso-user.png" width="200" height="200"></kbd>
- Final view only consists of `CISO Project` and the `Compliance` tab  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-cisoview.png" width="700" height="350"></kbd>