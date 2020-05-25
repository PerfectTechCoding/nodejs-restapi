Step 1 
create a database "crud"

step 2
create a table "users" with fields id(int)(PRIMARY KEY), name(varchar(100)), location(varchar(100))

step 3
create a folder "rest-api" 

step 4 
open the folder in vs code or any code editor

step 5 open terminal
npm init 
npm install --save express mysql body-parser

step 6
npm install -g nodemon
note : if you have already installed the nodemon then skip this step

step 7 
create a new file
index.js

step 8
`const express = require("express");
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
});`

