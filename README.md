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
