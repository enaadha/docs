# Widget form options

This is where you'll find a lot of the convenience of using the SiteOrigin Widgets Bundle as a framework for creating your own widgets. The widget form options are a way for you to define the configuration options you'd like to allow for your widget users. The more form options you provide, the more customizable your widget becomes.

## Form option field descriptors

Each value in the form options array is a form field descriptor, which is an associative array describing the form field to be rendered by the `SiteOrigin_Widget` base class, in order to capture configuration values for a widget instance. Each form field descriptor must at least have a type, however a few of the types won't be useful without additional configuration values. Optional base form field descriptor values are listed below:

- label: `string` Render a label for the field with the given value.
- default: `mixed` The field will be prepopulated with this default value.
- description: `string` Render small italic text below the field to desribe the field's purpose.
- optional: `bool` Append '(Optional)' to this field's label as a small green supertext.
- state_name: `string` Transforms into a class name, which, together with some JQuery, allows groups of elements to easily be set as visible or invisible simultaneously.
- hidden: `bool` Whether this field starts out visible or invisible.

In addition to these, some fields have their own specific configuration values, which are listed in the respective sections below.

## Form field types

### text
Renders a text input field.

#### Example
Form options input:
```php
$form_options = array(
	'some_text' => array(
		'type' => 'text',
		'label' => __('Some text goes here', 'widget-form-fields-text-domain'),
		'default' => 'Some default text.'
	)
);
```
Result:

![Widget Form Text Input](./images/form-field-type-text.png)

---

### color
Renders a color input field and color picker.

#### Example
Form options input:
```php
$form_options = array(
	'some_color' => array(
		'type' => 'color',
		'label' => __( 'Choose a color', 'widget-form-fields-text-domain' ),
		'default' => '#bada55'
	)
);
```
Result:

![Widget Form Color Picker](./images/form-field-type-color.png)

---

### number
Renders a text input field for entering a number. This is the same as the text type field, except that the input is cast as a `float`.

#### Example
Form options input:
```php
$form_options = array(
	'some_number' => array(
		'type' => 'number',
		'label' => __( 'Enter a number', 'widget-form-fields-text-domain' ),
		'default' => '12654'
	)
);
```
Result:

![Widget Form Number Input](./images/form-field-type-number.png)

---

### textarea
Renders a textarea field.

#### Additional options
- allow_html_formatting: `bool` Allows a few specific html tags to be passed through sanitization to the widget instance to influence display of the text. These are `<a>`, `<br>`, `<strong>`, and `<em>`.
- rows: `int` The number of visible rows in the textarea.

#### Example
Form options input:
```php
$form_options = array(
	'some_long_message' => array(
		'type' => 'textarea',
		'label' => __( 'Type a message', 'widget-form-fields-text-domain' ),
		'default' => 'An example of a long message.</br>It is even possible to add a few html tags.</br><a href="siteorigin.com" target="_blank"">Links!</a></br><strong>Strong</strong> and <em>emphasized</em> text.',
		'allow_html_formatting' => true,
		'rows' => 10
	)
);
```
Result:

![Widget Form Text Area](./images/form-field-type-textarea.png)

---

### slider
Renders a number slider field to allow the choice of a number in a range.

#### Additional options
- min: `int` The minimum value of the allowed range.
- max: `int` The maximum value of the allowed range.
- integer: `bool`

#### Example
Form options input:
```php
$form_options = array(
	'some_number_in_a_range' => array(
		'type' => 'slider',
		'label' => __( 'Choose a number', 'widget-form-fields-text-domain' ),
		'default' => 24,
		'min' => 2,
		'max' => 37,
		'integer' => true
	)
);
```
Result:

![Widget Form Slider](./images/form-field-type-slider.png)

---

### select
Renders a dropdown select field. This field is better for a long list of predefined values. For a short list the radio input field is a better choice.

#### Additional options
- prompt: `string` If present, it is included as a disabled (not selectable) value at the top of the list of options. If there is no default value, it is selected by default. You might even want to leave the label value blank when you use this.
- options `array` The list of options which may be selected.

