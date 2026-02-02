# Web-Programming - Exercise 1: Getting Started with PHP

## Task 1: Setting up web Development Environment and creating exercise folders.
1. Set up the web development local environment using the docker compose file. 
2. Create a local repository for individual tasks. Open the `src` folder and create a folder named `phpTasks`
3. Publish your repository to GitHub as a public repo. 

## Task 2: Creating your first PHP file. 

1. In the folder you created, make a new file called `index.php`
2. Write the following PHP code in the file:
```php
<?php
echo "Hello, World!";
?>
```
3. Save the file and open a web browser.
4. Go to localhost:81/yourfolder/index.php (replace your folder with the name of your folder). You should see “Hello, World!” displayed.

## Task 3: Creating ex1.php in the same folder. 

1. In the same folder, make a new file called `ex1.php`
2. Begin by using the HTML Boilerplate to create the initial structure of your HTML document. Make sure to update all the necessary information such as the title (Exercise 1: Getting Started with PHP - YourFirstName) of the page.
2.  Ensure that you use the `<h3>` element to write the titles for all the tasks below.

    1.  Write PHP code to output the following message:

        ```Hello world! My name is "David"```

    2. Create a PHP variable named `$title` and assign it the value "PHP is interesting." Then, use this variable as the content within an `<h4>` (heading 4) element.

    3. Define three variables: `$g1 = 5`, `$g2 = 4`, and `$g3 = 5`. These variables represent the grades of three students in the course. To display this information, create an HTML table within your PHP code. The table should be structured with columns for Serial Number (S.n.), Name, and Grade, and it should look like this:

        | S.n. | Name  | Grade |
        |------|-------|-------|
        | 1    | John  | 5     |
        | 2    | Alice | 4     |
        | 3    | Bob   | 5     |

    5. Take a screenshot that confirms your development environment setup and include it as an image in the "ex1.php" file.

    6. Commit all the changes you've made and push them to your GitHub repository to complete the task.

 
## Task 4: Your codes in shell.hamk.fi 

1. Upload the "phpTasks" folder into `shell.hamk.fi` within the `public_html` directory.
2. Retrieve the link to access `ex1.php` at `http://shell.hamk.fi/~Yourusername/phpTasks/ex1.php`.

## Task 5: Submit the required links

> Please submit both the GitHub link and the shell.hamk.fi link to the "ex1.php" file on Moodle.
