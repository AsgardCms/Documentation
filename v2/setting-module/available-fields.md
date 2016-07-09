title: Available fields
subtitle: Setting Module
-------

- [Available fields](#available-fields)

## <a name="available-fields" class="anchor" href="#available-fields">Available fields</a>

The setting module has the basic input fields available for you. These fields are available both for translatable fields as plain fields.

- input type text

    ``` .language-markup
    text
    ```
- input checkbox

  ``` .language-markup
  checkbox
  ```
- textarea

  ``` .language-markup
  textarea
  ```
- input radio

  ``` .language-markup
  radio
  ```
  The Radio field needs an additional `options` key with the wanted options. For instance:
  
  ``` .language-php
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

  ``` .language-markup
  number
  ```
  
