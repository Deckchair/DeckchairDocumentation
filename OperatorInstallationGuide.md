## Deckchair :: API Documentation [Draft 0.3-WIP] ##

---

## API Endpoints ##
---





#### GET.Cameras ####
`http://api.deckchair.com/v1/cameras`

Lists out all cameras. Will have a fulltext search parameter to support the desktop app currently under development.

**Response: [Array]**

*	`_id` Camera ID
	*	*Format*: String
*	`active` Indicates if the camera is active in the system
	*	*Format*: Boolean
*	`title` Camera Title - Primarily used internally and within Deckchair search indexes
	*	*Format*: String
*	`description` Camera Description - Primarily used internally and within Deckchair search indexes
	*	*Format*: String
*	`adTitle` Ad Title - Displayed on the upper line in the panel imprinted on all images
	*	*Format*: String
*	`adCaption` Ad Caption - Displayed on the lower line in the panel imprinted on all images, usually a URL
	*	*Format*: String
*	`active` Indicates if the camera is active in the system
	*	*Format*: Boolean


```
## Example Request
http://api.deckchair.com/v1/cameras

{
	"success": true,
	"data": [
		{
			"_id": "52faa4c7ad5b86bc2a267cd3",
			"active": true,
			"title": "Brunswick Square Hotel"
			"adTitle": "Brunswick Square Hotel",
			"adCaption": "www.mydomain.com",
			"description": "",
			"logoUid": "/logo_12341234123.jpg",
		},
		{
			"_id": "4567898765456789098765",
			"active": true,
			"title": "Camera Title"
			"adTitle": "Camera Title",
			"adCaption": "www.mydomain.com",
			"description": "",
			"logoUid": "/logo_12341234123.jpg",
		}
	]
}
```



---


#### GET.Camera ####
`http://api.deckchair.com/v1/camera/:id`

Retreives detailed information about a camera.

**Response: [Object]**

*	`_id` Camera ID
	*	*Format*: String
*	`active` Indicates if the camera is active in the system
	*	*Format*: Boolean
*	`title` Camera Title - Primarily used internally and within Deckchair search indexes
	*	*Format*: String
*	`description` Camera Description - Primarily used internally and within Deckchair search indexes
	*	*Format*: String
*	`adTitle` Ad Title - Displayed on the upper line in the panel imprinted on all images
	*	*Format*: String
*	`adCaption` Ad Caption - Displayed on the lower line in the panel imprinted on all images, usually a URL
	*	*Format*: String
*	`active` Indicates if the camera is active in the system
	*	*Format*: Boolean


```
## Example Request
http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3

{
	"success": true,
	"data": {
		"_id": "52faa4c7ad5b86bc2a267cd3",
		"active": true,
		"title": "Brunswick Square Hotel"
		"adTitle": "Brunswick Square Hotel",
		"adCaption": "www.mydomain.com",
		"description": "",
		"logoUid": "/logo_12341234123.jpg",
	}
}
```



---


#### GET.Camera/Images ####
`http://api.deckchair.com/v1/camera/:id/images[?[from=123456]&[to=123456]]`

Retreives a list of images taken by a camera. Optional `to`/`from` search range parameters.

**Request:**

*	`from` Limit the results by specifying a 'from' datetime.
	*	*Format*: Unixtime
	*	*Default*: Now - 24 hours
*	`to` Limit the results by specifying a 'to' datetime.
	*	*Format*: Unixtime
	*	*Default*: Now
	
**Response: [Array]**

*	`_id` Image ID
	*	*Format*: String
*	`taken` DateTime that the image was taken
	*	*Format*: ISO Date

```
## Example Request
http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/images

http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/images?from=12345&to=12345

{
	"success": true,
	"data": [
		{
			"_id": "5309fee92143de6b70632817",
			"taken": "2014-02-23T14:00:00.000Z"
		},
		{
			"_id": "5309fdbcc928e86a70ad978e",
			"taken": "2014-02-23T13:55:00.000Z"
		},
		{
			"_id": "5309fc902143de6b70632813",
			"taken": "2014-02-23T13:50:00.000Z"
		}
	]
}
```



