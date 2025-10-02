# DemoQA Checkbox Testing

This document contains **15 detailed test cases** for verifying the functionality of the [DemoQA Checkbox page](https://demoqa.com/checkbox).

---

## Test Cases

| Test Case ID | Description | Steps | Expected Result |
|--------------|-------------|-------|-----------------|
| CB_01 | Verify that the main checkbox expands all options when clicked. | 1. Go to the page. <br> 2. Click the dropdown arrow next to "Home". | All nested checkboxes should expand and be visible. |
| CB_02 | Verify selecting the root checkbox selects all child checkboxes. | 1. Click the "Home" checkbox. | All nested checkboxes under "Home" should be automatically checked. |
| CB_03 | Verify deselecting the root checkbox clears all child checkboxes. | 1. Check "Home". <br> 2. Uncheck "Home". | All nested checkboxes should be unchecked. |
| CB_04 | Verify selecting an intermediate node checkbox (e.g., "Desktop") selects its children. | 1. Expand "Home". <br> 2. Click "Desktop". | Both "Notes" and "Commands" checkboxes should be checked. |
| CB_05 | Verify deselecting an intermediate node clears its children. | 1. Select "Desktop". <br> 2. Unselect "Desktop". | "Notes" and "Commands" should be unchecked. |
| CB_06 | Verify individual leaf node selection works correctly. | 1. Expand "Desktop". <br> 2. Select only "Notes". | Only "Notes" should be checked. |
| CB_07 | Verify partially selected parent node is displayed correctly. | 1. Expand "Desktop". <br> 2. Select "Notes" only. | "Desktop" checkbox should show partially checked state. |
| CB_08 | Verify text output updates according to selected checkboxes. | 1. Select "Documents". <br> 2. Observe the output below the checkbox tree. | Selected checkbox names should be displayed correctly. |
| CB_09 | Verify that expanding and collapsing nodes works consistently. | 1. Expand "Home". <br> 2. Collapse "Home". | Checkboxes toggle visibility without losing state. |
| CB_10 | Verify state persistence on multiple actions. | 1. Select "Documents". <br> 2. Collapse "Home". <br> 3. Expand "Home" again. | Previously selected checkboxes remain checked. |
| CB_11 | Verify multiple selections across different branches. | 1. Select "Desktop > Notes". <br> 2. Select "Documents > Word File". | Both checkboxes remain selected independently. |
| CB_12 | Verify deselecting a child updates the parent state correctly. | 1. Select "Desktop". <br> 2. Deselect "Notes". | "Desktop" should show partially checked state. |
| CB_13 | Verify that the UI handles long click or double click. | 1. Double click on "Home" checkbox. | Only one click action should be triggered, not multiple toggles. |
| CB_14 | Verify responsiveness on different screen sizes. | 1. Resize the browser window (mobile/tablet). | Checkboxes and expand/collapse arrows should remain usable and aligned. |
| CB_15 | Verify accessibility with keyboard navigation. | 1. Use **Tab** and **Space/Enter** to navigate and toggle checkboxes. | All checkboxes should be accessible and selectable via keyboard. |

---

## Notes

-  **Selection Hierarchy**: Parent-child relationships should remain consistent, selecting a parent selects all children, and partial selection is reflected visually.  
-  **Partial State**: Parents should clearly indicate when only some children are selected.  
-  **Output Accuracy**: The selected checkbox list must match user interactions in real-time.  
-  **Persistence**: State should remain unchanged after collapsing/expanding.  
-  **Usability**: Actions like double click or long click must not cause duplicate behavior.  
-  **Cross-Device Testing**: Ensure the checkbox tree works correctly on mobile, tablet, and desktop views.  
-  **Accessibility**: Screen readers, keyboard navigation, and focus states must be supported.  
-  **Performance**: Expanding/collapsing nodes should be smooth, even with multiple selections.  
-  **Edge Cases**: Test rapid clicks, selecting/deselecting quickly, or using unusual input patterns.  

---

**Explanations for Checkbox Test Cases**

1. Main Checkbox Expands Options

 - Ensures the tree structure is accessible. If expansion doesn’t work, users cannot reach nested checkboxes, making the feature useless.

2. Root Checkbox Selects All Children

 - Confirms parent-to-child relationship. If broken, users may wrongly assume all child items are selected while some are not, leading to incomplete actions.

3. Root Checkbox Deselect Clears All Children

  - Prevents inconsistent states. Without this, children could remain checked even after the parent is unchecked, causing confusion.

4. Intermediate Node Selects Its Children

 - Validates that middle-level nodes (like Desktop) control their children. If missing, users must manually check each leaf, reducing usability.

5. Intermediate Node Deselect Clears Its Children

 - Ensures reversibility. A parent should uncheck all its children when deselected. Otherwise, selections may not reflect intended user actions.

6. Individual Leaf Node Selection

 - Checks independence of leaf nodes. Prevents situations where checking one leaf accidentally selects unrelated nodes.

7. Partial Parent Selection State

 - Visual feedback for partially checked parents is critical. Without it, users may think all or none of the children are selected, which is misleading.

8. Text Output Updates Correctly

 - Validates synchronization between UI and displayed results. Incorrect output could mislead users or break downstream processes that rely on it.

9. Expand/Collapse Consistency

 - Ensures visibility toggling works without errors. If state is lost, users may need to reselect checkboxes, wasting effort.

10. State Persistence After Multiple Actions

 - Confirms selections survive collapse/expand cycles. Without persistence, UI resets could lead to accidental data loss.

11. Multiple Selections Across Branches

 - Ensures independence of selections in different branches. Prevents a bug where one branch’s selection overrides another.

12. Deselecting Child Updates Parent State

 - Parent checkboxes must dynamically reflect child changes. Missing this could show a parent as fully selected even if one child is unchecked.

13. Handling Double Clicks / Long Clicks

 - Protects against duplicate toggle events. If not handled, double clicks may accidentally deselect immediately after selecting.

14. Responsiveness Across Devices

 - Confirms mobile and tablet usability. If UI breaks on small screens, users may be unable to interact with checkboxes at all.

15. Keyboard Accessibility

 - Ensures compliance with accessibility standards. Users relying on keyboard navigation must be able to select checkboxes without a mouse.


