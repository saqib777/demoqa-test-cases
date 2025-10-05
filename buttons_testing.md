# Buttons Page Testing — DemoQA

## Page Under Test
- **URL:** https://demoqa.com/buttons  
- **Feature:** Buttons with multiple click types (double click, right click, single click) and result messages.

---

## Test Cases

| TC ID | Scenario | Steps | Expected Result |
|-------|----------|-------|------------------|
| BTN_01 | Default state | Open page | No messages shown initially |
| BTN_02 | Single Click “Click Me” | Click on “Click Me” button | A message “You have done a dynamic click” (or similar) appears |
| BTN_03 | Double Click “Double Click Me” | Double-click that button | Message “You have done a double click” displayed |
| BTN_04 | Right Click “Right Click Me” | Right-click on that button | Message “You have done a right click” displayed |
| BTN_05 | Double-click then single-click | Double click, then single click another button | Only the last action message is shown |
| BTN_06 | Rapid alternating clicks | Click single, then right, then double in quick succession | Only final action’s message should persist |
| BTN_07 | Mixed click sequences | Right click + double click + single click in various order | Correct message for each action, no leftover incorrect messages |
| BTN_08 | Accessibility / keyboard click | Use keyboard (if possible) to focus + activate buttons | Buttons should respond and message updates accordingly |
| BTN_09 | Corner case: long-press | Press and hold on the button | Should behave as a single click (unless defined otherwise) |
| BTN_10 | Cross-browser consistency | Perform above actions in Chrome, Firefox, Edge | Same messages and behavior across browsers |

---

## Notes / Observations

- ✅ Buttons must respond correctly to their respective action types (single, double, right click).  
- ✅ Only one message should be visible at a time; previous messages should be replaced or cleared.  
- ✅ The “Right Click Me” and “Double Click Me” buttons must behave independently and not interfere with each other.  
- ✅ Rapid or mixed actions should not produce multiple overlapping messages.  
- ✅ Keyboard or accessibility support: users without mouse should be able to trigger (if enabled).  
- ✅ Layout and positioning of buttons should remain stable even after message appears.  
- ✅ Cross-browser UI parity (message text, button responsiveness) is important.  
- ✅ Edge case: what happens on invalid clicks or mis-clicks (e.g. clicking outside the button).  

---