---


#### GET.Camera/Timeline ####
`http://api.deckchair.com/v1/camera/:id/timeline[?[from=123456]&[to=123456]]`

Retreives an overview of images taken by a camera grouped and by a unit of time. Very useful for retrieving information about images which would otherwise require large amounts of data to be transferred using the `/images` call. Especially useful for overviews of a long period of time, e.g. months or years.

Optional `to`/`from`/`by` search range and grouping parameters.

**Request:**

*	`from` Limit the results by specifying a 'from' datetime
	*	*Format*: Unixtime
	*	*Default*: 00:00 7 days ago
*	`to` Limit the results by specifying a 'to' datetime
	*	*Format*: Unixtime
	*	*Default*: Now
*	`by` Group the results by specifying a 'by' unit
	*	*Format*: [`hour`|`day`|`week`|`month`|`year`]
	*	*Default*: `hour`


**Response: [Array]**

*	`_id` Information about the current group
	*	*Format*: Object
*	`imageCount` Number of images in the group
	*	*Format*: Integer
*	`images` Contains the first and last image of the group
	*	*Format*: Object

	
```
## Example Request
http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/timeline

http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/timeline?from=12345&to=12345&by=hour

{
    "success": true,
    "data": [
        {
            "_id": {
                "day": 23,
                "hour": 14,
                "month": 2,
                "week": 8,
                "year": 2014
            },
            "imageCount": 6,
            "images": {
                "first": {
                    "_id": "5309fee92143de6b70632817",
                    "taken": "2014-02-23T14:00:00.000Z"
                },
                "last": {
                    "_id": "530a05ed2143de6b7063282b",
                    "taken": "2014-02-23T14:30:00.000Z"
                }
            }
        },
        {
            "_id": {
                "day": 23,
                "hour": 13,
                "month": 2,
                "week": 8,
                "year": 2014
            },
            "imageCount": 12,
            "images": {
                "first": {
                    "_id": "5309f0d62143de6b706327db",
                    "taken": "2014-02-23T13:00:00.000Z"
                },
                "last": {
                    "_id": "5309fdbcc928e86a70ad978e",
                    "taken": "2014-02-23T13:55:00.000Z"
                }
            }
        },
        {
            "_id": {
                "day": 23,
                "hour": 12,
                "month": 2,
                "week": 8,
                "year": 2014
            },
            "imageCount": 12,
            "images": {
                "first": {
                    "_id": "5309e2c62143de6b706327bc",
                    "taken": "2014-02-23T12:00:00.000Z"
                },
                "last": {
                    "_id": "5309efaac928e86a70ad9751",
                    "taken": "2014-02-23T12:55:00.000Z"
                }
            }
        }
    }];
}
```

---




#### \*\*\*UNRELEASED\*\*\* GET.Camera/Videos ####
`http://api.deckchair.com/v1/camera/:id/videos[?[from=123456]&[to=123456]&[type=timelapse]]`

Retreives a list of videos (timelapse and video recordings) taken by a camera. Optional `to`/`from` search range parameters.

**Request:**

*	`from` Limit the results by specifying a 'from' datetime.
	*	*Format*: Unixtime
	*	*Default*: Now - 24 hours
*	`to` Limit the results by specifying a 'to' datetime.
	*	*Format*: Unixtime
	*	*Default*: Now
*	`type` Limit the results by specifying a 'type'.
	*	*Format*: [`recording`|`timelapse`]
	*	*Default*: Empty (show all)

**Response: [Array]**

TBC

```
## Example Request
http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/videos

http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3/videos?from=12345&to=12345&type=timelapse

TBC
```



---




#### GET.Image ####
`http://api.deckchair.com/v1/image/:id

Retrieves details for a single image.
	
**Response: [Object]**

*	`_id` Image ID
	*	*Format*: String
*	`active` If the image is available this will be true
	*	*Format*: Boolean
*	`taken` DateTime that the image was taken
	*	*Format*: ISO Date
*	`camera` Camera object the image relates to
	*	*Format*: Object


```
## Example Request
http://api.deckchair.com/v1/image/5301a23a5b09c11ebaa8bd44

