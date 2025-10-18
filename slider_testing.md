# Page Under Test  
**DemoQA Slider** – [https://demoqa.com/slider](https://demoqa.com/slider)  

---

## Objective  
To ensure the slider control works correctly: it responds to user actions (drag, arrow keys, input), respects min/max values, updates visible value correctly, and behaves consistently across browsers and screen sizes.

---

## Scope  
- Functional behavior of the slider control  
- Boundary conditions (minimum, maximum, middle, edge)  
- Keyboard interaction (arrow keys, tab navigation)  
- Manual input (if slider allows entering value) / Output display  
- Cross-browser and responsive behaviour  

---

## Test Scenarios & Test Cases  

| TC ID | Test Scenario | Test Case Description | Expected Result |
|-------|--------------|-----------------------|----------------|
| SL_01 | Page Load | Load the page and verify the slider element is visible and enabled. | Slider appears, value displays correctly (default) and is enabled for interaction. |
| SL_02 | Default Value | Check the starting value of the slider (before any interaction). | The value shown is as per specification (e.g., 25 if default is 25). |
| SL_03 | Drag Slider to Middle | Drag the slider handle to a midpoint (e.g., ~50% of range). | Value updates dynamically and shows approx midpoint value. |
| SL_04 | Drag Slider to Minimum | Drag the handle fully to the left (minimum). | Value updates to minimum value (e.g., 0) and stops at the limit. |
| SL_05 | Drag Slider to Maximum | Drag fully to the right (maximum). | Value updates to maximum (e.g., 100 or defined max) and cannot go beyond. |
| SL_06 | Arrow Key Decrease | With focus on slider, press Left Arrow (or Down Arrow) to decrease value. | Value decreases by one increment and updates two things: the display and underlying property. |
| SL_07 | Arrow Key Increase | With focus on slider, press Right Arrow (or Up Arrow) to increase value. | Value increases by one increment and updates display. |
| SL_08 | Keyboard Home/End Keys | With focus, press Home (go to minimum) and End (go to maximum). | Home sets to minimum; End sets to maximum. |
| SL_09 | Manual Value Setting (if input allowed) | If slider allows direct input of value, type a valid number (within range). | Slider handle moves accordingly; value display shows typed value; no error. |
| SL_10 | Manual Value Outside Range | Type a value outside the allowed range (e.g., -10 or 200). | Input is either rejected, reset to boundary, or shows validation message depending on spec. |
| SL_11 | Mouse Click on Track | Click at a position on the slider track (not dragging) to move handle there. | Handle jumps to clicked position; value updates accordingly. |
| SL_12 | Thumb Focus & Tab Navigation | Tab into the slider, ensure focus is visible, then interact. | Slider receives focus properly; keyboard interactions function; focus styling visible. |
| SL_13 | Responsive Behavior | Resize browser to smaller width (tablet/mobile) and test slider. | Slider remains visible, functional, and usable on smaller screen. |
| SL_14 | Browser Compatibility | Test slider on Chrome, Firefox, Edge. | Behavior and appearance consistent across browsers; no functional variance. |
| SL_15 | Increment Step Verification | Verify the slider changes in correct step size (e.g., increments of 1). | Each interaction changes value by expected step and no fractional or unexpected jumps. |
| SL_16 | Drag Fast & Release | Drag the handle quickly and release at random positions. | Value should reliably reflect handle position; handle doesn’t get stuck or mis‐place. |
| SL_17 | Tab Out Validation | After changing slider value, use Tab to move out and check application state. | Value remains as set; no unintended reset or error on blur. |
| SL_18 | Value Persistence After Refresh | Change slider value, refresh page and verify whether value resets or persists (as per spec). | Value resets to default or persists depending on requirement; behavior is consistent. |

---

## Detailed Notes & Explanations  

- **Slider Interaction Types:**  
  Dragging handle, clicking track, keyboard arrows/keys (Home/End), clicking input field (if exists) each represent a different interaction mode. All should map to underlying slider value and UI display.

- **Boundary Behavior:**  
  The slider must respect min and max values. Dragging beyond should either stop or be prevented. Arrow keys should not move handle beyond limits.

- **Increment Steps:**  
  If slider is defined with a step size (e.g., increment of 5 units), each value change must adhere to the step. Random increments indicate a bug.

- **Keyboard Accessibility:**  
  Slider should be focusable and controlled via keyboard. Tab navigation, arrow keys and accessibility labeling (aria attributes) are important for inclusivity.

- **Responsive & Cross-browser Considerations:**  
  On smaller screens, drag/touch gestures may behave differently. Use both mouse and touch simulation. Ensure appearance and functionality remain consistent across browsers.

- **Manual Entry vs Slider UI Sync:**  
  If there is an input box representing the slider value, test synchronization: changing one changes the other. Ensure invalid manual entries are handled gracefully.

- **Performance & Stability:**  
  Rapid or repeated interactions (dragging fast) should not cause the slider UI to freeze, jump, or misreport value.

- **Regression Impact:**  
  Sliders often are reused in forms like volume controls, price ranges, etc. Defects here may propagate across application flows.

---

## End Notes  
Testing a slider component may seem straightforward, but subtle bugs often hide in boundary conditions, keyboard interactions, and responsive contexts. Ensuring full coverage across interaction types (drag, keyboard, click, manual entry) helps uncover issues early.  
In automation, handling sliders often uses `Actions` class (Selenium) with `dragAndDropBy()` or offset clicks. :contentReference[oaicite:1]{index=1}  
When you design your repository, consider adding a short automation script folder (e.g., `slider_tests.py`) to accompany this documentation.

**File Name:** `slider_testing.md`  
**Category:** DemoQA UI Component Testing  
**Created For:** Manual & Automation testing coverage.

