# Modal Dialogs — Test Cases, Notes & Description

## Page Description

The **Modal Dialogs** page on DemoQA demonstrates two kinds of dialog boxes:
- **Small Modal** — A smaller dialog that appears on top of the main page content, containing limited text and a close button.
- **Large Modal** — A larger version with extended text content and a close button.

Testing modal dialogs ensures:
- Proper overlay appearance and dismissal.
- Correct focus trapping (background elements should not be interactable).
- Accurate content and UI consistency.
- Keyboard accessibility (like `ESC` or `Tab` handling).
- Dynamic state handling when opening/closing multiple modals.

---

## Test Cases

| **TC ID** | **Description** | **Preconditions** | **Steps** | **Expected Result** | **Notes / Edge Cases** |
|------------|------------------|-------------------|------------|----------------------|--------------------------|
| **TC_MD_01** | Verify presence of modal buttons | Page is loaded | 1. Check presence of "Small Modal" and "Large Modal" buttons | Both buttons visible and enabled | Verify visibility using `isDisplayed()` |
| **TC_MD_02** | Open Small Modal | Page loaded | 1. Click “Small Modal” button | Small modal appears in the center of the screen | Background content should dim / not be clickable |
| **TC_MD_03** | Validate Small Modal header and text | Small modal open | 1. Check modal title <br>2. Check modal body text | Title: “Small Modal” <br>Body: expected text appears | Use assert on header text |
| **TC_MD_04** | Close Small Modal using Close button | Small modal open | 1. Click “Close” button | Small modal closes and main page becomes active | Validate absence of modal element in DOM |
| **TC_MD_05** | Open Large Modal | Page loaded | 1. Click “Large Modal” button | Large modal opens with longer text content | Background content should be inaccessible |
| **TC_MD_06** | Validate Large Modal header and content length | Large modal open | 1. Check modal title and count text lines | Title: “Large Modal” <br>Text content > Small Modal | Compare character length between both modals |
| **TC_MD_07** | Close Large Modal using Close button | Large modal open | 1. Click “Close” button | Large modal closes properly | Confirm modal overlay removed |
| **TC_MD_08** | Attempt to open both modals sequentially | Page loaded | 1. Open small modal <br>2. Close it <br>3. Open large modal | Each modal works independently | Ensure no overlapping or duplication |
| **TC_MD_09** | Check focus trap inside modal | Modal open | 1. Try tabbing through elements | Focus stays within modal elements only | Accessibility behavior validation |
| **TC_MD_10** | Verify ESC key closes modal | Modal open | 1. Press ESC key | Modal should close | Keyboard control validation |
| **TC_MD_11** | Attempt background click | Modal open | 1. Click outside modal area | Modal remains open (should not close) | Tests overlay behavior |
| **TC_MD_12** | Validate modal visibility after multiple opens | After several interactions | 1. Open and close modal 3–4 times | Modal behaves consistently, no rendering issues | Checks for memory or state leakage |
| **TC_MD_13** | Validate z-index of modal overlay | Modal open | 1. Check modal CSS z-index value | Overlay and modal above all other elements | Ensures proper stacking order |
| **TC_MD_14** | Verify scroll behavior on large modal | Large modal open | 1. Scroll inside modal <br>2. Check main page scroll | Modal scrolls independently; main page fixed | Tests scroll isolation |
| **TC_MD_15** | Verify reusability after page refresh | Page reloaded | 1. Open and close both modals after refresh | Functionality remains intact | Confirms page reload resets correctly |

---

## Notes & Explanations

- Modal dialogs are **overlay elements** that block interaction with the rest of the page until dismissed.
- They should **trap keyboard focus** so users cannot navigate outside with `TAB`.
- Modals must be **center-aligned**, responsive, and rendered above all other components using proper `z-index`.
- The **Small Modal** and **Large Modal** differ mainly by content length and height, but share structure.
- Test both **UI appearance** and **behavioral logic**, including close buttons, overlay dimming, keyboard actions, and text verification.
- Ensure modals can’t be triggered repeatedly without closing — duplicate modal elements can cause memory leaks or overlapping layers.
- When closed, modals should **remove themselves completely from the DOM** (not just hide visually).

---

## Automation Snippets

### Selenium (Java)

```java
// Open Small Modal
driver.findElement(By.id("showSmallModal")).click();
WebElement smallModal = driver.findElement(By.id("example-modal-sizes-title-sm"));
assert smallModal.isDisplayed();

// Close Small Modal
driver.findElement(By.id("closeSmallModal")).click();
assert driver.findElements(By.id("example-modal-sizes-title-sm")).isEmpty();

// Open Large Modal
driver.findElement(By.id("showLargeModal")).click();
WebElement largeModal = driver.findElement(By.id("example-modal-sizes-title-lg"));
String modalText = driver.findElement(By.className("modal-body")).getText();
assert modalText.length() > 50;

// Close Large Modal
driver.findElement(By.id("closeLargeModal")).click();
assert driver.findElements(By.id("example-modal-sizes-title-lg")).isEmpty();
```

