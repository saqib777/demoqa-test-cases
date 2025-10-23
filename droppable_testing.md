# Droppable Component — Test Cases, Notes & Description

## Page Description  
The “Droppable” component on DemoQA enables a user to drag a draggable element and drop it into a target drop area.  
This component helps validate interactive UI behaviours including drag & drop interactions, event triggers, acceptance criteria, propagation handling and revert scenarios.  
It supports multiple tabs: e.g., *Simple*, *Accept*, *Prevent Propagation*, *Revert* — each with different behavioural rules. :contentReference[oaicite:2]{index=2}

---

## Test Cases

| TC ID       | Description                                                  | Pre-condition                        | Steps                                                                                                                                     | Expected Result                                                                 |
|-------------|--------------------------------------------------------------|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| **TC_DRB_01** | Verify “Simple” drag-and-drop functionality                     | Page loaded on “Simple” tab          | 1. Navigate to Droppable page. <br>2. Ensure “Simple” tab is selected. <br>3. Drag the source element (labeled “Drag me”) into the target box (“Drop here”). | Target box shows text change (e.g., “Dropped!”) and highlights/changes style.     |
| **TC_DRB_02** | Verify target rejects irrelevant elements in “Accept” tab         | Switch to “Accept” tab               | 1. Click the “Accept” tab. <br>2. Attempt to drop a “Not Acceptable” element into the drop area. <br>3. Attempt to drop the “Acceptable” element.   | First attempt fails (no text change or styling). Second attempt succeeds.        |
| **TC_DRB_03** | Verify event propagation in “Prevent Propagation” scenario        | Switch to “Prevent Propagation” tab  | 1. Click that tab. <br>2. Drag the draggable into the “Outer drop box” and then drop into the nested “Inner drop box”.                     | Inner drop handles drop; outer drop may not register both events or vice versa. |
| **TC_DRB_04** | Verify “Revert Draggable” behaviour                                  | Switch to “Revert Draggable” tab    | 1. Click its tab. <br>2. Drag the draggable element and drop into target. <br>3. Observe if source returns to origin after dropping.        | If configured to revert: element returns to its initial position. If not: remains dropped. |
| **TC_DRB_05** | Verify styling / visual feedback on drop                           | Any tab selected                    | 1. After a successful drop, inspect target and/or source element styles (color, border, text change).                                     | Visual feedback cues present (e.g., color changes, “Dropped!”, border highlight). |
| **TC_DRB_06** | Verify boundary / drop area limits                               | Page loaded                          | 1. Drag source near but not into drop area (e.g., edge). <br>2. Drop outside target.                                                       | Drop should fail or no state change; only valid drops accepted.                  |
| **TC_DRB_07** | Verify multi-drag attempts                                          | Page loaded                          | 1. Attempt dragging multiple draggable items (if allowed) into target sequentially.                                                       | Each valid drop recognized; invalid ones ignored or flagged.                     |
| **TC_DRB_08** | Verify keyboard accessibility (if supported)                       | Page loaded                          | 1. Focus on draggable via keyboard. <br>2. Use arrow/tab keys to move, and Enter/Space to drop (if supported).                            | The component supports keyboard-based drop; focus and drop work without mouse.  |
| **TC_DRB_09** | Verify responsiveness / mobile view behaviour                      | Resize to mobile width              | 1. On mobile viewport, drag and drop (touch / pointer device) the source into target.                                                     | Drop functionality works on touch devices; layout remains usable/responsive.    |
| **TC_DRB_10** | Verify state persistence after page reload                        | Perform valid drop                   | 1. Complete a drop action. <br>2. Reload the page.                                                                                           | either drop state resets (expected) or keeps drop (if spec); UI remains consistent. |
| **TC_DRB_11** | Edge‐Case: Rapid drag and drop back and forth                     | Page loaded                          | 1. Quickly drag/drop source in/out of target repeatedly.                                                                                   | No UI glitches, no duplication of events, drop state consistent.                 |
| **TC_DRB_12** | Edge‐Case: Drag and drop to incorrect element or invalid target   | Page loaded                          | 1. Drag source and drop into another area not designated as drop target (if exists).                                                      | No state change; drop must be ignored.                                          |
| **TC_DRB_13** | Verify script / automation compatibility                          | Page loaded                          | Automate the drop using drag-and-drop script (Selenium / Playwright) and assert target event triggers.                                   | Automation script can perform drop; target element text changes as expected.    |
| **TC_DRB_14** | Verify “Prevent Propagation” deeper nested behaviour             | “Prevent Propagation” tab active    | 1. Drop source into inner nested target first, then outer.                                                                                   | Correct event handling: either only inner triggers, or outer triggered second.   |
| **TC_DRB_15** | Styling and theme variation                                       | Page loaded                          | 1. Apply dark/light theme (if any) or different viewport. <br>2. Perform drop.                                                            | Styles remain clear; drop area visible; state changes visible across themes.    |

---

## Notes & Explanations  
- The droppable component relies heavily on user **drag-and-drop interactions**. Testing must cover dragging behaviour (click → hold → drag → drop) and target acceptance/rejection logic. :contentReference[oaicite:3]{index=3}  
- Ensure **visual feedback** is present and correct (text change, colour change, border highlight).  
- For the “Accept” tab: some draggable items are designated *acceptable*, others *not acceptable*; test both paths.  
- For the “Prevent Propagation” tab: nested drop areas may trigger parent/child events; ensure event logic is correct.  
- For the “Revert Draggable” tab: after dropping, the source may *revert* back to its original position depending on configuration — test both immediate and delayed revert behaviours.  
- **Accessibility & keyboard** support should not be ignored — check focus, keyboard actions and ARIA roles if applicable.  
- **Edge and negative cases**: dropping outside the target, multiple rapid drops, invalid drag targets — such cases often reveal bugs.  
- **Touch/drag on mobile**: Test drag & drop on touch devices, ensuring behaviours match desktop.  
- **Automation complexity**: Drag and drop via automation tools (Selenium Actions, Playwright `dragTo()`) often fails due to browser differences or offset issues; test scripts accordingly. :contentReference[oaicite:4]{index=4}

---

## End Notes  
While drag-and-drop may appear like a simple UI action, it’s technically complex under the hood (mouse or touch events, HTML5 drag/drop API, event propagation, DOM updates, style changes).  
By covering all behavioural paths (simple drop, accept/reject, nested propagation, revert), and ensuring usability (keyboard, mobile), you’ll ensure this interactive component is robust, reliable and user-friendly.

---

**File Name:** `droppable_testing.md`  
**Category:** DemoQA Interactions — Droppable Component  
**Created For:** Manual + Automation documentation  
