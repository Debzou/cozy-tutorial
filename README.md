# :whale: cozy-tutorial

## :pushpin: summary

- cozy-konnector
  - create konnector
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

```{bash}
git clone https://github.com/konnectors/cozy-konnector-template.git
cd cozy-konnector-template
yarn standalone
```
The script for your connector can be found in src/index.js. You can delete the file and create it from scratch. Here you will find the link to everything about cozy-konnector-libs functions: https://github.com/konnectors/libs/blob/master/packages/cozy-konnector-libs/docs/api.md

#### authenticate

if you want to identify yourself, it is preferable to use request-promise. An example is given on my github: https://github.com/Debzou/cozy-konnector-750g/blob/master/src/index.js 
To fill in the request-pomise information you just have to open a developer tool and look in the network part. 

#### save data
###### save data in a doctype


 
 
 
 
 


