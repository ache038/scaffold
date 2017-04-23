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
├── config                         # Define global configuration information
├── tests                          # Testing folder for unit testing
├── src                            # Source code of JavaScript
│   ├── redux
│   │   ├── actions                # Redux action source file
│   │   ├── models                 # redux-orm model source file
│   │   ├── epics                  # Epics of RxJS
│   │   ├── reducers               # Redux reducer source file
│   ├── core
│   │   ├── createStore.js         # Create Store file
│   │   ├── orm.js                 # redux-orm Model Manager ( Complex to connect to models )
│   │   ├── routes.js              # React-Router management.
│   ├── layout                     # Layout source file if needed.
│   │   ├── <LayoutName>           # Folder for layout definition, start with Upper case
│   │   │   ├── header             # The header of layout
│   │   │   ├── footer             # The footer of layout
│   │   │   ├── nav                # The navigator of layout
│   │   │   ├── aside/menu         # The aside/menu of layout
│   │   ├── ......
│   ├── components                 # React-Redux business module components.
│   │   ├── <ModuleName>           # Folder for all components.
│   │   │   ├── index.js           # UI Component JS file
│   │   │   ├── index.css          # Css files.
│   │   │   ├── vector.js          # State to props JS file
│   │   │   ├── dispatch.js        # Dispatch to props JS file
│   │   │   ├── ui.event.js        # Define event function that's related to UI
│   │   │   ├── controls           # Sub Component JS folder.
│   ├── shared
│   │   ├── <SharedName>           # Shared Components Name
│   │   ├── index.js               # Entry Js File
│   │   ├── package.json           # Private package using
│   ├── tool
│   │   ├── <FetureFolder>         # Feture Folder for different using.
│   │   ├── index.js               # Entry Js File
│   │   ├── package.json           # Private package using
```

## 2. Discussion Rules

* Packaged locally for shared/tool.
* All prop came from state tree named start with `rdx`；（rdx -&gt; redux）
* All prop came from parent named start with `rt`；（rt -&gt; react）
* All function start with `fn`；
* Each module contains following Js source file
  * vector.js——Define state to props, apply `reselect` library in future.
  * dispatch.js——Define dispatch to props.
  * ui.event.js——Define event function that related to ui.
  * index.js——Component JS, enable `prop-type` in development environment, apply DisplayName attribute to each component.
* redux-orm function name with lifecycle phase
  * Service Layer——fnInit、fnCreate、fnModify、fnGet、fnGetList、fnRemove
  * Orm Model——fnInsert、fnUpdate、fnSelect、fnDelete
  * Only one phase, Service Layer is high priority
* Variable name in component
  * event——Ui Event functions
  * dispatcher——Dispatcher functions
  * vector——State to Props files
* Html Element id names
  * Form start with `fm`
  * List start with `lst`
  * Aside start with `asd`
  * Button start with `btn`
* Field Element id names
  * Textbox/Textarea `txt`
  * Label `lbl`
  * Dropdown `ddl`
  * Checkbox `chk`
  * Radio `rdo`
  * Table `dt`
  * Row `dr`
  * Cell `dd`
* 




