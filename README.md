# OCTOBER CMS IMPROVED FILE UPLOAD FORM WIDGET

A simple extension for the October CMS's FileUpload form widget that lets the addition of user defined rules in the form YAML config files or the models where the field is declared.


## Installation

Manually from your terminal typing:

``` bash
$ composer require patroklo/octobercms-improved-fileupload
```

Or add this to your project's `composer.json` file:

``` json
"patroklo/octobercms-improved-fileupload": "*"
``` 

And it's done!

## New Rules

There are an additional set of rules developed to increase the performance of the form system:

### maxFiles:[number]

This rule must only be used in this form widget.

It checks the number of uploaded files linked into this model and, if it's more than the defined number, will throw an error and stop the upload.

## Configuration

### Add the form widget into your YAML config form files:

Since this is not a default form widget the better way to do this is declaring the class full namespace:

```
fields:
  // ...
  images:
    tab: Tab text
    label: Label text
    type: Patroklo\FormWidgets\FileUpload
    mode: image
  // ...
```
And now you can use the form widget as is it was the default version of FileUpload.

## User defined rules

The rules are the very same that are used in the Validation library, with additional ones defined in the [New Rules](#new_rules) section.

If you want to use user defined upload rules, there are two different ways to accomplish this: add a YAML option in the form config file or a method into the method class.

The YAML config file will have priority over the model's method one, so if you have both defined at the same time, it will be applied the YAML one. 

### Adding the rules into the YAML config file:

```
fields:
  // ...
  images:
    tab: Tab text
    label: Label text
    type: Patroklo\FormWidgets\FileUpload
    mode: image
    rules: required|image|maxFiles:5|max:1024
  // ...
```

### Adding the rules into a model's method

You can add a new method into the model that holds the attribute where you can add your files that will store all it's rules.

This way of adding rules has the benefit of allowing dynamic rules.

``` php

class User extends Model {

    ...

    public $attachMany = [
        'images' => 'System\Models\File'
    ];

    /**
     * File upload rules
     * @return array
     */
    public function fileUploadRules()
    {
        return ['images' => 'required|image|maxFiles:5|max:1024'];
    }

```

And that's all folks! Any question or idea you have will be welcomed!