# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

Step 1: Create a Spring Boot Project
Open IntelliJ IDEA.
Click on "Create New Project."
Choose "Spring Initializr" as the project type.
Set the project name, location, and base package.
Select the desired options (Java, Spring Boot version, packaging type, etc.).
Add the "Spring Web" dependency.
Click "Next" and then "Finish."

Step 2: Write a Simple Controller

// src/main/java/com/example/demo/controller/HelloController.java

package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}


Step 3: Run the Application

mvn spring-boot:run

Step 4: Access the Application
Open your web browser and go to http://localhost:8080/api/hello. You should see the message "Hello, Spring Boot!" displayed on the page.




#  Practice-Project 2
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

// Custom event class
class CustomEvent extends ActionEvent {
    public CustomEvent(Object source, int id, String command) {
        super(source, id, command);
    }

    public void customEventMethod() {
        System.out.println("Custom event triggered!");
    }
}

// Custom event listener interface
interface CustomActionListener extends ActionListener {
    void customActionPerformed(CustomEvent e);
}

// Custom button class
class CustomButton extends JButton {
    private CustomActionListener customActionListener;

    public CustomButton(String text) {
        super(text);

        // Add action listener to handle default events
        addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Default event triggered!");
            }
        });
    }

    // Set custom action listener
    public void setCustomActionListener(CustomActionListener listener) {
        this.customActionListener = listener;
        // Add action listener to handle custom events
        addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                if (customActionListener != null) {
                    CustomEvent customEvent = new CustomEvent(e.getSource(), e.getID(), e.getActionCommand());
                    customActionListener.customActionPerformed(customEvent);
                }
            }
        });
    }
}

// Main GUI class
public class EventHandlingDemo extends JFrame {
    public EventHandlingDemo() {
        super("Event Handling Demo");

        // Create a custom button
        CustomButton customButton = new CustomButton("Click Me");

        // Set custom action listener for the button
        customButton.setCustomActionListener(new CustomActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Custom action performed!");
            }

            @Override
            public void customActionPerformed(CustomEvent e) {
                e.customEventMethod();
            }
        });

        // Add the button to the frame
        getContentPane().setLayout(new FlowLayout());
        getContentPane().add(customButton);

        // Set frame properties
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(300, 200);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new EventHandlingDemo();
            }
        });
    }
}



# Practice Project 3

1. Create a MySQL Database:
CREATE DATABASE sampledb;
USE sampledb;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL
);

INSERT INTO users (username, email) VALUES
('user1', 'user1@example.com'),
('user2', 'user2@example.com');

2. Set Up the Spring Project:
<!-- Spring Core -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>5.3.12.RELEASE</version>
</dependency>

<!-- Spring JDBC -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.3.12.RELEASE</version>
</dependency>

<!-- MySQL Connector -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.26</version>
</dependency>


3. Create a Spring Configuration:
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.datasource.DriverManagerDataSource;

import javax.sql.DataSource;

@Configuration
public class SpringConfig {

    @Bean
    public DataSource dataSource() {
        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/sampledb");
        dataSource.setUsername("your_username");
        dataSource.setPassword("your_password");
        return dataSource;
    }

    @Bean
    public JdbcTemplate jdbcTemplate(DataSource dataSource) {
        return new JdbcTemplate(dataSource);
    }
}

4. Create a Spring Service:
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<User> getAllUsers() {
        return jdbcTemplate.query("SELECT * FROM users", new UserMapper());
    }
}

5. Create a User Model and Mapper:
public class User {
    private Long id;
    private String username;
    private String email;

    // Getters and setters
}

import org.springframework.jdbc.core.RowMapper;

import java.sql.ResultSet;
import java.sql.SQLException;

public class UserMapper implements RowMapper<User> {
    @Override
    public User mapRow(ResultSet resultSet, int rowNum) throws SQLException {
        User user = new User();
        user.setId(resultSet.getLong("id"));
        user.setUsername(resultSet.getString("username"));
        user.setEmail(resultSet.getString("email"));
        return user;
    }
}

6. Create a Main Application:
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import java.util.List;

public class MainApplication {

    public static void main(String[] args) {
        try (AnnotationConfigApplicationContext context =
                     new AnnotationConfigApplicationContext(SpringConfig.class)) {

            UserService userService = context.getBean(UserService.class);

            // Retrieve and display all users from the database
            List<User> users = userService.getAllUsers();
            for (User user : users) {
                System.out.println(user.getId() + ": " + user.getUsername() + ", " + user.getEmail());
            }
        }
    }
}

7. 
