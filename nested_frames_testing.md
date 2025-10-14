# Nested Frames — Test Cases, Notes & Description

## Page Description

The **Nested Frames** page on DemoQA features an HTML structure where one frame is embedded inside another (i.e. `iframe` within another `iframe`).  
In nested frames:
- You must switch through the parent frame into its child frame before interacting with elements inside the child frame.
- You must return up through the context stack to exit frames back to the main (default) content.
- Element access in parent and child frames must be carefully controlled to avoid context errors.

Testing nested frames ensures that your automation can correctly navigate hierarchical contexts, and that frame IDs, names, and content remain stable under load or dynamic UI changes.

---

## Test Cases

Here’s a set of test cases for nested frame behavior:

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|-------|--------------|----------------|-------|------------------|----------------------|
| **TC_NF_01** | Verify presence of parent frame | Page loaded | 1. Locate parent frame element in DOM | Parent iframe exists and is visible | Use reliable selector (id, name) |
| **TC_NF_02** | Switch to parent frame and read its content | Parent frame exists | 1. Switch context to parent frame <br>2. Fetch heading or text inside | Text content inside parent frame matches expected | Use `switchTo().frame()` or equivalent |
| **TC_NF_03** | Within parent frame, locate child (nested) frame element | In parent frame context | 1. Find nested frame element inside parent frame | Child iframe element present inside parent | Do not switch to child yet |
| **TC_NF_04** | Switch to nested child frame and read content | In parent frame | 1. Switch from parent context into child frame <br>2. Read element inside child | Content inside child frame is correct (e.g., “Child frame content”) | Use `switchTo().frame(childFrame)` |
| **TC_NF_05** | Validate switch back to parent context from child | After reading child content | 1. Switch to parent frame context <br>2. Read an element in parent frame | Parent frame element accessible and functional | Use `switchTo().parentFrame()` or equivalent |
| **TC_NF_06** | Switch from parent back to default content | In parent frame | 1. Exit to default content <br>2. Validate an element in main page | Main page element visible and interactive | Use `switchTo().defaultContent()` |
| **TC_NF_07** | Validate isolation — parent and child elements not accessible interchangeably | In default content | 1. Without switching, attempt to read child frame element | Should raise an error / no such element | Confirms context isolation |
| **TC_NF_08** | Reload nested frames and re-validate content | In child frame | 1. Refresh page or frame <br>2. Switch into frames again <br>3. Read content | Content persists as expected | After reload, frame context might fail if not re-switched |
| **TC_NF_09** | Invalid frame switch handling | In default context or parent context | 1. Try wrong frame name or index <br>2. Switch attempt | Exception or error thrown (frame not found) | Confirm robust error handling |
| **TC_NF_10** | Depth navigation consistency | Page loaded | 1. Switch into parent, then child <br>2. Do `defaultContent` <br>3. Then try switching child directly | Direct child switch fails (must go via parent) | Tests path enforcement |
| **TC_NF_11** | Nested frame content update after dynamic change | Page loaded | 1. Trigger update (if UI offers it) <br>2. Switch to nested frame <br>3. Read updated content | Child frame content reflects update | Some pages dynamically update content inside frames |
| **TC_NF_12** | Frame removal or disappearance | After initial load | 1. Remove or hide child frame via script (if possible) <br>2. Attempt to switch into child frame | Should error properly or detect absence gracefully | Good for robustness tests |

---

## Notes & Explanations

- Switching context in nested frames is hierarchical: **main → parent frame → child frame**. You cannot skip directly to child from default content without passing through the parent.  
- After any page reload or navigation, any previous frame context becomes stale; you must re-locate and re-switch frames.  
- Use robust selectors for frames (IDs, names) and avoid brittle XPath that depends on absolute positions.  
- Test negative or error pathways: switching to non-existent frames, attempting to interact without switching, or handling stale frame references.  
- Use explicit waits after switching to ensure inner elements are loaded before operations.  
- Always switch back properly: `parentFrame()` to go up one level, and `defaultContent()` to exit all frames. Incorrect switching leads to context errors.  
- If there are multiple nested layers beyond two levels, tests should be extended accordingly.  
- Logging intermediate frame handles (via `getWindowHandles` or frame ids) helps debugging context flow.

---

## Automation Snippets (Pseudo / Java / Python)

### Python (Selenium)

```python
# Switch to parent
parent = driver.find_element(By.id("frameParent"))
driver.switch_to.frame(parent)
parent_heading = driver.find_element(By.tag_name("h1")).text

# Locate and switch to child
child = driver.find_element(By.id("frameChild"))
driver.switch_to.frame(child)
child_body = driver.find_element(By.tag_name("body")).text

# Back to parent
driver.switch_to.parent_frame()
assert driver.find_element(By.tag_name("h1")).text == parent_heading

# Back to default content

driver.switch_to.default_content()
assert driver.find_element(By.xpath("//h1[text()='Nested Frames']")).is_displayed()

```

// Switch to parent frame by name or index
driver.switchTo().frame("frameParent");
String parentText = driver.findElement(By.tagName("h1")).getText();

// Switch to child frame inside parent
driver.switchTo().frame("frameChild");
String childText = driver.findElement(By.tagName("body")).getText();

// Back to parent
driver.switchTo().parentFrame();
assert driver.findElement(By.tagName("h1")).getText().equals(parentText);

// Exit to default content
driver.switchTo().defaultContent();
WebElement heading = driver.findElement(By.xpath("//h1[text()='Nested Frames']"));
assert heading.isDisplayed();

End Notes: 

 - Nested frames pose increased complexity — test scripts must rigorously manage context switching.
 - The tests above aim to cover both positive (happy path) and negative/edge behaviors.
 - In automation, always re-locate frames after page reloads, and guard against stale element references.
 - Future enhancements can include:
 - deeper nesting levels (iframe within iframe within iframe),
 - dynamic frame creation/removal,
 - parallel frame interactions,
 - visual validation via screenshot comparison inside frames.
