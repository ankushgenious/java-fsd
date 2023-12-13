# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

<!DOCTYPE html>
<html>
<head>
    <title>GET vs POST Example</title>
</head>
<body>
    <form action="MyServlet" method="get">
        <label for="data">Enter Data (GET):</label>
        <input type="text" id="data" name="data" required>
        <input type="submit" value="Submit">
    </form>

    <form action="MyServlet" method="post">
        <label for="data">Enter Data (POST):</label>
        <input type="text" id="data" name="data" required>
        <input type="submit" value="Submit">
    </form>
</body>
</html>


Create MyServlet.Java

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Get data from the request
        String data = request.getParameter("data");

        // Display data on the server side (for demonstration purposes)
        response.getWriter().println("GET Method - Data: " + data);
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Get data from the request
        String data = request.getParameter("data");

        // Display data on the server side (for demonstration purposes)
        response.getWriter().println("POST Method - Data: " + data);
    }
}






#  Practice-Project 2
package com.example;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Your servlet logic for handling GET requests
        response.getWriter().println("Hello from MyServlet (GET)");
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Your servlet logic for handling POST requests
        response.getWriter().println("Hello from MyServlet (POST)");
    }
}




# Practice Project 3

import java.io.IOException;
import javax.servlet.GenericServlet;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class MyGenericServlet extends GenericServlet {
    private static final long serialVersionUID = 1L;

    @Override
    public void service(ServletRequest request, ServletResponse response)
            throws ServletException, IOException {
        // Process the request and generate a response
        response.setContentType("text/html");
        response.getWriter().println("<html><body>");
        response.getWriter().println("<h2>Hello from MyGenericServlet!</h2>");
        response.getWriter().println("</body></html>");
    }
}


xml


<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>MyGenericServlet</servlet-name>
        <servlet-class>com.example.MyGenericServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>MyGenericServlet</servlet-name>
        <url-pattern>/myGenericServlet</url-pattern>
    </servlet-mapping>

</web-app>





# practice project : 4

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/MyServlet")
public class MyServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Process GET request
        response.setContentType("text/html");
        response.getWriter().println("<html><body>");
        response.getWriter().println("<h2>Hello from MyServlet (GET)!</h2>");
        response.getWriter().println("</body></html>");
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Process POST request
        response.setContentType("text/html");
        response.getWriter().println("<html><body>");
        response.getWriter().println("<h2>Hello from MyServlet (POST)!</h2>");
        response.getWriter().println("</body></html>");
    }
}

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http

   <servlet>
       <servlet-name>MyServlet</servlet-name>
       <servlet-class>com.example.MyServlet</servlet-class>
   </servlet>

   <servlet-mapping>
       <servlet-name>MyServlet</servlet-name>
       <url-pattern>/MyServlet</url-pattern>
   </servlet-mapping>






#practice project5


import java.io.IOException;
import javax.servlet.Filter;
import javax.servlet.FilterChain;
import javax.servlet.FilterConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;

public class LoggingFilter implements Filter {

    public void init(FilterConfig config) throws ServletException {
        // Initialization code, if needed
    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // Log information about the request
        System.out.println("LoggingFilter: Request received for " + request.getLocalAddr());

        // Pass the request and response to the next filter in the chain
        chain.doFilter(request, response);

        // Log information about the response
        System.out.println("LoggingFilter: Response sent for " + request.getLocalAddr());
    }

    public void destroy() {
        // Cleanup code, if needed
    }
}

web.xml file

<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <filter>
        <filter-name>LoggingFilter</filter-name>
        <filter-class>com.example.LoggingFilter</filter-class>
    </filter>

    <filter-mapping>
        <filter-name>LoggingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <!-- Other servlet and filter configurations go here -->

</web-app>



 # parctice project 6

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/SessionTrackingServlet")
public class SessionTrackingServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Retrieve the session object
        HttpSession session = request.getSession(true);

        // Get or create a session attribute
        Integer visitCount = (Integer) session.getAttribute("visitCount");
        if (visitCount == null) {
            visitCount = 1;
        } else {
            visitCount++;
        }

        // Update the session attribute
        session.setAttribute("visitCount", visitCount);

        // Create a cookie to store the visit count
        Cookie visitCountCookie = new Cookie("visitCountCookie", String.valueOf(visitCount));
        visitCountCookie.setMaxAge(3600); // Cookie will persist for 1 hour
        response.addCookie(visitCountCookie);

        // Set response content type
        response.setContentType("text/html");

        // Write the response
        PrintWriter out = response.getWriter();
        out.println("<html><head><title>Session Tracking Example</title></head><body>");
        out.println("<h2>Session Tracking Example</h2>");
        out.println("<p>Session ID: " + session.getId() + "</p>");
        out.println("<p>Visit Count (Session Attribute): " + visitCount + "</p>");
        out.println("<p>Visit Count (Cookie): " + visitCountCookie.getValue() + "</p>");
        out.println("</body></html>");
    }
}



