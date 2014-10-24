# Setting module : Available fields


## Available fields


The setting module has the basic input fields available for you. These fields are available both for translatable fields as plain fields.

- input type text

  `text`
- input checkbox

  `checkbox`
- textarea

  `textarea`
- input radio

  `radio`
  The Radio field needs an additionel `options` key with the wanted options. For instance:
  
  ``` php
  'this-is-a-radio' => [
       'description' => 'This is a radio',
       'options' => [
           'option1' => 'Option 1',
           'option2' => 'Option 2',
           'option3' => 'Option 3',
       ],
       'view' => 'radio'
   ],
   ```
- input number

  `number`
  
    
***

[Back to ToC](../readme.md)