# pretty-simple-autostextarea

## [Demo](https://codesandbox.io/s/pretty-simple-autostextarea-hyo4c)

## Props
| Name                  | Description                                                                                       |
|---                    |---	                                                                                              |
| parentMessage         | Transfered text to initialize value. This must equal to data binded v-model directive. Required.  |
| maxRow                | Not being displayed scrollbar below maxRow, default: 5                                            |
| width                 | Available units: % and px, default: '100%'                                                        |
| placeholder           | placeholder text. default: ''                                                                     |

## example
``
<AutosizeTextarea
:parentMessage="textValue"
v-model="textValue" :maxRow="3"/>
``