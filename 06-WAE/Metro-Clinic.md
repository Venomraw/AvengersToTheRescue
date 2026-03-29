**Metro Clinic Notes**

This task is a web security audit of the Metro Clinic medical directory system. The goal is to figure out how the website's search function is open to SQL injection attacks and then utilize that weakness to get the information needed to answer the challenge questions. The activity is exclusively for HTTPS; we shouldn't try any other ports or use brute-force tactics. This challenge shows how unsafe it is to handle user input in a database query, which can put sensitive records at risk.

To complete this task, we need a web browser, the website's search bar, and some basic knowledge of SQL. The search bar is the most important tool for this task. Browser Developer Tools can also help us see mistakes or figure out how the site works. The tutorial says that the site uses SQL queries on the backend, but it's still vital to know some basic SQL terms like SELECT, WHERE, and LIKE in order to answer the questions in this challenge.

Steps to answer the questions and solve the challenge

1.  **Open the challenge website** in a separate browser window so you can work more easily and reduce confusion while testing the site.
2.  **Test the search bar with simple inputs,** such as a or a **blank space,** to understand how the search function behaves.
3.  **Enter a letter “p”** in the search bar and press **Search**. This should return the full directory of medical professionals.
4.  **Review the full directory results** to answer the first three questions:
    1.  Find the name of the **only Orthopedist**.
    2.  Find **Katie Cain** and identify her profession.
    3.  Count the **total number of medical professionals** listed in the registry.
5.  **Move to the SQL injection portion** for Questions 4 and 5 after finishing the first three questions.
6.  Understand that the website likely uses a query similar to:  
    SELECT name, \[type\] FROM users WHERE name LIKE "%search%"  
    This means the search input is directly inserted into the SQL statement.
7.  **Enter the payload** below into the search bar exactly as shown:  
    1"; SELECT \* FROM USERS WHERE "%"="
8.  This payload will:
    1.  End the original SQL query.
    2.  Start a new query on the users table.
    3.  Return all columns, including hidden fields such as usernames and passwords.
9.  **Check the new results carefully** after running the payload.
10.  Use the returned data to answer the last two questions:
11.  Find the person whose password is **greyblob**.
12.  Find **Mike Torres** and identify his password.
13.  **Also, keep an eye** that some passwords may be randomly generated, so your result for Mike Torres’s password may be different from someone else’s.

Conclusion

In general, this challenge shows how SQL injection can be used to get at private database content through a weakly secured search function. All five questions have been answered systematically by first utilizing normal search behavior and then employing the SQL injection payload.