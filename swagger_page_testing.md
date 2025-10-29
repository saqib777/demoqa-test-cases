## Page Under Test  
**Swagger API Documentation – DemoQA**  
URL: [https://demoqa.com/swagger](https://demoqa.com/swagger)

---

## Objective  
To verify that the Swagger UI loads correctly, all documented API endpoints are functional, accessible, and return valid responses.  
Testing also ensures that the Swagger interface allows proper interaction (try-out, parameter input, and response viewing) without UI or network issues.

---

## Test Cases

| TC ID | Test Scenario | Pre-condition | Test Steps | Expected Result |
|-------|----------------|----------------|-------------|-----------------|
| TC_SW_01 | Verify that the Swagger page loads successfully | Internet connection available | 1. Open the URL `https://demoqa.com/swagger` in browser. | Swagger UI loads completely without errors. |
| TC_SW_02 | Verify that the Swagger logo and page title appear correctly | Page loaded | 1. Observe header and title area. | “Swagger UI” or “DemoQA API Docs” title visible. |
| TC_SW_03 | Verify all API sections are listed (e.g., Book Store, Account, User) | Page loaded | 1. Scroll through left panel. | All categories of APIs (Account, BookStore, etc.) are visible. |
| TC_SW_04 | Verify expand/collapse functionality for API groups | Page loaded | 1. Click the arrow beside any API group. | The endpoints within that group expand/collapse correctly. |
| TC_SW_05 | Verify the “Try it out” button functionality | Page loaded | 1. Expand an API endpoint. <br>2. Click on “Try it out”. | Parameter fields become editable, and “Execute” button activates. |
| TC_SW_06 | Verify executing a GET API from Swagger | API available | 1. Click “Try it out” for GET `/BookStore/v1/Books`. <br>2. Click “Execute”. | Status 200 with a JSON response containing book list. |
| TC_SW_07 | Verify POST request execution | API available | 1. Choose POST `/Account/v1/GenerateToken`. <br>2. Enter valid credentials. <br>3. Click “Execute”. | Response code 200 and a valid token returned. |
| TC_SW_08 | Verify API request with invalid data | API available | 1. For POST `/Account/v1/GenerateToken`, enter invalid credentials. | Response code 400 or 401; proper error message displayed. |
| TC_SW_09 | Verify response code display in Swagger | Page loaded | 1. Execute any endpoint. | Response status code displayed clearly in the response section. |
| TC_SW_10 | Verify JSON response formatting | Successful API execution | 1. Check response section. | JSON response formatted properly and readable. |
| TC_SW_11 | Verify that the “Clear” or “Cancel” button resets input fields | “Try it out” mode active | 1. Enter parameters. <br>2. Click “Cancel”. | All fields return to non-editable state. |
| TC_SW_12 | Verify availability of all HTTP methods (GET, POST, PUT, DELETE) | Page loaded | 1. Observe different endpoints. | Each HTTP method is color-coded and available for respective endpoints. |
| TC_SW_13 | Verify color coding for methods (GET=blue, POST=green, etc.) | Page loaded | 1. Observe visual distinction in UI. | Each HTTP method follows standard Swagger color scheme. |
| TC_SW_14 | Verify API response headers displayed correctly | Successful API call | 1. Execute API. <br>2. Check response headers. | Headers section shows valid metadata (e.g., Content-Type, Date). |
| TC_SW_15 | Verify server unavailability message | Disconnect internet temporarily | 1. Reload Swagger. | Displays appropriate connection error message. |
| TC_SW_16 | Verify performance – page load time | Page loaded | 1. Measure time from load to full render. | Page loads completely within 3–5 seconds. |
| TC_SW_17 | Verify CORS error handling | Try “Try it out” from external environment | 1. Observe network console. | No CORS issues occur; APIs execute correctly. |
| TC_SW_18 | Verify scrolling and navigation in Swagger | Page loaded | 1. Scroll through the list and click multiple endpoints. | Smooth scrolling and navigation; no lag or freezing. |
| TC_SW_19 | Verify “Models” section visibility | Page loaded | 1. Scroll to bottom of Swagger UI. | Model schemas are visible with data types and structure. |
| TC_SW_20 | Verify accuracy of API request models | API schema visible | 1. Compare “Model” data types to real API responses. | Model matches backend data types and format. |
| TC_SW_21 | Verify search/filter API functionality | Page loaded | 1. Use Swagger’s search/filter bar. | API list filters according to search input. |
| TC_SW_22 | Verify API authentication requirement | Some APIs require token | 1. Try accessing `/BookStore/v1/Books` without auth. | Public APIs accessible; secured APIs return 401 Unauthorized. |
| TC_SW_23 | Verify authorization field availability | Auth API available | 1. Observe top bar or specific endpoints. | Authorization token field present for secured APIs. |
| TC_SW_24 | Verify response after logout or expired token | Token expired | 1. Execute secured API with expired token. | Response 401 Unauthorized displayed. |
| TC_SW_25 | Verify Swagger’s dark/light mode visibility (if available) | Page loaded | 1. Observe page theme and readability. | Text readable and contrast maintained. |
| TC_SW_26 | Verify API schema version information | Page loaded | 1. Check header or metadata. | Swagger shows version info (e.g., OpenAPI 3.0). |
| TC_SW_27 | Verify broken link handling | Page loaded | 1. Click any API reference links. | All links redirect correctly; no broken references. |
| TC_SW_28 | Verify error handling for invalid endpoint execution | Modify URL manually | 1. Enter invalid API URL. | 404 or “Endpoint not found” message displayed. |
| TC_SW_29 | Verify “Copy” and “Expand Response” buttons | Response available | 1. Execute API and use response buttons. | Buttons work correctly and allow easy copying. |
| TC_SW_30 | Verify overall Swagger UI responsiveness | Test across devices | 1. Open Swagger on desktop, tablet, and mobile. | Interface adjusts properly to each screen size. |

---

## Notes and Explanations

- **Swagger** serves as a live documentation and testing interface for DemoQA’s backend APIs.  
  Thus, validating both **UI behavior** and **API correctness** is essential.  
- Testers should pay attention to:
  - Endpoint accessibility (200, 400, 401, 404 validations).  
  - Schema correctness (data types, required fields).  
  - Proper handling of invalid inputs and server errors.  
- UI-specific tests ensure the documentation remains accessible and user-friendly for both technical and non-technical users.  
- Performance and security validations (auth tokens, response codes) ensure robustness of the overall API layer.  

---

## End Notes

The **Swagger page** is the single source of truth for DemoQA’s backend APIs.  
Testing it ensures:
- Correct linkage between API documentation and functional endpoints.  
- Accuracy of schema, example data, and response handling.  
- Reliability of the live “Try it out” environment for real-time API testing.

**File Name:** `swagger_page_testing.md`  
**Category:** DemoQA – API Documentation Testing  
**Purpose:** To ensure Swagger documentation, endpoints, and API UI are functioning, accurate, and developer-friendly.
