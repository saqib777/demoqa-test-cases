# Broken Links & Images Test Cases - DemoQA

## Test Cases Table

| Test Case ID       | Test Objective                                       | Preconditions                      | Test Steps                                                                                           | Expected Result                                                | Status   |
|-------------------|-----------------------------------------------------|-----------------------------------|-----------------------------------------------------------------------------------------------------|----------------------------------------------------------------|---------|
| TC_BrokenLinks_01 | Verify Presence of Valid and Broken Links          | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Identify all <a> tags  3. Capture href & send HTTP request  4. Categorize links by status code  5. Document results | Page contains both valid and broken links                     | Pending |
| TC_BrokenImages_01| Verify Presence of Valid and Broken Images         | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Identify all <img> tags  3. Capture src & send HTTP request  4. Categorize images by status code  5. Document results | Page displays both valid and broken images                   | Pending |
| TC_BrokenLinks_02 | Verify Functional Links                             | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Identify all valid <a> tags  3. Click each link and verify destination  4. Document results | Each valid link redirects to the correct page                | Pending |
| TC_BrokenImages_02| Verify Functional Images                            | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Identify broken <img> tags  3. Observe display behavior  4. Document results | Broken images show a placeholder or error icon               | Pending |
| TC_Accessibility_01| Verify Accessibility of Links and Images          | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Use a screen reader  3. Verify all links/images are announced  4. Document results | All links and images are accessible by screen reader         | Pending |
| TC_Performance_01 | Verify Page Load Performance                        | Browser open & internet connected | 1. Navigate to https://demoqa.com/broken  2. Measure page load time using developer tools  3. Document results | Page loads within acceptable time (<3 seconds)               | Pending |

---

## Detailed Explanation of Test Cases

1. **TC_BrokenLinks_01:**  
   This test ensures all links on the page are accounted for and categorized as valid or broken. It uses HTTP status codes for classification. Links returning 2xx are valid, while 4xx or 5xx indicate broken links. This helps detect navigation issues early.

2. **TC_BrokenImages_01:**  
   Similar to links, this test checks the integrity of images on the page. By sending requests to the image `src` URLs, broken images can be detected. This ensures visual content is rendered correctly.

3. **TC_BrokenLinks_02:**  
   This functional test verifies that clicking on valid links leads to the correct destination. Even if a link returns 2xx, the redirection or page content may be incorrect; this test confirms proper behavior.

4. **TC_BrokenImages_02:**  
   Verifies the user experience for broken images. The test ensures that placeholders or error icons are displayed, avoiding blank or broken visuals that can confuse users.

5. **TC_Accessibility_01:**  
   Confirms that all links and images are accessible for users relying on assistive technologies like screen readers. This is critical for WCAG compliance and inclusive design.

6. **TC_Performance_01:**  
   Measures page load time. Broken links or images can affect performance, so this test ensures that load times remain acceptable (<3 seconds), providing a smooth user experience.

---

## Notes

- **Automation:** These tests can be automated using Selenium WebDriver, which can:
  - Detect all anchor `<a>` and image `<img>` tags.
  - Send HTTP requests to check status codes.
  - Click and verify links.
  - Check image display and placeholders.
- **Reporting:** Maintain a log of broken links and images with screenshots for reporting.
- **Environment:** Tests should be performed on multiple browsers to ensure cross-browser compatibility.
- **Screen Readers:** Tools like NVDA or JAWS can be used for accessibility verification.

---

## End Notes

1. Testing broken links and images is crucial for **user experience**, **SEO**, and **accessibility**.  
2. A single broken element can impact credibility and navigation; early detection prevents user frustration.  
3. Regular execution of these tests should be part of a **regression testing suite**, especially before releases or updates.  
4. Combining manual and automated testing provides a robust approach to maintaining website integrity.