{
    "success": true,
    "data": {
        "_id": "5301a23a5b09c11ebaa8bd44",
        "active": false,
        "taken": "2014-02-17T05:46:30.000Z",
        "camera": {
            "_id": "52fd060e722f8100004dc3aa",
            "active": true,
            "adCaption": "www.mydomain.co.uk",
            "adTitle": "Brunswick Town B&B",
            "description": "Brunswick Town, Hove",
            "logoUid": "",
            "title": "Brunswick Bed & Breakfast"
        }
    }
}
```



---


#### \*\*\*UNRELEASED\*\*\* GET.Video ####
`http://api.deckchair.com/v1/video/:id

Retrieves details for a single video.
	
**Response: [Object]**

*	`_id` Video ID
	*	*Format*: String
*	`active` If the video is available this will be true
	*	*Format*: Boolean
*	`taken` DateTime that the video was taken
	*	*Format*: ISO Date
*	`camera` Camera object the video relates to
	*	*Format*: Object


```
## Example Request
http://api.deckchair.com/v1/video/2345235634523453456

TBC
```


---


#### GET.Viewer/Image ####
`http://api.deckchair.com/v1/viewer/image/:id

Returns an image file.

If an image is too small to conveniently display the panel in the bottom left, it will not be added regardless of the panelMode value.

THe majority of the time an image will be served directly from our CDN, all generated images are heavily cached and we pre-cache images that are expected to be requested.

When manually tinkering with this API call (testing different sizes) the server will work quickly to generate a new image on the fly, return it to the browser then cache it for future requests in both our centralized storage and our CDN edge locations.

In the event of heavy traffic we have proprietary algorithms that will keep a web browser waiting for upto 5 minutes to return an image - in reality this cutoff will not be reached as most programmatically requested images will be cached or pre-cached, our systems are extremely high powered and process image requests quickly, and we have an auto scaling architecture that brings heavy computational systems online in the event of high load / traffic.

*Usage Notes:*

*	Use parameters in the order listed below and implement all parameters regardless of if they are the same as the default value. We string match URLs at the CDN level before calling our core servers so keeping these as uniform as possible will result in the lowest latency
*	Using `resizeMode=fit` will return an image of an unknown height *or* width. As we do not pad images out or alter the aspect ratio

**Request:**

*	`width` Width of the image
	*	*Format*: Integer [1-10000]
	*	*Default*: 1800
*	`height` Height of the image
	*	*Format*: Integer [1-7000]
	*	*Default*: 900
*	`resizeMode` Resize the image to 'fill' or 'fit' within the width and height. 'Fill' will crop when necessary
	*	*Format*: [`fill`|`fit`]
	*	*Default*: `fit`
*	`gravity` If `resizeMode` is set to `fill` the image will be cropped. This value allows you to set the area of the image to focus on before cropping.
	*	*Format*: [`Center`|`North`|`NorthEast`|`NorthWest`|`South`|`SouthEast`|`SouthWest`]
	*	*Default*: `Center`
*	`quality` Image quality, file size will be influenced by this value
	*	*Format*: Integer [0-100]
	*	*Default*: 75
*	`panelMode` Whether to display the panel in the bottom left of the image. For some clients this will be overridden internally
	*	*Format*: Boolean
	*	*Default*: `true`
*	`format` Image format, currently we only support JPEG
	*	*Format*: `jpg`
	*	*Default*: `jpg`
	
	
**Response: [image/jpeg]**

```
## Example Request
http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=800&height=600&resizeMode=fill

http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=800&height=7000&resizeMode=fit

http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=1800&height=900&resizeMode=fill&gravity=Center&quality=90&panelMode=true&format=jpg
```


---



#### GET.Viewer/Camera ####
`http://api.deckchair.com/v1/viewer/camera/:id

Returns an image file.

The image file will be the latest image from a camera. We use HTTP headers to manage cache expiry.

This request redirects to the `viewer/camera` endpoint passing the querystring with it. See documentation for endpoint `viewer/image` for more information 

**Request:**

*	`width` Width of the image
	*	*Format*: Integer [1-10000]
	*	*Default*: 1800
