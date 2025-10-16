# Autocomplete — Test Cases, Notes & Description

## Page Description

The **Autocomplete** page provides input boxes that suggest options as you type (auto-complete behavior).  
Often two modes are present:
- **Single Autocomplete**: You type text, the component shows suggestions, and you select one.
- **Multiple Autocomplete**: You can select multiple suggestions, sometimes with tags or chips.

Key behaviors to test:
- Suggestions appear as the user types.
- Selecting a suggestion populates the input.
- Clearing selections works correctly.
- Suggestions respond to partial matches, case differences, whitespace.
- Edge cases: no matching suggestions, typing too fast, suggestions gone.

---

## Test Cases

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|-------|-------------|----------------|-------|------------------|----------------------|
| **TC_AC_01** | Verify single-mode suggestion list appears | Page loaded | 1. Click single autocomplete input <br>2. Start typing few characters (e.g. “A”) | Suggestions dropdown appears with matching values | Dropdown should appear only after minimal input (maybe 1 character) |
| **TC_AC_02** | Select a suggestion in single mode | Suggestions visible | 1. Click one of the suggested entries | The suggestion is inserted into the input | Input’s value matches chosen suggestion |
| **TC_AC_03** | Case-insensitive matching | Page loaded | 1. Type lowercase or uppercase variant (e.g. “bLuE” instead of “Blue”) | Suggestions should include correct matches | Matching algorithm should ignore case |
| **TC_AC_04** | Partial substring matching | Page loaded | 1. Type partial substring (e.g. “rea” for “Bread”) | Suggestion list includes “Bread” | Tests in-string matching, not only prefix |
| **TC_AC_05** | No match results | Page loaded | 1. Type a random string with no matches (e.g. “xyzabc”) | No suggestions or display “No options” | Suggestion box should reflect absence |
| **TC_AC_06** | Clear suggestion in single mode | A suggestion chosen | 1. Clear input (backspace or delete) | Input becomes empty and suggestions vanish | No residual selection |
| **TC_AC_07** | Multiple autocomplete: multiple picks | Page loaded | 1. Type “Red” <br>2. Select suggestion <br>3. Type “Blue” <br>4. Select suggestion | Both suggestions appear as tags or values | Ensures multi mode works |
| **TC_AC_08** | Remove a selection in multi mode | Multiple suggestions selected | 1. Click remove icon (x) on one suggestion chip | That suggestion is removed but others remain | Ensure UI updates correctly |
| **TC_AC_09** | Suggestion list updates dynamically | Page loaded | 1. Type “B” <br>2. Note list <br>3. Type “Bl” <br>4. Observe list updates | List filters down as characters increase | Dynamic filtering should work |
| **TC_AC_10** | Fast typing no glitches | Page loaded | 1. Quickly type a string (e.g. “Green”) without pauses | Suggestions respond smoothly without errors | Tests debounce or throttle logic |
| **TC_AC_11** | Keyboard navigation through suggestions | Suggestions visible | 1. Type “Re” <br>2. Use arrow keys (up/down) to navigate <br>3. Press Enter | Highlight moves and pressing selects matching option | Accessibility / keyboard usability |
| **TC_AC_12** | Suggestion list closes when clicking outside | Suggestions visible | 1. Click outside the input area | Suggestion dropdown disappears | Behavior reset |
| **TC_AC_13** | Input placeholder / default text validation | Page loaded | 1. Inspect input placeholder attribute | Placeholder matches design spec (e.g. “Type color”) | Validate HTML placeholder text |
| **TC_AC_14** | Max suggestions limit enforcement | Page loaded | 1. Type “a” or broad character with many matches | Suggestion list shows only up to max number (e.g. 5 or 10) | Ensures UI is not overloaded |
| **TC_AC_15** | Clear all selections (multi mode) | Multi selections exist | 1. Use a “clear all” control (if exists) or delete chips <br>2. Ensure input cleared | No suggestions or tags remain | Some UIs support “clear all” |

---

## Notes & Explanations

- Autocomplete relies heavily on **debounce logic**, i.e., waiting before fetching suggestions; tests should account for small delay.
- Matching behavior (prefix, substring, fuzzy) depends on implementation — tests should verify according to spec.
- Must handle **empty state** gracefully — no suggestions if input empty or whitespace-only.
- Keyboard navigation (arrow keys, Enter, Esc) is critical for accessibility — must be tested thoroughly.
- Multi-autocomplete sometimes shows suggestion chips or tags — removal and re-adding should be robust.
- Click outside or blur events should hide suggestions.
- The system may impose a **maximum number of suggestions** shown — test for overflow limits.
- Fast typing and backspace should filter suggestions smoothly — watch UI flicker or stale dropdowns.
- Focus management: after selecting a suggestion, focus may stay in input or move — verify correct behavior.
- Ensure cleanup: deselect or remove tags to ensure test isolation.
- Cross-browser behavior differences in dropdown styling or event handling should be considered.

---

## Automation Snippets

### Selenium (Java)

```java
WebElement singleInput = driver.findElement(By.id("autoCompleteSingleInput"));
singleInput.sendKeys("Re");
List<WebElement> options = driver.findElements(By.cssSelector(".auto-complete__option"));
options.get(1).click();
assert singleInput.getAttribute("value").equals("Red");
