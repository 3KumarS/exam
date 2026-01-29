EXPERIMENT 2: HTML5 Page Creation

Code (index.html)
<!DOCTYPE html>
<html>
<head>
  <title>My HTML5 Page</title>
</head>
<body>

<h1>Welcome to My Website</h1>
<p>This is a simple HTML5 page.</p>

<img src="https://via.placeholder.com/150" alt="Sample Image">

<h3>My Skills</h3>
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<a href="https://www.google.com">Visit Google</a>

<h2>Contact Us</h2>
<form>
  Name: <input type="text"><br><br>
  Email: <input type="email"><br><br>
  Message:<br>
  <textarea></textarea><br><br>
  <input type="submit">
</form>

</body>
</html>
---------------------------
EXPERIMENT 3: Node.js FS Module (Read, Write, Close)
Code (fs_demo.js)
const fs = require('fs');

// Write file
fs.writeFileSync('demo.txt', 'Hello MCA Student');

// Read file
const data = fs.readFileSync('demo.txt', 'utf8');
console.log(data);

// Open & close file
const fd = fs.openSync('demo.txt', 'r');
console.log("File opened");
fs.closeSync(fd);
console.log("File closed");

--------------------------------
EXPERIMENT 4: PHP Insert & Display Data
Database Table
CREATE TABLE student (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50),
  email VARCHAR(50)
);

insert.php
<?php
$conn = mysqli_connect("localhost","root","","test");

mysqli_query($conn,
"INSERT INTO student(name,email) VALUES('Rohan','rohan@gmail.com')");

$result = mysqli_query($conn,"SELECT * FROM student");

echo "<table border='1'>
<tr><th>ID</th><th>Name</th><th>Email</th></tr>";

while($row = mysqli_fetch_assoc($result)) {
  echo "<tr>
        <td>{$row['id']}</td>
        <td>{$row['name']}</td>
        <td>{$row['email']}</td>
        </tr>";
}
echo "</table>";
?>
------------------------------------
EXPERIMENT 5: Two Tables (student & dept)
SQL
>>
CREATE TABLE dept (
  dept_id INT,
  dept_name VARCHAR(50)
);

PHP (display both)
>>
$result1 = mysqli_query($conn,"SELECT * FROM student");
$result2 = mysqli_query($conn,"SELECT * FROM dept");

--------------------------------------
EXPERIMENT 6: Country DB & City Table
SQL
>>
CREATE DATABASE country;
USE country;

CREATE TABLE city (
  cityname VARCHAR(50),
  area INT,
  population INT
);

HTML Form
>>
<form action="insert.php" method="post">
City: <input name="city"><br>
Area: <input name="area"><br>
Population: <input name="pop"><br>
<input type="submit">
</form>

insert.php
>>
$conn = mysqli_connect("localhost","root","","country");
mysqli_query($conn,
"INSERT INTO city VALUES('$_POST[city]',$_POST[area],$_POST[pop])");

----------------------------------------
EXPERIMENT 7: React Component Life Cycle
class Demo extends React.Component {
  constructor() {
    super();
    console.log("Constructor");
  }

  componentDidMount() {
    console.log("Component Mounted");
  }

  render() {
    return <h1>Hello</h1>;
  }
}
----------------------------------
EXPERIMENT 8: Light / Dark Mode (useState)

import { useState } from "react";

function Theme() {
  const [dark, setDark] = useState(false);

  return (
    <div style={{background: dark ? "black" : "white", color: dark ? "white" : "black"}}>
      <button onClick={() => setDark(!dark)}>Toggle</button>
    </div>
  );
}

export default Theme;

---------------------------------
EXPERIMENT 9: Change Document Title

import { useState, useEffect } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]);

  return <button onClick={() => setCount(count + 1)}>Click</button>;
}

-----------------------------------------
EXPERIMENT 10: Multilingual App (useContext)

import { createContext, useContext } from "react";

const LangContext = createContext();

function App() {
  return (
    <LangContext.Provider value="Hello">
      <Child />
    </LangContext.Provider>
  );
}

function Child() {
  const text = useContext(LangContext);
  return <h1>{text}</h1>;
}
