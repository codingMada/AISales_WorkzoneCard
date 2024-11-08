# Getting Started

to use this repository and deploy your own UI intergration card via Work Zone content package follow this step by step guide.

## How to deploy a Work Zone content package

### 1. Step
import this repository into your Business Application Studio or create a new content package via the wizzard. 

![jens_kristen_3-1706792305879](https://github.com/user-attachments/assets/d8f66c00-7367-43bd-b459-84448d6b64d7)

important is to include content samples.

![Screenshot2](https://github.com/user-attachments/assets/e7357de6-0935-4746-bff8-db2fcf61e391)

### 2. Step create the nessesary content (only if you created your own content package with the wizzard)

first open the **manifest.json** and set an id (max length 20), a title and a subtitle.
```json
{
	"sap.package": {
		"id": "<your ID>",
		"packageVersion": {
			"version": "1.0.0",
			"upgradeNotification": "all"
		},
		"i18n": "i18n/i18n.properties",
		"icon": "sap-icon://accept",
		"title": "<your Title>",
		"subTitle": "<your subtitle>",
		"shortTitle": "",
...
```
next you have to open the **content.json** and insert the code below. 
This code creates the nessesary role, workpage, space and the ui integration card.
```json
{"sample-role": {
    "type": "role",
    "src": {
      "from": "./internalsamples/src",
      "content": "role.json"
    }
  },
  "sample-space": {
    "type": "space",
    "src": {
      "from": "./internalsamples/src",
      "content": "space.json"
    }
  },
  "sample-workpage": {
    "type": "workpage",
    "src": {
      "from": "./internalsamples/src",
      "content": "workpage.json"
    }
  },
    "card-sample": {
        "type": "card",
        "src": {
            "from": "./internalsamples/card",
            "path": "./",
            "build": "",
            "package": "sap-workzone-cpkg-card-sample.zip",
            "manifest": "src/manifest.json"
        }
    }
}
```
After that add a new folder in the project folder **internalsample** and name it **src**. 
Into that folder create three new files with the following content:
- role.json
- workpage.json
- space.json

Sample code for role.json:
```json
{
    "_version": "3.2.0",
    "identification": {
      "id": "my.company.ns.contentpackage.role1",
      "title": "ContentPackageRole",
      "entityType": "role"
    },
    "payload": {
      "spaces": [
        {
          "id": "my.company.ns.contentpackage.space"
        }
      ],
      "apps": [
        {
          "id": "sap.workzone.cpkg.card.sample.app"
        }
      ]
    }
  }
```

Sample code for workpage.json:
```json
{
    "_version": "3.2.0",
    "identification": {
      "id": "my.company.ns.contentpackage.workpage",
      "entityType": "workpage"
    },
    "payload": {
      "workpageConfig": {
        "title": "My Workpage"
      },
      "rows": [
        {
          "id": "row-1",
          "rowConfig": {},
          "columns": [
            {
              "id": "col-11",
              "columnConfig": {},
              "cells": [
                {
                  "id": "cell-111",
                  "cellConfig": {},
                  "widgets": [
                    {
                      "id": "widg-1111",
                      "viz": {
                        "appId": "sap.workzone.cpkg.card.sample.app",
                        "vizId": "sap.workzone.cpkg.card.sample.viz"
                      }
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    }
  }
```

Sample code for space.json:
```json
{
    "_version": "3.1.0",
    "identification": {
      "id": "my.company.ns.contentpackage.space",
      "title": "MySpace",
      "entityType": "space"
    },
    "payload": {
      "contentNodes": [
        {
          "type": "workpage",
          "id": "my.company.ns.contentpackage.workpage"
        }
      ]
    }
  }
```

### 3. Step
Right click on the **manifest.json** and package the package.

![jens_kristen_6-1706792306099](https://github.com/user-attachments/assets/5c476eb0-7e4c-4cdb-8bcb-c2bcd6450ec2)

after you created the .zip file, right click it and download it.

### 4. Step
the next step is to import the .zip into your work zone.
Go to the content channels and create a new one.

![jens_kristen_8-1706792305832](https://github.com/user-attachments/assets/a635d9d7-1895-4fe2-9295-8c8e68b31b38)

### 5. Step 
to see your new deployed content package you have to give your user the newly created role on the BTP and edit the work zone site. 

![jens_kristen_12-1706792306199](https://github.com/user-attachments/assets/168a0752-6631-4b79-8173-b3f9c5c1ced5)

![jens_kristen_14-1706792306271](https://github.com/user-attachments/assets/23aaec63-9e98-4e6a-9517-7bfbbdf4da53)

### 6. Step 
after all the steps above you can now look at your created ui integration card:

<img width="200" alt="jens_kristen_0-1707137095475" src="https://github.com/user-attachments/assets/9c77641d-c21e-49b9-b03e-20eb1a3837bd">

if you need help with one of the steps above contact Niklas Ennser

## How to edit the UI intergration Card

if you want to edit or create your own UI integration Card, you can edit the manifest file by right clicking it and opening the editor.

![Picture-7](https://github.com/user-attachments/assets/22983b17-15c6-43db-804f-27b89dbcfb11)

by choosing preview, you can see the current version of your card. 
Here is a list with all the available UI Card types:
https://sapui5.hana.ondemand.com/test-resources/sap/ui/integration/demokit/cardExplorer/webapp/index.html#/exploreOverview/typesDeclarative 
Note that not every card type can use the manifest editor. 
