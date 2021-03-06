# pretty-simple-autostextarea

## [Demo](https://codesandbox.io/s/github/jnh0222/pretty-simple-autostextarea/tree/master)
&nbsp;


## Description

| Name  | Description   |
|--|--|
| parentMessage  | String from parent. This initializes default value of textarea. This must equal to data binded v-model directive. <br> **Required**.  |
| placeholder  | placeholder text. <br> default: ''|
| width | Available units: % and px. <br> default: '100%' |
| minRow | This means 'rows' of usual textarea. <br> default: 5 |
| autosize | Defined as just 'true'(without any specific value), the textarea will be expanded infinitely.<br> Defined as Object, it can expand its rows from minRow to maxRow(which is attribute of autosize Object).<br>default: false |
| simpleTextareaClass | custom class name. |



## Example                                                                                                                                                                                                    

### default
```
<SimpleTextarea
	:parentMessage="textValue"
	v-model="textValue"/>
```
&nbsp;
&nbsp;


### autosize - Object
Following textarea can expand from 3 to 10 rows. \
over 10, displays scrollbar.
```
<SimpleTextarea
	:parentMessage="textValue"
	v-model="textValue"
	placeholder="Insert the text."
	width="250px"
	:minRow="3"
	:autosize="{'maxRow': 10}"
  simpleTextareaClass="simple-class"/>
```
&nbsp;
&nbsp;


### autosize - Boolean
If autosize defined as true without specific value like following, \
the textarea will be expanded infinitely.
```
<SimpleTextarea
	:parentMessage="textValue"
	v-model="textValue"	
	:minRow="3"
	autosize />
```
