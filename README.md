# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

CREATE DATABASE testdb;
USE testdb;

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255),
    password VARCHAR(255)
);

INSERT INTO users (username, password) VALUES
    ('john_doe', 'password123'),
    ('jane_doe', 'securepass');


    import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class JDBCExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/testdb";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try {
            // Step 1: Load the JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Step 2: Establish a connection
            try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
                // Step 3: Execute a query
                String query = "SELECT * FROM users";
                try (PreparedStatement preparedStatement = connection.prepareStatement(query);
                     ResultSet resultSet = preparedStatement.executeQuery()) {
                    // Step 4: Process the results
                    while (resultSet.next()) {
                        int id = resultSet.getInt("id");
                        String username = resultSet.getString("username");
                        String password = resultSet.getString("password");

                        System.out.println("ID: " + id + ", Username: " + username + ", Password: " + password);
                    }
                }
            }
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}







#  Practice-Project 2
CREATE DATABASE testdb;
USE testdb;

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255),
    password VARCHAR(255)
);

INSERT INTO users (username, password) VALUES
    ('john_doe', 'password123'),
    ('jane_doe', 'securepass');


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class JDBCExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/testdb";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try {
            // Step 1: Load the JDBC driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Step 2: Establish a connection
            try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
                // Step 3: Execute a query
                String query = "SELECT * FROM users";
                try (PreparedStatement preparedStatement = connection.prepareStatement(query);
                     ResultSet resultSet = preparedStatement.executeQuery()) {
                    // Step 4: Process the results
                    while (resultSet.next()) {
                        int id = resultSet.getInt("id");
                        String username = resultSet.getString("username");
                        String password = resultSet.getString("password");

                        System.out.println("ID: " + id + ", Username: " + username + ", Password: " + password);
                    }
                }
            }
        } catch (ClassNotFoundException | SQLException e) {
            e.printStackTrace();
        }
    }
}



# Practice Project 3

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class JDBCExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/testdb";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        // Step 1: Establish a connection
        try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
            System.out.println("Connected to the database.");

            // Step 2: Create a statement
            try (Statement statement = connection.createStatement()) {
                // Step 3: Execute a query
                String query = "SELECT * FROM users";
                try (ResultSet resultSet = statement.executeQuery(query)) {
                    // Step 4: Process the results
                    while (resultSet.next()) {
                        int id = resultSet.getInt("id");
                        String username = resultSet.getString("username");
                        String password = resultSet.getString("password");

                        System.out.println("ID: " + id + ", Username: " + username + ", Password: " + password);
                    }
                }
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}





# practice project : 4

DELIMITER //
CREATE PROCEDURE GetUserInfo(IN userId INT, OUT username VARCHAR(255), OUT password VARCHAR(255))
BEGIN
    SELECT username, password FROM users WHERE id = userId;
END //
DELIMITER ;

import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class JDBCStoredProcedureExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/testdb";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
            System.out.println("Connected to the database.");

            // Calling a stored procedure
            int userId = 1;
            try (CallableStatement callableStatement = connection.prepareCall("{call GetUserInfo(?, ?, ?)}")) {
                // Set input parameter
                callableStatement.setInt(1, userId);

                // Register output parameters
                callableStatement.registerOutParameter(2, java.sql.Types.VARCHAR); // username
                callableStatement.registerOutParameter(3, java.sql.Types.VARCHAR); // password

                // Execute the stored procedure
                callableStatement.execute();

                // Retrieve output parameters
                String username = callableStatement.getString(2);
                String password = callableStatement.getString(3);

                System.out.println("User Info - Username: " + username + ", Password: " + password);
            } catch (SQLException e) {
                handleSQLException(e);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void handleSQLException(SQLException e) {
        System.err.println("SQL State: " + e.getSQLState());
        System.err.println("Error Code: " + e.getErrorCode());
        System.err.println("Message: " + e.getMessage());
        e.printStackTrace();
    }
}





#practice project5


