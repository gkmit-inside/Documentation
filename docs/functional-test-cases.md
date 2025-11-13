# **TC 1: Authentication and Authorization**

## TC 1.A: Login Test Cases

| Test Case No. | Module Name | Test Case Description                                                                | Acceptance Criteria                                                                                                                                        |
| ------------- | ----------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **T_C_1.1**   | Login       | Verify a valid combination of Employee email and Password allows successful login.   | The system must grant access to the Employee `/feed` page, and the correct name must be displayed.                                                         |
| **T_C_1.2**   | Login       | Verify a valid combination of Admin email and Password allows successful login.      | The system must grant access to the Admin dashboard, and the correct user name must be displayed.                                                          |
| **T_C_1.3**   | Login       | Verify login fails with a valid email and an invalid password (for any role).        | An appropriate error message must be displayed (e.g., "Invalid credentials" or "Invalid password"), and the user must remain on the login page.            |
| **T_C_1.4**   | Login       | Verify login fails with an invalid email and a valid password (for any role).        | An appropriate error message must be displayed (e.g., "Invalid credentials" or "Invalid email"), and the user must remain on the login page.               |
| **T_C_1.5**   | Login       | Verify login fails with both invalid email and invalid password.                     | An appropriate error message must be displayed, and the user must remain on the login page.                                                                |
| **T_C_1.6**   | Login       | Verify case sensitivity for the email field.                                         | Login must fail if the email case does not match the stored value (e.g., `JohnDoe@service.com` should fail if the correct email is `johndoe@service.com`). |
| **T_C_1.7**   | Login       | Verify the system handles repeated failed login attempts (Brute-Force Protection).   | After **N** consecutive failed attempts (e.g., 5), the account must be temporarily locked or a CAPTCHA/other protective measure must be required.          |
| **T_C_1.8**   | Login       | Verify login fails when the email field is empty and the password field has data.    | An error message for the missing email (e.g., "Email is required") must be displayed, and the user must remain on the login page.                          |
| **T_C_1.9**   | Login       | Verify login fails when the password field is empty and the email field has data.    | An error message for the missing password (e.g., "Password is required") must be displayed, and the user must remain on the login page.                    |
| **T_C_1.10**  | Login       | Verify login fails with an improperly formatted email (e.g., missing '@' or '.com'). | An appropriate format validation error message (e.g., "Please enter a valid email address") must be displayed.                                             |

---

## TC 1.B: Logout & Session Management Test Cases

This section covers the test scenarios for **session management** and **logout functionality**, ensuring security, stability, and user session integrity.

| **Test Case No.** | **Module Name** | **Test Case Description**                                                                                                       | **Acceptance Criteria**                                                                                                                                                                                |
| ----------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| T_C_1.11          | Logout          | Verify that clicking the Logout button successfully terminates the user session.                                                | The user must be redirected to the login page, and attempting to use the browser's "Back" button should not display any protected internal content.                                                    |
| T_C_1.12          | Logout          | Verify that session cookies are properly cleared/invalidated upon successful logout.                                            | After logging out, checking the browser's developer tools should show that the session identifier/token cookie is removed or set to expired/invalid.                                                   |
| T_C_1.13          | Session         | Verify a logged-in user is automatically logged out after a period of inactivity (Session Timeout).                             | The user must be redirected to the login page, and attempting to access an internal page must redirect them back to the login page.                                                                    |
| T_C_1.14          | Session         | Verify the system does not allow simultaneous logins for the same account (or enforces specific session rules).                 | When a user is logged in on Device A, a subsequent successful login on Device B must either terminate the session on Device A or the system must disallow the login on Device B and display a warning. |
| T_C_1.15          | Session         | Verify the application handles security vulnerability warnings when accessing the application over HTTP (if HTTPS is required). | If the application is accessed via `http://` instead of `https://`, the user should be automatically redirected to the secure HTTPS connection, or a security warning should be displayed.             |

---

## TC 1.C: Authorization (Role-based Access Control) Test Cases

This section validates that users can only access resources permitted by their assigned roles, ensuring **data security** and **role integrity** throughout the system.

| **Test Case No.** | **Module Name** | **Test Case Description**                                                                                     | **Acceptance Criteria**                                                                                                                           |
| ----------------- | --------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| T_C_1.16          | Authorization   | Verify an Employee user cannot access a URL/page specific to the Admin role via direct URL navigation.        | The system must display an “Access Denied” error message, or redirect the user to their own dashboard.                                            |
| T_C_1.17          | Authorization   | Verify an unauthenticated/Guest user cannot access any authenticated internal page via direct URL navigation. | The user must be immediately redirected to the Login page when attempting to access any protected resource (e.g., `/feed` or `/admin/dashboard`). |

---
