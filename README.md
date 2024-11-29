**Objective:**
The goal of this project is to demonstrate understanding and implementation of fundamental security concepts required for secure systems development:

Authentication: Securely verify user identities.
Authorization: Grant access to specific resources based on roles.
Role-Based Access Control (RBAC): Determine user permissions based on assigned roles, ensuring access control to endpoints and actions.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Key Features:**
Authentication
Secure user registration with password encryption using BCryptPasswordEncoder.
User login functionality with validation of credentials.
Session management using JWT or OAuth (future expansion).

**Authorization**
Different roles defined in the system:
ROLE_USER: Basic user role to create and view approved posts.
ROLE_ADMIN: Admin role for approving or rejecting posts and assigning roles.
ROLE_MODERATOR: Moderator role for approving or rejecting posts.
Endpoint access restricted based on roles using Spring Security's @PreAuthorize and @Secured annotations.

**Role-Based Access Control (RBAC)**
Access to system features is determined by the roles assigned to users.
Admins and moderators have elevated permissions to approve, reject, or delete posts.
Users can only create posts that require admin/moderator approval.

**System Architecture**
The project consists of the following components:

**User Management**

Users can register and have a default role (ROLE_USER).
Admins and moderators can assign additional roles to users.

**Post Management**

Users can create posts, which are marked as PENDING until approved.
Admins and moderators can approve or reject posts.
Approved posts are visible to all users.

**Database**

User table: Stores user details, including roles and encrypted passwords.
Post table: Stores posts created by users, along with their statuses (PENDING, APPROVED, REJECTED).

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**API Endpoints**
User APIs
Endpoint	HTTP Method	Description	Role Required
/user/join	POST	Register a new user with default or specified role(s).	None
/user/access/{userId}/{userRole}	GET	Assign a new role to a user.	ROLE_ADMIN or ROLE_MODERATOR
/user	GET	Retrieve all users in the system.	ROLE_ADMIN
/user/test	GET	Test access for basic users.	ROLE_USER

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Post APIs**
Endpoint	HTTP Method	Description	Role Required
/post/create	POST	Create a new post (status defaults to PENDING).	ROLE_USER
/post/viewAll	GET	View all approved posts.	None
/post/approvePost/{postId}	GET	Approve a specific post.	ROLE_ADMIN or ROLE_MODERATOR
/post/removePost/{postId}	GET	Reject a specific post.	ROLE_ADMIN or ROLE_MODERATOR
/post/approveAll	GET	Approve all pending posts.	ROLE_ADMIN or ROLE_MODERATOR
/post/rejectAll	GET	Reject all pending posts.	ROLE_ADMIN or ROLE_MODERATOR

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**How to Run the Project**

**Prerequisites**
Java 17 or higher.
Spring Boot.
MySQL database.

**Clone the Repository**
bash
Copy code
git clone **https://github.com/22MCMC22/rbac-backend **
cd project-directory  

**Set Up the Database**
Create a MySQL database named rbac_system.
Update the application.properties file with your database credentials.

**Run the Application**
bash
Copy code
mvn spring-boot:run 

**Test the APIs**
Use Postman or any REST client to test the endpoints mentioned above.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Project Structure**
plaintext
Copy code
src  
├── main  
│   ├── java  
│   │   ├── com.code.controller       # Controllers for User and Post APIs  
│   │   ├── com.code.entities         # Entity classes for User and Post  
│   │   ├── com.code.repositories     # Repository interfaces for database operations  
│   │   ├── com.code.security         # Spring Security configuration  
│   ├── resources  
│       ├── application.properties    # Application configuration  
├── test                              # Unit and integration tests  

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Future Enhancements**
Implement JWT-based session management.
Add detailed logging and exception handling.
Enhance user experience with frontend integration (React.js or Angular).
