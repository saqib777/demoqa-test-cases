# Bug Report – DemoQA Automation Practice Form

### Bug 1 – First Name accepts numbers
- **Steps**: Enter `1234` in First Name field.
- **Expected Result**: Only alphabets should be allowed.
- **Actual Result**: Numbers are accepted.
- **Severity**: Medium

### Bug 2 – Email field accepts invalid formats
- **Steps**: Enter `usertest.com` without '@'.
- **Expected Result**: Error should appear.
- **Actual Result**: Field accepts input.
- **Severity**: High

### Bug 3 – Mobile Number allows >10 digits
- **Steps**: Enter `1234567890123`.
- **Expected Result**: Should restrict to 10 digits.
- **Actual Result**: Accepts more than 10 digits.
- **Severity**: Medium

### Bug 4 – No error message for blank form submission
- **Steps**: Leave all fields blank → click Submit.
- **Expected Result**: Proper error messages for mandatory fields.
- **Actual Result**: Submit button does nothing, no clear error.
- **Severity**: High
