# Excpetion Handling
```Python
try:
	getfile = open("myfile", "r")
	getfile.write("My file for exception handling.")
except IOError:
	print("Unable to open or read the data in the file.")
else:
	print("The file was writeen successfully!")
finally:
	getfile.close()
```

# APIs
An **Application Program Interface** (API) lets two pieces of software talk to each other via inputs and outputs.

## REST APIs
* REST APIs are used to interact with web services, i.e., Applications that you call through the Internet.
* They have a set of Rules regarding:
	1. Communication
	2. Input of request
	3. Output or Response

## HTTP Protocol

#### HTTP Methods

| HTTP METHODS | Description |
|-------------|----------|
| GET | Retrieves data from the server |
| POST | Submits data to server|
| PUT | Updates data already on server |
| DELETE | Deletes data from server|


**Requests** (`import requests`) is a python library that allows you to send HTTP/1.1 requests easily.

**Webscraping** is a process that can be used to automatically extract information from a website.

**Reading JSON Files**
```Python
import json
with open('filesample.json', 'r') as openfile
	json_object = json.load(openfile)
print(json_object)
```










