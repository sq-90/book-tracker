# Prompt log

This log records the prompts and checks used while building the Book Tracker. The initial request covered most features at once rather than following the suggested one-feature-at-a-time sequence; the implementation was then refined and checked incrementally.

## Prompt 1 — Initial feature request

**Prompt (summary):** “Build a Book Tracker with required title and author, a To read/Reading/Finished status, newest-first ordering, search, status changes, and data that survives refresh.”

**What happened:** The AI created a single `index.html` with the form, responsive layout, book list, search, status controls, and local-storage persistence. Title and author are required and show inline validation messages.

## Prompt 2 — Add sample data

**Prompt:** “Add some dataset into it.”

**What happened:** The AI added five starter books with a mix of statuses. They are saved as initial data only when the browser has no existing shelf, so returning users’ saved books are not overwritten.

## Prompt 3 — Check the required features

**Prompt:** “It should satisfy these conditions: add books with required title and author, list newest first, search by title or author, change status, and keep data after refresh.”

**What happened:** The AI tested required-field errors, adding a book, searching by its title and author, changing its status, and checking the saved book after a refresh.

**What the AI initially missed:** The first version used `Date.now()` directly for each book’s ordering timestamp. Two books added in the same millisecond could have equal timestamps, so their newest-first order would not be deterministic.

**Correction:** The AI changed timestamp generation to ensure each new book sorts after the existing books, even when several books are added almost simultaneously. A browser check confirmed two quickly added books remained in the correct order after refresh.

## Verification notes

- Submitting with a blank title and author displays “Please enter a title” and “Please enter an author”.
- Search was checked against both title and author.
- Uppercase search (`BEN`) found the author Benyamin.
- A very long title displayed in a narrow browser viewport without horizontal page overflow.
- Status changes and book data persisted after reloading the page.
- Two quickly added books appeared newest first before and after reload.
- Temporary test books were removed after testing.
