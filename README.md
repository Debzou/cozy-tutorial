# :whale: cozy-tutorial

## :pushpin: summary

- [Cozy-konnector](https://github.com/Debzou/cozy-tutorial#space_invader-Cozy-konnector)
  - [General](https://github.com/Debzou/cozy-tutorial#General)
  - [Create konnector](https://github.com/Debzou/cozy-tutorial#Create-konnector)
  - [Authenticate](https://github.com/Debzou/cozy-tutorial#Authenticate)
  - [Save data](https://github.com/Debzou/cozy-tutorial#Save-data)
  - [Launch a konnector](https://github.com/Debzou/cozy-tutorial#Launch-a-konnector)
  - [Deploy a konnector](https://github.com/Debzou/cozy-tutorial#Deploy-a-konnector)
- [CouchDB](https://github.com/Debzou/cozy-tutorial#space_invader-CouchDB)
  - general
  - POST data without konnector
- cozy
  - lauch container (version simple)
  - lauch conatainer with volumes
  - add an application in cozy ( react and natif )
  - gather data
 
## :space_invader: Cozy-konnector

#### General

The script for your connector can be found in src/index.js. You can delete the file and create it from scratch. Here you will find the link to everything about cozy-konnector-libs functions: https://github.com/konnectors/libs/blob/master/packages/cozy-konnector-libs/docs/api.md

create a konnector-dev-config.json at the root of the project 
example :
```json
{
    "COZY_URL": "http://cozy.tools:8080",
    "fields": {
      "login": "",
      "password": ""
    }
 }
 
```

install package :
```sh
yarn install
```
if you want get login and password just go to index.js and call field.login and field.password

#### Create konnector
template cozy-konnector :
https://github.com/konnectors/cozy-konnector-template 

```sh
git clone https://github.com/konnectors/cozy-konnector-template cozy-konnector-newservice
cd cozy-konnector-newservice
rm -rf .git
git init
yarn install # or npm install
```


#### Authenticate

An example is given on my github: https://github.com/Debzou/cozy-konnector-750g/blob/master/src/index.js

if you want to identify yourself, it is preferable to use the request-promise. 
```js
async function authenticate(fields) {
  const authRequest = {
    method: 'POST',
    uri: `${baseurl}/login_check`,
    jar: cookiejar,
    headers: {
      Host: 'www.750g.com',
      'Content-Type': 'application/x-www-form-urlencoded'
    },
    form: {
      email: fields.login,
      password: fields.password,
      redirect_url: '',
      client_id: ''
    },
    followAllRedirects: true
  }
  // request
  const authRequestLength = Buffer.byteLength(qs.stringify(authRequest.form))
  authRequest.headers['Content-Length'] = authRequestLength
  return rp(authRequest)
    .catch(() => {
      throw new Error(errors.LOGIN_FAILED)
    })
    .then(html => getName(html))
}
```

To fill in option of request-pomise information you just have to open a developer tool and look in the network part. 


#### Save data

doctype 

```js
async function storeData(documents) {
  hydrateAndFilter(documents, 'io.cozy.namedoctype', {
    keys: ['recipes']
  }).then(filteredDocuments => addData(filteredDocuments, 'namedoctype'))
}
```
:warning: When you use dev mode, you have to add a permission in ./manifest.konnector 

your connector is asking the cozy for permission to create and modify the doctype

```js
"permissions": {
    "permissionname":{
      "type":"namedoctype"
    },
    "otherpermssion":{
    }
}
```

#### Launch a konnector
###### mode alone
Tested your Konnector without cozy
```sh
yarn standalone
```
It can be handy to run a konnector without inserting the data in a cozy.
Your data appear in Data/importedData.json

###### mode dev
Your konnector is linked with your cozy

:warning: Remove the token for other permission test

```sh
yarn dev
```

This command will register your konnector as an OAuth application to the cozy-stack and then set the COZY_CREDENTIALS and COZY_FIELDS environment variable. By default, the cozy-stack is expected to run at http://cozy.tools:8080. If it's is not your case, update the COZY_URL field in /konnector-dev-config.json.

Your browser will open to ask for permission to modify your data on the cozy server.

```sh
curl -X GET http://127.0.0.1:5984/_all_dbs
```

Doctype should be appear in the list

#### Deploy a konnector

The package.json file from cozy-konnector-template gives you the commands to do this : yarn build and yarn deploy but the last one needs to be configured in package.json.


Changed the configuration of package.json.

Remplace $npm_package_repository_url such as :
```json
"deploy": "git-directory-deploy --directory build/ --branch ${DEPLOY_BRANCH:-build} --repo=${DEPLOY_REPOSITORY:-https://github.com/YourGithub.git}",
```


## :space_invader: CouchDB

Official documentation : https://docs.couchdb.org/en/stable/intro/curl.html

Gui interface : http://127.0.0.1:5984/_utils/ 

# brouillon

not working in localhost

.......
:octocat: not yet :octocat:
.......

#### more information
https://docs.cozy.io/en/tutorials/konnector/


 
 #### couchdb

si le nom d'une database contient un / remplace par %2F
 
 
 
 


