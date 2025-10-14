# DemoQA Form Testing

This repository contains manual testing documentation and test-case designs for the DemoQA practice site:
https://demoqa.com

## Project purpose
- Design and document manual test cases for UI components on the DemoQA site.
- Capture bugs, observations, and reproducible steps.
- Provide a reference for future automation and learning.

## Repository contents
Below is the current set of documentation files in this repository.

- `test_cases.md` — Test cases for the Automation Practice Form.
- `bug_report.md` — Issues and bug reports discovered during testing.
- `11_alerts_testing.md` — Test cases for Alerts and modal dialogues.
- `browser_windows_testing.md` — Test cases for opening and managing windows/tabs.
- `buttons_testing.md` — Test cases for various button interactions.
- `checkbox_testing.md` — Test cases for checkbox behaviors.
- `dynamic_properties_testing.md` — Tests for elements whose properties change with time.
- `links_testing.md` — Tests for links (valid/broken).
- `radio_button_testing.md` — Test cases for radio button interactions.
- `text_box_testing.md` — Tests for text input and form submission.
- `upload_download_test_cases.md` — Tests for uploading and downloading files.
- `webtables_testing.md` — Tests for web tables CRUD operations.

If any filename is different in your repo, use the actual filename.

## How this repo is organized
- Each `.md` file is a standalone testing document:
  - page description and purpose
  - preconditions and environment
  - detailed test cases (ID, steps, expected result, notes)
  - occasional automation snippets and advice
- `bug_report.md` contains logged issues and steps-to-reproduce.

## How to contribute
1. Create a new branch: `git checkout -b feature/<short-description>`
2. Add or update `.md` content.
3. Commit with a meaningful message: `git commit -am "Add <file>: <short description>"`
4. Push branch and open a pull request for review.

## Recommended improvements (next steps)
- Add screenshots for failing tests and expected behavior.
- Add a top-level `README_images/` folder to store evidence screenshots.
- Add a `CONTRIBUTING.md` that states format and naming conventions for tests.
- Add a `tests/` folder later if you add automation scripts.
- Add simple status badges (e.g., manual test coverage, last run date).

## Notes & good practices
- Keep test cases atomic and traceable (one check per test).
- Use explicit waits in automation for dynamic elements (avoid hard sleeps).
- When adding automation, store test data separately from the code.
- Keep the README updated when adding or renaming files.

## License
This project is available under the MIT License. Use and adapt for learning and educational purposes.

