# BuyBox

BuyBox is a Java-based e-commerce web application for browsing electronic products, managing a shopping cart, placing demo orders, and administering product inventory. The project uses JSP and Servlets for the web layer, JDBC for database access, MySQL for persistence, and Bootstrap for the user interface.

> This project is intended for learning and demonstration. The payment screen accepts demo card details and is not connected to a real payment gateway.

## Features

- User registration and login
- Product listing with category-based browsing
- Shopping cart with quantity updates
- Demo checkout and order placement
- Order history and shipment status tracking
- Admin login for inventory and order management
- Add, update, and remove products
- View stock, shipped orders, and pending shipments
- Email notifications for registration, order updates, shipment updates, and restocked products

## Tech Stack

| Layer | Technologies |
| --- | --- |
| Frontend | HTML, CSS, JavaScript, Bootstrap, JSP |
| Backend | Java 8, Servlets, JDBC |
| Database | MySQL |
| Build | Maven |
| Server | Apache Tomcat 8+ |
| Mail | Jakarta Mail with Gmail SMTP |

## Project Structure

```text
BuyBox
|-- WebContent/              # JSP pages, static assets, WEB-INF config, libraries
|-- databases/               # MySQL schema and seed data
|-- src/com/shashi/beans/    # Data models
|-- src/com/shashi/service/  # Service interfaces
|-- src/com/shashi/service/impl/
|-- src/com/shashi/srv/      # Servlet controllers
|-- src/com/shashi/utility/  # Database, mail, and helper utilities
`-- pom.xml                  # Maven WAR build configuration
```

## Requirements

- Git
- Java JDK 8 or later
- Apache Maven
- Apache Tomcat 8 or later
- MySQL Server
- Eclipse IDE for Enterprise Java and Web Developers, or another Java EE-compatible IDE

## Database Setup

1. Start MySQL.
2. Log in with an admin user:

```bash
mysql -u <username> -p
```

3. Run the database script:

```sql
source databases/mysql_query.sql;
```

The script creates the `shopping-cart` schema, required tables, sample product data, and default users.

## Application Configuration

The application reads database and email settings from an `application.properties` resource using `ResourceBundle.getBundle("application")`.

Create this file under `src/application.properties`:

```properties
db.connectionString=jdbc:mysql://localhost:3306/shopping-cart
db.driverName=com.mysql.cj.jdbc.Driver
db.username=your_mysql_username
db.password=your_mysql_password

mailer.email=your_gmail_address@gmail.com
mailer.password=your_gmail_app_password
```

For Gmail mail support, enable 2-Step Verification on the Gmail account and generate an app password. Use that app password for `mailer.password`; do not use your regular Gmail password.

## Run Locally

1. Clone the repository:

```bash
git clone https://github.com/keerthip73/buybox.git
cd buybox
```

2. Import the project into Eclipse:

- File > Import > Git > Projects from Git
- Select the cloned repository
- Import it as an existing Maven project

3. Update `src/application.properties` with your MySQL and Gmail settings.
4. Run a Maven build:

```bash
mvn clean install
```

5. Configure Tomcat 8+ in Eclipse.
6. Run the project on the Tomcat server.
7. Open the application:

```text
http://localhost:8080/shopping-cart/
```

If your Tomcat HTTP port is different, update the URL accordingly, for example:

```text
http://localhost:8083/shopping-cart/
```

## Default Accounts

| Role | Email | Password |
| --- | --- | --- |
| Admin | `admin@gmail.com` | `admin` |
| User | `guest@gmail.com` | `guest` |

## Main Pages

- `index.jsp` - public home and product listing
- `login.jsp` - user and admin login
- `register.jsp` - new user registration
- `cartDetails.jsp` - cart review and quantity updates
- `payment.jsp` - demo checkout
- `orderDetails.jsp` - user order status
- `adminHome.jsp` - admin dashboard
- `addProduct.jsp` - add products to inventory
- `adminStock.jsp` - stock overview
- `unshippedItems.jsp` - pending shipment management
- `shippedItems.jsp` - shipped order records

## Troubleshooting

**Database connection fails**

- Confirm MySQL is running.
- Confirm the `shopping-cart` schema exists.
- Check `db.connectionString`, `db.username`, and `db.password` in `src/application.properties`.
- Rebuild the project with `mvn clean install`.

**Emails are not sent**

- Confirm `mailer.email` and `mailer.password` are set.
- Use a Gmail app password, not the normal account password.
- Check whether 2-Step Verification is enabled for the Gmail account.

**Tomcat port is already in use**

- Open the Tomcat server configuration in Eclipse.
- Change the HTTP port from `8080` to another available port such as `8083`.
- Restart Tomcat and open the app with the updated port.

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.
