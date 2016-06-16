---
title: Elemeno Documentation

language_tabs:
  - http

includes:

search: false
---

# Introduction

Elemeno is a content manangement platform that lets you create and manage content and deliver it to any device using a RESTful API.

# Single Items

Single Items are items that stand alone and do not belong to a collection. They have their own unique content model, and the item is returned via the API as a single resource. Single items are perfect for things like "About Us" or "Contact" pages on a website, or the landing screen of an application. Any content that will exist on its own can be thought of as a Single Item.

# Collections

Collections are collections of multiple items with the same content model. Items are returned from the API as an array and each item can be accessed individually via its ID or "slug". Collections also support filtering so you can find a specific subset of items from a collection based on your query parameters.

# Content Models

Every item, whether it is a Single Item or part of a Collection, is based on a Content Model. This Content Model defines the item's content structure and the type of inputs used to create an item. You can think of Content Models as the template for creating items.

## Creating

When you create a new Single Item or Collection, you are presented with an interface for creating a content model. This is essentially a blank slate with a list of all the input types on the right side of the screen. Simply drag an input type onto the screen to add an input to your content model. Click on any of your inputs to edit that input's settings. You can also drag your inputs up and down by their handle to reorganize your content model. If you need to remove an input, simply click the red "x" button on an input.

### Collections

Collections will start with a "Title" input which will be linked to the item's title attribute when creating an item. However, you can rename this field, or hide it altogether if you would prefer to leave your items in this collection untitled. For example, if you had a collection of Authors you may want to rename the title field to "Name" so that it makes more sense for that collection.

## Editing

You can edit a content model at any point. However, the changes that you make may impact the structure of the items returned by the API, or the content for existing items may become inaccessible.

### Examples

- When you rename an input, any content for that input in existing items will be inaccessible and the content returned from the API for the renamed input will be blank.
- Changing the validation rules for an input will only affect new items, or items that are edited in the future.
- Adding, removing, or renaming an input will affect the structure of the items returned via the API. This may mean you will need to make changes to the front-end applications that make use of content from the API.

# Input Types

There are a variety of input types to choose from when defining your content models. Each input has its own settings, validations, and API output. Below is a list of input types currently available, however more inputs will be added in the future to help capture a wider variety of data.

## Group

> API results for groups will look something like:

```json
{
	"author": {
	  "name": "Mark Twain",
	  "bio": "An American author and humorist ..."
	}
}
```

> API results for repeating groups will return an array of items:

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

The Input Group allows you to group multiple inputs under a single heading. You can also enable the "repeatable" option to create a repeating group of inputs.

### Example:

If you were creating a collection of books you might use a group to group all of the inputs related to the author. Things like the author's name, bio, and picture could all be grouped together. If some books in your collection have multiple authors you may want to make your authors group repeatable so that when you're creating items for your collection you will have the option to add multiple authors.

## Plain Text

> API results for Plain Text fields will look something like:

```json
{
	"title": "The Adventures of Tom Sawyer"
}
```

The Plain Text field supports plain text strings. The Plain Text field has an optional setting to allow for multi-line input.

### Validations

Name | Description
--------- | -----------
Min Length | The minimum number of characters the field will accept
Max Length | The maximum number of characters the field will accept
Matches Pattern | The text pattern the content must match

## Markdown

> API results for Markdown fields will look something like:

```json
{
	"description": {
		"markdown": "The Adventures of Tom Sawyer",
		"html": "<p>The Adventures of Tom Sawyer</p>"
	}
}
```

The Markdown field is a multi-line text area that supports Markdown formatting.

### Validations

Name | Description
--------- | -----------
Min Length | The minimum number of characters the field will accept
Max Length | The maximum number of characters the field will accept

## Number

> API results for Number fields will look something like:

```json
{
	"price": {
		"string": "25.50",
		"number": 25.5
	}
}
```

The Number field is single line field that only accepts numbers. The "Number of Decimal Places" setting will dictate the number of decimal places for the number. The API will return two values for the number field.