# practice project7

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/SessionTrackingURLRewriteServlet")
public class SessionTrackingURLRewriteServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Retrieve the session object
        HttpSession session = request.getSession(true);

        // Get or create a session attribute
        Integer visitCount = (Integer) session.getAttribute("visitCount");
        if (visitCount == null) {
            visitCount = 1;
        } else {
            visitCount++;
        }

        // Update the session attribute
        session.setAttribute("visitCount", visitCount);

        // Append the session ID to the URL
        String urlWithSessionId = response.encodeURL("SessionTrackingURLRewriteServlet");

        // Set response content type
        response.setContentType("text/html");

        // Write the response
        PrintWriter out = response.getWriter();
        out.println("<html><head><title>Session Tracking URL Rewrite Example</title></head><body>");
        out.println("<h2>Session Tracking URL Rewrite Example</h2>");
        out.println("<p>Session ID: " + session.getId() + "</p>");
        out.println("<p>Visit Count: " + visitCount + "</p>");
        out.println("<p><a href=\"" + urlWithSessionId + "\">Reload with Session ID</a></p>");
        out.println("</body></html>");
    }
}



 # practice project 8

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/SessionTrackingHiddenFieldServlet")
public class SessionTrackingHiddenFieldServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Retrieve the session object
        HttpSession session = request.getSession(true);

        // Get or create a session attribute
        Integer visitCount = (Integer) session.getAttribute("visitCount");
        if (visitCount == null) {
            visitCount = 1;
        } else {
            visitCount++;
        }

        // Update the session attribute
        session.setAttribute("visitCount", visitCount);

        // Set response content type
        response.setContentType("text/html");

        // Write the response
        PrintWriter out = response.getWriter();
        out.println("<html><head><title>Session Tracking Hidden Field Example</title></head><body>");
        out.println("<h2>Session Tracking Hidden Field Example</h2>");
        out.println("<form action=\"SessionTrackingHiddenFieldServlet\" method=\"post\">");
        out.println("  <input type=\"hidden\" name=\"sessionID\" value=\"" + session.getId() + "\">");
        out.println("  <p>Session ID: " + session.getId() + "</p>");
        out.println("  <p>Visit Count: " + visitCount + "</p>");
        out.println("  <input type=\"submit\" value=\"Reload\">");
        out.println("</form>");
        out.println("</body></html>");
    }

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Process the post request, if needed
        doGet(request, response);
    }
}



# practice project 9

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/SessionTrackingHttpSessionServlet")
public class SessionTrackingHttpSessionServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Retrieve the session object
        HttpSession session = request.getSession(true);

        // Get or create a session attribute
        Integer visitCount = (Integer) session.getAttribute("visitCount");
        if (visitCount == null) {
            visitCount = 1;
        } else {
            visitCount++;
        }

        // Update the session attribute
        session.setAttribute("visitCount", visitCount);

        // Set response content type
        response.setContentType("text/html");

        // Write the response
        PrintWriter out = response.getWriter();
        out.println("<html><head><title>Session Tracking HttpSession Example</title></head><body>");
        out.println("<h2>Session Tracking HttpSession Example</h2>");
        out.println("<p>Session ID: " + session.getId() + "</p>");
        out.println("<p>Visit Count: " + visitCount + "</p>");
        out.println("<a href=\"SessionTrackingHttpSessionServlet\">Reload</a>");
        out.println("</body></html>");
    }
}

# practice project 10


import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/LoginServlet")
public class LoginServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Get the username and password from the login form
        String username = request.getParameter("username");
        String password = request.getParameter("password");

        // In a real application, you would validate the username and password against a database
        // For simplicity, let's use a hardcoded username and password
        if ("demo".equals(username) && "password".equals(password)) {
            // Create a session and store the username as a session attribute
            HttpSession session = request.getSession(true);
            session.setAttribute("username", username);

            // Redirect to the home page after successful login
            response.sendRedirect("home.jsp");
        } else {
            // Display an error message if login fails
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<html><head><title>Login Failed</title></head><body>");
            out.println("<h2>Login Failed. Please check your username and password.</h2>");
            out.println("<a href=\"login.jsp\">Back to Login</a>");
            out.println("</body></html>");
        }
    }
}


logout servlet


import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

@WebServlet("/LogoutServlet")
public class LogoutServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        // Invalidate the session on logout
        HttpSession session = request.getSession(false);
        if (session != null) {
            session.invalidate();
        }

        // Redirect to the login page after logout
        response.sendRedirect("login.jsp");
    }
}



 


 
