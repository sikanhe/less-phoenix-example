# less-phoenix-example
A take on phoenix project structure (>= 1.3)

We have two apps: 
- `/less` - Business logic with database interactions
- `/less_web` - REST Interface between business logic app and the user 

### `/less`
Inside `less`  app folder, we seperate modules into contexts(concerns), such as Auth, Billing,  Blog and etc.. . Under the root of each context, we have the main module file - for example, a  `auth.ex` will live in `/auth`, with module name `Less.Auth`. This file has the APIs that interacts with everything in that concern. so stuff like `create_user` and `change_password` functions would be in this module. 

Then, we have all relevant schemas used in this context under the `/schemas` folder. We discussed earlier that it might be confusing to put the schema modules next to all the interaction modules so why not have a `/schemas` folder under each context? This way we would know where all the schemas live and therefore won't be confused/mixed in with with the interaction modules. 

### `/less_web`
This is more straight forward than `/less`.

Inside the `less_web`  app folder we have the main module `less_web.ex` file that is responsible for grouping imports and macros - so we can do stuff like `use Less.Web, :controller`. 

Inside `/lib` we have your familar rest folders `/controllers`, `/views`,  and `/templates`, and we also have the `router.ex` and `endpoint.ex` files for routes and REST API entry point. 

### Further Possible Seperation for `Web`
We could also have seperate `web` app for admin and user-facing parts. Although I am not so sure about this because there is going to be a lot of logic(esp. view files) shared between admin and user-facing api. So maybe just having folders inside `/less_web`might be enough to seperate them conceptually.

Example:
- `less_web_user` - User-facing api/frontend
- `less_web_admin` - Admin-only api/frontend