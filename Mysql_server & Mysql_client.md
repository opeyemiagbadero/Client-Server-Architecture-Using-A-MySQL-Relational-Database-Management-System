I spun up two ubuntu servers (EC2 instances in AWS). 
Server 1: Mysql_server and Server 2:Mysql_client.

![1](https://user-images.githubusercontent.com/79456052/176446822-6577205e-2dd9-4c50-aaaf-c3ca80337dd8.png)

Installed mysql server software on Server A using the command *$ sudo apt install mysql-server -y* and mysql client on Server B using the command *$sudo apt install mysql-client -y* after carrying out an update and ugrade on both servers.

![2](https://user-images.githubusercontent.com/79456052/176447734-7756dda3-e4ff-49d1-a567-e514f073b1eb.png)

![3  3  Install mysql server on Server A and mysql client on server B](https://user-images.githubusercontent.com/79456052/176447857-7bc31038-9e11-428f-95d7-c66ab4dd30d8.png)

Confirmed the installation of mysql on server A by logging into mysql as the root user.

![4  confirm the installation of my sql on server A](https://user-images.githubusercontent.com/79456052/176448190-137bcc83-7a17-42f9-9463-85b1e73aee48.png)

Since MySQL server uses TCP port 3306 by default, I opened up the port by creating a new entry in ‘Inbound rules’ in ‘mysql server' security groups, such that access to 'mysql server' was only restricted to the local ip address of my 'mysql client'
 
![5  include the  private ip address of the client on the SG of server A for port 3306](https://user-images.githubusercontent.com/79456052/176448694-31c3efe8-fe9f-4218-a8db-53144a22aa86.png)

I set a password for the root user of mysql server using mysql_native_password as default authentication method  (user's password was PassWord.1) and ran a security script that comes pre-installed with MySQL which removes some insecure default settings and locks down access to the database system.

![7  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord 1 sudo mysql_secure_installation](https://user-images.githubusercontent.com/79456052/176453616-25ff5733-e8d6-4c34-969a-b8629a150a7e.png)

Created a 'remote_user' ( with a password) and a test database (test_db) on my mysql server to test the connectivity of the database from 'mysql client' using the client's private ip address.

![8  create a user on the mysql database](https://user-images.githubusercontent.com/79456052/176455961-8ee0d4a9-0485-493b-9219-e96e6570349e.png)

Configured MySQL server to allow connections from remote hosts by replacing ‘127.0.0.1’ to ‘0.0.0.0’ of the bind address on mysqld.cnf file *sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf* and saved the file.

![9  configure MySQL server to allow connections from remote hosts and restart the service](https://user-images.githubusercontent.com/79456052/176456860-224faf23-b047-46d1-a5d4-15ca70810e8e.png)


From 'mysql client' server,  I  connected remotely to mysql server database engine without using ssh, but the command *sudo mysql -u remote_user -h <mysql_client private ip address> -p* I succesfully logged into my_sql servers database server from my client and accessd the remote_user and the test database test_db 


![10  From mysql client Linux Server connect remotely to mysql server Database Engine without using SSH  You must use the mysql utility to perform this action   Show databases afterwards](https://user-images.githubusercontent.com/79456052/176457402-36b34a57-9a21-41c5-bac8-48a961ae29b1.png)

![11  last slide](https://user-images.githubusercontent.com/79456052/176458439-4115b77a-66d3-4bb8-8e36-fbf95b3a4aab.png)








