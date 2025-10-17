# Page Under Test:

**DemoQA Date Picker** — [https://demoqa.com/date-picker](https://demoqa.com/date-picker)

---

## Objective:

To test the functionality, usability, and validation behavior of the **Date Picker** controls on the DemoQA page — ensuring correct date selection, format validation, and calendar interactions.

---

## Scope:

* Functional testing of both date and date-time pickers.
* Validation of input field behavior, format restrictions, and boundary conditions.
* Usability testing for navigation and selection in the calendar widget.

---

## Test Scenarios and Test Cases:

| **TC ID** | **Test Scenario**      | **Test Case Description**                                                      | **Expected Result**                                                                        |
| --------- | ---------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| DP_01     | Page Load              | Verify that both date picker fields load correctly on page load.               | Both fields (Select Date, Date and Time) are visible and enabled.                          |
| DP_02     | Default Values         | Check if the default placeholder values are correct.                           | The fields should display default placeholder text such as “Select Date”.                  |
| DP_03     | Manual Date Entry      | Enter a valid date manually in the date picker input field (e.g., 10/17/2025). | The system accepts the date and displays it correctly in the expected format (MM/DD/YYYY). |
| DP_04     | Invalid Manual Entry   | Enter an invalid date (e.g., 13/40/2025).                                      | The system rejects the input or resets to the previous valid value.                        |
| DP_05     | Calendar Open          | Click the calendar icon and verify if the calendar widget opens.               | The calendar widget should open below the input field.                                     |
| DP_06     | Calendar Navigation    | Navigate between months and years using the arrows.                            | The calendar updates accordingly and displays the selected month/year.                     |
| DP_07     | Date Selection         | Select a valid date from the calendar (e.g., 25th of a month).                 | The selected date should appear correctly formatted in the input field.                    |
| DP_08     | Date-Time Picker Open  | Click on the “Date and Time” picker field.                                     | A combined date and time picker opens successfully.                                        |
| DP_09     | Time Selection         | Select a specific time (e.g., 2:30 PM) from the list.                          | The time should reflect correctly in the field with the date.                              |
| DP_10     | Manual Time Entry      | Enter a custom time manually (e.g., 08:45 AM).                                 | The picker should accept the input and reflect correctly.                                  |
| DP_11     | Date-Time Combination  | Select both date and time through the picker.                                  | The selected date and time display in the correct format.                                  |
| DP_12     | Clear Date             | Use backspace/delete to clear the date input.                                  | The field becomes empty without error.                                                     |
| DP_13     | Boundary Dates         | Try selecting very old or future years (e.g., 1900 or 2100).                   | The widget navigates to those years correctly without breaking UI.                         |
| DP_14     | Tab Navigation         | Use the keyboard Tab key to move between date and date-time fields.            | The focus moves correctly; accessibility maintained.                                       |
| DP_15     | Arrow Key Selection    | Use arrow keys to change dates after opening the picker.                       | The date changes accordingly and updates in real-time.                                     |
| DP_16     | Input Field Validation | Paste a random string (e.g., “abcd1234”) into the field.                       | The system either rejects or clears invalid input automatically.                           |
| DP_17     | Responsive Behavior    | Test on smaller screen or window size.                                         | Calendar widget resizes correctly and remains usable.                                      |
| DP_18     | Browser Compatibility  | Open page in Chrome, Firefox, and Edge.                                        | Functionality and layout remain consistent across browsers.                                |

---

## Detailed Notes and Explanations:

1. **Calendar Widget Behavior:**
   The calendar pop-up must always align below or beside the input field regardless of screen width.

2. **Date Format Validation:**
   DemoQA typically follows the **MM/DD/YYYY** format. Any entry outside this format should be handled gracefully.

3. **Accessibility Considerations:**
   Ensure that keyboard navigation (Tab, Enter, Arrow keys) and screen readers can interact with both pickers without issue.

4. **Automation Insight:**
   For Selenium automation, use date input attributes and calendar DOM controls (e.g., `driver.findElement(By.id("datePickerMonthYearInput"))`).

5. **Usability Factor:**
   Users should be able to easily distinguish between “Select Date” and “Select Date and Time” — consider tooltips or placeholder differentiation if implementing similar systems.

6. **Edge Case:**

   * Selecting February 29 on a non-leap year should either auto-correct or reject input.
   * Switching months rapidly should not freeze or cause lag.

---

## End Notes:

* Testing the **Date Picker** ensures that users can input and select dates accurately without confusion or validation errors.
* Always verify **timezone correctness** when testing “Date and Time” pickers in real-world applications.
* Automated scripts can be enhanced using **JavaScriptExecutor** to validate picker pop-ups.
* Date components are often reused across systems — so any bug here can cascade into multiple UI features (like forms, bookings, or schedulers).

---

**File:** `date_picker_testing.md`
**Category:** DemoQA UI Component Testing
**Created For:** Manual + Automation Testing documentation