Value | Description
--------- | -----------
string | The number with specified number of decimal places
number | The number will only significant numbers to the right of the decimal point

### Validations

Name | Description
--------- | -----------
Min Value | The minimum value the field will accept
Max Value | The maximum value the field will accept


## Drop Down

> API results for Drop Down fields will look something like:


```json
{
	"category": {
		"label": "Fiction",
		"value": "cat15"
	}
}
```

The Drop Down field is a select list field which allows users to select a single option from list of options. The API will return an object with two values:

Value | Description
--------- | -----------
label | This is the text displayed to the user for the selected option
value | This hidden value associated with the selected option


## Check List

> API results for Check List fields will look something like:


```json
{
	"features": [
		{
			"label": "Hard Cover",
			"value": "feature-hard-cover",
			"checked": true
		},
		{
			"label": "Gilded Pages",
			"value": "feature-gilded",
			"checked": false
		}
	]
}
```

The Check List field is list of checkboxes that allows the user to select multiple values. The value returned by the API will be an array of objects with three values:

Value | Description
--------- | -----------
label | This is the text displayed to the user for the selected option
value | This hidden value associated with the selected option
checked | If the item is checked or not

## Switch

> API results for Switch fields will look something like:

```json
{
	"active": false
}
```

The Switch field is a simple on/off switch that represents a boolean value. The API will return a boolean value of `true` if the switch is on (green), or `false` if the switch is off (red).

## Image Picker

> API results for Image Picker fields will look something like:

```json
{
	"coverImage": {
		"dateCreated": "2016-05-12T14:10:09.539Z",
		"dateUpdated": "2016-05-12T14:10:09.539Z",
		"title": "Tom Sawyer Cover Image",
		"fileSize": "887126",
		"mimeType": "image/jpeg",
		"metaData": {
			"width": 4000,
			"height": 2248,
			"colors": {
				"dominant": {
					"rgb": {
						"r": 53,
						"g": 45,
						"b": 39
					},
					"hex": "352D27",
					"isLight": false
				},
				"palette": null
			},
			"alternativeText": null,
			"copyrightInformation": null,
			"exifData": {
				"CreateDate": "2016:03:04 18:19:40",
				"Make": "Panasonic",
				"Model": "DMC-GF1",
				"FNumber": 1.7,
				"FocalLength": 20,
				"ExposureTime": 0.02,
				"ISO": 400,
				"GPSLatitudeRef": null,
				"GPSLatitude": null,
				"GPSLongitudeRef": null,
				"GPSLongitude": null,
				"GPSAltitudeRef": null,
				"GPSAltitude": null
        	}
        },
		"tags": [],
		"imageUrl": "http://image.elemeno.io/full/4d533683-d309-4ae0-8387-31ec9523cde2.jpg",
		"thumbnails": {
			"small": "http://image.elemeno.io/cover/100/100/4d533683-d309-4ae0-8387-31ec9523cde2.jpg",
			"large": "http://image.elemeno.io/contain/1000/1000/4d533683-d309-4ae0-8387-31ec9523cde2.jpg"
		}
    }
}
```

The Image Picker field allows you to select an image from your existing image files, or upload a new image file. The Image Picker settings allow you to define thumbnails which will be auto-generated and a full URL will be returned in the API results for each thumbnail defined.

### Thumbnail Settings

Value | Description
--------- | -----------
width | The width of the generated thumbnail in pixels
height | The height of the generated thumbnail in pixels
Crop Type: contain | The image will be resized to fit within the dimensions specified. No cropping will occur.
Crop Type: cover | The image will be resized so the entire area defined by the dimensions is covered by the image. Cropping will likely occur.


## File Picker

> API results for File Picker fields will looks something like:

```json
{
	"digitalDownload": {
    	"dateCreated": "2016-05-11T14:05:50.917Z",
		"dateUpdated": "2016-05-11T14:05:50.917Z",
		"title": "Tom Sawyer PDF",
		"fileSize": "6553600",
		"mimeType": "text/pdf",
		"metaData": null,
		"tags": [],
		"fileUrl": "http://file.elemeno.io/35f3f5b0-e183-435b-9e6e-42c10a8098e0.pdf"
	}
}
```

The File Picker field allows you to upload a new file or select a one from your existing files. The File Picker settings allow you to specify the type of file that can be selected with the input. The API will return a URL for the file hosted on our CDN (content delivery network).

## Date and Time

> API results for Date and Time fields will looks something like:

```json
{
  "dateOnly": "2016-05-12",
  "timeOnly": "12:10",
  "dateAndTime": "2016-05-12T16:10:00+00:00"
}
```

The Date and Time field allows you to easily select date and time values. The settings allow you to choose from three different variations of the Date and Time input.

### Variations

Name | Description | Example
--------- | ----------- | -----------
Date Only | Select a calendar date | May 12, 2016
Time Only | Select a time | 12:10 PM
Date and Time | Select a specific moment in time | May 12, 2016 12:10PM EDT

### Date and Time Variation
When using the Date and Time variation of the input, you are selecting a specific moment in time. From the interface you will select a point in time based on your current time zone. From the API, Date and Time values will be returned in UTC (Coordinated Universal Time). If two different users in different time zone look at an item with a Date and Time field, they will see the moment in time converted to their local time zone. I.e., the value displayed will be different for each user, but the value will represent the same moment in time for each user.


# API

The Elemeno API is a RESTful API accessed via HTTP. This means that you can access your content via simple, straightforward HTTP requests from any platform or device that can communicate via HTTP. We are building libraries for a variety of popular programming languages and frameworks which will make working with the API even easier.


## Authentication

```http
GET /v1/collections HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

All requests to the API must include an API Key in an `Authorization` header. You can generate API Keys within the settings section of the Elemeno web app. We recommend generating a separate API Key for each of your websites and applications. For example, you might have a different API Key for your website, iOS application, Android application, and an Arduino prototype. This separation provides more security, finer grain control, and more visibility into which applications are making the most requests to the API.


## All Single Items

```http
GET /v1/singles HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
	"status": "success",
	"data": [
		{
			"id": "6e30f490-0bb1-11e6-900b-7f6d43d3f6e0",
			"slug": "about-us",
			"title": "About Us",
			"projectId": "98ce44d2-2985-11e5-8329-93cb1bd92cc3",
			"dateCreated": "2016-04-26T13:18:56.704Z",
			"dateUpdated": "2016-04-29T15:59:26.276Z",
			"links": {
				"self": "https://api.elemeno.io/v1/singles/about-us"
			}
		},
		...
	],
	"links": {
		"self": "https://api.elemeno.io/v1/singles?page=1&size=50",
		"first": "https://api.elemeno.io/v1/singles?page=1&size=50",
		"last": "https://api.elemeno.io/v1/singles?page=1&size=50",
		"next": null,
		"prev": null
	},
	"meta": {
		"totalRecords": 2,
		"pageSize": 50
	}
}
```

To access a list of all published Single Items, send a `GET` request to `/v1/singles`. This will return an array of Single Item objects.

## Specific Single Item

```http
GET /v1/singles/YOUR-ITEM-SLUG-HERE HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
    "status": "success",
    "data": {
        "id": "6e30f490-0bb1-11e6-900b-7f6d43d3f6e0",
        "slug": "about-us",
        "title": "About Us",
        "dateCreated": "2016-05-10T12:59:48.699Z",
        "content": {
            "headline": "The Best Books!",
            ...
        }
    },
    "links": {
        "self": "https://api.elemeno.io/v1/singles/about-us"
    },
    "meta": {
        "totalRecords": 1
    }
}
```

To access a specific Single Item, send a `GET` request to `/v1/singles/YOUR-ITEM-SLUG-HERE`. This will return a Single Item object along with its content.


## All Collections
```http
GET /v1/collections HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
	"status": "success",
	"data": [
		{
			"id": "fe4f04c2-1b6a-11e6-9883-ab6703adb701",
			"slug": "books",
			"title": "Books",
			"projectId": "98ce44d2-2985-11e5-8329-93cb1bd92cc3",
			"dateCreated": "2016-05-12T14:10:00.162Z",
			"dateUpdated": "2016-05-12T14:10:00.162Z",
			"links": {
				"self": "https://api.elemeno.io/v1/collections/books",
				"items": "https://api.elemeno.io/v1/collections/books/items"
			}
		},
		...
	],
	"links": {
		"self": "https://api.elemeno.io/v1/collections?page=1&size=50",
		"first": "https://api.elemeno.io/v1/collections?page=1&size=50",
		"last": "https://api.elemeno.io/v1/collections?page=1&size=50",
		"next": null,
		"prev": null
	},
	"meta": {
		"totalRecords": 4,
		"pageSize": 50
	}
}
```

To access a list of all published Collections, send a `GET` request to `/v1/collections/`. This will return an array of Collection objects.

## Specific Collection

```http
GET /v1/collections/YOUR-COLLECTION-SLUG-HERE HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response:

