# Typescript path aliases

before
```ts
import AuthService from '../../../../auth.service'
```

after

```ts
import AuthService from '@services/auth.service'
```
---

Install packages

```shell
npm i -D tsconfig-paths module-alias
```

Configure `tsconfig.json`

```jsonc
{
  // add this for register ts paths 
  "ts-node": {
    "require": ["tsconfig-paths/register"]
  },
  
  "compilerOptions": {
    // define root and out dirs
    "rootDir": "./src",
    "outDir": "./lib",
    
    // ...

    // define base path for paths
    "baseUrl": "./src",
    // define paths
    "paths": {
      // do not fogot add to end '/*'
      "@modules/*": ["./modules/*"],
      "@services/*": ["./services/*"],
    }
  },
  // include all files from src
  "include": ["src/**/*"]
}
```

Configure `package.json`

add directories
```jsonc
"directories": {
    "lib": "lib"
}
```

run script with register aliases for js

run option `-r module-alias/register` register all paths before start app 

```jsonc
"scripts": {
    // for single start
    "start": "node -r module-alias/register ./lib/main.js",
    // for demonize
    "start:d": "nodemon -r module-alias/register ./lib/main.js",
    // for development
    "dev": "nodemon src/main.ts"
}
```

add aliases for js files

```jsonc
// ! '/*' not needed here 
"_moduleAliases": {
    "@modules": "lib/modules",
    "@services": "lib/services"
}
```

## Run

```
tsc
npm start
```