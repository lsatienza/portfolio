<body>

# <hg>Project Setup</hg>
<hg>_________________________________________________________________________________________________________________________</hg>


## I. Installation

### &emsp; *A. React Installation*
1. Initialize React Project
   - <o> npm init -y
2. Install create-next-app
   - <o>npm install create-next-app@latest</o>
3. Create project with create-next-app 
   - <o>npx create-next-app@latest frontend</o>

### &emsp; [*B. Formatting*](https://dev.to/ivadyhabimana/setup-eslint-prettier-and-husky-in-a-node-project-a-step-by-step-guide-946)
1. <b> ESLint </b>
   + Configure ESLint to use AirBNB Style Guide
     + <o>npm init @eslint/config</o>
2. <b>Prettier</b>
   + Install Prettier
     + <o>npm install --save-dev --save-exact prettier</o>
   + Configure Prettier
     + create <aq>.prettierrc.json</aq> file
      ```
      {
         "tabWidth": 2,
         "useTabs": true,
         "printWidth": 80,
         "semi": true,
         "trailingComma": "es5",
         "singleQuote": true,
         "endOfLine": "lf"
      }
      ```
3. Integrate Prettier with ESLint
   + Integrate
     + <o>npm install --save-dev eslint-config-prettier</o>
   + Configure <aq>.eslintrc.json</aq>
   ```
   {
      "env": {
         "browser": true,
         "es2021": true
      },
      "extends": ["plugin:prettier/recommended", "google"],
      "parserOptions": {
         "ecmaFeatures": {
            "jsx": true
         },
         "ecmaVersion": "latest",
         "sourceType": "module"
      },
      "plugins": ["react"],
      "rules": {
      }
   }   
   ```
4. Configure Scripts
   + Configure package.json
   ```
   "scripts": {
                ... // other scripts you have
        "lint": "eslint . --fix --max-warnings=0",
        "format": "prettier . --write"
    },
   ```
5. <b>Husky</b>
   + Install lint-staged
     + <o>npx mrm@2 lint-staged</o>
   + Validate that the following code is in package.json
   ```
   "lint-staged": {
        "*.js": "eslint --fix ",
        "*.{js,css,md,html,json}": "prettier --cache --write"
   }
   ```
### &emsp; *C. Docker*
1. Install Docker
2. Create <aq>**Dockerfile.dev**</aq>
   + Configure file
   ```
   FROM node:20-alpine

   WORKDIR /frontend
   COPY package.json .

   RUN npm install

   COPY . .

   CMD ['npm','run','dev']
   ```
3. Create <aq>**Dockerfile.prod**</aq>
   + Configure file
   ```
   FROM node:20-alpine AS build

   WORKDIR /frontend
   COPY package.json .

   RUN npm install

   COPY . .

   RUN npm run build 
   ```
   > FROM nginx
   >
   > COPY --from=build /frontend/build /usr/share/nginx/html
4. Create <aq>**.dockerignore**</aq> file
   ```
   .git
   .vscode
   .dockerignore
   .gitignore
   .env
   config
   build
   node_modules
   docker-compose.yaml
   docker-compose.dev.yaml
   docker-compose.prod.yaml
   Dockerfile
   Dockerfile.dev
   Dockerfile.prod
   README.md
   ```
5. Create <aq>**docker-compose.yaml**</aq> file at the root
   ```
   version: '1.0'
   services:
      frontend:
         build:
            context: ./frontend
   ```
6. Create <aq>**docker-compose.dev.yaml**</aq> file at the root
   ```
   version: '1.0'
   services:
      frontend:
         image: frontend-dev-i
         build:
            dockerfile: Dockerfile.dev
         container_name: frontend-dev-c
         volumes:
            - ./frontend:/frontend
            - node_modules:/frontend/node_modules/
         ports:
            - '8080:8080'
         environment:
            - NODE_ENV=development
   volumes:
      node_modules:
   ```
7. Create <aq>**docker-compose.prod.yaml**</aq> file at the root
   ```
   version: '1.0'
   services:
      frontend:
         image: frontend-prod-i
         build:
            dockerfile: Dockerfile.prod
         container_name: frontend-prod-c
         volumes:
            - ./frontend:/frontend
            - node_modules:/frontend/node_modules/
         ports:
            - '8080:80'
         environment:
            - NODE_ENV=production
   volumes:
      node_modules
   ```
8. Create **bin** folder then <aq>*deploy.sh*</aq> file
   ```
   #!/bin/bash
   if [[$1 = 'prod' || $1 = 'dev']] && [[$2 = 'down' || $2 = 'up']] then
      cd ..
      fileEnv='docker-compose.${1}.yaml'
      downOrUp=$2
      echo 'Running docker-compose -f docker-compose.yaml -f $fileEnv $downOrUp'
      docker-compose -f docker-compose.yaml -f $fileEnv $downOrUp
   else
      echo 'Need to follow format. ./deploy.sh prod|dev down|up'
   fi
   ```
### &emsp; *D. Styling*
1. <b>[MUI](https://mui.com/material-ui/getting-started/installation/)</b>
   + Default Installation
     + <o>npm install @mui/material @emotion/react @emotion/styled</o>
   + Icons
     + <o>npm install @mui/icons-material</o>
</body>
<style>
   aq    { color: #7FFFD4 }
   b     { color: #89CFF0 }
   hg    { color: #F0FFF0 }   
   pg    { color: #00A550 }
   o     { color: #FFBF00 }
   body  { color: #F0FFF0 }
</style>
