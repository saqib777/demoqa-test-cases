# Selectable Component — Test Cases, Notes & Description

## Page Description  
The “Selectable” component on DemoQA allows users to select one or more items from a UI list or grid.  
It supports clicking, multi-selection (Ctrl/Shift keys), dragging selection boxes, and deselecting items.  
This component is often used in UI workflows where multiple choices are possible (e.g., selecting files, items in a list, etc.).

---

## Test Cases

| TC ID       | Description                                             | Pre-condition                        | Steps                                                                 | Expected Result                                                    | Notes / Edge Cases                                      |
|-------------|---------------------------------------------------------|--------------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------------|--------------------------------------------------------|
| **TC_SEL_01** | Verify list view is visible and items are selectable     | Page loaded                          | 1. Navigate to Selectable page <br>2. Click on “List” tab if needed  | List of items (Item 1…Item 7) appears and each is visible & enabled | Use a locator list for items                          |
| **TC_SEL_02** | Select a single item in list view                        | List view visible                    | 1. Click “Item 1”                                                      | “Item 1” becomes highlighted/selected; others remain unselected   | Check CSS class/state of selected item                |
| **TC_SEL_03** | Select multiple adjacent items using Shift in list view  | List view visible                    | 1. Click “Item 1” <br>2. Hold Shift and click “Item 3”                | Items 1, 2, 3 all selected                                         | Check use of Shift key behavior                       |
| **TC_SEL_04** | Select multiple non-adjacent items using Ctrl/Cmd        | List view visible                    | 1. Hold Ctrl (or Cmd on Mac) <br>2. Click “Item 1”, “Item 3”, “Item 5” | Items 1, 3, 5 selected; others not selected                        | Platform differences: Ctrl vs Cmd                     |
| **TC_SEL_05** | Deselect a selected item using Ctrl                       | Multiple selected items              | 1. From items selected above, Ctrl-click “Item 3”                     | Items 1 and 5 remain selected; item 3 is deselected                 | Ensure state toggles on Ctrl-click                    |
| **TC_SEL_06** | Drag to select a range of items in list view             | List view visible                    | 1. Click and drag from Item 2 to Item 6                                | Items 2-6 become selected                                         | Test mouse drag behavior; verify range selection      |
| **TC_SEL_07** | Switch to the “Grid” view and attempt selection          | Grid tab available                   | 1. Click “Grid” tab <br>2. View items                                 | Grid layout appears, items labeled (e.g., Item 1…Item 9)         | Some items repositioned in grid view vs list view     |
| **TC_SEL_08** | Select items in grid view                                | Grid view visible                    | 1. Click “Item 2” <br>2. Ctrl-click “Item 4”, “Item 7”                | Items 2, 4, 7 selected                                              | Confirm multi-selection works in grid context         |
| **TC_SEL_09** | Deselect all selected items                              | Items selected                        | 1. Click “Clear” or click outside list (if supported)                 | No items are highlighted/selecting state reset                     | If no clear button, clicking outside should deselect  |
| **TC_SEL_10** | Keyboard navigation and selection                         | List or Grid view visible            | 1. Tab to first item <br>2. Use arrow keys to navigate <br>3. Press Space or Enter | Focus moves; pressing selects the focused item                     | Accessibility: focus styling, keyboard select         |
| **TC_SEL_11** | Responsive behavior on smaller screen                     | Resize browser window                | 1. Use mobile viewport <br>2. Attempt selection                       | Component remains usable; items selectable; layout appropriate     | Test touch vs mouse on mobile                         |
| **TC_SEL_12** | State persistence after page reload                       | Items selected                        | 1. Select some items <br>2. Reload the page                           | Either selections persist (if spec says) or reset (consistently)   | Compare behavior with spec                            |
| **TC_SEL_13** | Performance under rapid selection                        | List/Grid visible                    | 1. Quickly click many items or drag repeatedly                        | No UI glitches; selection state consistent                         | Check for UI lag or missed clicks                     |
| **TC_SEL_14** | Accessibility – ARIA roles & multi-select attributes       | Page loaded                          | 1. Inspect WK DOM <br>2. Verify role=”listbox” or “grid” and aria-selected properties | Items reflect correct aria attributes when selected/deselected     | Screen reader compatibility                           |
| **TC_SEL_15** | Negative: attempt keyboard deselect when none selected    | No items selected                    | 1. Press Ctrl, Shift or use keyboard deselect                         | No crash; selection remains none; UI remains stable                | Ensure no error thrown                                |

---

## Notes & Explanations

- The component supports **multiple selection modes**: single click, Ctrl/Cmd click, Shift click, drag-select.  
- Ensure the correct **selection state** is reflected visually (highlight, background color) as well as in the DOM (CSS class or attribute).  
- Proper handling of **keyboard interactions** is important for accessibility; focus and selection should be controllable without mouse.  
- For grid vs list view, verify layout changes, selection behavior remains consistent.  
- On mobile/touch devices, test tap vs long-press vs drag selection if supported.  
- Rapid interactions or drag and drop can sometimes cause state sync issues — performance and visual consistency should be validated.  
- State persistence (if required) across reload or navigation should be defined by spec — test accordingly.  
- Accessibility: Each selectable list item should have correct ARIA attributes (`role`, `aria-selected`, appropriate focus).  
- Edge conditions: No items selected, all items selected, partial selection, unexpected deselection should not cause UI failures.  
- Integration: If selectable component is part of larger page (e.g., interactions tab), assure other components don’t interfere with its behavior.

---

## Automation Snippets (Pseudo Code / Python / Java)

### Python (Selenium)

```python
# Single selection
item1 = driver.find_element(By.XPATH, "//li[text()='Item 1']")
item1.click()
assert 'selected' in item1.get_attribute('class')

# Multi-select using Ctrl (Windows)
from selenium.webdriver import ActionChains
item2 = driver.find_element(By.XPATH, "//li[text()='Item 2']")
item4 = driver.find_element(By.XPATH, "//li[text()='Item 4']")
actions = ActionChains(driver)
actions.key_down(Keys.CONTROL).click(item2).click(item4).key_up(Keys.CONTROL).perform()
assert 'selected' in item2.get_attribute('class')
assert 'selected' in item4.get_attribute('class')

# Drag select (if supported)
actions.drag_and_drop(item3, item6).perform()
# Or use click and move
```

```
WebElement item1 = driver.findElement(By.xpath("//li[text()='Item 1']"));
item1.click();
assertTrue(item1.getAttribute("class").contains("selected"));

Actions builder = new Actions(driver);
WebElement item2 = driver.findElement(By.xpath("//li[text()='Item 2']"));
WebElement item4 = driver.findElement(By.xpath("//li[text()='Item 4']"));
builder.keyDown(Keys.CONTROL).click(item2).click(item4).keyUp(Keys.CONTROL).build().perform();
assertTrue(item2.getAttribute("class").contains("selected"));
assertTrue(item4.getAttribute("class").contains("selected"));
```

End Notes

The “Selectable” component is deceptively simple, but supports a rich set of interactions (click, multi-select, drag, keyboard) all of which must behave consistently, responsively, and accessibly.
Testing it ensures that end-users can reliably pick one or multiple items, using whichever device or input method they prefer.
Any regression in this component (especially after script or layout changes) can degrade UX significantly — for example, missing multi-select support will frustrate power users.
Therefore it is wise to include this component in both functional test suits and regression automation.
