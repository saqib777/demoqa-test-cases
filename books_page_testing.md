## Page Under Test  
**Book Store – DemoQA** — [https://demoqa.com/books](https://demoqa.com/books)

---

## Objective  
To validate the book listing, filtering, search, pagination, selection, detail view, user interactions (login required), and UI/UX behaviour of the book-store page in the DemoQA application.

---

## Test Cases

| TC ID      | Description                                               | Pre-condition                   | Steps                                                                 | Expected Result                                                |
|------------|-----------------------------------------------------------|--------------------------------|----------------------------------------------------------------------|----------------------------------------------------------------|
| TC_BK_01   | Page loads and book list is visible                        | Page opened                    | 1. Navigate to the books page.                                       | List of books appears; each book entry shows title, author, ISBN etc. |
| TC_BK_02   | Verify book count / pagination                              | Page loaded                    | 1. Observe number of book entries <br>2. Navigate next page (if pagination) | Correct count displayed; next page loads new books correctly |
| TC_BK_03   | Search for a book by title                                  | Page loaded                    | 1. Enter a valid book title in search box <br>2. Press Enter/Search | Search results show only matching books                        |
| TC_BK_04   | Search using partial title                                   | Page loaded                    | 1. Enter partial title (e.g., “JavaScript”) <br>2. Search         | Matching books appear; non-matches filtered out                |
| TC_BK_05   | Search with invalid string or random characters              | Page loaded                    | 1. Enter a gibberish string <br>2. Search                            | Either “No records found” message or empty list appears       |
| TC_BK_06   | Sort books by title (if sorting supported)                   | Page loaded                    | 1. Click on “Title” column header or relevant sort control         | Books list sorted ascending/descending by title               |
| TC_BK_07   | Filter by author (if filter exists)                           | Page loaded                    | 1. Use author filter dropdown/input <br>2. Apply filter             | List shows books by selected author only                      |
| TC_BK_08   | Click a book to open its detail view                          | Page loaded                    | 1. Click on a book title link                                           | Book detail page appears showing full info (title, subtitle, isbn, description) |
| TC_BK_09   | Validate book detail fields                                   | Book detail page              | 1. On detail view observe fields                                     | Title, subtitle, author, isbn, pages, publisher, website etc are displayed |
| TC_BK_10   | Add book to user’s collection (requires login)                 | User logged in                | 1. Login <br>2. On detail page click “Add To Your Collection”        | Book is added; confirmation message shown                     |
| TC_BK_11   | Remove book from user’s collection                             | Book already in collection    | 1. On detail page click “Remove” or go to collection and remove      | Book removed from collection; UI updates accordingly          |
| TC_BK_12   | Behaviour when user is not logged in and tries to add book     | User not logged in            | 1. Try to click “Add To Your Collection”                              | Prompt to login or error message shown                         |
| TC_BK_13   | Verify responsive layout on mobile                               | Browser resized/mobile view   | 1. View page on smaller viewport <br>2. Scroll, interact books        | List and details adapt; no layout breaks; elements accessible |
| TC_BK_14   | Accessibility: keyboard navigation in book list                 | Page loaded                   | 1. Tab through list items <br>2. Press Enter on a book                | Focus moves logically; opening book detail via keyboard works |
| TC_BK_15   | Accessibility: screen reader & ARIA roles                      | Page loaded                   | 1. Inspect list and detail view elements                              | Proper semantic roles (list, listitem), aria-labels present   |
| TC_BK_16   | Verify search clears and resets to full list                   | Page filtered via search      | 1. Clear search box <br>2. Press Enter/Search                          | Full book list appears again                                  |
| TC_BK_17   | Verify page load performance under slow network                 | Page opened                   | 1. Simulate slow network <br>2. Load page and check behaviour        | Page loads with fallback/spinner; no broken UI               |
| TC_BK_18   | Verify no duplicate book entries in list                        | Page loaded                   | 1. Inspect list entries                                              | Each book entry unique; no duplicates                         |
| TC_BK_19   | Invalid ISBN in book detail link                                 | Page loaded                   | 1. On list, find link to ISBN that is invalid / broken               | Either book detail is not found or error handled gracefully   |
| TC_BK_20   | Verify collection persistence after browser refresh              | User logged in + book added  | 1. Add book <br>2. Refresh page                                       | Book remains in user’s collection                             |
| TC_BK_21   | Verify removing book then logging out then login restores state  | User logged in                | 1. Add book <br>2. Logout <br>3. Login again                             | Previously added book still in collection                    |
| TC_BK_22   | Verify UI behaviour when backend API returns error               | Page loaded                   | 1. Simulate API failure                                               | Graceful error message shown; UI fallback                      |
| TC_BK_23   | Verify columns/fields align correctly in list and detail view    | Page loaded                   | 1. Inspect UI in list & detail                                        | No misalignment; text not clipped; readable                  |
| TC_BK_24   | Verify removing book from collection via list (if supported)     | Book in user’s collection     | 1. Navigate to user’s collection <br>2. Remove book                   | Book removed; list updates; UI feedback shown                 |
| TC_BK_25   | Verify bookmark/favourite functionality (if exists)               | Page loaded                   | 1. On book detail, click “Bookmark” or similar                        | Book marked favourite; UI indicates state                     |
| TC_BK_26   | Verify sorting default state on list                              | Page loaded                   | 1. Inspect list on initial load                                       | Default sort order correct (by title or recent)               |
| TC_BK_27   | Verify load more / infinite scroll behaviour (if implemented)     | Page loaded                   | 1. Scroll to bottom <br>2. Check if more books loaded                 | Additional books load or “No more records” message shows      |
| TC_BK_28   | Verify filtering by multiple criteria (search + author + publisher) | Page loaded                  | 1. Apply search + filter by author/publisher                          | List accurately reflects combination filter results            |
| TC_BK_29   | Verify UI theme (light/dark mode) effect on list display         | Page loaded                   | 1. Switch theme <br>2. View book list                                | UI adapts; readability and contrast maintained                 |
| TC_BK_30   | Cross browser compatibility (Chrome, Firefox, Edge)                | Page loaded                   | 1. Open in different browsers                                          | Behaviour and layout consistent across browsers                |

---

## Notes & Explanations  
- The Book Store page lists multiple books (title, subtitle, author, isbn, publisher) — verifying all fields ensures data integrity.  
- User interactions like search, filter, sort, detail view and user-collections are critical and must be reliable.  
- Authentication is required for some interactions (adding/removing books) — test both logged-in and not logged-in states.  
- Accessibility, responsiveness, performance, error-handling and cross-browser behaviour must also be covered.  
- Negative and boundary cases (invalid search strings, broken links, API downtime) often reveal hidden issues.

---

## End Notes  
The Book Store application is a full-featured mini-site embedded within DemoQA, and serves as a realistic scenario for list/detail workflows, user-personalized data and state management. Comprehensive test coverage across functional, non-functional and user state aspects will ensure the module is robust and trustworthy.

**File Name:** `books_page_testing.md`  
**Category:** DemoQA – Book Store Module  
**Created For:** Manual + Automation Testing documentation  
