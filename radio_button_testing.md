# Radio Button Page Testing — DemoQA

## Page Under Test
- **URL:** https://demoqa.com/radio-button  
- **Feature:** Radio button options (“Yes”, “Impressive”, “No”) with message output.

---

## Test Cases

| TC ID | Scenario | Steps | Expected Result |
|-------|----------|-------|------------------|
| RB_01 | Default state | Open page | No radio button is selected initially |
| RB_02 | Select “Yes” | Click “Yes” | “Yes” becomes selected and message displays “You have selected Yes” |
| RB_03 | Select “Impressive” | Click “Impressive” | “Impressive” becomes selected and message displays “You have selected Impressive” |
| RB_04 | Selecting “No” (disabled) | Click “No” | Should not be selectable or should ignore click |
| RB_05 | Switching selection | Click “Yes”, then click “Impressive” | “Yes” is deselected, “Impressive” becomes selected |
| RB_06 | Re-click same selected | Click “Yes” when “Yes” is already selected | Selection remains on “Yes”, message remains correct |
| RB_07 | Message accuracy | After selecting each option, check message text | Message should exactly match “You have selected {option}” |
| RB_08 | Rapid selection changes | Quickly click “Yes” then “Impressive” multiple times | Final selection should stabilize reliably |
| RB_09 | Browser back/forward behavior | Select one option → refresh or navigate back → reload page | Page should reset or maintain behavior as per design |
| RB_10 | Accessibility / keyboard | Use Tab + Space/Enter to navigate and select | Radio buttons should be selectable via keyboard and message updates |

---

## Notes / Observations

- ✅ The “No” radio button is **disabled** (cannot be clicked) — this is intended behavior.  
- ✅ The message area updates immediately upon selection.  
- ✅ Only one radio button should be selectable at a time (mutual exclusivity).  
- ✅ Rapid toggling should not cause inconsistent UI or crash.  
- ✅ Verify keyboard accessibility and focus states.  
- ✅ Check message text formatting (capitalization, punctuation).  
- ✅ On page reload, selection resets (expected for demo).  
- ✅ Cross-browser check: behavior should match in Chrome, Firefox, Edge.  
- ✅ Consider screen reader feedback: aria attributes should indicate selection.  

---

## Detailed Notes for Each Test Case

### RB_01 — Default state
- When the page loads, **no radio button should be preselected**.  
- This ensures users start with a neutral state and must explicitly choose.  
- If any option is already selected, it may mislead users or cause incorrect assumptions.

---

### RB_02 — Select “Yes”
- Clicking on “Yes” should mark the radio button as selected.  
- A message box should update with the exact text: **“You have selected Yes”**.  
- This validates that the selection triggers the expected event and UI feedback.

---

### RB_03 — Select “Impressive”
- Similar to RB_02 but validates another option.  
- After clicking, “Impressive” must be selected and message must show **“You have selected Impressive”**.  
- Confirms that each option has a unique and correct output message.

---

### RB_04 — Selecting “No” (disabled)
- The “No” radio button is visibly present but **disabled**.  
- Clicking should have **no effect**: no highlight, no message update.  
- Confirms that disabled options cannot be interacted with, preventing user confusion.

---

### RB_05 — Switching selection
- Selecting “Yes” first, then “Impressive” should **deselect “Yes”**.  
- Radio buttons must enforce **mutual exclusivity** — only one selection at a time.  
- Verifies correct group behavior of radio buttons.

---

### RB_06 — Re-click same selected
- Clicking an already selected option (“Yes” when “Yes” is active) should not change state.  
- Message should remain unchanged.  
- This ensures stability and avoids unnecessary re-triggering of events.

---

### RB_07 — Message accuracy
- After each selection, message text must be **exactly correct**:  
  - “You have selected Yes”  
  - “You have selected Impressive”  
- This test checks for typos, case-sensitivity, spacing, and punctuation issues.

---

### RB_08 — Rapid selection changes
- Quickly clicking between “Yes” and “Impressive” multiple times should result in a **stable final state**.  
- The last clicked option should remain selected and message should match.  
- Helps ensure no lag, freeze, or incorrect dual-selection bug occurs.

---

### RB_09 — Browser back/forward behavior
- After selecting an option, refreshing or navigating away then back should reset the page state.  
- This validates how the application handles **session persistence**.  
- In demo environments, selections usually reset (expected behavior).  

---

### RB_10 — Accessibility / keyboard
- Users should be able to tab into the radio group and use **Space/Enter** to select.  
- Focus highlight should be visible.  
- Message box should update same as with mouse click.  
- Confirms accessibility compliance for keyboard-only and assistive technology users.

---

## General Notes for Radio Button Testing

1. **Mutual Exclusivity**  
   - Only one radio button in a group should be selectable at a time.  
   - Ensure no scenario exists where two options appear selected simultaneously.

2. **Disabled State Validation**  
   - Disabled options (“No”) should remain unclickable and provide no feedback.  
   - Confirms that the system prevents invalid selections.

3. **UI Feedback**  
   - The output message must always match the selected radio option exactly.  
   - Typos or incorrect mapping reduce user trust.

4. **Cross-Browser Compatibility**  
   - Test across browsers (Chrome, Firefox, Edge, Safari) to ensure consistent behavior.  
   - Special attention to keyboard navigation differences between browsers.

5. **Responsiveness**  
   - On smaller screens, the radio buttons and output message should remain visible and usable.  
   - Verify no layout breaking or overlapping text.

6. **Accessibility Considerations**  
   - Radio buttons must be accessible via keyboard (Tab, Arrow keys, Space/Enter).  
   - Labels should be properly linked with inputs (`<label for="id">`).  
   - Screen readers should announce the selected option correctly.

7. **Performance / Stress Testing**  
   - Rapid or repeated clicks should not freeze UI or delay message updates.  
   - Helps check robustness under fast user interactions.

8. **Reset and Refresh Behavior**  
   - Refreshing or reloading the page should reset the state to “no option selected”.  
   - Confirms correct default state handling.

9. **Visual Indicators**  
   - Selected state must be clearly distinguishable (color or marker).  
   - Disabled state must look different from active options to avoid confusion.

10. **Error Prevention**  
    - Users should never end up in an undefined state (e.g., blank message after valid selection).  
    - The system should always provide clear feedback for any valid action.

---


