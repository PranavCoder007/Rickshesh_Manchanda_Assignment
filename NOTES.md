# Notes

## Summary of Changes

I fixed several bugs across the backend and frontend:

* Fixed the SQL search filter in `TaskRepository.java` by grouping the title/description `OR` conditions so archive and status filters are applied correctly.
* Added validation for invalid task status values and return HTTP 400 instead of allowing an exception to reach the server.
* Removed the artificial `Thread.sleep()` delay from `TaskController.java`.
* Added validation for `page` and `pageSize`, including a maximum page size of 100.
* Reset pagination to page 1 when the search query or status filter changes.
* Fixed stale error state in `useTasks.js` and ensured loading is cleared after both successful and failed requests.

## What I Chose Not to Change

I did not change the `TaskStatus` enum because the enum values (`OPEN`, `IN_PROGRESS`, `DONE`) are consistent with the backend normalization logic.

I also did not add an arbitrary maximum value for `page`. Extremely large values could theoretically cause integer overflow in the pagination calculation, but I considered this a lower-priority edge case for the scope of this exercise.

## Biggest Remaining Risk

The backend currently retrieves all matching tasks before performing pagination in Java. As the number of tasks grows, this could increase memory usage and response time. Pagination should ideally be performed at the database level using `LIMIT/OFFSET` or Spring Data pagination.

## Tools / AI Used

I first used GitHub Copilot in VS Code to identify potential bugs and issues in the code. I then used ChatGPT to gain a deeper understanding of the identified bugs, including SQL operator precedence, exception handling, React state management, and pagination behavior. I reviewed the suggestions and applied the relevant fixes to the code.