# Test Cases – DemoQA Automation Practice Form

| TC ID | Test Scenario | Steps | Expected Result | Status |
|-------|--------------|-------|-----------------|--------|
| TC01  | Verify mandatory fields | Leave all fields blank → click Submit | Error message should appear | Pass |
| TC02  | Validate First Name field | Enter alphabets only | Should accept alphabets | Pass |
| TC03  | Validate First Name field with numbers | Enter `1234` | Should reject numbers | Fail |
| TC04  | Validate Email field with valid format | Enter `user@test.com` | Accepted | Pass |
| TC05  | Validate Email field with invalid format | Enter `usertest.com` | Should show error | Fail |
| TC06  | Select Gender | Click Male/Female/Other | Should allow only one option | Pass |
| TC07  | Validate Mobile Number field | Enter 10 digits | Accepted | Pass |
| TC08  | Validate Mobile Number with >10 digits | Enter 1234567890123 | Should reject | Fail |
| TC09  | Upload Picture | Attach a valid JPG file | File accepted | Pass |
| TC10  | Validate Hobbies checkboxes | Select multiple hobbies | Multiple selections should work | Pass |
| TC11  | Validate Date of Birth | Open calendar & select a date | Date updates correctly | Pass |
| TC12  | Validate State/City dropdown | Select State = NCR → City should update accordingly | Pass |
| TC13  | Validate Submit button | Fill all mandatory fields → click Submit | Form should be submitted successfully | Pass |
