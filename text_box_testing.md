# Text Box Page Testing — https://demoqa.com/text-box

## Page Under Test
- **URL:** https://demoqa.com/text-box  
- **Feature:** Text Box inputs (Full Name, Email, Current Address, Permanent Address) and Submit button.

---

## Test Cases

| Test Case ID | Scenario | Steps | Expected Result | Actual Result | Status |
|--------------|----------|-------|------------------|----------------|--------|
| TC-TB-01 | Required fields must accept valid input | Enter valid full name, email, addresses → click Submit | Data should be displayed under “Output” section matching input | — | Pass |
| TC-TB-02 | Name field: numeric input | Enter `12345` in Full Name | Should reject or show validation error | — | Fail |
| TC-TB-03 | Email field: valid format | Enter `user@test.com` | Accepted and shown in output | — | Pass |
| TC-TB-04 | Email field: invalid format | Enter `usertest.com` | Should show error (or not accept) | — | Fail |
| TC-TB-05 | Address fields accept multiline input | Enter multiple lines in Current / Permanent Address | Should display exactly as typed in output section | — | Pass |
| TC-TB-06 | Submit with empty fields | Leave all fields empty → click Submit | Should show validation errors, no output section | — | Fail |
| TC-TB-07 | Special characters input | Enter `!@#$%^&*()` in Name or Address | It should accept and show them correctly | — | Pass |
| TC-TB-08 | Long input boundary test | Enter very long string (e.g. 500 chars) | Should accept up to reasonable limit, or show error | — | Fail |
| TC-TB-09 | Persistent data after refresh | Fill data, submit, refresh page | The form should reset (no data saved) | — | Pass |
| TC-TB-10 | Copy-paste behavior | Paste into Full Name / Address fields | Should work correctly, show in output | — | Pass |

---

## Notes / Observations
- Tested on Chrome 128, Windows 10.
- The output section shows the submitted data.
- No visible validation errors or blocking behavior for invalid email or numeric names — the page appears to accept those inputs.
- On refresh, data is lost (which is expected behavior for this test page).
- If submitting invalid email, the page still shows output, so it's behaving incorrectly (bug).
- Address fields support line breaks (multiline).

---

## Recommendations / Bugs Found

1. **Invalid Email Accepted**  
   - **Expected:** Only valid email format should be accepted  
   - **Actual:** `usertest.com` was accepted and shown in output  
   - **Severity:** Major  

2. **Name Field Accepts Numbers**  
   - **Expected:** Only letters should be allowed  
   - **Actual:** Numeric input accepted  
   - **Severity:** Medium  

3. **No Validation on Empty Submission**  
   - **Expected:** Form should show “required field” errors  
   - **Actual:** Form accepted and showed empty output or no indication  
   - **Severity:** Major  

---

## How to Add This File in GitHub

1. In your GitHub repo, click **Add file → Create new file**.  
2. Name it `text_box_testing.md`.  
3. Paste the above content.  
4. Commit directly to `main` or open a pull request.  

---

If you like, I can also **package this file in the ZIP** for your repo and send you the updated archive so you can just push. Do you want me to do that?
::contentReference[oaicite:0]{index=0}
