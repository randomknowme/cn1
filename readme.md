https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER

1.

<!DOCTYPE html>
<html>
<head>
    <title>Product Table</title>
</head>
<body>

<h2>Product List</h2>

<table border="1" id="productTable">
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Price</th>
        </tr>
    </thead>
    <tbody></tbody>
</table>

<script>
    // JSON array
    const products = [
        { id: 1, name: "Laptop", price: 50000 },
        { id: 2, name: "Mobile", price: 20000 },
        { id: 3, name: "Headphones", price: 2000 }
    ];

    const tableBody = document.querySelector("#productTable tbody");

    products.forEach(product => {
        let row = `<tr>
            <td>${product.id}</td>
            <td>${product.name}</td>
            <td>${product.price}</td>
        </tr>`;
        tableBody.innerHTML += row;
    });
</script>

</body>
</html>



2.

<form action="LoginServlet" method="post">
    Username: <input type="text" name="username"><br>
    Password: <input type="password" name="password"><br>
    <input type="submit" value="Login">
</form>



import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        String user = request.getParameter("username");
        String pass = request.getParameter("password");

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        if(user.equals("admin") && pass.equals("1234")) {
            out.println("<h2>Login Successful</h2>");
        } else {
            out.println("<h2>Invalid Username or Password</h2>");
        }
    }
}





3.

<%@ page import="java.sql.*" %>
<html>
<body>

<h2>Employee Records</h2>

<table border="1">
<tr>
    <th>ID</th>
    <th>Name</th>
    <th>Salary</th>
</tr>

<%
    try {
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection con = DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/testdb", "root", "password");

        Statement stmt = con.createStatement();
        ResultSet rs = stmt.executeQuery("SELECT * FROM employee");

        while(rs.next()) {
%>
<tr>
    <td><%= rs.getInt("id") %></td>
    <td><%= rs.getString("name") %></td>
    <td><%= rs.getDouble("salary") %></td>
</tr>
<%
        }
        con.close();
    } catch(Exception e) {
        out.println(e);
    }
%>

</table>
</body>
</html>






4.

<!DOCTYPE html>
<html ng-app="myApp">
<head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
</head>

<body ng-controller="myCtrl">

<form name="regForm" novalidate>

    Name:
    <input type="text" name="name" ng-model="user.name" required>
    <span style="color:red" ng-show="regForm.name.$touched && regForm.name.$invalid">
        Name is required
    </span>
    <br><br>

    Email:
    <input type="email" name="email" ng-model="user.email" required>
    <span style="color:red" ng-show="regForm.email.$touched && regForm.email.$invalid">
        Valid email required
    </span>
    <br><br>

    Password:
    <input type="password" name="password" ng-model="user.password" required>
    <span style="color:red" ng-show="regForm.password.$touched && regForm.password.$invalid">
        Password is required
    </span>
    <br><br>

    <button ng-disabled="regForm.$invalid">Register</button>

</form>

<script>
    var app = angular.module("myApp", []);
    app.controller("myCtrl", function($scope) {});
</script>

</body>
</html>



# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
