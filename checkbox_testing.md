# Checkbox Page Testing — https://demoqa.com/checkbox

## Page Under Test
- **URL:** https://demoqa.com/checkbox  
- **Feature:** Hierarchical checkboxes (Home, Desktop, Documents, Downloads etc.) with expandable tree structure.

---

## Test Cases

| Test Case ID | Test Scenario | Steps | Expected Result | Actual Result | Status |
|--------------|----------------|-------|------------------|----------------|--------|
| TC-CB-01 | Expand “Home” node | Click expand arrow next to Home | Child nodes (Desktop, Documents, Downloads) should display | — | Pass |
| TC-CB-02 | Select a leaf node (Desktop) | Expand Home → expand Desktop → click checkbox next to “Notes” | Only “Notes” should be selected; parent may show partial state | — | Pass |
| TC-CB-03 | Select parent node (Documents) | Click checkbox next to “Documents” | All children under Documents should get selected | — | Pass |
| TC-CB-04 | Deselect child after parent selected | After selecting Documents, deselect one child | Parent’s checkbox should show partial (indeterminate) state | — | Pass |
| TC-CB-05 | Select multiple branches | Select nodes in multiple branches (Desktop, Downloads) | All selected should appear in output section | — | Pass |
| TC-CB-06 | Unselect root (Home) while children selected | Click checkbox next to Home when all children are selected | All checkboxes should become unselected | — | Pass |
| TC-CB-07 | Verify output display | After selections, the “You have selected :” section should list selected leaf nodes | — | Pass |
| TC-CB-08 | Uncheck leaf node under hierarchy | Expand and uncheck a previously checked node | Output section should update removing that node | — | Pass |
| TC-CB-09 | Expand/collapse behavior | Expand then collapse a node | Child nodes should hide when collapsed | — | Pass |
| TC-CB-10 | Persistent state after refresh | Select some nodes → refresh the page | Selections should reset (page behavior) | — | Pass |

---

## Notes / Observations

- Tested using Chrome 128 on Windows 10.  
- Output section (below) shows selected items with full paths (e.g. “desktop > notes”).  
- Parent nodes use indeterminate state (partially selected) when not all children are checked.  
- On refresh, checkbox selections are cleared (expected for this demo page).  
- No validation or constraint logic — the page seems lenient in selection behavior.  

---

## Recommendations / Potential Bugs

1. **No limitation on selecting multiple nodes**  
   - **Expected:** Some UI may restrict disallowed combinations, but here all combinations allowed.  
   - **Severity:** Low (for demo pages).  

2. **Indeterminate behavior not obvious**  
   - **Expected:** Parent checkbox should clearly indicate partial selection (maybe via styling).  
   - **Actual:** Visual feedback is minimal or not obvious.  
   - **Severity:** Minor  

3. **No validation of child selections before submission**  
   - **Expected:** Perhaps a “Submit” button could enforce at least one selection.  
   - **Actual:** Demo page does not have explicit submit, just shows output.  

---


