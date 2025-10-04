# Web Tables Testing — DemoQA

## Page Under Test
- **URL:** https://demoqa.com/webtables  
- **Feature:** Web tables with CRUD operations (Add, Edit, Delete), paging, filtering, sorting.

---

## Test Cases

| TC ID | Scenario | Steps | Expected Result |
|-------|----------|-------|------------------|
| WT_01 | Verify table loads | Open page | Table displays existing records with correct columns (First Name, Last Name, Age, Email, Salary, Department, Actions) |
| WT_02 | Add new record | Click “Add”, fill valid data, submit | New record appears in the table |
| WT_03 | Edit existing record | Click edit icon on a row, change fields, submit | Updated data reflected in the table |
| WT_04 | Delete record | Click delete icon on a row | Row should be removed from table |
| WT_05 | Paging behavior | If more than page size, navigate pages | Next/Previous page buttons should work |
| WT_06 | Search/filter | Enter text in search box (e.g. “Cierra”) | Only matching rows appear |
| WT_07 | Sort by column | Click column header (e.g. “Age”) | Table rows reorder ascending; click again ⇒ descending |
| WT_08 | Invalid data validation for add | Try adding record with invalid email or missing required fields | Show validation error, record not added |
| WT_09 | Special character input | Add a record with special characters in name e.g. “O’Neil” | Table should accept and display it correctly |
| WT_10 | Edit to invalid data | Edit record with invalid salary (negative number) | Should reject or flag error |
| WT_11 | Pagination persistence after actions | After adding record and moving to next page, go back | Table state should persist correctly |
| WT_12 | Maximum input length limits | Enter very long strings in name fields | Should constrain input or truncate |
| WT_13 | Delete then undo (if available) | Delete a record and see if undo or confirm dialog appears | Table should restore if undo is supported |
| WT_14 | Bulk delete functionality (if exists) | Select multiple rows (if checkbox) and delete | All selected rows removed |
| WT_15 | Export / download (if feature) | Click export/download (CSV, PDF) | File generated with correct table data |

---

## Notes / Observations

- ✅ Validate column headers and order consistency.  
- ✅ CRUD operations should instantly reflect changes without needing page reload.  
- ✅ Actions (Edit / Delete) icons should be visible and responsive.  
- ✅ Search filter should be case-insensitive unless specified.  
- ✅ Sorting should handle numeric and string columns properly.  
- ✅ Input validation must prevent invalid data (email format, negative salary, etc.).  
- ✅ Boundary tests: minimal and maximal values accepted.  
- ✅ After table modifications, UI should remain stable and not flicker.  
- ✅ Cross-browser checks for table rendering, scrolling, and layout.  
- ✅ Responsiveness: Table and controls must work on mobile / narrow screens.  
- ✅ Check message or confirmation dialogs when deleting (if any).  
- ✅ Zero records state: after deleting all rows, table should handle “no records found” gracefully.  
- ✅ Performance with many rows: as table grows, check UI lag, sorting delay, etc.

---

To add it in GitHub:

1. **Add file → Create new file**  
2. Name it `webtables_testing.md`  
3. Paste the content above  
4. Commit to `main`

---

Do you want me to also prepare detailed notes for each test case (explanations) like we did earlier, or a matching bug report for web tables?
::contentReference[oaicite:0]{index=0}