#### Example 1 - default value without prompt
Form options input:
```php
$form_options = array(
	'some_selection' => array(
		'type' => 'select',
		'label' => __( 'Choose a thing from a long list of things', 'widget-form-fields-text-domain' ),
		'default' => 'the_other_thing',
		'options' => array(
			'this_thing' => __( 'This thing', 'widget-form-fields-text-domain' ),
			'that_thing' => __( 'That thing', 'widget-form-fields-text-domain' ),
			'the_other_thing' => __( 'The other thing', 'widget-form-fields-text-domain' ),
		)
	)
);
```
Result:

![Widget Form Select 1](./images/form-field-type-select-1.png)

#### Example 2 - prompt without default value
Form options input:
```php
$form_options = array(
	'another_selection' => array(
		'type' => 'select',
		'prompt' => __( 'Choose a thing from a long list of things', 'widget-form-fields-text-domain' ),
		'options' => array(
			'this_thing' => __( 'This thing', 'widget-form-fields-text-domain' ),
			'that_thing' => __( 'That thing', 'widget-form-fields-text-domain' ),
			'the_other_thing' => __( 'The other thing', 'widget-form-fields-text-domain' ),
		)
	)
);
```
Result:

![Widget Form Select](./images/form-field-type-select-2.png)

---

### checkbox
Renders a checkbox field.

#### Example
Form options input:
```php
$form_options = array(
	'some_boolean' => array(
		'type' => 'checkbox',
		'label' => __( 'Allow this thing?', 'widget-form-fields-text-domain' ),
		'default' => true
	)
);
```
Result:

![Widget Form Checkbox](./images/form-field-type-checkbox.png)

---

### radio
Renders a radio input field. This field is better for a short list of predefined values. For a long list the dropdown select field is a better choice.

#### Additional options
- options `array` The list of options which may be selected.

#### Example
Form options input:
```php
$form_options = array(
	'radio_selection' => array(
		'type' => 'radio',
		'label' => __( 'Choose a thing from a short list of things', 'widget-form-fields-text-domain' ),
		'default' => 'that_thing',
		'options' => array(
			'this_thing' => __( 'This thing', 'widget-form-fields-text-domain' ),
			'that_thing' => __( 'That thing', 'widget-form-fields-text-domain' ),
			'the_other_thing' => __( 'The other thing', 'widget-form-fields-text-domain' )
		)
	)
);
```
Result:

![Widget Form Radio Input](./images/form-field-type-radio.png)

---

### media
Renders a media selector field. This fields requires at least WordPress 3.5.

#### Additional options
- choose: `string` A label for the title of the media selector dialog.
- update: `string` A label for the confirmation button of the media selector dialog.
- library: `string` Sets the media library which to browse and from which media can be selected. Allowed values are `'image'`, `'audio'`, `'video'`, and `'file'`. The default is `'file'`.

#### Example
Form options input:
```php
$form_options = array(
	'some_media' => array(
		'type' => 'media',
		'label' => __( 'Choose a media thing', 'widget-form-fields-text-domain' ),
		'choose' => __( 'Choose image', 'widget-form-fields-text-domain' ),
		'update' => __( 'Set image', 'widget-form-fields-text-domain' ),
		'library' => 'image'
	)
);
```
Result:

![Widget Form Media Selector](./images/form-field-type-media.png)

---

### posts
Renders a post selector field. This can be used to build custom queries with which to select posts from your database. The field displays a small red indicator which shows the number of posts currently being selected. By default, all posts are selected.

#### Example
Form options input:
```php
$form_options = array(
	'some_posts' => array(
		'type' => 'posts',
		'label' => __('Some posts query', 'widget-form-fields-text-domain'),
	)
);
```
Result:

![Widget Form Posts Selector](./images/form-field-type-posts.png)

---

