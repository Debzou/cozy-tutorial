# :whale: cozy-tutorial

## :pushpin: summary

- cozy-konnector
  - create konnector
  - general
  - authenticate
  - save data
- cozy
  - lauch container
  - couchdb and view data
- add an application in cozy
 
## :link: cozy-konnector
#### create konnector
template cozy-konnector :
https://github.com/konnectors/cozy-konnector-template 

```sh
git clone https://github.com/konnectors/cozy-konnector-template cozy-konnector-newservice
cd cozy-konnector-newservice
rm -rf .git
git init
yarn install # or npm install
```
#### general

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
if you want get login and password just go to index.js and call field.login and field.password

#### authenticate

if you want to identify yourself, it is preferable to use request-promise. 
An example is given on my github: https://github.com/Debzou/cozy-konnector-750g/blob/master/src/index.js
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

To fill in the request-pomise information you just have to open a developer tool and look in the network part. 

#### save data

save your data in a doctype. 

```js
```


 
 
 
 
 


