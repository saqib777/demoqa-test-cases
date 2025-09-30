# Alerts Page Testing - https://demoqa.com/alerts

## Test Cases Executed

| Test Case ID | Test Scenario | Steps | Expected Result | Actual Result | Status |
|--------------|--------------|-------|----------------|---------------|--------|
| TC-AL-01 | Verify alert with "OK" button | Click the button that triggers an alert | Alert should appear with correct message and dismiss when "OK" is clicked | Works as expected | Pass |
| TC-AL-02 | Verify alert with "OK" and "Cancel" | Click button to trigger confirm alert | Alert should allow "OK" or "Cancel" selection | Both options work correctly | Pass |
| TC-AL-03 | Verify alert with prompt input | Trigger prompt alert | User can enter text and confirm | Input is accepted and displayed correctly | Pass |
| TC-AL-04 | Verify timing alert | Click button with 5-second timer | Alert should appear after 5 seconds | Works correctly | Pass |
| TC-AL-05 | Verify prompt alert cancel option | Trigger a prompt alert and click Cancel | The prompt should close without displaying text | Works as expected | Pass
| TC-AL-06 | Verify multiple alerts do not overlap | Trigger one alert, dismiss it, then trigger another | Each alert should appear separately and not overlap | Works fine | Pass 
| TC-AL-07 | Verify page is not interactive when alert is open | Try clicking another element while alert is active | Other page elements should not be clickable | Page is blocked as expected | Pass 

## Notes
- All tested alerts behaved as expected.  
- No functional bugs were found during testing.