### icon
Renders an icon selector field. This allows you to select an icon from a default set of icon families, namely <a href="http://fortawesome.github.io/Font-Awesome/" target="_blank">Font Awesome</a>, <a href="https://icomoon.io/" target="_blank">IcoMoon</a>, <a href="http://genericons.com/" target="_blank">Genericons</a>, <a href="http://typicons.com/" target="_blank">Typicons</a>, and <a href="http://www.elegantthemes.com/blog/freebie-of-the-week/free-line-style-icons" target="_blank">Elegant Themes' Line Icons</a>. You can include your own icon families with the `siteorigin_widgets_icon_families` filter.

#### Example
Form options input:
```php
$form_options = array(
	'some_icon' => array(
		'type' => 'icon',
		'label' => __('Select an icon', 'widget-form-fields-text-domain'),
	)
);
```
Result:

![Widget Form Icon Selector](./images/form-field-type-icon.png)

---

### section
The section field type provides a convenient way to group and hide related form fields. This is useful when you have a large form which can appear overwhelming.

#### Additional options
- hide: `bool` Whether or not this section should start out collapsed or expanded.
- fields: `array` The set of fields to be grouped together. This should contain any combination of other field types, even sections and repeaters.

#### Example
Form options input:
```php
$form_options = array(
	'a_section' => array(
		'type' => 'section',
		'label' => __( 'A section containing related fields.' , 'widget-form-fields-text-domain' ),
		'hide' => true,
		'fields' => array(
			'grouped_text' => array(
				'type' => 'text',
				'label' => __( 'A grouped text field', 'widget-form-fields-text-domain' )
			),
			'grouped_checkbox' => array(
				'type' => 'checkbox',
				'label' => __( 'A grouped checkbox', 'widget-form-fields-text-domain' )
			)
		)
	)
);
```
Result:

![Widget Form Section](./images/form-field-type-section.png)

---

### repeater
The repeater field type allows repeating of the specified set of fields. 

#### Additional options
- item_name: `string` A default label for each repeated item.
- item_label: `array` This array descibes how the repeater may retrieve the item labels from HTML elements as they are updated. The options are:
  - selector: `string` A JQuery selector which is used to find an element from which to retrieve the item label.
  - update_event: `string` The event on which to bind and update the item label.
  - value_method: `string` The function which should be used to retrieve the item label from an element.
- fields: `array` THe set of fields to be repeated together as one item. This should contain any combination of other field types, even sections and repeaters.

#### Example
Form options input:
```php
$form_options = array(
	'a_repeater' => array(
		'type' => 'repeater',
		'label' => __( 'A repeating repeater.' , 'widget-form-fields-text-domain' ),
		'item_name'  => __( 'Repeater item', 'siteorigin-widgets' ),
		'item_label' => array(
			'selector'     => "[id*='repeat_text']",
			'update_event' => 'change',
			'value_method' => 'val'
		),
		'fields' => array(
			'repeat_text' => array(
				'type' => 'text',
				'label' => __( 'A text field in a repeater item.', 'widget-form-fields-text-domain' )
			),
			'repeat_checkbox' => array(
				'type' => 'checkbox',
				'label' => __( 'A checkbox in a repeater item.', 'widget-form-fields-text-domain' )
			)
		)
	)
);
```
Result:

Empty repeater:

![Widget Form Repeater 1](./images/form-field-type-repeater-1.png)

Repeater containing two items (the first item is collapsed and the second item is expanded):
![Widget Form Repeater 2](./images/form-field-type-repeater-2.png)

---

### widget
Includes the entire form of an existing widget class.

#### Additional options
- class: `string` The class name of the widget to be included.
- hide: `bool` Whether or not this section should start out collapsed or expanded.

#### Example
Form options input:
```php
$form_options = array(
	'some_widget' => array(
		'type' => 'widget',
		'label' => __( 'Button Widget', 'widget-form-fields-text-domain' ),
		'class' => 'SiteOrigin_Widget_Button_Widget',
		'hide' => true
	)
);
```
Result:

![Widget Form Widget Field](./images/form-field-type-widget.png)

---