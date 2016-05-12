---
title: API Reference

language_tabs:
  - rest

includes:

search: false
---

# Introduction

Fill this in later

# Single Items

Single Items are items that standalone and do not belong to a collection. They have their own unique content model, and the item is returned via the API as a single resource. Single items are perfect for things like an "About Us" or "Contact" pages on a website, or the landing screen of an application. Any content that will exist on it's own can be thought of as a Single Item. 

# Collections

Collections are collections of multiple items with the same content model. Items are returned from the API as an array and each item can be accessed individually via it's ID or "slug". Collections also support searching and filtering so you can find a specific subset of items from a collection based on your query parameters.

# Content Models

Every item whether it's a Single Item or part of a Collection is based a Content Model which defines the item's content structure, and the type of inputs used to create an item. You can think of Content Models as the template for creating items.
 
## Creating

When you create a new Single Item or Collection you are presented with an interface for creating a content model. This is essentially a blank slate with list of all the input types on right side of the screen. Simply drag an input type onto the screen to add an input to your content model. Click on any of your inputs to edit that input's settings. You can also drag your inputs up and down to reorganize your content model. If you need to remove an input, simple click the red x button on an input.

### Collections

Collections will start with a "Title" input which will be linked to the item's title attribute when creating an item. However you can rename this field, or hide it altogether if you would prefer to leave your items in this collection untitled. For example, if you had a collection of Authors you may want to rename the title field to be "Name" so that it makes more sense for that collection.

## Editing

You can edit a content model at any point. However, the changes that you make may impact the structure of the items returned by the API, or the content for existing items may become inaccessible.

### Examples

- When you rename an input any content for that input in existing items will be inaccessible and the content returned from the API for the renamed input will be blank.
- Changing the validation rules for an input will only affect new items, or items that are edited in the future.
- Adding, removing, or renaming an input will affect the structure of the items returned via the API. This may mean you will need to make changes to the front-end applications that make use of content from the API.

# Input Types

There are a variety of input types to choose from when defining your content models. Each input has it's own settings, validations, and API output. Below is a list of input types currently available, however more inputs will be added in the future to help capture a wider variety of data.

## Group

> API results for groups will look something like 

```json
{
	"author": {
	  "name": "Mark Twain",
	  "bio": "An American author and humorist ..."
	}
}
```

> API results for repeating groups will return an array of items

```json
{
	"authors": [
		{
	  		"name": "Mark Twain",
	  		"bio": "An American author and humorist ..."
	  	},
	  	{
	  		"name": "Jane Austen",
	  		"bio": "An English novelist ..."
	  	}
	]
}
```

The Input Group allows you to group multiple inputs under a single heading. You can also turn on the "repeating" option to create a repeatable group of inputs. 

### Example:

If you were creating a collection of books you might use a group to group all of the inputs related to the author. Things like the author's name, bio, and picture could all be grouped together. If some books in our collection have multiple authors we may want to make our authors group repeatable so that when we're creating items for our collection we will have option to add multiple authors.

## Short Text

> API results for Short Text fields will look something like

```json
{
	"title": "The Adventures of Tom Sawyer"
}
```

The Short Text field is single line text field used to capture shorter text strings. 

### Validations

Name | Description
--------- | -----------
Min Length | The minimum number of characters the field will accept
Max Length | The maximum number of characters the field will accept
Matches Pattern | The text pattern the content must match

## Long Text

> API results for Long Text fields will look something like

```json
{
	"description": {
		"text":"The Adventures of Tom Sawyer",
		"html":""
	}
}
```

The Long Text field is a multi line text field that supports Markdown formatting. 

### Validations

Name | Description
--------- | -----------
Min Length | The minimum number of characters the field will accept
Max Length | The maximum number of characters the field will accept

## Number

> API results for Number fields will look something like

```json
{
	"price": {
		"text":"25.50",
		"number":25.5
	}
}
```

The Number field is single line field that accepts only numbers. The "Number of Decimal Places" setting will dictate the number of decimal places for the number. The API will return two values for the number field.

Value | Description
--------- | -----------
text | The number with specified number of decimal places 
number | The number will only signifcant numbers to the right of the decimal point

### Validations

Name | Description
--------- | -----------
Min Value | The minimum value the field will accept
Max Value | The maximum value the field will accept


## Drop Down

> API results for Drop Down fields will look something like


```json
{
	"category": {
		"label":"Fiction",
		"value":"cat15"
	}
}
```

The Drop Down field is a select list field which allows users to select a single option from list of options. The API will return an object with two values:

Value | Description
--------- | -----------
label | This is the text displayed to the user for the selected option
value | This hidden value associated with the selected option


## Check List

> API results for Check List fields will look something like


```json
{
	"features": [
		{
			"label":"Hard Cover",
			"value":"feature-hard-cover"
		},
		{
			"label":"Gilded Pages",
			"value":"feature-gilded"
		}
	]
}
```

The Check List field is list of checkboxes that allows the user to select multiple values. The value returned by the API will be an array of objects with two values:

Value | Description
--------- | -----------
label | This is the text displayed to the user for the selected option
value | This hidden value associated with the selected option

## Switch

> API results for Switch fields will look something like

```json
{
	"active": false
}
```

The Switch field is a simple on/off switch that is represents a boolean value. The API will return a boolean value of true if the switch is on (green), or false if the switch is off (red).

## Image Picker

> API results for Image Picker fields will look something like

```json
{
	"coverImage": {
		"stuff":"here"
	}
}
```

The Image Picker field allows you to select an image from your existing image files, or upload a new image file. The Image Picker settings allow you to define thumbnails which will be auto generated and a full url will be returned in the API results for each thumbnail defined.

### Thumbnail Settings

Value | Description
--------- | -----------
Width | The width of the generated thumbnail in pixels
Height | The height of the generated thumbnail in pixels
Crop Type: Contain | The image will be resized to fit within the dimensions specified. No cropping will occur.
Crop Type: Cover | The image will be resized so the entire area defined by the dimensions is covered by the image. Cropping will likely occur.


## File Picker

> API results for File Picker fields will looks something like

```json
{
	"digitalDownload": {
		"stuff":"here"
	}
}
```

The File Picker field allows you to select a file from your existing files, or upload a new file. The File Picker settings allow you to specify the type of file that can be selected with the input. The API will return a url for the file hosted on our CDN. 

## Date and Time

> API results for Date and Time fields will looks something like

```json
{
  "dateOnly":"2016-05-12",
  "timeOnly":"12:10",
  "dateAndTime":"2016-05-12 16:10:00Z"
}
```

The Date and Time field allows you to easily select date and time values. The settings allow you to choose from three different variations of the Date and Time input.

### Variations

Name | Description | Example
--------- | ----------- | -----------
Date Only | Select a calendar date | May 12, 2016
Time Only | Select a time | 12:10 PM
Date and Time | Select a specific moment in time | May 12, 2016 @ 12:10PM EDT

### Date and Time Variation
When using the Date and Time variation of the input, you are selecting a specific moment in time. From the interface you will select a point in time based on your current timezone. From the API, Date and Time values will be returned in UTC (Coordinated Universal Time). If two different users in different timezone look at an item with a Date and Time field, they will see the moment in time converted to their local timezone. IE: the value displayed will be different for each user, but the value will represent the same moment in time for each user.


# API
## Authentication
## Single Items
## Collections
## Searching and Filtering
## Errors

# Issues and Support

