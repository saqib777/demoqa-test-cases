
# TEST PLAN: https://demoqa.com/select-menu


## Page Components
- Select Value (custom single-select, searchable)
- Select One (custom single-select, non-searchable)
- Old Style Select Menu (native <select>)
- Multi Select Dropdown (custom, tokens)
- Standard Multi Select (native <select multiple>)

────────────────────────────────────────────
## TEST CASES
────────────────────────────────────────────
| ID | Area | Test | Steps | Expected Result |
|----|------|------|-------|----------------|
| TC-01 | Select Value | Select single value | Click → choose "Group 2, option 1" | Value displayed correctly |
| TC-02 | Select Value | Search & select | Type "Option 3", Enter | Option selected & visible |
| TC-03 | Select One | Choose option | Click → choose "Dr." | Dropdown closes, selection shown |
| TC-04 | Old Style Select | Select by text | Pick "Purple" | "Purple" selected |
| TC-05 | Old Style Select | Select by index/value | Use index or value | Correct option selected |
| TC-06 | Multi Select Dropdown | Select multiple | Open → pick 2–3 options | Tokens shown for each |
| TC-07 | Multi Select Dropdown | Deselect | Click token remove | Token removed, value cleared |
| TC-08 | Standard Multi Select | Multi-select via CTRL | CTRL-click multiple | getAllSelectedOptions() correct |
| TC-09 | Validation | Persistence reload | Select → refresh | Defaults restored (check expected behavior) |
| TC-10 | Accessibility | Keyboard nav | Tab, arrows, Enter, Escape | Focus & selection work |
| TC-11 | Negative | Invalid search | Type random string | No results selectable |
| TC-12 | Concurrency | Rapid selection | Repeat select/deselect | UI stable, no stale element |
| TC-13 | Responsiveness | Mobile viewport | Resize → perform actions | Dropdown adapts & works |
| TC-14 | Performance | High volume | Repeat 500 selections | No UI freeze or errors |
| TC-15 | Security | XSS attempt | Type "<script>" text | Rendered as plain text, no execution |

────────────────────────────────────────────
## Locators (adjust to DOM)
────────────────────────────────────────────
- Select Value: `div[class*='css-1hwfws3']`, input inside `.select__input-container`  
- Select One: `.css-yk16xz-control`  
- Old Style Select: `#oldSelectMenu`  
- Multi Select Dropdown: `#react-select-4-input`  
- Standard Multi Select: `#cars`  

────────────────────────────────────────────
## Selenium (Java + TestNG) Example
────────────────────────────────────────────
```java
import org.openqa.selenium.*;
import org.openqa.selenium.chrome.ChromeDriver;
import org.openqa.selenium.support.ui.*;
import org.testng.annotations.*;
import java.time.Duration;
import java.util.List;

public class SelectMenuTests {
    WebDriver driver;
    WebDriverWait wait;

    @BeforeClass
    public void setup() {
        driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(6));
        wait = new WebDriverWait(driver, Duration.ofSeconds(8));
        driver.get("https://demoqa.com/select-menu");
    }

    @Test
    public void tcOldStyleSelect_ByVisibleText() {
        WebElement oldSelect = driver.findElement(By.id("oldSelectMenu"));
        Select sel = new Select(oldSelect);
        sel.selectByVisibleText("Purple");
        assert "Purple".equals(sel.getFirstSelectedOption().getText());
    }

    @Test
    public void tcSelectValue_SearchAndChoose() {
        WebElement selectValueControl = driver.findElement(By.cssSelector("div[id^='react-select'][class*='css-']"));
        selectValueControl.click();
        WebElement input = wait.until(ExpectedConditions.elementToBeClickable(
            By.cssSelector("input[type='text'][id*='react-select']")));
        input.sendKeys("Option 3");
        input.sendKeys(Keys.ENTER);
        WebElement selected = selectValueControl.findElement(By.cssSelector(".css-1uccc91-singleValue"));
        assert selected.getText().contains("Option 3");
    }

    @Test
    public void tcStandardMultiSelect_SelectMultiple() {
        WebElement multi = driver.findElement(By.id("cars"));
        Select s = new Select(multi);
        s.deselectAll();
        s.selectByVisibleText("Volvo");
        s.selectByVisibleText("Opel");
        List<WebElement> selected = s.getAllSelectedOptions();
        assert selected.size() == 2;
    }

    @AfterClass
    public void teardown() {
        if (driver != null) driver.quit();
    }
}

```

End Note

────────────────────────────────────────────
This test plan and automation blueprint covers all selectable elements on the DemoQA select menu page, including native and custom components, single and multi-select behavior, keyboard accessibility, edge cases, and basic security checks. Following this ensures comprehensive coverage for functional validation, UI consistency, and automation readiness. Always validate locators against the live DOM, and combine UI verification with underlying DOM checks to ensure robust test results.
