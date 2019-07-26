# pretty-simple-autostextarea

## [Demo](https://codesandbox.io/s/pretty-simple-autostextarea-01xdc)

## Props
| Name                  | Description                                                                                       |
|---                    |---	                                                                                              |
| parentMessage         | Transfered text to initialize value. This must equal to data binded v-model directive. Required.  |
| minRow                | default height, default: 1                                                                        |
| maxRow                | Not being displayed scrollbar below maxRow, default: 5                                            |
| width                 | Available units: % and px, default: '100%'                                                        |
| placeholder           | placeholder text. default: ''                                                                     |

## example
``
<AutosizeTextarea
:parentMessage="textValue"
v-model="textValue" :maxRow="3"/>
``
