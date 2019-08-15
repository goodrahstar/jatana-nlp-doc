# Jatana API endpoints

## For Upload API's



### Ignition Route

To test if the service is up and running.


**Request**

```
	GET http://localhost:8080/api/ms/v3.0/ignition
```

**Response**

```

    {
      "Engine Status" : "Microservice for UPLOAD is alive and kicking"
    }
```



### Upload Route


This API is used to send the JSON data to the Upload service

.. todo:: Add data format reference or sample

**Request**

```

	import requests

	url = "http://localhost:8080/api/ms/v3.0/upload"

	querystring = {"client":"netto"}

	payload = "{ [{\"ticket\": {\"via\": {\"source\": {\"to\": {\"name\": \"XYZ\", \HTML, like Gecko) Chrome/47.0.2526.80 Safari/537.36\", \"ip_address\": \"80.254.154.59\", \"location\": \"Denmark\", \"longitude\": 12.056399999999996}, \"custom\": {}}}]}]}"
	
	headers = {
	    'Content-Type': "application/json",
	    }

	response = requests.request("POST", url, data=payload, headers=headers, params=querystring)

	print(response.text)
```

**Response**

```

	{
	'Message' : 'Training Successsful' 
	}
```

### Training Route


.. warning:: This endpoint is for internal use only.

This training endpoint is a backdoor to train any model on ML ENGINE which is only to be used by the AI Team.



.. todo:: Add params for `lang` 

**Request**

```
	
	import requests

	url = "https://localhost:8080/api/ms/v3.0/train"

	querystring = {
		"client":"new_client"
		}

	payload = ""

	response = requests.request("GET", url, data=payload, params=querystring)

	print(response.text)
```

**Response**


```

	{
	'job_name' : 'new_cleint_ml_jos12344',
	'job_result': 'Model Trained' 
	}
```




## For Query API's



### Query Route [TF Serving Version]

.. note:: The ``instances`` object in json needs to be a list of int of 100 elements.

**Request**

```

	curl -X POST \
	  http://localhost:8501/v1/models/jatanademo_macro:predict \
	  -d '{
	    "signature_name": "predict",
	    "instances": [
	        [
            33,
            114,
            9,
            30,
            0,
            30,
            0,
            50,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0,
            0]]}'

```

**Response**

```

	{"predictions": [[
	            2.36913e-16,
	            5.55834e-32,
	            2.54004e-7,
	            1,
	            4.11396e-10
	        ]
	    ]}
```	

### Query Route [WRAPPER VERSION]


**Request**

.. todo:: Fix Payload

```
	import requests

	url = "http://localhost:8080/api/ms/v3.0/query"

	payload = "Content-Disposition: form-data; 
				name=\"q\"\r\n\r\n\"Hi,\n\nLast week I have ordered a product from your web shop after seeing an ad on my Facebook feed.\n\nWhile completing the purchase I’ve selected the express shipment option to make sure I would receive the product as fast as possible.\n\nMore than a week has passed but and I haven’t received anything yet!\n\nCan you please check what’s going on with my shipment?\n\nThanks,\n\nFrenk\"\r\n------WebKitFormBoundary7MA4YWxkTrZu0gW\r\nContent-Disposition: form-data; name=\"client\"\r\n\r\njatana\r\n"
	
	headers = {
	    'content-type': "multipart/form-data",
	    'Authorization': "Bearer TOKEN"
	    }

	response = requests.request("POST", url, data=payload, headers=headers)

	print(response.text)
```

**Response**

```

	{
	    "macros": [
	        {
	            "macro_title": "SHIPMENT_ISSUE",
	            "confidence": 0.93,
	            "macro_id": 360008597720
	        },
	        {
	            "macro_title": "WRONG_PRODUCT",
	            "confidence": 0.08,
	            "macro_id": 360008661139
	        },
	        {
	            "macro_title": "OPENING_HOURS",
	            "confidence": 0.07,
	            "macro_id": 360008598900
	        },
	        {
	            "macro_title": "PRODUCT_LAUNCHES",
	            "confidence": 0.06,
	            "macro_id": 360008661339
	        },
	        {
	            "macro_title": "REPAIRS",
	            "confidence": 0.05,
	            "macro_id": 360008661359
	        }
	    ],
	    "suggested_routes": [],
	    "client": "jatana",
	    "suggested_tags": []
	}
```      