```json
{
	"status": "success",
	"data": {
		"id": "fe4f04c2-1b6a-11e6-9883-ab6703adb701",
		"slug": "books",
		"title": "Books",
		"projectId": "98ce44d2-2985-11e5-8329-93cb1bd92cc3",
		"dateCreated": "2016-05-12T14:10:00.162Z",
		"dateUpdated": "2016-05-12T14:10:00.162Z",
		"links": {
			"self": "https://api.elemeno.io/v1/collections/books",
			"items": "https://api.elemeno.io/v1/collections/books/items"
		}
	},
	"meta": {
		"totalRecords": 1
	}
}
```

To access a specific Collection, send a `GET` request to `/v1/collections/YOUR-COLLECTION-SLUG-HERE`. This will return a Collection object.

## Collection Items

```http
GET /v1/collections/YOUR-COLLECTION-SLUG-HERE/items HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
	"status": "success",
	"data": [
		{
			"id": "22e0c474-1b6b-11e6-aec3-d72ab41dc475",
			"slug": "the-adventures-of-tom-sawyer",
			"title": "The Adventures of Tom Sawyer",
			"dateCreated": "2016-05-12T14:10:00.102Z",
			"content": {
				"description": {
					"markdown": "The Adventures of Tom Sawyer by **Mark Twain** is an 1876 novel...",
					"html": "The Adventures of Tom Sawyer by <strong>Mark Twain</strong> is an 1876 novel..."
				},
				...
			},
			"links": {
				"self": "https://api.elemeno.io/v1/collections/books/items/the-adventures-of-tom-sawyer",
				"collection": "https://api.elemeno.io/v1/collections/books"
			}
		},
		...
	],
	"links": {
		"self": "https://api.elemeno.io/v1/collections/books/items?page=1&size=50",
		"first": "https://api.elemeno.io/v1/collections/books/items?page=1&size=50",
		"last": "https://api.elemeno.io/v1/collections/books/items?page=1&size=50",
		"next": null,
		"prev": null
	},
	"meta": {
		"totalRecords": 5,
		"pageSize": 50
	}
}
```

To access the items within a specific Collection, send a `GET` request to `/v1/collections/YOUR-COLLECTION-SLUG-HERE/items`. This will return an array of published Items from the specified Collection. If there are many Items in a Collection, the results will split into multiple pages. You can request a specific page, and a specific number of items per page using query parameters.

> Requesting a specific page of results with a custom size:

