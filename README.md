# pretty-simple-autostextarea

## [Demo](https://codesandbox.io/s/pretty-simple-autostextarea-hyo4c) 
&nbsp;


## Description

| Name  | Description   |
|--|--|
| parentMessage  | String from parent. This initializes default value of textarea. This must equal to data binded v-model directive. <br> Required.  |
| placeholder  | placeholder text. <br> default: ''|
| width | Available units: % and px. <br> default: '100%' |
| minRow | If autosize is defined as True or Object, minRow initializes number of rows not being displayed scrollbar. If not, minRow initializes 'rows' of usual textarea. <br> default: 5 |
| autosize | Defined as Boolean or Object, can expand its rows from minRow to maxRow(which is attribute of autosize Object). <br> Defined as true, default value of maxRow is minRow + 5. <br>default: false |
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
If autosize defined as true without specific value like following,
```
<SimpleTextarea
	:parentMessage="textValue"
	v-model="textValue"	
	:minRow="3"
	autosize />
```
8 is assigned to maxRow according to the internal rule, minRow + 5
