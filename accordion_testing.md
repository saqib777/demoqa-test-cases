# Accordion — Test Cases, Notes & Description

## Page Description

The **Accordion** page on DemoQA presents a set of expandable/collapsible panels (sections).  
Typical behavior includes:
- Clicking a section’s header toggles expansion/collapse.
- Only one panel may expand at a time (depending on implementation).
- The content inside each section is dynamically shown/hidden.
- UI state should persist across interactions.

Accordion components are common in UI design to save space and manage content visibility.

---

## Test Cases

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|-------|-------------|----------------|-------|------------------|----------------------|
| **TC_ACC_01** | Verify presence of all accordion headers | Page loaded | 1. Scroll to accordion area <br>2. Detect header titles | All section headers (e.g. “What is an accordion?”, “Where can I use it?” etc.) are present and visible | Use identifiers or header texts |
| **TC_ACC_02** | Expand first panel | Page loaded | 1. Click first section header | The panel content expands and becomes visible | Assert `aria-expanded` or appropriate CSS classes |
| **TC_ACC_03** | Collapse first panel | First panel expanded | 1. Click first section header again | The panel content collapses (hides) | Check that content is not visible / hidden in DOM |
| **TC_ACC_04** | Expand second panel when first is open | First panel expanded | 1. Click second section header | First panel collapses, second panel expands | If accordion is exclusive mode */
| **TC_ACC_05** | Expand all panels sequentially | Page loaded | 1. Click first header <br>2. Click second <br>3. Click third | Each click collapses the previous and expands the new | Verifies exclusivity logic |
| **TC_ACC_06** | Content correctness for each panel | Expand each panel | 1. Expand panel <br>2. Read inner text | Inner content matches expected descriptive text | Compare full text or substring |
| **TC_ACC_07** | Rapid toggle | Page loaded | 1. Quickly click header multiple times (e.g. 5 times) | Accordion remains stable; final state consistent | Tests debounce or collision logic |
| **TC_ACC_08** | Keyboard navigation: expand/collapse via keyboard | Page loaded | 1. Tab to header <br>2. Press `Enter` or `Space` | Panel toggles | Accessibility test |
| **TC_ACC_09** | Accessibility ARIA roles and attributes | Page loaded | Inspects markup of accordion | Each header has `role="button"` or `aria-controls`/`aria-expanded` attributes | Ensures screen reader compatibility |
| **TC_ACC_10** | Collapse one panel by expanding another | First panel expanded | 1. Expand second panel | First collapses automatically | Confirms only one can be open if exclusive mode |
| **TC_ACC_11** | Verify CSS transitions / animation | Expand / collapse panel | 1. Expand panel <br>2. Observe transition interval | Accordion animates smoothly (not instant jerk) | Test visual fluidity or presence of `transition` CSS |
| **TC_ACC_12** | Persistence after page refresh | After interacting | 1. Expand a panel <br>2. Refresh page <br>3. Check which panel is open | Accordion may revert to default (depends on design) | Behavior depends on implementation choice |
| **TC_ACC_13** | Expand panel in narrow viewport / responsive view | On mobile or small width | 1. Resize browser <br>2. Expand panel | Accordion functionality should still work | Ensure UI is responsive |
| **TC_ACC_14** | Click header when already expanded | Panel expanded | 1. Click its header again | It collapses | Tests toggle logic |
| **TC_ACC_15** | Click inside content area should not collapse | Panel expanded | 1. Click inside content area (text) | Panel stays open | Ensures collapse only by header |

---

## Notes & Explanations

- Accordions often implement via CSS classes like `.collapsed`, `.expanded` or ARIA attributes (`aria-expanded="true/false"`). Use both attribute and style checks.  
- For exclusive mode accordion, only one panel should be open at any point — others auto-collapse when opening new.  
- Rapid toggling verifies race condition safety — ensure no panel state becomes inconsistent.  
- Keyboard accessibility is important — test `Enter`, `Space`, and possibly `Arrow` keys per design.  
- ARIA compliance: `role="button"` on headers, `aria-controls` pointing to content container IDs.  
- After page reload, state persistence may or may not be expected — verify according to UI spec or default behavior.  
- Responsive behavior: on small screens, accordion should adapt—test collapse functionality across widths.  
- CSS transitions or animations add slight delay — tests should account for transition durations (use slight wait or polling).  
- Ensure clicking inside the content body (not header) does not unintentionally collapse the panel.  

---

## Automation Snippets

### Java (Selenium)

```java
// Expand first panel
driver.findElement(By.id("section1Heading")).click();
WebElement content = driver.findElement(By.id("section1Content"));
assert content.isDisplayed();

// Expand second panel
driver.findElement(By.id("section2Heading")).click();
assert !driver.findElement(By.id("section1Content")).isDisplayed();
assert driver.findElement(By.id("section2Content")).isDisplayed();
```
