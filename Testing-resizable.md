# Test Cases for Resizable Component - DemoQA

| S.No | Test Case | Description | Expected Result | Notes |
|------|-----------|-------------|----------------|-------|
| 1 | Verify default size | Check the initial size of the resizable box | The box should load with its default width and height | Important to confirm baseline dimensions |
| 2 | Resize box horizontally | Drag the right edge of the box to increase/decrease width | Width of the box should change according to drag | Verify min/max width restrictions |
| 3 | Resize box vertically | Drag the bottom edge of the box to increase/decrease height | Height of the box should change according to drag | Verify min/max height restrictions |
| 4 | Resize box diagonally | Drag the bottom-right corner to resize both width and height | Both width and height should adjust proportionally | Corner drag affects both dimensions simultaneously |
| 5 | Verify min width | Try to resize the box below its minimum width | Box width should not go below minimum allowed value | Prevents collapsing the element |
| 6 | Verify max width | Try to resize the box above its maximum width | Box width should not exceed maximum allowed value | Ensures layout consistency |
| 7 | Verify min height | Try to resize the box below its minimum height | Box height should not go below minimum allowed value | Prevents collapsing the element |
| 8 | Verify max height | Try to resize the box above its maximum height | Box height should not exceed maximum allowed value | Ensures layout consistency |
| 9 | Check smooth dragging | Drag the edges/corners slowly and quickly | The resizing should be smooth without lag | Detects rendering or UI issues |
| 10 | Verify responsiveness | Resize the window and test resizing | Box should remain resizable within visible area | Ensures component adapts to screen changes |

---

### Explanation of Test Cases:

1. **Default Size**: Confirms that the resizable element loads correctly and dimensions are as expected.  
2. **Horizontal Resize**: Validates the functionality of resizing width independently.  
3. **Vertical Resize**: Validates the functionality of resizing height independently.  
4. **Diagonal Resize**: Tests combined width & height resizing using the corner handle.  
5-8. **Min/Max Width & Height**: Ensures the component respects constraints and doesn’t break layout.  
9. **Smooth Dragging**: Checks performance and user experience during rapid or slow dragging.  
10. **Responsiveness**: Confirms the component adapts to viewport changes without breaking the resize feature.

---

### Notes:

- Always check for browser compatibility since drag-and-drop/resizing may behave slightly differently.  
- Verify that resizing doesn’t overlap other elements or break the page layout.  
- Use both mouse and keyboard (if accessible) to ensure full functionality.  
- Min/Max dimension values may differ depending on the specific resizable box type (default vs constrained).  
- Consider edge cases like extremely fast dragging or very small/large sizes.  

---

### End Notes:

- These test cases cover functional, boundary, and UX aspects of the resizable component.  
- Automation can be implemented using Selenium or Cypress by simulating drag events and validating dimensions.  
- Manual testing is recommended for checking smoothness and visual behavior.  
