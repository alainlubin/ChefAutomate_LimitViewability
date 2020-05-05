### Default view:
My current A2 instance has 10 targets reporting their CIS_level_1 compliance:
    - 5 Rhel7 
    - 5 Win2016
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-defaultview1.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-defaultview2.png" width="380" height="190"></kbd>   
Real environments could have 100s or 1000s of nodes reporting back their compliance information.  
Certain Teams might only be interested in seeing specific prod-level data.   
  
We will be using the `Environment` data as a filter.  
Since there is no `prod` environments in my current instance, we will use `dev-rhel`.  


### Filtering data to your Project:
1. Access CISO Project Rules: `Settings`>`Projects`>`CISO Project`>`Create Rule`
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-projects-accesscisoproject.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-projects-accessrulecreation.png" width="380" height="190"></kbd>  
2. Modify Rules: `name: Production Machines`>`Resource Type: Node`>`Conditions: Environment=dev-rhel`>`Save Rule`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-projects-saverule.png" width="450" height="270"></kbd>
3. Update Project: `Update Project` (This will enable the new changes to take effect)  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-projects-updateproject.png" width="450" height="270"></kbd>
4. Select CISO Project: `All projects`>`Checkmark: CISO Project`>`Apply Changes`  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-filterbyproject.png" width="700" height="200"></kbd>

- Filtered Project View: We are now filtering based on the `dev-rhel` environment so we only see 5 nodes:  
<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-filteredview1.png" width="380" height="190"></kbd>→<kbd><img src="https://raw.githubusercontent.com/danf425/ChefAutomate_LimitViewability/master/images/a2-filteredview2.png" width="380" height="190"></kbd>  


### Takeaways:
- You should now know how to filter Projects based on rules
- This was a simplistic example, but you can use this logic to shape your A2 Projecs
    - A Project can have several rules
    - A Rule can have several conditions
- Project view is great, but [next we need to limit access so that users only see this view](./A2_api.md)