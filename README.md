Steps to create a simple web interface to control a bot and display its latest movement using XAMPP and Visual Studio Code (VS Code)
### 1.Set up XAMPP and VS Code:
* Install XAMPP on your system, which includes Apache, MySQL , and other components needed for web development.
* Install VS Code, a popular code editor, on your system.
### 2.Create a new project directory:
* In the htdocs folder of XAMPP, create a new directory for your project.
### 3. Database setup:
* Register XAMMP control panel and we can allow Apache and MySQL modules.
* Within XAMMP, go to Admin to access the MySQL management interface.
* Create a new database, on Control.
  Create the robot_movements table within SQL:
```
CREATE TABLE robot_movements (
id INT AUTO_INCREMENT PRIMARY KEY,
direction VARCHAR(255) NOT NULL
);
```
### 4. Create the control page:
* In VS Code, create a new file named index1.php
* Add the following code to create a simple control interface:
  
```
  <!DOCTYPE html>
<html>
<head>
<title>Welcome to Robot Control🤖</title>
<style>
    .button-container {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 20px;
    }

    .button-container button {
        margin: 0 10px;
        width: 100px;
        height: 100px;
        font-size: 20px;
        background-color: #BB78A7;
        border-radius: 0; /* Changed border-radius to 0 to make the buttons square */
    }
</style>
</head>
 <body>
<h1>Welcome to Robot Control🤖</h1>
<form method="post" action="control1.php">
    <div class="button-container">
        <button name="direction" value="forward">Forward</button>
    </div>
    <div class="button-container">
        <button name="direction" value="left">Left</button>
        <button name="direction" value="stop">Stop</button>
        <button name="direction" value="right">Right</button>
    </div>
    <div class="button-container">
        <button name="direction" value="backward">Backward</button>
    </div>
</form>
</body>
</html>
```

 ### 5. Create the control script:
* In VS Code, create a new file named control1.php in.
* Add the following code to process movement orders and update the database:
* 
```
<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "robot__control";

$conn = new mysqli($servername, $username, $password, $dbname);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $direction = $_POST['direction'];
    $sql = "INSERT INTO robot_movements (direction) VALUES ('$direction')";

    if ($conn->query($sql) === TRUE) {
      echo "Robot movement successfully👏🏻.";
  } else {
      echo "Error: " . $sql . "<br>" . $conn->error;
  }
  } else {
  echo "No 'direction' value submitted in the POST request.";
  }

$conn->close();
?>
```
### 6. Create the last page:
* In VS Code, create a new file named last value.php .
* Add the following code to retrieve the last recorded movement direction from the database and display it:
```
<!DOCTYPE html>
<html>
<head>
<title> Robot Movement</title>
<style>
  .movement-circle {
      width: 100px;
      height: 100px;
      background-color: #BB78A7;
      border-radius: 0; /* Changed border-radius to 0 to make the button square */
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 24px;
      font-weight: bold;
      color: #333;
      margin: 50px auto;
      border:1px solid black;
  }
  .back-link {
      display: block;
      text-align: center;
      margin-top: 20px;
  }
  .back-button {
      display: block;
      background-color: #BB78A7;
      color: #333;
      text-decoration: none;
      padding: 10px 20px;
      border-radius: 5px;
      margin: 20px auto;
      width: fit-content;
      font-size: 18px;
  }
</style>
</head>
<body>
<h1> Here is the last value🤖 </h1>
<div class="movement-circle">
  <?php
  $servername = "localhost";
  $username = "root";
  $password = "";
  $dbname = "robot__control";

  $conn = new mysqli($servername, $username, $password, $dbname);

  if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
  }

  $sql = "SELECT direction FROM robot_movements ORDER BY id DESC LIMIT 1";
  $result = $conn->query($sql);

  if ($result->num_rows > 0) {
      $row = $result->fetch_assoc();
      $lastDirection = $row["direction"];
      echo $lastDirection;}
   else {
      echo "No data";
  }

  $conn->close();
  ?>
</div>
<a href="index1.php" class="back-button">Return to the home page👉🏻</a>
</body>
</html>
```
### Web-based control interface:
![لقطة شاشة 2024-07-08 103933](https://github.com/Ohood-Saleh2003/my-project/assets/173670281/52666402-41fc-41dd-a56e-a37bf2b61740)

### Database interation:
![لقطة شاشة 2024-07-08 045619](https://github.com/Ohood-Saleh2003/my-project/assets/173670281/ddd2598e-45c0-43dd-ace8-604831e28d8c)

### Last movement dirction:
![لقطة شاشة 2024-07-08 104243](https://github.com/Ohood-Saleh2003/my-project/assets/173670281/ee299cf5-2ab8-4e47-99e3-8c3b41e6677c)