*	`height` Height of the image
	*	*Format*: Integer [1-7000]
	*	*Default*: 900
*	`resizeMode` Resize the image to 'fill' or 'fit' within the width and height. 'Fill' will crop when necessary
	*	*Format*: [`fill`|`fit`]
	*	*Default*: `fit`
*	`gravity` If `resizeMode` is set to `fill` the image will be cropped. This value allows you to set the area of the image to focus on before cropping.
	*	*Format*: [`Center`|`North`|`NorthEast`|`NorthWest`|`South`|`SouthEast`|`SouthWest`]
	*	*Default*: `Center`
*	`quality` Image quality, file size will be influenced by this value
	*	*Format*: Integer [0-100]
	*	*Default*: 75
*	`panelMode` Whether to display the panel in the bottom left of the image. For some clients this will be overridden internally
	*	*Format*: Boolean
	*	*Default*: `true`
*	`format` Image format, currently we only support JPEG
	*	*Format*: `jpg`
	*	*Default*: `jpg`
	
	
**Response: [image/jpeg]**

```
## Example Request
http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=800&height=600&resizeMode=fill

http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=800&height=7000&resizeMode=fit

http://api.deckchair.com/v1/viewer/image/5301a23a5b09c11ebaa8bd44?width=1800&height=900&resizeMode=fill&gravity=Center&quality=90&panelMode=true&format=jpg
```


---



#### GET.Widget ####
`http://api.deckchair.com/v1/widget/:id`

Returns a HTML page containing the Deckchair Widget intended to be IFramed within a website. The camera ID is required in the URL.
	
**Response: [HTML Page]**

```
## Example Request
http://api.deckchair.com/v1/widget/52faa4c7ad5b86bc2a267cd3
```




## Miscellaneous ##
---

#### Domain throttling workaround ####

By default browsers will only open a limited number of connections to a single server, despite our servers being very capable of sustaining more. If you wish to display lots of images in a timeline on a single page it is recommended you split your requests over a number of domains.

We support API calls to the following domains:

*	http://api.deckchair.com
*	http://api.a.deckchair.com
*	http://api.b.deckchair.com
*	http://api.c.deckchair.com
*	http://api.d.deckchair.com

We are developing an open-source client-side library to assist the utilisation of multiple domains that takes into account browser caching.


#### HTTPS Support ####

We do have HTTP support. Contact us at mail@deckchair.com to find out more.


#### NoCookie Domain Support ####

We are looking into the performance benefits of domain-wide 'NoCookie' support. If you have such a requirement contact us at mail@deckchair.com to discuss further.



---




## Cross Domain Requests ##
---

#### JSONP Support ####

JSONP support is implemented and available.

**Request:**

*	`callback`
	*	*Format*: String

The expected callback parameter is  `callback`. Keeping your callback value the same will improve cache and CDN distribution performance. Using CORS or proxying requests from your server will provide better performance as they should be served more often from caching and CDN layer.

```
## Example Request
http://api.deckchair.com/v1/camera/52faa4c7ad5b86bc2a267cd3?callback=deckchairCameraCallback

typeof deckchairCameraCallback === 'function' && deckchairCameraCallback({
	"success": true,
	"data": {
		"_id": "52faa4c7ad5b86bc2a267cd3",
		"active": true,
		"title": "Brunswick Square Hotel"
		"adTitle": "Brunswick Square Hotel",
		"adCaption": "www.mydomain.com",
		"description": "",
		"logoUid": "/logo_12341234123.jpg",
	}
});

```




#### CORS Support ####

CORS support is implemented and available.

Requirements

**Request:**

*	`origin`
	*	*Format*: String

Add an origin parameter to the query string of your URL request with the value of the parameter set to your source domain and the `://` replaced by an underscore (`_`);

```
## Example Request
http://api.deckchair.com/v1/camera/12345?origin=http_mydomain.com
-
## Example Request with HTTPS origin
http://api.deckchair.com/v1/camera/12345?origin=https_mysecuredomain.com

## Response Headers
Access-Control-Allow-Headers: X-Requested-With
Access-Control-Allow-Origin: http://mydomain.com
```

