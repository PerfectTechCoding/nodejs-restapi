# REST-API in nodejs
## Step 1 
Create a new database "crud" in phpmyadmin

## Step 2
Create a table "users" with fields id(int)(PRIMARY KEY), name(varchar(100)), location(varchar(100))

## Step 3
Create a folder "rest-api" 

## Step 4 
Open in vs code or any code editor

## Step 5 
Open the terminal
```bash
npm init 
npm install --save express mysql body-parser
```

## Step 6 
```bash
npm install -g nodemon
```
Note : if you have already installed the nodemon then skip this Step

## Step 7 
Create a new file "index.js"

## Step 8
Firstly connect with database
```javascript
const express = require("express");
const bodyParser = require("body-parser");
const app = express();
const mysql = require("mysql");

// parse application/json
app.use(bodyParser.json());

//Create Database Connection
const conn = mysql.createConnection({
	host: "localhost",
	user: "root",
	password: "",
	database: "crud",
});
```
```javascript
//at the bottom of the code
app.listen(8000, () => {
	console.log("server started on port 8000...");
});

```

## Step 9
Write code creating a new record

```javascript
// creat a new Record
app.post("/api/create", (req, res) => {
	let data = { name: req.body.name, location: req.body.location };
	let sql = "INSERT INTO users SET ?";
	let query = conn.query(sql, data, (err, result) => {
		if (err) throw err;
		res.send(JSON.stringify({ status: 200, error: null, response: "New Record is Added successfully" }));
	});
});
```

## Step 10
Write code for view all records
```javascript
// show all records
app.get("/api/view", (req, res) => {
	let sql = "SELECT * FROM users";
	let query = conn.query(sql, (err, result) => {
		if (err) throw err;
		res.send(JSON.stringify({ status: 200, error: null, response: result }));
	});
});

```
## Step 11
Write code for view a single record

```javascript
// show a single record
app.get("/api/view/:id", (req, res) => {
	let sql = "SELECT * FROM users WHERE id=" + req.params.id;
	let query = conn.query(sql, (err, result) => {
		if (err) throw err;
		res.send(JSON.stringify({ status: 200, error: null, response: result }));
	});
});
```

## Step 12
Write code for delete a record
```javascript

// delete the record
app.delete("/api/delete/:id", (req, res) => {
	let sql = "DELETE FROM users WHERE id=" + req.params.id + "";
	let query = conn.query(sql, (err, result) => {
		if (err) throw err;
		res.send(JSON.stringify({ status: 200, error: null, response: "Record deleted successfully" }));
	});
});

```

## Step 13
Write code for update a record
```javascript
// update the Record
app.put("/api/update/", (req, res) => {
	let sql = "UPDATE users SET name='" + req.body.name + "', location='" + req.body.location + "' WHERE id=" + req.body.id;
	let query = conn.query(sql, (err, result) => {
		if (err) throw err;
		res.send(JSON.stringify({ status: 200, error: null, response: "Record updated SuccessFully" }));
	});
});
```

## Step 14 
Start the server
```bash
nodemon index.js
```
