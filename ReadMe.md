### Summary: Modify the A2 default view to only allow for specific information
 - For this exercise, we will limit viewability to only see Compliance (CISO-only view), but it provides the lay of the land on how to customize whatever you want.

### This exercise runs through the following objectives:
  - Become Familiarized with Chef Automate
  - Learn about the new IAM/RBAC capabilities within A2
  - Interact with API requests using Postman 

### These instructions will be tackled in x different setups:
1. [Chef Automate Setup](./instructions/A2_setup.md)
2. [Modifying Project View](./instructions/A2_projectview.md)
3. [API connectivity](./instructions/A2_api.md)
4. [Final A2 Setup](.instructions//A2_finalsetup.md)
  
  
Result:  
- Default View → Compliance Only View  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-defaultview.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-cisoview.png" width="380" height="190"></kbd>  

For more information on the A2 API, please go to: 
- https://automate.chef.io/docs/iam-v2-guide/
- https://automate.chef.io/docs/api/#operation/UpdateRole