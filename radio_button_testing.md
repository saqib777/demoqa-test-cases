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

You can add this file via GitHub:
1. **Add file → Create new file**  
2. Name it `radio_button_testing.md`  
3. Paste the content above  
4. Commit to `main`  

If you like, I can also bundle this into your repo’s ZIP and send it to you so you just push. Do you want me to zip it now?
::contentReference[oaicite:0]{index=0}
