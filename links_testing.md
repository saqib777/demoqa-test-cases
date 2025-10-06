# DemoQA Links Testing

## Overview
This document contains detailed **test cases** and **notes** for verifying the functionality of the “Links” section on [DemoQA Links Page](https://demoqa.com/links).  
The objective is to ensure that all link elements trigger correct responses, open appropriate pages, and display expected server response messages.

---

## Test Cases

### **TC01 - Verify Home Link (Simple)**
**Description:**  
Click on the **Home** link and verify that a new browser tab opens with the DemoQA homepage.  

**Steps:**
1. Open [https://demoqa.com/links](https://demoqa.com/links)
2. Click on the “Home” link.
3. Verify a new tab is opened and navigates to `https://demoqa.com/`.

**Expected Result:**  
The DemoQA homepage should open in a new tab.

---

### **TC02 - Verify Home Link (Dynamic)**
**Description:**  
Click on the **Home (Dynamic)** link and verify similar functionality as the static link.

**Steps:**
1. Navigate to the Links page.
2. Click “Home (Dynamic)” link.
3. Observe if the same page opens in a new tab.

**Expected Result:**  
Homepage opens in a new tab successfully.

---

### **TC03 - Verify Created Link (201 Response)**
**Description:**  
Ensure that clicking the “Created” link returns a **201 Created** response from the API.

**Steps:**
1. Click the “Created” link.
2. Wait for the response message to appear under “Link Response”.

**Expected Result:**  
Message should display `Link has responded with staus 201 and status text Created`.

---

### **TC04 - Verify No Content Link (204 Response)**
**Description:**  
Validate the **No Content** link’s API response.

**Steps:**
1. Click “No Content”.
2. Observe the message displayed below.

**Expected Result:**  
Message shows: `Link has responded with staus 204 and status text No Content`.

---

### **TC05 - Verify Moved Link (301 Response)**
**Description:**  
Check that clicking the “Moved” link returns a **301 Moved Permanently** response.

**Steps:**
1. Click the “Moved” link.
2. Observe the system message.

**Expected Result:**  
Message: `Link has responded with staus 301 and status text Moved Permanently`.

---

### **TC06 - Verify Bad Request Link (400 Response)**
**Description:**  
Ensure that clicking the “Bad Request” link shows **400 Bad Request**.

**Steps:**
1. Click on “Bad Request”.
2. Observe the response message below.

**Expected Result:**  
Message should read: `Link has responded with staus 400 and status text Bad Request`.

---

### **TC07 - Verify Unauthorized Link (401 Response)**
**Description:**  
Confirm the “Unauthorized” link triggers a **401 Unauthorized** API response.

**Steps:**
1. Click on “Unauthorized”.
2. Observe the displayed message.

**Expected Result:**  
Message: `Link has responded with staus 401 and status text Unauthorized`.

---

### **TC08 - Verify Forbidden Link (403 Response)**
**Description:**  
Ensure clicking the “Forbidden” link displays the correct 403 Forbidden response.

**Steps:**
1. Click “Forbidden”.
2. Verify message.

**Expected Result:**  
Message: `Link has responded with staus 403 and status text Forbidden`.

---

### **TC09 - Verify Not Found Link (404 Response)**
**Description:**  
Validate that clicking the “Not Found” link shows a **404 Not Found** response.

**Steps:**
1. Click “Not Found”.
2. Observe message under Link Response.

**Expected Result:**  
Message: `Link has responded with staus 404 and status text Not Found`.

---

## Detailed Notes & Explanations

### **1. Home Link (Static and Dynamic)**
- **Purpose:** Verifies navigation to DemoQA homepage through both static and dynamic elements.  
- **Critical Check:** Ensure both open in **new tabs** (check browser tab count).  
- **Common Defect:** Link may open in same tab or fail if `target="_blank"` is missing.  
- **Validation Tip:** Compare opened tab’s URL using browser automation or DevTools.

---

### **2. API Response Validation Links (201–404)**
- **Purpose:** Each of these links simulates a different HTTP status code response from the server.  
- **Why Important:** Ensures front-end correctly **handles and displays server responses**.  
- **Common Failures:**
  - Delayed response or no message displayed.
  - Incorrect mapping between link and status code.
  - Typographical error in message text (e.g., “staus” instead of “status” — appears intentionally in DemoQA).
- **Test Technique:** 
  - Verify both response **status number** and **text**.  
  - Ensure **asynchronous behavior** (use `await` or waits in automation).
- **Automation Notes:**
  - Capture text under element `#linkResponse`.
  - Validate using string comparison against expected message.

---

### **3. Browser Behavior**
- **Observation:**  
  Some browsers (like Chrome) may block tab opening due to popup restrictions; allow popups before testing.  
- **Expected Behavior:**  
  Links should open in **new tabs**, not within the same page.

---

### **4. Accessibility & UI Testing**
- Verify that each link:
  - Is visually distinct and clickable.
  - Has proper focus indicators (keyboard navigation test).
  - Displays a cursor change (`pointer`) on hover.

---

### **5. Negative Testing Ideas**
- Attempt clicking links while offline → No response should appear.  
- Simulate slow network to ensure loading message isn’t stuck indefinitely.  
- Try refreshing page mid-response to confirm no persistent data remains.

---

## Final Summary

| Category | Covered Area |
|-----------|---------------|
| Navigation | Home (Static & Dynamic) |
| API Response Validation | 201, 204, 301, 400, 401, 403, 404 |
| Browser Behavior | Tab management & popup behavior |
| Accessibility | Keyboard focus, visual cues |
| Negative Testing | Offline & delayed response handling |

---

### ✅ **End Notes**
This suite covers both **functional** and **UI behavior** of the DemoQA Links section.  
It validates the complete flow from **user interaction** to **API response rendering**.  
You can further extend the suite by including:
- Network condition testing (Slow/Offline modes)
- Tab handling automation validation  
- Text validation for internationalization if supported.

---

**File Name:** `links_testing.md`  
**Author:** Mohammed Saqib 
**QA Documentation** — *software-testing-handbook-v3*  
**Last Updated:** October 2025
