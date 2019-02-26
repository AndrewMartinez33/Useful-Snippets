#JSON

## Data types that can be used with JSON
---

* Number: no difference between integer and float
* String: string of Unicode characters. Use "DOUBLE" quotes
* Boolean: true or false
* Array: ordered list of 0 or more values
* Object: unordered collection of key/value pairs
* Null: empty value

## Syntax Rules
---

* Uses key/value pairs - {"name" : "Andrew"}
* Uses double quotes around key and value
* Must use data types specified above
* File type is ".json"
* MIME type is "Application/json"

## JSON Example
---
```js

let person = {
  "Name":"Andrew Martinez",
  "Age": 30,
  "Address": {
    "Street": "4100 Road St.",
    "City": "Los Angeles"
  },
  "Children": ["Ethan","Anya"]
}

// turns JS object into a properly formatted JSON object
let jsonObject = JSON.stringify(person);

// turns a JSON object into a JS object
let jsObject = JSON.parse(jsonObject);

```

## JSON file

remember: file type is .json

File: people.json
```json

{
  "people": [
    {
      "Name": "Andrew",
      "Age": 30
    },
    {
      "Name": "Jessica",
      "Age": 31
    },
    {
      "Name": "Jorge",
      "Age": 32
    }
  ]
}

```

## Making a Request to a JSON File

```js

let xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
  if (this.readyState = 4 && this.status == 200) {

    // the response is stored in xhttp.responseText
    // we use JSON.parse() to turn the JSON object into a JS object we can work with.
    let response = JSON.parse(xhttp.responseText);
    
    // Your code here. Do whatever you want with the data
    console.log(response);
  }
};

// we want to make a GET request to a specific json file and send the request
xhttp.open("GET", "jsonFileURL.json", true);
xhttp.send();

```
