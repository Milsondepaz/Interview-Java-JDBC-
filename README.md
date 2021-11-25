# Java JDBC Interview Questions

## 1- What is JDBC?
JDBC is a Java API that is used to connect and execute the query to the database. JDBC API uses JDBC drivers to connect to the database. JDBC API can be used to access tabular data stored into any relational database.

![image](https://user-images.githubusercontent.com/16039211/143330285-f2d80176-733b-490f-9362-5bf4d8f2aec5.png)


## 2- What is JDBC Driver?
JDBC Driver is a software component that enables Java application to interact with the database. There are 4 types of JDBC drivers:

**JDBC-ODBC bridge driver:** The JDBC-ODBC bridge driver uses the ODBC driver to connect to the database. The JDBC-ODBC bridge driver converts JDBC method calls into the ODBC function calls. This is now discouraged because of the thin driver. It is easy to use and can be easily connected to any database.

**Native-API driver (partially java driver):** The Native API driver uses the client-side libraries of the database. The driver converts JDBC method calls into native calls of the database API. It is not written entirely in Java. Its performance is better than JDBC-ODBC bridge driver. However, the native driver must be installed on each client machine.

**Network Protocol driver (fully java driver):** The Network Protocol driver uses middleware (application server) that converts JDBC calls directly or indirectly into the vendor-specific database protocol. It is entirely written in Java. There is no requirement of the client-side library because of the application server that can perform many tasks like auditing, load balancing, logging, etc.

**Thin driver (fully java driver):** The thin driver converts JDBC calls directly into the vendor-specific database protocol. That is why it is known as the thin driver. It is entirely written in Java language. Its performance is better than all other drivers however these drivers depend upon the database.

## 3- What are the steps to connect to the database in java?
The following steps are used in database connectivity.
- **Registering the driver class:**
The forName() method of the Class class is used to register the driver class. This method is used to load the driver class dynamically. Consider the following example to register OracleDriver class.
```
Class.forName("oracle.jdbc.driver.OracleDriver");
```

- **Creating connection:**
The getConnection() method of DriverManager class is used to establish the connection with the database. The syntax of the getConnection() method is given below.

```
- 1) public static Connection getConnection(String url) throws SQLException  
- 2) public static Connection getConnection(String url,String name,String password)  
throws SQLException
```

Consider the following example to establish the connection with the Oracle database.
```
Connection con=DriverManager.getConnection(  
"jdbc:oracle:thin:@localhost:1521:xe","system","password");  
```

**Creating the statement:**
The createStatement() method of Connection interface is used to create the Statement. The object of the Statement is responsible for executing queries with the database.
```
public Statement createStatement()throws SQLException
```
consider the following example to create the statement object
```
Statement stmt=con.createStatement();  
```

**Executing the queries:**
The executeQuery() method of Statement interface is used to execute queries to the database. This method returns the object of ResultSet that can be used to get all the records of a table.

Syntax of executeQuery() method is given below.
```
public ResultSet executeQuery(String sql)throws SQLException  
```
Example to execute the query
```
ResultSet rs=stmt.executeQuery("select * from emp");  
while(rs.next()){  
System.out.println(rs.getInt(1)+" "+rs.getString(2));  
}  
```
However, to perform the insert and update operations in the database, executeUpdate() method is used which returns the boolean value to indicate the successful completion of the operation.

**Closing connection:**
By closing connection, object statement and ResultSet will be closed automatically. The close() method of Connection interface is used to close the connection.

Syntax of close() method is given below.
```
public void close()throws SQLException  
```
Consider the following example to close the connection.
```
con.close();  
```

## 4- What are the JDBC API components?
The java.sql package contains following interfaces and classes for JDBC API.

**Interfaces:**

- **Connection:** The Connection object is created by using getConnection() method of DriverManager class. DriverManager is the factory for connection.

- **Statement:** The Statement object is created by using createStatement() method of Connection class. The Connection interface is the factory for Statement.

- **PreparedStatement:** The PrepareStatement object is created by using prepareStatement() method of Connection class. It is used to execute the parameterized query.

- **ResultSet:** The object of ResultSet maintains a cursor pointing to a row of a table. Initially, cursor points before the first row. The executeQuery() method of Statement interface returns the ResultSet object.

- **ResultSetMetaData:** The object of ResultSetMetaData interface cotains the information about the data (table) such as numer of columns, column name, column type, etc. The getMetaData() method of ResultSet returns the object of ResultSetMetaData.

- **DatabaseMetaData:** DatabaseMetaData interface provides methods to get metadata of a database such as the database product name, database product version, driver name, name of the total number of tables, the name of the total number of views, etc. The getMetaData() method of Connection interface returns the object of DatabaseMetaData.

- **CallableStatement:** CallableStatement interface is used to call the stored procedures and functions. We can have business logic on the database through the use of stored procedures and functions that will make the performance better because these are precompiled. The prepareCall() method of Connection interface returns the instance of CallableStatement.

**Classes:**

- **DriverManager:** The DriverManager class acts as an interface between the user and drivers. It keeps track of the drivers that are available and handles establishing a connection between a database and the appropriate driver. It contains several methods to keep the interaction between the user and drivers.

- **Blob:** Blob stands for the binary large object. It represents a collection of binary data stored as a single entity in the database management system.

- **Clob:** Clob stands for Character large object. It is a data type that is used by various database management systems to store character files. It is similar to Blob except for the difference that BLOB represent binary data such as images, audio and video files, etc. whereas Clob represents character stream data such as character files, etc.

- **SQLException** It is an Exception class which provides information on database access errors.

## 5- What are the JDBC statements?
In JDBC, Statements are used to send SQL commands to the database and receive data from the database. There are various methods provided by JDBC statements such as execute(), executeUpdate(), executeQuery, etc. which helps you to interact with the database.

There is three type of JDBC statements given in the following table.
| Statements | Explanation |
| ----------- | ----------- |
| Statement | Statement is the factory for resultset. It is used for general purpose access to the database. It executes a static SQL query at runtime. |
| PreparedStatement	| The PreparedStatement is used when we need to provide input parameters to the query at runtime. |
| CallableStatement | CallableStatement is used when we need to access the database stored procedures. It can also accept runtime parameters. |

## 6- What is the return type of Class.forName() method?
The Class.forName() method returns the object of java.lang.Class object.

## 7- What are the differences between Statement and PreparedStatement interface?
| Statements | PreparedStatement |
| ----------- | ----------- |
| The Statement interface provides methods to execute queries with the database. The statement interface is a factory of ResultSet; i.e., it provides the factory method to get the object of ResultSet. | The PreparedStatement interface is a subinterface of Statement. It is used to execute the parameterized query. |
| In the case of Statement, the query is compiled each time we run the program.	| In the case of PreparedStatement, the query is compiled only once. |
| The Statement is mainly used in the case when we need to run the static query at runtime.	| PreparedStatement is used when we need to provide input parameters to the query at runtime. |

## 8- How can we set null value in JDBC PreparedStatement?
By using setNull() method of PreparedStatement interface, we can set the null value to an index. The syntax of the method is given below.
```
void setNull(int parameterIndex, int sqlType) throws SQLException  
```

## 9- What are the benefits of PreparedStatement over Statement?
The benefits of using PreparedStatement over Statement interface is given below.

- The PreparedStatement performs faster as compare to Statement because the Statement needs to be compiled everytime we run the code whereas the PreparedStatement compiled once and then execute only on runtime.
- PreparedStatement can execute Parameterized query whereas Statement can only run static queries.
- The query used in PreparedStatement is appeared to be similar every time. Therefore, the database can reuse the previous access plan whereas, Statement inline the parameters into the String, therefore, the query doesn't appear to be same everytime which prevents cache reusage.

## 10- What are the differences between execute, executeQuery, and executeUpdate?
| execute | executeQuery | executeUpdate |
| ----------- | ----------- | ----------- |
| The execute method can be used for any SQL statements(Select and Update both). | The executeQuery method can be used only with the select statement. | The executeUpdate method can be used to update/delete/insert operations in the database. |
| The execute method returns a boolean type value where true indicates that the ResultSet s returned which can later be extracted and false indicates that the integer or void value is returned.	 | The executeQuery() method returns a ResultSet object which contains the data retrieved by the select statement. | The executeUpdate() method returns an integer value representing the number of records affected where 0 indicates that query returns nothing. |

## 11- What are the different types of ResultSet?
ResultSet is categorized by the direction of the reading head and sensitivity or insensitivity of the result provided by it. There are three general types of ResultSet.
| Type | Description |
| ----------- | ----------- |
| ResultSet.TYPE_Forward_ONLY	| The cursor can move in the forward direction only. |
| ResultSet.TYPE_SCROLL_INSENSITIVE	| The cursor can move in both the direction (forward and backward). The ResultSet is not sensitive to the changes made by the others to the database. |
| ResultSet.TYPE_SCROLL_SENSITIVE	 | The cursor can move in both the direction. The ResultSet is sensitive to the changes made by the others to the database. |

## 12- The cursor can move in both the direction. The ResultSet is sensitive to the changes made by the others to the database.
| ResultSet | RowSet |
| ----------- | ----------- |
| ResultSet cannot be serialized as it maintains the connection with the database. | RowSet is disconnected from the database and can be serialized. |
| ResultSet object is not a JavaBean object | ResultSet Object is a JavaBean object. |
| ResultSet is returned by the executeQuery() method of Statement Interface. | Rowset Interface extends ResultSet Interface and returned by calling the RowSetProvider.newFactory().createJdbcRowSet() method. |
| ResultSet object is non-scrollable and non-updatable by default. | RowSet object is scrollable and updatable by default. |

## 13- How can we execute stored procedures using CallableStatement?
Following are the steps to create and execute stored procedures. Here, we are creating a table user420 by using a stored procedure and inserting values into it.

- **Create the procedure in the database.**
To call the stored procedure, you need to create it in the database. Here, we are assuming that the stored procedure looks like this.
```
create or replace procedure "INSERTR"  
(id IN NUMBER,  
name IN VARCHAR2)  
is  
begin  
insert into user420 values(id,name);  
end;  
/     
The table structure is given below:

create table user420(id number(10), name varchar2(200));  
```

- **Establish a network connection.**
```
Class.forName("oracle.jdbc.driver.OracleDriver");  
Connection con=DriverManager.getConnection(  
"jdbc:oracle:thin:@localhost:1521:xe","system","oracle");  
```

- **Create the Object of CallableStatement.**
```
CallableStatement stmt=con.prepareCall("{call insertR(?,?)}");  
```

- **Provide the values and execute the query by using the following syntax.**
```
stmt.setInt(1,1011);  
stmt.setString(2,"Amit");  
stmt.execute();  
```

- **Check the database; the values will be found there. However, the complete code will look like the following.**
```
import java.sql.*;  
public class Proc {  
public static void main(String[] args) throws Exception{  
  
Class.forName("oracle.jdbc.driver.OracleDriver");  
Connection con=DriverManager.getConnection(  
"jdbc:oracle:thin:@localhost:1521:xe","system","oracle");  
  
CallableStatement stmt=con.prepareCall("{call insertR(?,?)}");  
stmt.setInt(1,1011);  
stmt.setString(2,"Amit");  
stmt.execute();  
  
System.out.println("success");  
}  
}
```
