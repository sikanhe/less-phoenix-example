# less-phoenix-example
A take on phoenix project structure (>= 1.3)

We have two apps: 
- `/less` - Business logic with database interactions
- `/less_web` - REST Interface between business logic app and the user 

### `/less`
Inside `/less` app , we seperate modules into contexts(concerns), such as `Auth`, `Billing`,  `Blog` and etc...

```
|____less
| |____lib
| | |____auth
| | | |____auth.ex
| | | |____schemas
| | | | |____organization.ex
| | | | |____session.ex
| | | | |____user.ex
| | |____billing
| | | |____billing.ex
| | | |____schemas
| | | | |____charge.ex
| | | | |____refund.ex
| | |____less.ex
| |____mix.exs
```
Under the root of each context, we have the main module file - for example, an  `auth.ex`  module will live in `/lib/less/auth`, with module name `Less.Auth`. This file has the APIs that interacts with everything that concerns with authentication. so stuff like `create_user` and `change_password` would be defined in this module. 

Then, we have all relevant schemas used in `auth`context under the `/auth/schemas` folder. We discussed earlier that it might be confusing to put the schema modules next to all the interaction modules, so why not have a `/schemas` folder under each context? This way we would know where all the schemas for a particular context live and therefore they won't be confused/mixed in with with the interaction modules. 

### `/less_web`
This is pretty straight forward, basically we just take the stuff in web folder from Phoenix 1.2 and put them inside `/lib/less_web`,

```
|____less_web
| |____lib
| | |____less_web
| | | |____controllers/
| | | |____templates/
| | | |____views/
| | | |____endpoint.ex
| | | |____router.ex
| | |____less_web.ex
| |____mix.exs
```

Inside the `/lib`  we have the main module `less_web.ex` file that is responsible for grouping imports and macros - so we can do stuff like `use Less.Web, :controller`. 

Inside `/lib/less_web` we have your familar rest folders `/controllers`, `/views`,  and `/templates`, and we also have the `router.ex` and `endpoint.ex` files for routes and REST API entry point. 

### Further Possible Seperation for `Web`
We could also have seperate `web` app for admin and user-facing parts. Although I am not so sure about this because there is going to be a lot of logic(esp. view files) shared between admin and user-facing api. So maybe just having folders inside `/less_web`might be enough to seperate them conceptually.

```
|__apps
| | |___less
| | |___less_web_user
| | |___less_web_admin
```