import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class JDBCDatabaseExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";
    private static final String DATABASE_NAME = "exampledb";

    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
            System.out.println("Connected to the MySQL server.");

            // Create a database
            createDatabase(connection, DATABASE_NAME);

            // Select the database
            selectDatabase(connection, DATABASE_NAME);

            // Perform operations on the selected database (you can add your own logic here)

            // Drop the database
            dropDatabase(connection, DATABASE_NAME);

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void createDatabase(Connection connection, String databaseName) throws SQLException {
        try (Statement statement = connection.createStatement()) {
            String createDatabaseSQL = "CREATE DATABASE " + databaseName;
            statement.executeUpdate(createDatabaseSQL);
            System.out.println("Database '" + databaseName + "' created successfully.");
        }
    }

    private static void selectDatabase(Connection connection, String databaseName) throws SQLException {
        try (Statement statement = connection.createStatement()) {
            String selectDatabaseSQL = "USE " + databaseName;
            statement.executeUpdate(selectDatabaseSQL);
            System.out.println("Selected database '" + databaseName + "'.");
        }
    }

    private static void dropDatabase(Connection connection, String databaseName) throws SQLException {
        try (Statement statement = connection.createStatement()) {
            String dropDatabaseSQL = "DROP DATABASE " + databaseName;
            statement.executeUpdate(dropDatabaseSQL);
            System.out.println("Database '" + databaseName + "' dropped successfully.");
        }
    }
}



 # practice project 6

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class JDBCDataManipulationExample {
    private static final String JDBC_URL = "jdbc:mysql://localhost:3306/exampledb";
    private static final String USER = "your_username";
    private static final String PASSWORD = "your_password";

    public static void main(String[] args) {
        try (Connection connection = DriverManager.getConnection(JDBC_URL, USER, PASSWORD)) {
            System.out.println("Connected to the MySQL server.");

            // Insert a record
            int insertedId = insertRecord(connection, "John Doe", "john@example.com");
            System.out.println("Record inserted with ID: " + insertedId);

            // Update a record
            updateRecord(connection, insertedId, "John Doe Jr.");

            // Delete a record
            deleteRecord(connection, insertedId);

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int insertRecord(Connection connection, String name, String email) throws SQLException {
        String insertSQL = "INSERT INTO users (name, email) VALUES (?, ?)";
        try (PreparedStatement preparedStatement = connection.prepareStatement(insertSQL, PreparedStatement.RETURN_GENERATED_KEYS)) {
            preparedStatement.setString(1, name);
            preparedStatement.setString(2, email);

            int affectedRows = preparedStatement.executeUpdate();

            if (affectedRows == 0) {
                throw new SQLException("Insertion failed, no rows affected.");
            }

            // Retrieve the auto-generated key (if any)
            try (var generatedKeys = preparedStatement.getGeneratedKeys()) {
                if (generatedKeys.next()) {
                    return generatedKeys.getInt(1);
                } else {
                    throw new SQLException("Insertion failed, no ID obtained.");
                }
            }
        }
    }

    private static void updateRecord(Connection connection, int userId, String newName) throws SQLException {
        String updateSQL = "UPDATE users SET name = ? WHERE id = ?";
        try (PreparedStatement preparedStatement = connection.prepareStatement(updateSQL)) {
            preparedStatement.setString(1, newName);
            preparedStatement.setInt(2, userId);

            int affectedRows = preparedStatement.executeUpdate();

            if (affectedRows == 0) {
                System.out.println("Update failed, no rows affected.");
            } else {
                System.out.println("Record updated successfully.");
            }
        }
    }

    private static void deleteRecord(Connection connection, int userId) throws SQLException {
        String deleteSQL = "DELETE FROM users WHERE id = ?";
        try (PreparedStatement preparedStatement = connection.prepareStatement(deleteSQL)) {
            preparedStatement.setInt(1, userId);

            int affectedRows = preparedStatement.executeUpdate();

            if (affectedRows == 0) {
                System.out.println("Deletion failed, no rows affected.");
            } else {
                System.out.println("Record deleted successfully.");
            }
        }
    }
}
