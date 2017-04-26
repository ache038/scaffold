# React Scaffold

## 1. Project Structure

```
├── public                         # [Static Resources]
│   └── js                         # Local resource of javascript ( Referred directly )
│   └── css                        # User defined css files
│   └── upload                     # Upload folder to hold all files
│   └── img                        # Image files for icon/pictures that used in our system

├── src                            # [Source code]
│   ├── components                 # - [UI Component]
│   │   ├── <Name>                 # Component name folder
│   │   │   ├── Component.css      # Component css style file
│   │   │   ├── Component.js       # React component source code ( Major )
│   │   │   ├── Component.<Sub>.js # React sub component source code ( Do not connect in common )
│   │   │   ├── Redux.Mapping.js   # State -> Props, Dispatch -> Props
│   │   │   ├── Ts.UI.js           # Tradeshift UI Component to render
│   │   ├── index.js               # The entry of each component.

│   ├── container                  # - [UI Container] ( The structure is the same as component )
│   │   ├── index.js               # The entry of each container.

│   ├── data                       # - [Shared data information]
│   │   ├── i18n                   # language resources file.
│   │   │   ├── cn.json            # Chinese Language Supported.
│   │   │   Config.json            # Global configuration data.
│   │   │   Data.js                # [Uniform Interface]
│   │   │   Doc.js                 # Document Text/Status type information
│   │   │   package.json           <package meta>
│   │   │   Routes.js              # Routing table for bind, uniform to manage routes.

│   ├── entry                      # Environment initializing entry
│   │   ├── createStore.js         # Redux store initialize
│   │   ├── routes.js              # React-Router entry initialize.

│   ├── redux                      # - [Redux]
│   │   ├── epics                  # Observable to access remote api folder
│   │   │   ├── index.js           # [Uniform Interface]
│   │   │   ├── urls.js            # Bind epic action to remote URI.
│   │   ├── reducers               # Reducer of redux folder
│   │   │   ├── index.js           # [Uniform Interface]
│   │   │   ├── RemoteReducer.js   # Global Reducer component for writing data to tree store, forceUpdate.
│   │   │   actionTypes.js         # Action types for all redux workflow.

│   ├── ts                         # - [Tradeshift React Component]
│   │   ├── <category>             # Web component category folder.
│   │   │   ├── <TsName>           # Tradeshift component folder, start with "TS".
│   │   ├── index.js               # [Uniform Interface]

│   ├── utils                      # - [Shared Tool]
│   │   ├── ajax                   # Ajax library
│   │   │   ├── Ajax.js            # [Uniform Interface]
│   │   │   ├── Ajax.<Cat>.js      # Secondary categories of this library
│   │   │   ├── package.json       <package meta>
│   │   ├── event                  # UI event library
│   │   ├── kit                    # Common tool library
│   │   ├── index.js               # [Uniform Interface]

├── tests                          # [Testing]

├── tool                           # [Development]
│   ├── code-tpl                   # Code snap to help copy and parse the code template
│   ├── mock-json-server           # Mock Json server for mocking server end

├── tpl                            # [Template File]
│   ├── pdf                        # Html Template Files.
├── lib.js                         # Library connect point -> Data, Ts, Util, (ID function)


```

## 2. Naming

* State -&gt; Props: All the prop name started with underline dash `_`
* Dispatch -&gt; Props: All the dispatch name started with `fn`
* ActionName: Example -&gt; `$$SUC/DOCUMENT/FETCH_LIST`
  * All success redux action start with `$$SUC`
  * All failure redux action start with `$$ERR`
  * The separator character is `/`
  * The first level recommend to be module name
* All the internal used function start with `_`
* Ts.UI.js interface could be mix with `verb + componentName`such as 
  * init：initialize major component
  * initFilter: initialize sub component
* Redux.Mapping.js: Exposed interface should be function with name`connect<Component>`, the main component name is fixed: `connectIndex`.
* Component.js: named Component with static attribute displayName to be distinguish.
  * mapping -&gt; `import mapping from './Redux.Mapping`:Recommend fixed name to connect Redux.Mapping.js
  * ui -&gt; `import ui from './Ts.UI`: Recommend fixed name to connect Tradeshift Component
  * Lib -&gt; `import Lib from '../../lib`: Recommend fixed name to connect our Library.
  * Name -&gt; current component name
  * \_config -&gt; \[Function\] Build some configuration information for component in jsx
  * \_style -&gt; \[Function\] Build some style information for component in jsx.
  * \_options -&gt; \[Function\] Build dropdown options for component.
* All the form html id start with `fm`prefix.

## 3. Code Structure

All the source code file should be divide into different area with the same sequence in each file. If there is no part, we could ignore the comment and code content.

### 3.1. Component.js

```
<Import third part library such as react, react-redux>
// -----------------------------------------------------------
// External Importing
// -----------------------------------------------------------
*: Import the file we defined that is out of our current component folder

// -----------------------------------------------------------
// Internal Importing ( Uniform )
// -----------------------------------------------------------
*: Import the file we defined that is in current component folder such as Ts.UI.js, Redux.Mapping.js. 
For this part, the sub component should be followed by all importing.

// -----------------------------------------------------------
// ID, Name
// -----------------------------------------------------------
*: Constant values such as html id, component name here.
```





