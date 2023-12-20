# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

<%@ page language="java" contentType="text/html; charset=ISO-8859-1" pageEncoding="ISO-8859-1"%> <!DOCTYPE html> <html> <head> <meta charset="UTF-8"> <title>Simple JSP</title> </head> <body> <% out.println("<h2>My first JSP page.</h2>"); %> </body> </html>






#  Practice-Project 2
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSP Implicit Objects</title>
</head>
<body>
<%
String responseCheck = request.getParameter("office");
if (responseCheck != null ) {
response.setStatus(response.SC_MOVED_TEMPORARILY);
response.setHeader("Location", "response-redirect.jsp?office=" + 
responseCheck);
}
String errorCheck = request.getParameter("error");
if (errorCheck != null ) {
int x = 0;
if (x == 0)
throw new RuntimeException("Exception has been raised");
}
%>
<%
int serverPort = request.getServerPort() ;
out.println("The Server is running on port " + String.valueOf(serverPort) + 
"<br>");
out.println("Servlet Name is " + config.getServletName() + "<br>");
out.println("Server Info:" + application.getServerInfo() + "<br>");
String pageName = page.toString();
out.println("The name of the page is " + pageName + "<br>");
pageContext.setAttribute("userid", "John Doe");
out.println("userId attribute from pageContext: " + 
pageContext.getAttribute("userid") + 
"<br>"); 
%>
<a href="index.jsp?office=head_office">Show usage of response 
object</a><br>
<a href="index.jsp?error=1">Show usage of error object</a><br>
<%
if (response.containsHeader("Office"))
out.println("Current location is " + response.getHeader("Office"));
%>
</body>
</html>
response-redirect.jsp:
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Get Header Example</title>
</head>
<body>
<%
String office = request.getParameter("office");
if (office != null)
out.println("value of Office obtained :" + office + "<br>");
else
out.println("No value of Office found<br>");
%>
</body>
</html>
Handle-error.jsp :
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Error Handling page</title>
</head>
<body>
<br>
An exception was generated. Details are above:<br>
</body>
</html>



# Practice Project 3

<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%> 
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSP Directives</title>
</head>
<body>
This is content from the main file.
<%@ include file="included.jsp" %>
<hr>
Example of using JSTL taglibs for formatting output<br>
<p>
Currency = <fmt:formatNumber value = "145" type = "currency"/>
<p>
<p>
<c:set var = "now" value = "<%= new java.util.Date()%>" />
Current date and time is <fmt:formatDate pattern = "yyyy-MM-dd hh:mm:ss"
value = 
"${now}" />
</p>
</body>
</html>
Included.jsp:
<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<% out.println("This is content from included file.<br><br>"); %>
</body>
</html>
Web.xml:
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
version="2.5">
<display-name>JSPDirectives</display-name>
<welcome-file-list>
<welcome-file>index.html</welcome-file>
<welcome-file>index.jsp</welcome-file>
<welcome-file>index.htm</welcome-file>
<welcome-file>default.html</welcome-file>
<welcome-file>default.jsp</welcome-file>
<welcome-file>default.htm</welcome-file>
</welcome-file-list>
</web-app>





# practice project : 4

<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>JSP Action Tags</title>
</head>
<body>
Usage of useBean tag<br>
<jsp:useBean id="productBean" class="com.ecommerce.ProductBean"
scope="session"></jsp:useBean>
<jsp:setProperty property="productId" name="productBean" value="18791"/>
<jsp:setProperty property="productName" name="productBean" value="Optical 
Wireless 
Mouse"/>
<jsp:setProperty property="price" name="productBean" value="600.00"/>
<a href="showbean.jsp">Access bean properties from another page</a><br>
<a href="forward.jsp">Use Forward action to go to Google</a><br>
<hr>
<jsp:text>
<![CDATA[This is my content.<br/>This will show within a text action tag 
exactly as it has 
been entered]]>
</jsp:text>
</body>
</html>
Forward.jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<jsp:forward page="forwarded.jsp"></jsp:forward>
Forwarded.jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Forward Test</title>
</head>
<body>
This page came from forward.jsp by using jsp:forward action tag
</body>
</html>
Showbean.jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" 
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Display Bean properties</title>
</head>
<body>
<jsp:useBean id="productBean" class="com.ecommerce.ProductBean"
scope="session"></jsp:useBean>
Product Id: <jsp:getProperty name="productBean" property="productId" />
<br>
Product Name: <jsp:getProperty name="productBean" property="productName" />
<br>
Product Price: <jsp:getProperty name="productBean" property="price" /> <br>
</body>
</html>
ProductBean.java ( Servlet ):
package com.ecommerce;
import java.io.Serializable;
public class ProductBean implements Serializable {
private String productId;
private String productName;
private double price;
public void setProductId(String value) {
this.productId = value;
}
public void setProductName(String value) {
this.productName = value;
}
public void setPrice(double value) {
this.price = value;
}
public String getProductId() {
return this.productId;
}
public String getProductName() {
return this.productName;
}
public double getPrice() {
return this.price;
}
}



# practice project5

Index.jsp:
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>JSP Sessions</title>
</head>
<body>
<%
if (request.getParameter("error") != null)
out.println("<b>Your session has expired or is invalid.</b><br>");
%>
<form action="login.jsp" method="post">
Name <input name="name" id="name" maxlength=40><br>
Password <input type="password" name="pwd" id="pwd" maxlength="10"><br>
<button>Submit</button>
</form>
</body>
</html>
Login.jsp:
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF 8"%>
<%
String name = request.getParameter("name");
String pwd = request.getParameter("pwd");
if (name == null || name.equals("") || pwd == null || pwd.equals("")) {
response.sendRedirect("index.jsp?error=1");
} else {
session.setAttribute("name", name);
response.sendRedirect("dashboard.jsp");
}
%>
Dashboard.jsp:
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Dashboard</title>
</head>
<body>
<%
if (session.getAttribute("name") == null) {
response.sendRedirect("index.jsp?error=1");
}
%>
<b>Hello <%= session.getAttribute("name") %></b><br>
<a href="logout.jsp">Click here to logout</a>
</body>
</html>
Logout.jsp:
<%@ page language="java" contentType="text/html; charset=UTF-8"
pageEncoding="UTF 8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Session Logout</title>
</head>
<body>
<%
session.invalidate();
%>
<b>Your session has terminated.</b><br>
<a href="index.jsp">Login again</a>
</body>
</html>
