title: Form Macros
subtitle: Core Module
-------

- [Translatable fields](#translatable-fields)
	- [input](#translatable-input)
	- [textarea](#translatable-textarea)
	- [checkbox](#translatable-checkbox)
	- [select](#translatable-select)
- [Non-translatable fields](#non-translatable-fields)
	- [input](#normal-input)
	- [textarea](#normal-textarea)
	- [checkbox](#normal-checkbox)
	- [select](#normal-select)

In order to avoid writing the same thing over and over, AsgardCms provides you with form macros that help to avoid writing the same code for form fields. This will generate the necessary code working for the **AdminLTE backend theme**.

They exists in two kinds, translatable fields and non translatable fields.

## <a class="anchor" name="translatable-fields" href="#translatable-fields"></a> Translatable fields


### <a class="anchor" name="translatable-input" href="#translatable-input"></a> Translatable Input

This is the method signature:

``` .language-php
Form::macro('i18nInput', function ($name, $title, $errors, $lang, $object = null, array $options = [])
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$lang` is the language of the input,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form::i18nInput('name', 'field title', $errors, $lang) !!} // Create view
{!! Form::i18nInput('name', 'field title', $errors, $lang, $object) !!} // Edit view
```


### <a class="anchor" name="translatable-textarea" href="#translatable-textarea"></a> Translatable Textarea

This is the method signature:

``` .language-php
Form::macro('i18nTextarea', function ($name, $title, $errors, $lang, $object = null, array $options = [])
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$lang` is the language of the input,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form::i18nTextarea('body', 'field title', $errors, $lang) !!} // Create view
{!! Form::i18nTextarea('body', 'field title', $errors, $lang, $object) !!} // Edit view
```


### <a class="anchor" name="translatable-checkbox" href="#translatable-checkbox"></a> Translatable Checkbox

This is the method signature:

``` .language-php
Form::macro('i18nCheckbox', function ($name, $title, $errors, $lang, $object = null)
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$lang` is the language of the input,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form::i18nCheckbox('is_online', 'field title', $errors, $lang) !!} // Create view
{!! Form::i18nCheckbox('is_online', 'field title', $errors, $lang, $object) !!} // Edit view
```

### <a class="anchor" name="translatable-select" href="#translatable-select"></a> Translatable Select

This is the method signature:

``` .language-php
Form::macro('i18nSelect', function ($name, $title, ViewErrorBag $errors, $lang, array $choice, $object = null, array $options = [])
```

- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$lang` is the language of the input,
- `$choice` the possible choices,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form::i18nSelect(‘test’, ‘test’, $errors, $lang, [1,2,3]) !!} // Create view
{!! Form::i18nSelect(‘test’, ‘test’, $errors, $lang, [1,2,3], $object) !!} // Edit view
```


## <a class="anchor" name="non-translatable-fields" href="#non-translatable-fields"></a> Non-translatable fields

These are pretty much identical to the translatable macros, except they don't have a `$lang` argument.

### <a class="anchor" name="normal-input" href="#normal-input"></a> Normal Input

This is the method signature:

``` .language-php
Form::macro('normalInput', function ($name, $title, $errors, $object = null, array $options = [])
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form::normalInput('name', 'field title', $errors) !!} // Create view
{!! Form::normalInput('name', 'field title', $errors, $object) !!} // Edit view
```



### <a class="anchor" name="normal-textarea" href="#normal-textarea"></a> Normal Textarea

This is the method signature:

``` .language-php
Form::macro('normalTextarea', function ($name, $title, $errors, $object = null, array $options = [])
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form:: normalTextarea('body', 'field title', $errors) !!} // Create view
{!! Form:: normalTextarea('body', 'field title', $errors, $object) !!} // Edit view
```



### <a class="anchor" name="normal-checkbox" href="#normal-checkbox"></a> Normal Checkbox

This is the method signature:

``` .language-php
Form::macro('normalCheckbox', function ($name, $title, $errors, $object = null)
```
- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:

``` .language-php
{!! Form:: normalCheckbox('is_online', 'field title', $errors) !!} // Create view
{!! Form:: normalCheckbox('is_online', 'field title', $errors, $object) !!} // Edit view
```

### <a class="anchor" name="normal-select" href="#normal-select"></a> Normal Select

This is the method signature:

``` .language-php
Form::macro('normalSelect', function ($name, $title, ViewErrorBag $errors, array $choice, $object = null, array $options = [])
```

- `$name` is the name of the input (also called on the `$object` if given to fill the input),
- `$title` is used for the place holder and label,
- `$errors` is the errors message bag,
- `$choice` the possible choices,
- `$object` is the object used to fill the input,
- `$options` an array of options that'll be sent to the `Form::input` method.

This will look like the following:


``` .language-php
{!! Form:: normalSelect(‘test’, ‘test’, $errors, [1,2,3]) !!} // Create view
{!! Form:: normalSelect(‘test’, ‘test’, $errors, [1,2,3], $object) !!} // Edit view
```


