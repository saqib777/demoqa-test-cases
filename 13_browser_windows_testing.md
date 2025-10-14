# Browser Windows – Test Cases, Notes & Description

## Page Description

The **Browser Windows** page in DemoQA provides buttons that open new browser contexts:  
- **New Tab** — opens a new browser tab  
- **New Window** — opens a separate window  
- **New Window Message** — opens a window (or popup) containing a message  

The goal of tests here is to verify:
1. That new windows / tabs open correctly  
2. That context switching works (parent ↔ child)  
3. That content in child windows is correct  
4. That closing, navigation, and cleanup behave as expected  

According to documentation:  
> “Taking an example of ToolsQA demo site … click on ‘New Window’ button … WebDriver must switch context to the child window and read the text.” :contentReference[oaicite:0]{index=0}

---

## Color Key / Marking Legend (for visual differentiation)

- 🟩 **Green** — Normal / happy‐path flow  
- 🟨 **Yellow** — Timing / waiting / context switching complexity  
- 🟥 **Red** — Edge cases / negative / cleanup / error conditions  

You can annotate test rows or text with these colors in your Markdown viewer.

---

## Test Cases

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|---|-------------|----------------|-------|------------------|---------------------|
| **TC_BW_01** 🟩 | New Tab opens with correct content | Parent window loaded | 1. Click “New Tab” <br>2. Switch to new tab <br>3. Read content | Child tab opens & content (e.g. “This is a sample page”) visible | Ensure switch logic handles multiple windows |
| **TC_BW_02** 🟩 | New Window opens & content visible | Parent window loaded | 1. Click “New Window” <br>2. Switch to new window <br>3. Read heading/text | Child window opens & correct content shown | Window handle switching must be robust |
| **TC_BW_03** 🟨 | New Window Message shows custom message | Parent window loaded | 1. Click “New Window Message” <br>2. Switch to that window <br>3. Read message | Popup window or message window appears with expected text | Some windows are not full HTML pages (may lack standard DOM) |
| **TC_BW_04** 🟨 | Parent window still active after child open | After opening child window | 1. Switch back to parent <br>2. Confirm parent title or element present | Parent window remains functional and its content accessible | Ensure focus returns properly |
| **TC_BW_05** 🟥 | Multiple child windows open & manage them | Parent window loaded | 1. Click “New Tab” & “New Window” & “New Window Message” <br>2. Gather all window handles <br>3. Iterate through each child and verify content <br>4. Close each child <br>5. Return to parent | All child windows are handled, closed, and parent remains | Be careful with ordering and handle identification |
| **TC_BW_06** 🟥 | Closing child window and then performing parent actions | After child window open | 1. Close child window <br>2. Switch to parent <br>3. Attempt parent interaction | Parent actions succeed (e.g. clicking button) | If context not switched, may cause “no such window” errors |
| **TC_BW_07** 🟨 | Timing / wait for window handle appearance | Parent window loaded | 1. Click child button <br>2. Poll getWindowHandles until count increases <br>3. Switch <br>4. Validate content | Delay handling works; test waits as required | Use explicit wait for new window handle |
| **TC_BW_08** 🟥 | Behavior if child window closes unexpectedly | After opening child | 1. Open child <br>2. Close it manually or via script <br>3. Switch back to parent <br>4. Perform action | No error; parent context stable | Handles thrown exceptions gracefully |
| **TC_BW_09** 🟥 | Attempt to access child content before switching | Parent window loaded | 1. Click “New Window” <br>2. Without switching, try find child element <br>3. Expect failure or error | Throws “no such element” or “context not found” | Validates that switching is mandatory |
| **TC_BW_10** 🟩 | Verify window handles list size | Parent window loaded | 1. Get current handles count <br>2. Click child open <br>3. Get handles count again | New count = previous + 1 | Ensures handle tracking works reliably |

---

## Notes and Explanations

- The **window handle** concept is central: use `getWindowHandles()` and `getWindowHandle()` to manage switching. :contentReference[oaicite:1]{index=1}  
- Always keep the **parent window handle** stored before opening child windows, so you can reliably switch back.  
- **Switching logic**: iterate through all handles and pick those != parent.  
- Some child windows (e.g. message window) might not be full HTML pages or might not have full DOM — tests must adapt accordingly.  
- Wait strategy: after clicking “New Window,” wait for the handle set to grow (e.g., via explicit wait or polling) rather than fixed sleep.  
- Clean-up: close child windows after verification so they don’t clutter or cause side effects.  
- Edge condition: if child window fails to open (due to browser popup blocking), test should detect and report gracefully.  
- In multi-window scenarios, order of handles is **not guaranteed**, so do not assume the second handle is always the child.  
- Switching focus is essential — if you attempt to interact without switching, Selenium will report no such element.  
- After closing child, ensure your driver context returns to parent before further commands; otherwise “no such window” errors appear.

---

## Sample Automation Snippets (Pseudo / Selenium or Playwright style)

```python
# Python / Playwright style
main = page.context.pages[0]  # parent
page.click("#windowButton")
# wait and get all pages
new_page = page.context.wait_for_event("page")
assert "sample" in new_page.locator("h1").text_content()
new_page.close()
# back to parent
assert main.is_visible("#windowButton")

---

// JavaScript / WebDriver style
const parent = await driver.getWindowHandle();
await driver.findElement(By.id("messageWindowButton")).click();
const handles = await driver.getAllWindowHandles();
for (const h of handles) {
  if (h !== parent) {
    await driver.switchTo().window(h);
    const bodyText = await driver.findElement(By.tagName("body")).getText();
    // validate message content
    await driver.close();
  }
}
await driver.switchTo().window(parent);

---

// JavaScript / WebDriver style
const parent = await driver.getWindowHandle();
await driver.findElement(By.id("messageWindowButton")).click();
const handles = await driver.getAllWindowHandles();
for (const h of handles) {
  if (h !== parent) {
    await driver.switchTo().window(h);
    const bodyText = await driver.findElement(By.tagName("body")).getText();
    // validate message content
    await driver.close();
  }
}
await driver.switchTo().window(parent);

---
