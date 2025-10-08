# Upload & Download – Test Cases, Notes & Description

## Page Description

The **Upload & Download** page allows users to:
- Upload a file via a file-input control, and then display a message or path confirming upload.
- Download a sample file by clicking a “Download” button/link.

Key elements:
- A file input (often `<input type="file">`) for selecting a file to upload.
- Display area showing the uploaded filename or path.
- A download link or button initiating file download (e.g. `downloadButton`). :contentReference[oaicite:0]{index=0}  
- Behavior of download: the file should be downloaded to user’s machine or default Download folder.

There are potential pitfalls:
- Uploading files of unsupported types or sizes.
- The download link might not respond if the test ends too quickly or file isn’t ready.  
- Duplicate downloads might append suffixes (e.g. `file (1).jpg`) depending on browser. :contentReference[oaicite:1]{index=1}  

---

## Test Cases

Below is a sample set of test cases. Each test case includes its **ID, Description, Preconditions, Steps, Expected Result**, and **Notes / Edge conditions**.

| TC ID | Description | Preconditions | Steps | Expected Result | Notes / Edge Cases |
|---|-------------|----------------|-------|------------------|---------------------|
| TC_UPLOAD_01 | Upload a valid file | Page is loaded | 1. Click “Choose File” <br>2. Select a valid file (e.g. `.txt`, `.pdf`) <br>3. Check displayed message or path | The page should display the uploaded file name or path correctly | Use a small file; ensure file path is correct for OS |
| TC_UPLOAD_02 | Upload a file with unsupported extension | Page is loaded | 1. Click “Choose File” <br>2. Select a disallowed extension (if restriction applies) | System should reject or show an error (if functionality restricts it) | If restrictions are not enforced, this may pass |
| TC_UPLOAD_03 | Upload a very large file (if supported) | Page is loaded | 1. Choose large file (size near limit) <br>2. Upload | Either successful upload or graceful error | Check timeout, UI responsiveness |
| TC_UPLOAD_04 | Upload with no file selected | Page is loaded | 1. Click upload (if there’s a separate “Upload” button) without selecting file | System should not break; either show “please select file” or remain idle | Might need to handle UI behavior |
| TC_UPLOAD_05 | Verify path is hidden for security | File uploaded | 1. Upload a valid file <br>2. Inspect displayed path | The actual absolute file path should not be revealed to user | Many systems mask path for security |
| TC_DOWNLOAD_01 | Download the sample file | Page is loaded | 1. Click “Download” button <br>2. Wait for file download to complete | The file is saved to Downloads with expected name | Use wait logic; check file exists in system |
| TC_DOWNLOAD_02 | Download twice | After first download | 1. Click download <br>2. Wait <br>3. Click download again | Second download should save with suffix (e.g. `file (1).ext`) depending on browser behavior | Browser rules may differ (Chrome, Firefox) :contentReference[oaicite:2]{index=2} |
| TC_DOWNLOAD_03 | Partial download abort / interruption | Page loaded | 1. Trigger download <br>2. Cancel network mid-download (if possible) | Application or browser should handle gracefully (error or partial) | Hard to simulate; may require network throttling |
| TC_DOWNLOAD_04 | Verify file integrity | After download | 1. Download file <br>2. Compare checksum or content with expected | Content should match original file | Useful if sample file is known |
| TC_DOWNLOAD_05 | Download under slow network | Page loaded | 1. Simulate slow network <br>2. Click download | System should still download, possibly slower, with no corruption | Tests performance under stress |
| TC_UI_01 | UI controls present | Page loaded | 1. Inspect page | The “Choose File / Upload” control and “Download” button should be present and enabled | Check element visibility |
| TC_UI_02 | Button states after upload | After upload | 1. Upload file <br>2. Inspect control states | The upload control or download control remains functional | UI shouldn’t freeze |
| TC_SECURITY_01 | Attempt to upload script file (.js, .exe) | Page loaded | 1. Select malicious file extension <br>2. Upload | Should reject or sanitize | If system allows arbitrary upload, may succeed |
| TC_SECURITY_02 | Check download link URL manipulation | Page loaded | 1. Inspect download link `href` <br>2. Modify query parameters <br>3. Trigger download | Should work only for valid file or redirect safely | Prevent arbitrary file download |
| TC_PERF_01 | Measure upload time | Page loaded | 1. Start timer <br>2. Upload file <br>3. Record completion time | Should be within acceptable threshold (set by requirement) | Useful for performance testing |
| TC_PERF_02 | Measure download time | Page loaded | 1. Click download <br>2. Time until file present <br>3. Compare | Acceptable threshold per requirement | Network dependent |

---

## Notes and Explanations for Test Cases

- **Preconditions**: Ensure the page is fully loaded and elements are interactive.  
- **Waiting mechanisms**: Use explicit waits (e.g. `waitUntil`, `expect_download`) rather than simple sleeps. :contentReference[oaicite:3]{index=3}  
- **File path issues**: On different operating systems, file paths differ. Use absolute paths tailored to OS.  
- **Download suffix behavior**: When downloading the same file more than once, many browsers append suffixes (like `file (1).ext`). :contentReference[oaicite:4]{index=4}  
- **Masking of paths**: For security, the UI often shows a masked file path (just filename) rather than full local path.  
- **Checksum/content validation**: To ensure file correctness, compare downloaded file contents with original.  
- **Network handling**: Simulate slow, dropped connections to test resilience.  
- **Edge vs nominal**: Use both typical files (small text/image) and edge files (large size, weird characters).  
- **Browser compatibility**: Test functionality across browsers (Chrome, Firefox, Edge) because download/behavior may differ.  
- **Clean-up**: After each test, delete downloaded or uploaded test artifacts to maintain test isolation.  
- **Security tests**: Try uploading forbidden file types; inspect download URLs for path traversal or unauthorized access.

---

## Example Automation Snippets (Pseudo / Playwright style)

> python
# Example: Download using Playwright
with page.expect_download() as download_info:
    page.locator("a:has-text('Download')").click()
download = download_info.value
path = download.path()
assert download.suggested_filename == "sampleFile.jpeg"
# Optionally read content and verify length or checksum

**Additional Considerations & Tips**

1. Timeouts & waits: After triggering download, the script must wait until the file is fully saved; without waiting, the test may close early, causing failures. 
Stack Overflow

2. Download behavior in headless / CI: In headless browser mode or CI environments, download directory configuration is necessary (e.g. setting download.default_directory in Chrome).

3. Cross-browser file name handling: Some browsers do not include space in suffix filenames (e.g. file(1).jpg) — adapt tests accordingly.

4. File upload field hidden: Some UI designs hide the <input type="file"> behind styled elements; you may need to trigger it via JS or expose underlying input.

5. Permission / sandbox issues: In secure environments, writing to default download folder may be restricted — tests need sandbox awareness.

5. Logging & artifact capture: On failure, capture screenshots, console logs, and file existence logs to debug issues.

6. Versioning of sample file: Use a stable sample file version for download validation, so it doesn’t change and break tests.


