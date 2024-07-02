# micro-frontends

Create workspace:
$ npx create-nx-workspace matchmaker

Generate host:
$ npx nx generate @nx/angular:host --name=host --ssr=true --directory=apps/host --prefix=matchmaker --dynamic=true --projectNameAndRootFormat=as-provided --standalone=false --style=scss

Generate remote:
$ npx nx generate @nx/angular:remote --name=[naam van remote] --host=host --directory=apps/[naam van remote] --port=[port nummer] --prefix=matchmaker —projectNameAndRootFormat=as-provided --ssr=true --standalone=false --style=scss 

Generate component in remote:
$ npx nx generate @nx/angular:component --name=[naam van component] --directory=apps/[naam van remote project]/src/app/remote-entry/[gegeven naam van component] --standalone=false --prefix=matchmaker --style=scss 

Generate shared library
$ npx nx g @nx/angular:lib libs/shared/data-access-[naam van library dat gedeeld wordt]

Generate shared service
 $ npx nx g @nx/angular:service [naam van service] --project=data-access-[naam van library dat gedeeld wordt]  --standalone=false
