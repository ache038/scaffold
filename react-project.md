# React Scaffold

## 1. Project Structure

```
├── develop                        # Development Tool Folder
│   └── mock-json-server           # Mock Json Web Server for Restful
├── public                         # Static public assets ( Not Js source code )
│   └── js                         # Local resource of javascript ( Referred directly )
│   └── css                        # User defined css files
│   └── upload                     # Upload folder to hold all files
│   └── img                        # Image files for icon/pictures that used in our system
├── tests                          # Testing folder for unit testing
├── src                            # Source code of JavaScript
│   ├── core
│   │   ├── createStore.js         # Create Store file
│   │   ├── orm.js                 # redux-orm Model Manager ( Complex to connect to models )
│   │   ├── routes.js              # React-Router management.
│   ├── layout                     # Layout source file if needed.
│   │   ├── <LayoutName>           # Folder for layout definition, start with Upper case
│   │   ├── ......
│   ├── modules                    # React-Redux business module components.
│   │   ├── <ModuleName>           # Folder for all components.
│   │   │   ├── index.js           # UI Component JS file
│   │   │   ├── index.css          # Css files.
│   │   │   ├── controls           # Sub Component JS folder.
│   ├── shared
│   │   ├── <SharedName>           # Shared Components Name
│   │   ├── index.js               # Entry Js File
│   │   ├── package.json           # Private package using
│   ├── tool
│   │   ├── index.js               # Entry Js File
│   │   ├── package.json           # Private package using
```



