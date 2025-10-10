# Dynamic Properties — Test Cases, Notes, and Description

## Page Description

The **Dynamic Properties** page includes UI elements whose properties change over time or under certain conditions.  
Common dynamic behaviors include:
- Button(s) becoming enabled after a delay  
- Button(s) changing color after some time  
- A button or element that appears (becomes visible) after a delay  
- Perhaps changes when you hover, or properties like “will enable after 5 seconds” etc.

Because the UI is dynamic, tests must incorporate **timing, waits, state verification**, and careful handling of asynchronous behavior.

---

## Test Cases

Below is a set of test cases tailored to typical dynamic property behaviors. You can adapt according to the actual behavior on DemoQA’s implementation.

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|---|-----------------------------|----------------|-------|---------------------|----------------------|
| TC_DP_01 | Verify that a button is initially disabled | Page is loaded | 1. Inspect the button that should enable later | The button is disabled initially | Confirm disabled property (e.g. `disabled` attribute) |
| TC_DP_02 | Verify button becomes enabled after delay | Page is loaded | 1. Wait for the specified delay (e.g. 5 seconds) <br>2. Check the button’s enabled state | The button becomes clickable/enabled | Use explicit wait rather than fixed sleep if possible |
| TC_DP_03 | Verify color change after time | Page is loaded | 1. Get initial CSS color property of element <br>2. Wait for change interval <br>3. Get new CSS color | The CSS color property should change as per spec | Assert that old color ≠ new color |
| TC_DP_04 | Verify element appears after delay (becomes visible) | Page is loaded | 1. Ensure element is not visible initially <br>2. Wait for the appearance delay <br>3. Check that element is now visible | Element becomes visible after delay | Visibility checks: display, opacity, presence in DOM |
| TC_DP_05 | Verify hover or focus triggers change (if applicable) | Page loaded & element visible | 1. Hover/focus over element <br>2. Observe any property change | A style or property change should occur (e.g. color, border) | Use proper hover simulation in automation |
| TC_DP_06 | Timing precision / boundary test | Page loaded | 1. Check just before the delay <br>2. Then exactly at the delay <br>3. Then after delay | Behavior should change exactly at or after the defined time, not too early | Use high-resolution wait or time measurement |
| TC_DP_07 | Verify no flicker / transient states | Page loaded | 1. Monitor the changing element over the interval <br>2. Observe intermediate states | No unintended intermediate states or flickering before final state | Helps detect flapping behavior |
| TC_DP_08 | Cross-browser dynamic behavior consistency | Page loaded | 1. Perform tests in Chrome, Firefox, Edge <br>2. Compare timing and state changes | Same behavior across browsers (enable time, visibility, color) | Account for browser-specific rendering delays |

---

## Notes and Explanations

- Because elements change over time, **explicit waits** should be used (e.g. `waitFor`, `ExpectedConditions`) instead of simple sleeps, to avoid brittle tests.  
- Use **time measurement** (timestamps) to verify correct delay, not just pass/fail.  
- CSS property changes may require reading **computed style** rather than inline style attribute.  
- Visibility changes might be implemented by changing CSS properties (`visibility`, `display`, `opacity`), or moving elements in/out of DOM — your tests need to inspect accordingly.  
- Some dynamic features may use CSS transitions or animations — account for the transition duration before asserting final state.  
- Consider adding **margins** (small buffer) to waits (e.g. wait 5.2 seconds for a 5-second enable) to account for slight delays.  
- Ensure your tests do **cleanup or reset state** if interacting (though dynamic properties often don’t persist).  
- For cross-browser consistency, tests should include tolerance ranges (e.g. ±100 ms) because rendering engine timings vary slightly.  

---

## Sample Automation Snippets (Pseudo / Playwright style)

```python
# Example: Wait for enable
button = page.locator("#enableAfter")
assert not button.is_enabled()
page.wait_for_timeout(5500)  # 5.5 seconds
assert button.is_enabled()
```
// Selenium Java: wait until enabled
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
WebElement btn = driver.findElement(By.id("enableAfter"));
assertFalse(btn.isEnabled());
wait.until(ExpectedConditions.elementToBeClickable(btn));
assertTrue(btn.isEnabled());

// Example: CSS color change assertion (for color change test)
const elem = await page.locator("#colorChange");
const initialColor = await elem.evaluate(el => window.getComputedStyle(el).color);
await page.waitForTimeout(6000);
const changedColor = await elem.evaluate(el => window.getComputedStyle(el).color);
if (initialColor === changedColor) {
  throw new Error("Color did not change after expected delay");
}

