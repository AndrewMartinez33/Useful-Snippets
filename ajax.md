# AJAX

## What is Ajax?
---
* Asynchronous JavaScript And XML
* It is a set of technologies to send and receive data from a client to a server asynchronously
* Does not interfere with the current web page
* JSON has replaced XML for the most part

## XmlHttpRequest (XHR) Object
---
* API in the form of an object, meaning it has properties and methods
* Provided by the browser's JS environment
* Methods transfer data between client and server
* Can be used with protocols other than HTTP
* Can work with data other than XML (JSON, plain text)

## Libraries and Other Methods to Make Ajax Calls
---
* jQuery
* Axios
* Superagent
* Fetch API
* Prototype
* Node HTTP

## Example 1: Ajax Reuest to a Text File
---

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax Request to Text File</title>
</head>
<body>
  <button id="button">Get Text File</button>
  <p id="text"></p>

  <script>
    // create event listener
    document.querySelector('#button').addEventListener('click', loadText);

    function loadText() {
      // Create XHR object
      let xhr = new XMLHttpRequest();
      
      // OPEN - type, url/file name, async
      xhr.open("GET", 'sample.txt', true);

      // this runs at ReadyState 3. It is optional, but can be used for loader, like the rainbow wheel.
      xhr.onprogress = function () {
        console.log('loading...')
      }

      // we an also use xhr.onreadystatechange but then you have to check that this.readyState == 4 && this.status == 200
      xhr.onload = function () {
        // check that the response status is 'OK' before we do anything else.
        if (this.status == 200) {
          // responseText is where the response is stored. In this case, the text in the file.
          document.querySelector('#text').innerHTML = this.responseText;
        }
      }

      // if you are using onload, you can use xhr.onerror to catch errors
      xhr.onerror = function () {
        console.log('Request error...')
      }

      // we need to send to get anything back
      xhr.send();
    }
  </script>
</body>
</html>
```
## Example 2 - Ajax request to a local JSON file
---
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax Request to Local JSON File</title>
</head>
<body>
  <button id="button1">Get User</button>
  <button id="button2">Get Users</button>
  <br />
  <br />
  <h1>User</h1>
  <div id="user"></div>
  <h1>Users</h1>
  <div id="users"></div>

  <script>
    document.querySelector('#button1').addEventListener('click', loadUser);

    document.querySelector('#button2').addEventListener('click', loadUsers);

    function loadUser() {
      let xhr = new XMLHttpRequest();
      xhr.open('GET', 'user.json', true)
      xhr.onload = function () {
        if (this.status == 200) {
          let user = JSON.parse(this.responseText);
          let output = `
          <ul>
            <li>Id: ${user.id}</li>
            <li>Name: ${user.name}</li>
            <li>Email: ${user.email}</li>
          <ul>`;
          document.querySelector('#user').innerHTML = output;
        }
      }
      xhr.send();
    }
    function loadUsers() {
      let xhr = new XMLHttpRequest();
      xhr.open('GET', 'users.json', true)
      xhr.onload = function () {
        if (this.status == 200) {
          let users = JSON.parse(this.responseText);
          let output = '';

          for (let i in users) {
            output += `<ul>
            <li>Id: ${users[i].id}</li>
            <li>Name: ${users[i].name}</li>
            <li>Email: ${users[i].email}</li></ul>`;
          }

          document.querySelector('#users').innerHTML = output;
        }
      }
      xhr.send();
    }
  </script>
</body>
</html>
```

## Example 3 - Ajax request to external API
---

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Ajax Request to External API</title>
</head>
<body>
  <button id="button">Load Github Users</button>
  <br /><br />
  <h1>Github Users</h1>
  <div id="users"></div>

  <script>
    document.querySelector('#button').addEventListener('click', loadUsers);

    function loadUsers() {
      let xhr = new XMLHttpRequest();

      xhr.open('GET', 'https://api.github.com/users', true);

      xhr.onload = function () {
        if (this.status == 200) {
          let users = JSON.parse(this.responseText);
          let output = '';
          for (var i in users) {
            output += `
              <div>
                <img src="${ users[i].avatar_url}  width="70" height="70">
                <ul>
                  <li>Id: ${ users[i].id} </li>
                  <li>Id: ${ users[i].login} </li>
                </ul>
              </div>`;
          }
          document.querySelector('#users').innerHTML = output;
        }
      }
      xhr.send();
    }
  </script>
</body>
</html>
```