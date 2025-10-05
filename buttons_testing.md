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

---

## 🧩 Detailed Test Case Explanations

### TC_01 — Default State (Page Load)
**Explanation:**  
When the Buttons page is loaded for the first time, no user interaction has occurred. This test ensures that no click-related messages are visible in the result section before any button is clicked. It confirms that the initial state of the DOM is clean, and no residual or cached messages from prior tests appear. This is important to validate a proper reset or initialization of UI components when the page is freshly loaded.

---

### TC_02 — Single Click on “Click Me” Button
**Explanation:**  
This test validates the single-click functionality of the “Click Me” button. Upon clicking, a success message should appear — typically “You have done a dynamic click.” The test ensures that this button responds specifically to a single left-click action, and not to right-click or double-click events. It also verifies correct DOM event binding (e.g., `onClick`) and ensures that the message displays correctly in both position and text.

---

### TC_03 — Double Click on “Double Click Me” Button
**Explanation:**  
This test focuses on verifying whether the button labeled “Double Click Me” properly identifies a double-click event. The system should register two consecutive clicks within a short time interval and trigger the message “You have done a double click.” It also checks that a single click does **not** mistakenly trigger the same message. This ensures that the event handler is set specifically to `ondblclick` rather than `onclick`.

---

### TC_04 — Right Click on “Right Click Me” Button
**Explanation:**  
The “Right Click Me” button should respond only to right-click events (context menu clicks). The appearance of the message “You have done a right click” validates that the `oncontextmenu` event is functioning correctly. This test also ensures that left or double clicks on this button do not produce any message — verifying strict event separation and preventing overlapping triggers.

---

### TC_05 — Double-Click then Single-Click Sequence
**Explanation:**  
This scenario checks event independence when multiple buttons are clicked sequentially. After performing a double click on one button and then a single click on another, the page should display only the last performed action’s message. This test ensures that the message container resets or updates properly, preventing message stacking or duplication. It also validates message isolation between buttons.

---

### TC_06 — Rapid Alternating Clicks
**Explanation:**  
Here, the user performs multiple rapid interactions across different buttons (single, right, and double click) within a short time. The UI should remain stable, show only the most recent valid message, and not lag, freeze, or overlap messages. This test helps identify potential race conditions in event handling and ensures efficient DOM updates under high interaction frequency.

---

### TC_07 — Mixed Click Sequences
**Explanation:**  
This test explores all possible permutations of click sequences — e.g., double → right → single, or right → single → double. It confirms that each action triggers its respective message correctly without interfering with others. The system should clear previous messages or replace them accurately. It’s an important behavioral test to confirm robust event management and DOM refresh behavior.

---

### TC_08 — Accessibility / Keyboard Click
**Explanation:**  
Accessibility testing ensures inclusivity. Here, the tester navigates to each button using the keyboard (`Tab` key for focus, `Enter` or `Space` to trigger click). The button should respond just as it would for a mouse click, displaying the correct message. This ensures ARIA compliance and validates that the buttons are not mouse-dependent. It’s a vital check for accessibility (a11y) standards.

---

### TC_09 — Long Press / Hold Action
**Explanation:**  
This test validates behavior for prolonged button press (press and hold). Since the UI is designed to respond to discrete click events, holding the mouse button should **not** produce multiple or repeated triggers. The button should register it as a single click (if released normally) or no click (if not released). This confirms
