# less-phoenix-example
A take on phoenix project structure (>= 1.3)

We have two apps: 
- `/less` - Business logic with database interactions
- `/less_web` - REST Interface between business logic app and the user 

### Less
Inside `less`  app folder, we seperate modules into contexts(concerns), such as Auth, Billing,  Blog and etc.. . Under each of these context, we have the main module file, which is the same name as the folder (ie `auth.ex` for Auth context), which has the API that interacts with everything in that concern. Then we have all relevant schemas used in this context under the `/schemas` folder so we know where all the schmas live and therefore won't be confused/mixed in with with the interaction modules. 

### Less.Web
Inside the `less_web`  app folder we have the main `less_web.ex` file that is responsible for grouping imports and macros (example: `use Less.Web, :controller`). Then inside lib we have your typical rest folders `/controllers`, `/views`,  and `/templates`, and we also have the `router.ex` and `endpoint.ex` files for routes and REST API entry point. 

### Possible Seperation
We could also have seperate web api app for admin and user-facing app. Although I am not so sure about this because there is going to be a lot of logic(esp. view files) shared between admin and user-facing api. So having folders inside /less_web might be enough to seperate them conceptually.

- `less_web_user` - User-facing api/frontend
- `less_web_admin` - Admin-only api/frontend