# Frames — Test Cases, Notes & Description

## Page Description

The **Frames** page (DemoQA) uses **iframes** to embed content.  
Typically, there are one or more frames shown side by side (nested HTML pages) whose content must be validated individually.

Key behaviors to test:
- Ability to switch into the frame context to read inner content (e.g. header text).
- Ensure the parent page’s content is unaffected when interacting inside a frame.
- Switching back from the frame to default content.
- Validate that frame content stays consistent even after reloads or interactions.

---

## Color Legend

| Color | Meaning |
|-------|----------|
| 🟩 Green | Happy path / normal workflows |
| 🟨 Yellow | Context switching or timing scenarios |
| 🟥 Red | Edge cases, negative behavior, frame errors |

---

## Test Cases

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|------|-------------|----------------|-------|------------------|----------------------|
| 🟩 **TC_FR_01** | Verify frame exists and is visible | Frames page is loaded | 1. Locate the iframe element <br>2. Check it’s present and displayable | The iframe is present in DOM and visible | Use `.is_displayed()` or equivalent |
| 🟩 **TC_FR_02** | Switch into frame and validate inner content | Frame on page | 1. Switch WebDriver context to the frame <br>2. Read header text inside frame | Text inside the frame matches expected (e.g. “This is a sample page”) | Use `switchTo().frame()` (Java) or `frame()` (Playwright/Puppeteer) |
| 🟨 **TC_FR_03** | Switch back to default content | Already in frame | 1. Switch back (parent) context <br>2. Verify element on parent page (e.g. page header) exists | Parent page content is accessible | Ensure you do correct switch method (e.g. `defaultContent()` vs `parentFrame()`) |
| 🟨 **TC_FR_04** | Reload frame and re-validate | In frame context | 1. Refresh frame (if possible) <br>2. Read content again | Content remains correct after reload | Some drivers require re-switching after reload |
| 🟩 **TC_FR_05** | Validate multiple frames (if present) | Page loads multiple iframes | 1. Iterate through frames <br>2. Switch to each <br>3. Validate content in each | All frames hold expected content | Do not rely on frame order — find by name or index dynamically |
| 🟥 **TC_FR_06** | Attempt interaction in frame without switching | Page loaded | 1. Try to find element inside frame without switching <br>2. Attempt click or text read | Expect error like “NoSuchElementException” or context error | Confirms the necessity of switching |
| 🟥 **TC_FR_07** | Switch to a non-existent frame | Page loaded | 1. Attempt `switchTo().frame("invalid")` or index out-of-range | Should throw a frame-not-found exception | Catch the exception and assert expected error |
| 🟨 **TC_FR_08** | Validate dynamic load delay (if content loads slower) | Page loaded | 1. Switch to frame <br>2. Wait for inner content to appear <br>3. Read content | Content shows after delay, no errors | Use explicit waits for frame load |

---

## Notes & Explanations

- When dealing with frames, you **must switch context** to inside the frame in order to interact or read content. Without this, the driver stays in the parent document and cannot see inside.  
- Use reliable frame identifiers — by `name`, `id`, or index. Avoid brittle methods like absolute XPath to the frame.  
- After switching into a frame, if the page is reloaded or navigated, **you must re-establish the frame context** (switch again).  
- Always switch back to **default content** after interacting inside a frame before doing parent-level actions.  
- Use **explicit waits** for elements within the frame — sometimes the frame loads slower than main page.  
- Test negative cases: invalid frame names, stale references, switching frames that do not exist.  
- If there are **nested frames** (iframe inside iframe), tests should handle multi-level switch appropriately (parent → child → parent).  
- Clean-up context switching in teardown to avoid stale driver context issues.

---

## Automation Snippets (Pseudo / Java / Python)

### Python (Playwright / Selenium)

```python
# Switch to frame
frame = driver.find_element(By.id("frame1"))
driver.switch_to.frame(frame)

inner_text = driver.find_element(By.tag_name("h1")).text
assert inner_text == "This is a sample page"

# Switch back to default
```
// switch to frame by name or index
driver.switchTo().frame("frame1");
String heading = driver.findElement(By.tagName("h1")).getText();
assert heading.equals("This is a sample page");

// switch back
driver.switchTo().defaultContent();
boolean visible = driver.findElement(By.id("mainHeader")).isDisplayed();
assert visible;

driver.switch_to.default_content()
assert driver.find_element(By.id("someParentElement")).is_displayed()
