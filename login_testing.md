# Login Page — Test Cases, Notes & Description

## Page Under Test  
**Login – DemoQA Book Store Application** — [https://demoqa.com/login](https://demoqa.com/login) :contentReference[oaicite:1]{index=1}

---

## Test Cases

| TC ID     | Description                                                      | Pre-condition                | Steps                                                                                   | Expected Result                                                                 |
|-----------|------------------------------------------------------------------|------------------------------|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **TC_LG_01** | Verify page loads and login form is visible                        | Navigate to login page       | 1. Open URL <br>2. Observe form fields and buttons                                     | Username and Password fields visible; “Login” button enabled; links for “New User” present |
| **TC_LG_02** | Verify placeholder or label of Username / Password fields         | Login page loaded            | Inspect input fields                                                                    | Proper labels or placeholders (e.g., “UserName :”, “Password :”) present        |
| **TC_LG_03** | Positive login with valid credentials                              | Valid credentials exist      | Enter valid username & password <br>Click “Login”                                       | Login succeeds; user redirected to profile or book store page                   |
| **TC_LG_04** | Invalid login with wrong username                                  | Login page loaded            | Enter wrong username + valid password <br>Click “Login”                                 | Error message displayed (e.g., “Invalid username or password”)                  |
| **TC_LG_05** | Invalid login with wrong password                                  | Login page loaded            | Enter valid username + wrong password <br>Click “Login”                                 | Error message displayed                                                      |
| **TC_LG_06** | Blank username submission                                           | Login page loaded            | Leave username blank <br>Enter password <br>Click “Login”                                | Error or validation message about missing username                             |
| **TC_LG_07** | Blank password submission                                           | Login page loaded            | Enter username <br>Leave password blank <br>Click “Login”                               | Error or validation message about missing password                             |
| **TC_LG_08** | Both fields blank                                                   | Login page loaded            | Leave both username & password blank <br>Click “Login”                                  | Validation message(s) appear; login not allowed                              |
| **TC_LG_09** | Case sensitivity of username / password                              | Login page loaded            | Enter correct credentials but change case in username or password                         | Either username/password recognized or login fails — check expected behaviour   |
| **TC_LG_10** | Remember/Keep-Me or session behaviour (if present)                 | Login page loaded            | Check if “Remember me” or similar <br>Login <br>Close browser <br>Reopen                | Session persists if feature present; otherwise new login required             |
| **TC_LG_11** | URL redirect after login                                           | Valid credentials login      | Login successfully                                                                       | Redirect URL changes to /profile, /books or home                             |
| **TC_LG_12** | Verify “New User” / registration link                              | Login page loaded            | Click “New User” or similar link                                                         | Registration page opens (https://demoqa.com/register)                         |
| **TC_LG_13** | Security: Password masking / show-hide toggle                      | Login page loaded            | Enter password <br>Check if it’s masked <br>If show toggle present, toggle it            | Password hidden by default; show-toggle reveals value, then hides again        |
| **TC_LG_14** | Input field max length / special characters                         | Login page loaded            | Enter extremely long username/password and special characters                            | Behaviour consistent: either accept up to limit and login succeeds/fails or shows validation |
| **TC_LG_15** | SQL injection / security input                                     | Login page loaded            | Enter `' OR '1'='1`; `; DROP TABLE users;` etc in username/password                     | Login fails; no error stack trace or database error exposed                    |
| **TC_LG_16** | XSS vulnerability in inputs                                         | Login page loaded            | Enter `<script>alert(1)</script>` in username/password                                  | Input sanitized; no alert or script executed                                   |
| **TC_LG_17** | Keyboard accessibility: Tab navigation to fields & button            | Login page loaded            | Use Tab key to navigate fields and button <br>Press Enter on login                        | Focus goes to username → password → login button; Enter submits                |
| **TC_LG_18** | Enter key behaviour in fields                                       | Login page loaded            | Enter username & password <br>Press Enter in password field                              | Login triggers same as clicking “Login” button                                  |
| **TC_LG_19** | Login error message content and style                               | Login fails                   | Trigger invalid login                                                                      | Error message visible, correct text, styling readable                          |
| **TC_LG_20** | Login from mobile / responsive layout                                | Mobile or narrow viewport     | Resize browser or use mobile device <br>Perform login                                    | Layout is usable; fields visible; login functions correctly                    |
| **TC_LG_21** | Session timeout / logout behaviour                                  | Logged in                     | Remain idle > certain period or close tab <br>Revisit site                              | User redirected to login; session expired message (if implemented)             |
| **TC_LG_22** | Logout functionality (if present)                                   | Logged in                     | Click logout                                                                               | User is logged out; redirected to login page                                   |
| **TC_LG_23** | Multiple login attempts lockout (if implemented)                     | Login page loaded            | Attempt invalid login repeatedly (5–10 times)                                            | Account locked or Captcha triggered or message appears                         |
| **TC_LG_24** | Browser back button after login                                     | Logged in                     | Navigate to profile/bookstore <br>Click back                                                 | Either stays logged in and shows last page or returns to login depending on spec |
| **TC_LG_25** | Cookie and local-storage behaviour                                  | Logged in                     | Login successfully <br>Inspect cookies/localStorage                                           | Appropriate tokens present; secure attributes set                              |
| **TC_LG_26** | Input field auto-fill and browser saved credentials                   | Login page loaded             | Use browser saved credentials and login                                                  | Login works; auto-fill appears; secure auto-fill behaviour                       |
| **TC_LG_27** | Link validation (Forgot Password, Terms, etc)                          | Login page loaded             | Click “Forgot Password” or other auxiliary links                                          | The correct page opens or message appears                                      |
| **TC_LG_28** | Field validation: leading/trailing spaces                              | Login page loaded            | Enter username with leading/trailing spaces + correct password                             | System trims spaces or rejects with validation; consistent behaviour            |
| **TC_LG_29** | Back-end API failure / server error handling                           | Login page loaded             | Simulate server down or API returns 500                                                  | User sees friendly error message; login not allowed                             |
| **TC_LG_30** | Visual-regression: login page styling across browsers                 | Login page loaded             | Compare page rendering on Chrome, Firefox, Edge                                          | Layout consistent; no broken fields or mis-alignment                             |

---

## Notes & Explanations  
- The login page for DemoQA’s Book Store app requires valid credentials. :contentReference[oaicite:2]{index=2}  
- Important functional aspects: fields for username & password, login button, registration link.  
- Security aspects: prevent SQLi, XSS, safe password handling, masked input.  
- Accessibility: Tab navigation, Enter key submission, visible error/success states.  
- Session & persistence behaviour: cookies, tokens, logout, back button, responsiveness.  
- Negative and edge-case inputs: invalid credentials, blank inputs, special characters, very large inputs.  
- Visual and cross-browser consistency: make sure login page behaves the same across environments and viewports.  

---

## End Notes  
Login is often the **gateway** to the rest of the application — any defect here can compromise user access, security, or data integrity. Covering both standard and edge cases ensures robust authentication functionality and prevents simple entry points from becoming vulnerabilities.

**File Name:** `login_testing.md`  
**Category:** DemoQA – Authentication / Book Store App  
**Created For:** Manual + Automation Testing documentation  
