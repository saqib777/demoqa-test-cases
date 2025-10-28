# Page Under Test  
**Profile Page – DemoQA**  
URL: [https://demoqa.com/profile](https://demoqa.com/profile)

---

## Objective  
To validate all functionalities, UI components, and user interactions available on the Profile page of the DemoQA Book Store application — including login sessions, user collection management, logout flow, and security validations.

---

## Test Cases

| TC ID | Description | Pre-condition | Steps | Expected Result |
|-------|--------------|----------------|--------|-----------------|
| TC_PR_01 | Verify navigation to profile page | User logged in | 1. Login to DemoQA Book Store. <br>2. Click on “Profile” in sidebar. | User lands on profile page displaying username and user data. |
| TC_PR_02 | Verify username display | User logged in | 1. Navigate to Profile page. | Correct logged-in username displayed at top of the profile. |
| TC_PR_03 | Verify books listed in user’s collection | User has added books | 1. Go to Profile page. <br>2. Check listed books. | All previously added books appear with correct details. |
| TC_PR_04 | Verify profile page with no books in collection | Fresh user or removed all books | 1. Login. <br>2. Open Profile page. | No books shown; empty state message like “No books available”. |
| TC_PR_05 | Verify navigation to book details from profile | User has books in collection | 1. Click on any book title from profile. | User is redirected to that book’s detail page. |
| TC_PR_06 | Verify “Delete All Books” button visibility | User logged in | 1. Observe UI elements. | “Delete All Books” button visible below book list. |
| TC_PR_07 | Verify “Delete All Books” functionality | User has books | 1. Click on “Delete All Books”. <br>2. Confirm deletion in popup. | All books are removed; success message displayed. |
| TC_PR_08 | Verify cancel action in “Delete All Books” popup | User has books | 1. Click “Delete All Books”. <br>2. Click “Cancel”. | No deletion happens; all books remain intact. |
| TC_PR_09 | Verify delete single book from collection | User has books | 1. Click “Delete” icon next to any book. <br>2. Confirm. | Selected book is removed; others remain. |
| TC_PR_10 | Verify logout button visibility | User logged in | 1. Navigate to profile page. | Logout button is visible on top or bottom of profile. |
| TC_PR_11 | Verify logout functionality | User logged in | 1. Click “Logout”. | User session ends; redirected to login page. |
| TC_PR_12 | Verify re-login after logout | User logged out | 1. Login again with same credentials. | User is authenticated successfully; collection persists. |
| TC_PR_13 | Verify persistence of book collection after relogin | User added books | 1. Logout. <br>2. Login again. | Previously added books still appear in profile. |
| TC_PR_14 | Verify session expiration handling | Session expired | 1. Wait until session timeout or simulate expired token. <br>2. Reload page. | User redirected to login; session invalidated. |
| TC_PR_15 | Verify profile page access without login | User not logged in | 1. Navigate directly to /profile URL. | Redirected to login page; access denied. |
| TC_PR_16 | Verify API response integrity for profile data | Network dev tools open | 1. Check network request for profile data (GET /BookStore/v1/User). | Response code 200; correct JSON data for user and books. |
| TC_PR_17 | Verify error handling for failed profile API | API simulated failure | 1. Block network or simulate API 500. | Appropriate error message displayed; UI doesn’t crash. |
| TC_PR_18 | Verify UI alignment and layout | Page loaded | 1. Observe username, buttons, table layout. | All elements aligned properly; no overlaps or misplacements. |
| TC_PR_19 | Verify responsiveness on smaller screens | Mobile view | 1. Resize browser window or open on mobile. | Profile adjusts layout properly; elements visible and accessible. |
| TC_PR_20 | Verify book list sorting order | User has multiple books | 1. Observe list order (default or sorted). | Consistent ordering (alphabetical or by addition date). |
| TC_PR_21 | Verify browser refresh doesn’t log out user | Active session | 1. Refresh profile page. | User stays logged in; data reloads successfully. |
| TC_PR_22 | Verify “Back to Book Store” navigation | Page loaded | 1. Click “Go To Book Store” or “Back” button. | Redirected to books list page. |
| TC_PR_23 | Verify delete confirmation popup text | User has books | 1. Trigger delete popup. | Popup text clearly states confirmation for deletion. |
| TC_PR_24 | Verify logout and re-login from different browsers | Active user | 1. Logout from Chrome. <br>2. Login via Firefox. | Works fine; no data inconsistency. |
| TC_PR_25 | Verify unauthorized API request behaviour | User token invalid | 1. Clear auth token manually. <br>2. Refresh page. | User logged out automatically; redirected to login. |
| TC_PR_26 | Verify success message after deleting all books | User has books | 1. Delete all books. | “All books deleted successfully” message displayed. |
| TC_PR_27 | Verify “Profile” page title and URL | Page loaded | 1. Check browser title and URL. | Title contains “Profile”; URL = https://demoqa.com/profile. |
| TC_PR_28 | Verify “Profile” content loaded time | Page load | 1. Use dev tools. | Page loads fully under 2 seconds. |
| TC_PR_29 | Verify invalid book reference handling | Backend corrupted data | 1. Simulate invalid book ID in collection. | System gracefully skips/ignores invalid entry. |
| TC_PR_30 | Verify keyboard accessibility | Page loaded | 1. Use tab/enter keys to navigate and trigger actions. | All buttons accessible via keyboard navigation. |

---

## Notes & Explanations
- The **Profile page** acts as a personalized dashboard — verifying correctness, data persistence, and deletion actions is crucial.  
- Test both **logged-in** and **non-logged-in** scenarios for access control.  
- Focus on API validation, UI consistency, and session handling for a complete check.  
- Security and session-related tests (unauthorized access, token expiry) are critical for web-app integrity.  
- Negative cases (API failures, unauthorized access) ensure stability and resilience.

---

## End Notes
The Profile module connects authentication, data management, and UI elements. Testing must ensure:
- Data sync between frontend and backend APIs.  
- No information leakage or unauthorized access.  
- Consistent user experience across sessions and devices.

A well-tested Profile page guarantees a trustworthy user experience throughout the DemoQA Book Store Application.

**File Name:** `profile_page_testing.md`  
**Category:** DemoQA – Book Store Application  
**Purpose:** Manual + Automation Test Documentation
