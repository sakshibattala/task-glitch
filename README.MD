# TaskGlitch – Bug Fix Assignment

## Bugs Identified & Fixes

### Bug 1: Duplicate Tasks on Load

**Problem:**
Tasks were being fetched twice on initial load due to multiple `useEffect` hooks
triggering API calls. This caused duplicate tasks to appear unpredictably.

**Fix:**
Removed the redundant `useEffect` responsible for the second fetch and ensured
tasks are loaded only once during initial mount.

**Commit:**
`Fix duplicate task fetch by removing redundant useEffect`

---

### Bug 2: Undo Snackbar Restores Old Tasks

**Problem:**
The undo feature relied on a `lastDeleted` state. When the snackbar auto-closed
or was manually dismissed, this state was not cleared. As a result, clicking
Undo after a later delete could restore an older, already-deleted task
(phantom data).

**Expected Behavior:**
A deleted task should only be recoverable while the undo snackbar is visible.
Once the snackbar closes, the deleted task should be forgotten.

**Fix:**
Added an explicit cleanup function in the `useTasks` hook to clear the
`lastDeleted` state. This function is called when the snackbar closes,
regardless of whether it closes due to timeout or user action.

This ensures undo is only possible during the active snackbar window.

**Commit:**
`Fix undo snackbar by clearing lastDeleted state on close`

---

### Bug 3: Unstable Sorting for Tasks with Equal ROI and Priority

**Problem:**
Tasks with identical ROI and priority were sorted using a random fallback,
causing the list order to change on each re-render.

**Fix:**
Added a deterministic alphabetical title tie-breaker to ensure stable and
consistent ordering across renders.

---

### Bug 4: Double Dialog Opening on Edit/Delete

**Problem:**
Clicking Edit or Delete also triggered the row click handler due to event bubbling,
causing multiple dialogs to open simultaneously.

**Fix:**
Stopped event propagation in Edit and Delete button handlers to ensure only the
intended dialog opens.

---

### Bug 5: ROI Calculation and Validation Errors

**Problem:**
ROI calculations produced `Infinity` or invalid values when time taken was zero
or inputs were invalid.

**Fix:**
Added input validation to safely handle zero and invalid values, returning `null`
instead of allowing invalid calculations. ROI formatting is handled in the UI.
Also ensured invalid revenue values no longer render as `$NaN` in the UI.
