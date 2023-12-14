# java-fsd
This repository contains PracticeProjects


# Practice-Project 1

<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>

    <session-factory>
        <!-- JDBC Database connection settings -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/your_database_name</property>
        <property name="hibernate.connection.username">your_username</property>
        <property name="hibernate.connection.password">your_password</property>
        <!-- JDBC connection pool settings -->
        <property name="hibernate.c3p0.min_size">5</property>
        <property name="hibernate.c3p0.max_size">20</property>
        <property name="hibernate.c3p0.timeout">300</property>
        <property name="hibernate.c3p0.max_statements">50</property>
        <property name="hibernate.c3p0.idle_test_period">3000</property>
        <!-- Specify dialect -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
        <!-- Echo all executed SQL to stdout -->
        <property name="hibernate.show_sql">true</property>
        <!-- Drop and re-create the database schema on startup -->
        <property name="hibernate.hbm2ddl.auto">update</property>
        <!-- Mention annotated class -->
        <!-- <mapping class="com.example.model.YourEntityClass" /> -->
    </session-factory>
</hibernate-configuration>


import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateDemo {
    public static void main(String[] args) {
        // Create a Hibernate configuration and session factory
        Configuration configuration = new Configuration().configure("hibernate.cfg.xml");
        SessionFactory sessionFactory = configuration.buildSessionFactory();

        // Create a session
        try (Session session = sessionFactory.openSession()) {
            // Perform database operations using Hibernate
            // ...

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}







#  Practice-Project 2
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- JDBC Database connection settings -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/your_database_name</property>
        <property name="hibernate.connection.username">your_username</property>
        <property name="hibernate.connection.password">your_password</property>
        <!-- JDBC connection pool settings -->
        <property name="hibernate.c3p0.min_size">5</property>
        <property name="hibernate.c3p0.max_size">20</property>
        <property name="hibernate.c3p0.timeout">300</property>
        <property name="hibernate.c3p0.max_statements">50</property>
        <property name="hibernate.c3p0.idle_test_period">3000</property>
        <!-- Specify dialect -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
        <!-- Echo all executed SQL to stdout -->
        <property name="hibernate.show_sql">true</property>
        <!-- Drop and re-create the database schema on startup -->
        <property name="hibernate.hbm2ddl.auto">update</property>
        <!-- Mention annotated class -->
        <!-- <mapping class="com.example.model.YourEntityClass" /> -->
    </session-factory>
</hibernate-configuration>

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateXMLDemo {
    public static void main(String[] args) {
        // Create a Hibernate configuration and session factory
        Configuration configuration = new Configuration().configure("hibernate.cfg.xml");
        SessionFactory sessionFactory = configuration.buildSessionFactory();

        // Create a session
        try (Session session = sessionFactory.openSession()) {
            // Perform database operations using Hibernate
            // ...

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}




# Practice Project 3

<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- JDBC Database connection settings -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/your_database_name</property>
        <property name="hibernate.connection.username">your_username</property>
        <property name="hibernate.connection.password">your_password</property>
        <!-- JDBC connection pool settings -->
        <property name="hibernate.c3p0.min_size">5</property>
        <property name="hibernate.c3p0.max_size">20</property>
        <property name="hibernate.c3p0.timeout">300</property>
        <property name="hibernate.c3p0.max_statements">50</property>
        <property name="hibernate.c3p0.idle_test_period">3000</property>
        <!-- Specify dialect -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>
        <!-- Echo all executed SQL to stdout -->
        <property name="hibernate.show_sql">true</property>
        <!-- Drop and re-create the database schema on startup -->
        <property name="hibernate.hbm2ddl.auto">update</property>
        <!-- Scans packages for annotated classes -->
        <property name="hibernate.archive.autodetection">class, hbm</property>
    </session-factory>
</hibernate-configuration>

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String username;
    private String password;

    // Constructors, getters, setters, etc.
}

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class HibernateAnnotationDemo {
    public static void main(String[] args) {
        // Create a Hibernate configuration and session factory
        Configuration configuration = new Configuration().configure();
        SessionFactory sessionFactory = configuration.buildSessionFactory();

        // Create a session
        try (Session session = sessionFactory.openSession()) {
            // Create a transaction
            Transaction transaction = session.beginTransaction();

            // Perform database operations using Hibernate annotations
            User user = new User();
            user.setUsername("john_doe");
            user.setPassword("password123");

            // Save the user
            session.save(user);

            // Commit the transaction
            transaction.commit();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}





# practice project : 4

<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="WARN">
    <Appenders>
        <File name="HibernateLogFile" fileName="logs/hibernate.log">
            <PatternLayout>
                <Pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n</Pattern>
            </PatternLayout>
        </File>
    </Appenders>
    <Loggers>
        <Logger name="org.hibernate" level="debug" additivity="false">
            <AppenderRef ref="HibernateLogFile" />
        </Logger>
        <Root level="error">
            <AppenderRef ref="HibernateLogFile" />
        </Root>
    </Loggers>
</Configuration>

<!-- Other properties in hibernate.cfg.xml -->
<property name="hibernate.show_sql">true</property>
<property name="hibernate.format_sql">true</property>
<property name="hibernate.use_sql_comments">true</property>
<property name="hibernate.generate_statistics">true</property>
<property name="hibernate.hbm2ddl.auto">update</property>

<!-- Log4j configuration -->
<property name="hibernate.jdbc.log.was.flush.statement">true</property>
<property name="hibernate.jdbc.log.was.formatted">true</property>
<property name="hibernate.jdbc.log.was.sql">true</property>
<property name="hibernate.jdbc.log.was.parameters">true</property>
<property name="hibernate.jdbc.log.was.log_statement">true</property>
<property name="hibernate.jdbc.log.was.log_statement_with_id">true</property>
<property name="hibernate.connection.provider_disables_autocommit">true</property>
<property name="hibernate.transaction.jta.platform">org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform</property>




# practice project5

List Mapping Example:
import java.util.List;

public class Employee {
    private int id;
    private String name;
    private List<String> phoneNumbers;

    // Constructors, getters, setters, etc.
}
<!-- hibernate-mapping for Employee entity with List mapping -->
<hibernate-mapping>
    <class name="com.example.Employee" table="employee">
        <id name="id" type="int">
            <generator class="native" />
        </id>
        <property name="name" type="string" />
        <list name="phoneNumbers" cascade="all">
            <key column="employee_id" />
            <index column="phone_index" type="integer" />
            <element column="phone_number" type="string" />
        </list>
    </class>
</hibernate-mapping>

SET MAPPING EXAMPLE:

import java.util.Set;

public class Course {
    private int id;
    private String name;
    private Set<String> students;

    // Constructors, getters, setters, etc.
}

<!-- hibernate-mapping for Course entity with Set mapping -->
<hibernate-mapping>
    <class name="com.example.Course" table="course">
        <id name="id" type="int">
            <generator class="native" />
        </id>
        <property name="name" type="string" />
        <set name="students" cascade="all">
            <key column="course_id" />
            <element column="student_name" type="string" />
        </set>
    </class>
</hibernate-mapping>

3.BAG MAPPING EXAMPLE

import java.util.Collection;

public class Department {
    private int id;
    private String name;
    private Collection<String> employees;

    // Constructors, getters, setters, etc.
}
<!-- hibernate-mapping for Department entity with Bag mapping -->
<hibernate-mapping>
    <class name="com.example.Department" table="department">
        <id name="id" type="int">
            <generator class="native" />
        </id>
        <property name="name" type="string" />
        <bag name="employees" cascade="all">
            <key column="department_id" />
            <element column="employee_name" type="string" />
        </bag>
    </class>
</hibernate-mapping>

4. MAP MAPPING EXAMPLE
   import java.util.Map;

public class Student {
    private int id;
    private String name;
    private Map<String, Integer> subjectMarks;

    // Constructors, getters, setters, etc.
}
<!-- hibernate-mapping for Student entity with Map mapping -->
<hibernate-mapping>
    <class name="com.example.Student" table="student">
        <id name="id" type="int">
            <generator class="native" />
        </id>
        <property name="name" type="string" />
        <map name="subjectMarks" cascade="all">
            <key column="student_id" />
            <index column="subject_name" type="string" />
            <element column="marks" type="integer" />
        </map>
    </class>
</hibernate-mapping>



 # practice project 6
1.EMPLOYEE DETAIL

import javax.persistence.*;

@Entity
@Table(name = "employee")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // Getters, setters, etc.
}

2. Department Entity
   import javax.persistence.*;
import java.util.List;

@Entity
@Table(name = "department")
public class Department {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // Lazy-loaded collection
    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    private List<Employee> employees;

    // Getters, setters, etc.
}

3.Hibernet Configuration

<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- Other configuration properties -->

        <!-- Enable lazy loading outside of transactions -->
        <property name="hibernate.enable_lazy_load_no_trans">true</property>
    </session-factory>
</hibernate-configuration>

#Example 

import org.hibernate.Session;
import org.hibernate.Transaction;

public class LazyLoadingExample {
    public static void main(String[] args) {
        try (Session session = HibernateUtil.getSessionFactory().openSession()) {
            Transaction transaction = session.beginTransaction();

            // Fetch a department (lazy loading will be triggered when accessing employees)
            Department department = session.get(Department.class, 1L);

            // Access the employees collection (lazy loading will be triggered)
            List<Employee> employees = department.getEmployees();

            // Print employee names
            for (Employee employee : employees) {
                System.out.println("Employee Name: " + employee.getName());
            }

            transaction.commit();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}



# practice project: 7

1.Address Component

import javax.persistence.Embeddable;

@Embeddable
public class Address {
    private String street;
    private String city;
    private String zipCode;

    // Constructors, getters, setters, etc.
}


2.Employee Entity

import javax.persistence.*;

@Entity
@Table(name = "employee")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Embedded
    private Address address;

    // Constructors, getters, setters, etc.
}
3. Hibernet Configuration
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- Other configuration properties -->
    </session-factory>
</hibernate-configuration>


3. Example

   import org.hibernate.Session;
import org.hibernate.Transaction;

public class ComponentMappingExample {
    public static void main(String[] args) {
        try (Session session = HibernateUtil.getSessionFactory().openSession()) {
            Transaction transaction = session.beginTransaction();

            // Create an Address component
            Address address = new Address();
            address.setStreet("123 Main St");
            address.setCity("Cityville");
            address.setZipCode("12345");

            // Create an Employee entity with the embedded Address component
            Employee employee = new Employee();
            employee.setName("John Doe");
            employee.setAddress(address);

            // Save the Employee entity
            session.save(employee);

            transaction.commit();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


# practice project 8

1. MAVEN

   <!-- Add Hibernate and Spring dependencies in your pom.xml -->
<dependencies>
    <!-- Hibernate -->
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.6.5.Final</version>
    </dependency>

    <!-- Spring -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.10</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>5.3.10</version>
    </dependency>

    <!-- Database driver and connection pool (e.g., for MySQL) -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.27</version>
    </dependency>
</dependencies>


2.GRADLE

// Add Hibernate and Spring dependencies in your build.gradle
dependencies {
    // Hibernate
    implementation 'org.hibernate:hibernate-core:5.6.5.Final'

    // Spring
    implementation 'org.springframework:spring-context:5.3.10'
    implementation 'org.springframework:spring-orm:5.3.10'

    // Database driver and connection pool (e.g., for MySQL)
    implementation 'mysql:mysql-connector-java:8.0.27'
}


3.HIBERNET CONFIGURATION 

<!-- src/main/resources/hibernate.cfg.xml -->
<!DOCTYPE hibernate-configuration PUBLIC "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <!-- JDBC Database connection settings -->
        <property name="hibernate.connection.driver_class">com.mysql.cj.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/your_database_name</property>
        <property name="hibernate.connection.username">your_username</property>
        <property name="hibernate.connection.password">your_password</property>

        <!-- JDBC connection pool settings -->
        <property name="hibernate.c3p0.min_size">5</property>
        <property name="hibernate.c3p0.max_size">20</property>
        <property name="hibernate.c3p0.timeout">300</property>
        <property name="hibernate.c3p0.max_statements">50</property>
        <property name="hibernate.c3p0.idle_test_period">3000</property>

        <!-- Specify dialect -->
        <property name="hibernate.dialect">org.hibernate.dialect.MySQLDialect</property>

        <!-- Echo all executed SQL to stdout -->
        <property name="hibernate.show_sql">true</property>
        <property name="hibernate.format_sql">true</property>

        <!-- Drop and re-create the database schema on startup -->
        <property name="hibernate.hbm2ddl.auto">update</property>
    </session-factory>
</hibernate-configuration>



4.SPRING CONFIGURATION

<!-- src/main/resources/applicationContext.xml -->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/tx
       http://www.springframework.org/schema/tx/spring-tx.xsd">

    <!-- Enable component scanning -->
    <context:component-scan base-package="com.example"/>

    <!-- Enable transaction management -->
    <tx:annotation-driven/>

    <!-- DataSource configuration -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/your_database_name"/>
        <property name="username" value="your_username"/>
        <property name="password" value="your_password"/>
    </bean>

    <!-- Hibernate SessionFactory -->
    <bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <property name="hibernateProperties">
            <props>
                <prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
                <prop key="hibernate.show_sql">true</prop>
                <prop key="hibernate.format_sql">true</prop>
                <prop key="hibernate.hbm2ddl.auto">update</prop>
            </props>
        </property>
        <property name="packagesToScan" value="com.example"/>
    </bean>

    <!-- Transaction Manager -->
    <bean id="transactionManager" class="org.springframework.orm.hibernate5.HibernateTransactionManager">
        <property name="sessionFactory" ref="sessionFactory"/>
    </bean>
</beans>

5.Entity and DAO Classes


// Employee.java
@Entity
@Table(name = "employee")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // Getters, setters, etc.
}

// EmployeeDAO.java
@Repository
public class EmployeeDAO {
    @Autowired
    private SessionFactory sessionFactory;

    @Transactional
    public void saveEmployee(Employee employee) {
        Session session = sessionFactory.getCurrentSession();
        session.save(employee);
    }

    @Transactional(readOnly = true)
    public Employee getEmployeeById(Long id) {
        Session session = sessionFactory.getCurrentSession();
return session.get(Employee.class, id);
}
}


### 5. Service Class:

Create a service class that uses the DAO to perform business logic:

```java
// EmployeeService.java
@Service
public class EmployeeService {
    @Autowired
    private EmployeeDAO employeeDAO;

    @Transactional
    public void saveEmployee(Employee employee) {
        employeeDAO.saveEmployee(employee);
    }

    @Transactional(readOnly = true)
    public Employee getEmployeeById(Long id) {
        return employeeDAO.getEmployeeById(id);
    }

    // Other business logic methods
}

6.Main Application

// MainApp.java
public class MainApp {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context =
                new AnnotationConfigApplicationContext();
        context.scan("com.example");
        context.refresh();

        EmployeeService employeeService = context.getBean(EmployeeService.class);

        // Test Hibernate-Spring integration
        Employee employee = new Employee();
        employee.setName("John Doe");
        employeeService.saveEmployee(employee);

        Employee retrievedEmployee = employeeService.getEmployeeById(employee.getId());
        System.out.println("Retrieved Employee: " + retrievedEmployee.getName());

        context.close();
    }
}



