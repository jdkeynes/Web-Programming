# Exercise 7: CRUD APP

To understand the concept of CRUD, we will create a simple PHP application that demonstrates the fundamental operations of CRUD (Create, Read, Update, Delete) using a MySQL database. 

## Create Data

### Step 1: Database Setup

To get started with our CRUD application, you can use your existing MySQL database or create a new one. You can create a new database using various tools like phpMyAdmin, MySQL Workbench, or the MySQL command line.

For this example, we will create a database named `crud_app`.

### Step 2: Create a Table(s)
**Step 2: Create Tables**

To store data for your application, you'll need to create the necessary tables in your database. In this example, we'll create a table named `studentsinfo` to store the data. Here's the table structure:

```sql
CREATE TABLE studentsinfo (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    groupId VARCHAR(50) NOT NULL,
    city VARCHAR(50) NOT NULL,
);
```

### Step 3: Create the HTML Interface

To facilitate user interaction with CRUD operations, you'll need to create an HTML interface. This interface allows users to interact with your application and to create, read, update, and delete records within the database.

For the purpose of this example, we will create a form that collects data from end-users and stores it in the database.

```html
<h2>Input Your Information Below:</h2>
<form name="form1" method="post" action="">
    <div class="form-group">
        <div class="row">
            <div class="col">
                <label for="fname">First Name:</label>
                <input type="text" class="form-control" id="fname" placeholder="Enter your first name" name="fname" required>
            </div>
            <div class="col">
                <label for="lname">Last Name:</label>
                <input type="text" class="form-control" id="lname" placeholder="Enter your last name" name="lname" required>
            </div>
        </div>
    </div>
    <div class="form-group">
        <div class="row">
            <div class="col">
                <label for="city">City:</label>
                <input type="text" class="form-control" id="city" placeholder="Enter your city" name="city" required>
            </div>
            <div class="col">
                <label for="groupid">Group ID:</label>
                <select class="form-control" id="groupid" name="groupid">
                    <option value="BBCAP19">BBCAP19</option>
                    <option value="BBCAP20">BBCAP20</option>
                    <option value="BBCAP21">BBCAP21</option>
                    <option value="BBCAP22">BBCAP22</option>
                    <option value="Others">Others</option>
                </select>
            </div>
        </div>
    </div>
    <button type="submit" class="btn btn-primary" name="submit">Submit</button>
</form>
```

### Step 4: Database Configuration (db.php)

In order to store your database configuration in a centralized and reusable manner, you should create a dedicated file for this purpose. Let's name this file `db.php` and include the following content:

```php
<?php
$servername = "your_servername"; // Replace with your MySQL server hostname
$username = "your_username";     // Replace with your MySQL username
$password = "your_password";     // Replace with your MySQL password
$dbname = "your_database";       // Replace with the name of your MySQL database

// Create a database connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```
### Step 5: Process the Form Data and Insert into MySQL (process.php)

To handle the data submitted through the form and insert it into the MySQL database, we'll create  `process.php`. This script will execute when a user clicks the "Submit" button on the form.

```php
<?php
// Check if the 'submit' button in the form was clicked
if (isset($_POST['submit'])) {
    // Retrieve data from the form and store it in variables
    $fname = $_POST['fname'];     // First name
    $lname = $_POST['lname'];     // Last name
    $city = $_POST['city'];       // City
    $groupid = $_POST['groupid']; // Group ID

    // Include the database connection file
    include 'db.php';

    // Define an SQL query to insert data into the 'studentsinfo' table
    $sql = "INSERT INTO studentsinfo (fname, lname, city, groupid)
            VALUES ('$fname', '$lname', '$city', '$groupid')";

    // Execute the SQL query using the database connection
    if ($conn->query($sql) === TRUE) {
        // If the query was successful, display a success message
        echo "New record added";
    } else {
        // If there was an error in the query, display an error message
        echo "Error: " . $sql . "<br>" . $conn->error;
    }

    // Close the database connection
    $conn->close();
}
?>

```

## Read Data 

Let's learn the process of retrieving and displaying data from a database table. 

### Step 1: Establish a Database Connection

You should establish a database connection using PHP's mysqli or PDO extension. Since you've already created a connection in your code (in the 'db.php' file), you can continue using the same file.

### Step 2: Write SQL query 

You will then write an SQL query to fetch the data you need from the database table & execute the SQL query. 

### Step 3: Fetch & Display Data

You'll then loop through the result set and present the data as required. Using an HTML table is a common and organized way to display the retrieved data.

