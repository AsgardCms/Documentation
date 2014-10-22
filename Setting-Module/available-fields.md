# Setting module : Available fields


## Available fields


The setting module has the basic input fields available for you:

- input type text

  `setting::admin.partials.module-text-field`
- input checkbox

  `setting::admin.partials.module-checkbox-field`
- textarea

  `setting::admin.partials.module-textarea-field`
- input radio

  `setting::admin.partials.module-radio-field`
  The Radio field needs an additionel `options` key with the wanted options. For instance:
  
  ``` php
  'this-is-a-radio' => [
       'description' => 'This is a radio',
       'options' => [
           'option1' => 'Option 1',
           'option2' => 'Option 2',
           'option3' => 'Option 3',
       ],
       'view' => 'setting::admin.partials.module-radio-field'
   ],
   ```
  
***

[Back to ToC](../readme.md)