```http
GET /v1/collections/YOUR-COLLECTION-SLUG-HERE/items?page=2;size=20 HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

Supported Query Parameter

Parameter | Description
--------- | -----------
page | the page number you are requesting
size | the number of items to be returned per page (Min: 1, Max: 100, Default: 50)

For example, if your collection had 210 published items and you requested a `size` of 20 items per page, there would be 11 pages of results but the last page would only contain 10 items.

## Collection Item

```http
GET /v1/collections/YOUR-COLLECTION-SLUG-HERE/items/YOUR-ITEM-SLUG-HERE HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
	"status": "success",
	"data": {
		"id": "22e0c474-1b6b-11e6-aec3-d72ab41dc475",
		"slug": "the-adventures-of-tom-sawyer",
		"title": "The Adventures of Tom Sawyer",
		"dateCreated": "2016-05-16T13:53:39.102Z",
		"content": {
			"description": {
				"markdown": "The Adventures of Tom Sawyer by **Mark Twain** is an 1876 novel...",
				"html": "<p>The Adventures of Tom Sawyer by <strong>Mark Twain</strong> is an 1876 novel...</p>"
			},
			...
		},
		"links": {
			"self": "https://api.elemeno.io/v1/books/items/the-adventures-of-tom-sawyer",
			"collection": "https://api.elemeno.io/v1/books"
		}
	},
	"meta": {
		"totalRecords": 1
	}
}
```

To access a specific item from your Collection, send a `GET` request to `/v1/collections/YOUR-COLLECTION-SLUG-HERE/items/YOUR-ITEM-SLUG-HERE`.

You can also access an Item via its ID by using the `byID` query parameter. This would look something like: `/v1/collections/YOUR-COLLECTION-SLUG-HERE/items/YOUR-ITEM-ID-HERE?byID=true`

## Filtering

```http
GET /v1/collections/YOUR-COLLECTION-SLUG-HERE/items?filters={"$title":{"contains":"adventure"}} HTTP/1.1
Host: api.elemeno.io
Accept: application/json
Authorization: YOUR-API-KEY-HERE
```

> An example response (truncated for simplicity):

```json
{
	"status": "success",
	"data": [
		{
			"id": "22e0c474-1b6b-11e6-aec3-d72ab41dc475",
			"slug": "the-adventures-of-tom-sawyer",
			"title": "The Adventures of Tom Sawyer",
			"dateCreated": "2016-05-12T14:10:00.102Z",
			"content": {
				"description": {
					"markdown": "The Adventures of Tom Sawyer by **Mark Twain** is a novel written in 1876...",
					"html": "<p>The Adventures of Tom Sawyer by <strong>Mark Twain</strong> is a novel written in 1876...</p>"
				},
				...
			},
			"links": {
				"self": "https://api.elemeno.io/v1/collections/books/items/the-adventures-of-tom-sawyer",
				"collection": "https://api.elemeno.io/v1/collections/books"
			}
		},
		{
			"id": "2033cc9c-0572-11e6-b578-379c039aa13b",
			"slug": "alices-adventures-in-wonderland",
			"title": "Alice's Adventures in Wonderland",
			"dateCreated": "2016-05-12T14:25:03.002Z",
			"content": {
				"description": {
					"markdown": "Alice's Adventures in Wonderland (commonly shortened to _Alice in Wonderland_)",
					"html": "<p>Alice's Adventures in Wonderland (commonly shortened to <em>Alice in Wonderland</em>)</p>"
				},
				...
			},
			"links": {
				"self": "https://api.elemeno.io/v1/collections/books/items/alices-adventures-in-wonderland",
				"collection": "https://api.elemeno.io/v1/collections/books"
			}
		}
	],
	"meta": {
		"totalRecords": 2
	}
}
```

You will not always want to return every Item from a Collection. Often you will only require a subset of the results, based on some type of filtering. As an example, you may want Items whose title contains a certain keyword or Items that were created between two sets of dates. To filter Items within a specific Collection, send a `GET` request to `/v1/collections/YOUR-COLLECTION-SLUG-HERE/items?filters={"YOUR-FILTER-KEY-HERE":"YOUR-FILTER-VALUE-HERE"}`. This will return an array of published Items from the specified Collection that match the filters.

<aside class="warning">
The `filters` parameter must be formatted as JSON and URL encoded
</aside>

### Filter Meta Keywords

Title and (creation) date are stored differently than the rest of your content. In order to filter by them, they require the use of meta keywords. This helps avoid confusion with your other input keys.

Filter Keyword | Meaning
-------------- | -------
`$title` | This keyword will allow you to filter by your title, regardless if it has been renamed. If was renamed, you can additionally use that name
`$date` | This keyword will allow you to filter by the date created using a standard date format - This should be a string value
`$timestamp` | This keyword will allow you to filter by the date created using the UNIX epoch format (e.g. 1463585225) - This should be a numeric value

### Filter Operators

Filter Keyword | Usage
-------------- | -----
`$not` | `{ "$title": { $not: [ "Moby Dick", "The Great Gatsby"] } }`
`$contains` | `{ "$title": { "$contains": "adventure" } }`
`$startsWith` | `{ "$title": { "$startsWith": "The Adventures" } }`
`$endsWith` | `{ "$title": { "$endsWith": "Sawyer" } }`
`$lessThan` | `{ "price": { "$lessThan": 30" } }`
`<` | `{ "price": { "<": 30" } }`
`$lessThanOrEqual` | `{ "price": { "$lessThanOrEqual": 30" } }`
`<=` | `{ "price": { "<=": 30" } }`
`$greaterThan` | `{ "price": { "$greaterThan": 20" } }`
`>` | `{ "price": { ">: 20" } }`
`$greaterThanOrEqual` | `{ "price": { "$greaterThanOrEqual": 20" } }`
`>=` | `{ "price": { ">=": 20" } }`

### Chaining Filters

It is possible to chain multiple filters. To do this, simply add them to an object:

`{ "$title": { "$contains": "Adventure" }, "$date": { ">" : "2016-01-01", "lessThanOrEqual": "2020-12-31" } }`

### Filtering Strings

Inputs that result in string values, `$title`, `Plain Text`, `Markdown`, may use the following filters:

Filter | Description
------ | -----------
`{ "$title": "The Adventures of Tom Sawyer" }` | Exact match - The title matches the value exactly
`{ "$title": { "$contains": "adventure" } }` | Pattern match - The title contains the value "adventure"
`{ "$title": { "$startsWith": "The" } }` | The title starts with "The"
`{ "$title": { "$endsWith": "sawyer" } }` | The title ends with "sawyer"
`{ "$title": { "$startsWith: "the", endsWith: "Sawyer" } }` | Multiple conditions - The title starts with "the" and ends with "Sawyer"
`{ "$title": [ "The Adventures of Tom Sawyer", "Moby Dick" ] }` | The title is one of the items in the array
`{ "$title": { $not: [ "Moby Dick", "The Great Gatsby"] } }` | The title is **not** one of the items in the array

### Filtering Numbers

Inputs that result in number values, `Number`, may use the following filters:

Filter | Description
------ | -----------
`{ "price": 25.5 }` | Exact match - The price matches the value exactly
`{ "price": { "$lessThan": 30 } }` | The price is less than 30
`{ "price": { ">": 30" } }` | Less than (short form) - The price is less than 30
`{ "price": { "$lessThanOrEqual": 30 } }` | The price is less than or equal to 30
`{ "price": { ">=": 30 } }` | Less than or equal to (short form) - The price is less than or equal to 30
`{ "price": { "$greaterThan": 20 } }` | The price is greater than 20
`{ "price": { "<": 20 } }` | Greater than (short form) - The price is greater than 20
`{ "price": { "$greaterThanOrEqual": 20 } }` | The price is greater than or equal to 20
`{ "price": { "<=": 20 } }` | Greater than or equal to (short form) - The price is greater than or equal to 20

### Filtering Dates

Inputs that result in date values, `$date`, `$timestamp`, `Date and Time`, may use the following filters:

Filter | Description
------ | -----------
`{ "$date": "2016-04-01" }` | Exact match - The date matches the value exactly
`{ "$date": { "$lessThan": "2020-12-31" } }` | The date is before December 31, 2020
`{ "$date": { ">": "2020-12-31" } }` | Less than (short form) - The date is before December 31, 2020
`{ "$date": { "$lessThanOrEqual": "2020-12-31" } }` | The date is before or equal to December 31, 2020
`{ "$date": { ">=": "2020-12-31" } }` | Less than or equal to (short form) - The date is before or equal to December 31, 2020
`{ "$date": { "$greaterThan": "2016-04-01" } }` | The date is after April 1, 2016
`{ "$date": { "<": "2016-04-01" } }` | Greater than (short form) - The date is after April 1, 2016
`{ "$date": { "$greaterThanOrEqual": "2016-04-01" } }` | The date is after or equal to April 1, 2016
`{ "$date": { ">=": "2016-04-01" } }` | Greater than or equal to (short form) - The date is after or equal to April 1, 2016
`{ "$timestamp": { "$greaterThan": 1463585225 } }` | The date is before December 31, 2020

### Filtering Drop Down

Filtering drop downs use similar filters to string types

Filter | Description
------ | -----------
`{ "edition": "first" }` | Exact match - The `edition` matches the value exactly
`{ "edition": { "$contains": "irst" } }` | Pattern match - The `edition` contains the value "irst"
`{ "edition": { "$startsWith": "fir" } }` | The `edition` starts with "fir"
`{ "edition": { "$endsWith": "st" } }` | The `edition` ends with "st"
`{ "edition": { "$startsWith: "fir", endsWith: "st" } }` | Multiple conditions - The `edition` starts with "fir" and ends with "st"
`{ "edition": [ "first", "second" ] }` | The `edition` is one of the items in the array
`{ "edition": { $not: [ "third", "fourth" ] } }` | The `edition` is **not** one of the items in the array

### Filtering Checklist

Filtering checklists use similar filters to string types, and will only return values if they are checked

Filter | Description
------ | -----------
`{ "edition": "first" }` | Exact match - The `edition` matches the value exactly
`{ "edition": { "$contains": "irst" } }` | Pattern match - The `edition` contains the value "irst"
`{ "edition": { "$startsWith": "fir" } }` | The `edition` starts with "fir"
`{ "edition": { "$endsWith": "st" } }` | The `edition` ends with "st"
`{ "edition": { "$startsWith: "fir", endsWith: "st" } }` | Multiple conditions - The `edition` starts with "fir" and ends with "st"
`{ "edition": [ "first", "second" ] }` | The `edition` is one of the items in the array
`{ "edition": { $not: [ "third", "fourth" ] } }` | The `edition` is **not** one of the items in the array

### Filtering Switches

Filter | Description
------ | -----------
`{ "available": true }` | Exact match - `available` is `true`
`{ "hardcover": false }` | Exact match - `hardcover` is `false`

### Filter Image Picker

Filtering for images has not been implemented. Filtering, based on whether or not an image has been set, will be implemented soon.

### Filtering Files

Filtering for files has not been implemented. Filtering, based on whether or not a file has been set, will be implemented soon.


### Filtering Groups

Filtering within a group, either non-repeatable or repeatable, is not implemented.

## Errors

> Example Error Response:

```json
{
  "status": "error",
  "error": {
    "message": "Single Item or API key issue",
    "description": "Single Item with the slug about-uss could not be found or API key does not have the appropriate permissions"
  }
}
```

While interacting with Elemeno API you may encounter errors. Below is a list of the most common error status codes and their meanings:

Error Code | Meaning
---------- | -------
400 | Bad Request -- Something was wrong with your request. The error message will provide more details.
401 | Unauthorized -- The API Key provided does not have access to the resource requested.
404 | Not Found -- The resource requested could not be found. This could mean the item doesn't exist, or that it's simply not published.
429 | Too Many Requests -- You have exceeded the request limit for your project's current plan.
500 | Internal Server Error -- We had a problem with our server. Try again later.