```php
<?php
include 'db.php';
// SQL query to retrieve data from the 'studentsinfo' table
$sql = "SELECT * FROM studentsinfo";

// Execute the SQL query and store the result
$result = $conn->query($sql);

// Check if there are any results
if ($result->num_rows > 0) {
    echo "<table class='table'>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>First Name</th>
                    <th>Last Name</th>
                    <th>City</th>
                    <th>Group ID</th>
                </tr>
            </thead>
            <tbody>";

    // Loop through the result set and display data in rows
    while ($row = $result->fetch_assoc()) {
        echo "<tr>
                <td>{$row['id']}</td>
                <td>{$row['first_name']}</td>
                <td>{$row['last_name']}</td>
                <td>{$row['city']}</td>
                <td>{$row['groupId']}</td>
              </tr>";
    }

    echo "</tbody></table>";
} else {
    // Display a message if no results are found
    echo "No results";
}
// close the connection when done
$conn->close();
?>

```
## Update & Delete Data 

Data updates are crucial for maintaining accurate and up-to-date records. Consider an example where you're responsible for managing a customer database for an e-commerce website. In this dynamic environment, customers often need to update their contact details, shipping addresses, or preferences as their circumstances change. Without the capability to update data, you risk retaining outdated or incorrect information, which can result in shipping errors &  communication challenges. 

### Step 1: Create PHP script to handle the data update. 

- You can create a new file such as `update_info.php` to handle the data update. In this case, we will instead add a link to each record in `read.php` that allows to update the specific record.

- You are required to  establish a database connection. Once again, you can use the same `db.php` file that was created above. 

### Step 2: Use HTML form to collect the data you want to update. 

- You can add update links to individual records in the `read.php` file where data is displayed.
- To achieve this, you will create a link within the 'Id' column for each record.

```html
<a href='updatesingle.php?id=$row[id]'>$row[id]</a>
```

### Step 3: Create a `updatesingle.php` file

- In the `updatesingle.php` script, retrieve the input data  and construct an SQL UPDATE query to update the required information in the database. 

```php
<?php
include 'db.php';
$a = $_GET['id'];
$result = mysqli_query($conn,"SELECT * FROM studentsinfo WHERE id= '$a'");
$row= mysqli_fetch_array($result);
?>
<h2> Update your information below: </h2>
<form name= "form1" method="post" action="">
  <div class="row">
    <div class="col">
      <input type="text" class="form-control" placeholder="First name" name="fname" required value="<?php echo $row['first_name']; ?>">
    </div>
    <div class="col">
      <input type="text" class="form-control" placeholder="Last name" name="lname" required value="<?php echo $row['last_name']; ?>" >
    </div>
  </div>
  <br>
  <div class="row">
    <div class="col">
      <input type="text" class="form-control" placeholder="City" name="city" required value="<?php echo $row['city']; ?>">
    </div>

    <div class="col">
      <input type="text" class="form-control" placeholder="City" name="city" required value="<?php echo $row['groupId']; ?>">    
    </div>

  </div>
<br>
  <div class="row">
  <div class="col"><button type="submit" class="btn btn-primary" name="submit">Update your Information</button></div>
  <div class="col"><button type="submit" class="btn btn-primary" name="delete">Delete your Information</button></div>
</div>
</form>
<?php 
/* 
The isset() function is used to check if a variable is set and not NULL.
 In this case, it's checking if the $_POST['submit'] 
value is set and not NULL. If the form has been submitted, the value of $_POST['submit'] will be set,
and the code inside the if block will be executed. If the form has not been submitted, 
the value of $_POST['submit'] will not be set, and the code inside the if block will not be executed.
*/
if (isset($_POST['submit'])){
    
    $fname = $_POST['fname'];
    $lname = $_POST['lname'];
    $query = mysqli_query($conn,"UPDATE studentsinfo set first_name='$fname', last_name='$lname' where id='$a'");
    if($query){
        echo "<h2>Your information is updated Successfully</h2>";
        // if you want to redirect to update page after updating
    }
    else { echo "Record Not modified";}
    }

    if (isset($_POST['delete'])){
        $query = mysqli_query($conn,"DELETE FROM studentsinfo where id='$a'");
        if($query){
            echo "Record Deleted with id: $a <br>";
            // if you want to redirect to update page after updating
            //header("location: update.php");
        }
        else { echo "Record Not Deleted";}
        }

$conn->close();

?>

```

# Perform the same task on shell.hamk.fi

We will now learn to move this app from local development environment to shell.hamk.fi. 

 phpMyAdmin (shell.hamk.fi): http://shell.hamk.fi/pma
