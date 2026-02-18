# **Frontend Engineer Assignment (No Code, High-Quality UI Focus)**

## **Evaluation Criteria**

* Frontend tech selection and reasoning (framework, state, data fetching)
* UI architecture (routing, component design, reusable patterns)
* API calling strategy (error handling, retries, abort, pagination)
* Browser-level caching + offline-friendly patterns
* Debugging + observability (logging, tracing, error boundaries)
* Security basics on client (token handling, safe downloads, XSS considerations)
* UX quality for async jobs (progress, partial results, resilience)

---

## **Problem 1: Video-to-Notes Platform (Frontend System Design)**

**Goal:** Upload video → job runs async → user sees status + outputs: Summary.md, highlights (timestamps), assets. [READ MORE ABOUT THE PROJECT](./Video-summary-platform.md)

**Your solution must include**

* **Screens:** Upload, Jobs list, Job detail (status/logs), Results (markdown + highlights)
* **UI states:** loading, queued, processing, success, failed, retry, partial output
* **API calling plan:** how you poll/stream job progress (polling vs SSE), abort on navigation
* **Caching:** what to cache in browser (job list, job detail, results), TTL strategy, invalidation
* **Debugging plan:** how you would debug “stuck processing” from frontend side (network logs, correlation id display)

**Your Solution for problem 1:**

You need to put your solution here.
My Understanding of the System

In this platform, a user uploads a video and the backend processes it to generate a summary, highlights with timestamps, and some assets. Since video processing can take time, the most important part from a frontend perspective is handling long-running jobs properly and keeping the user informed about what is happening.

My main goal would be to make the experience clear and predictable so the user never feels confused.

Screens Design
1. Upload Screen

On this screen, I would include:

Drag and drop video upload area

File validation (file type and size limit)

Upload progress bar

“Start Processing” button

Once the upload is complete and the job is created, I would redirect the user to the Job Detail page instead of keeping them on the upload screen. This makes more sense because processing can take time.

2. Jobs List Screen

This screen would show all previously uploaded jobs.

Each job row would contain:

Video name

Status (Queued / Processing / Success / Failed)

Created time

A button to view details

I would use color-coded badges for status so users can quickly understand the state of each job.

3. Job Detail Screen

This is the most important screen because this is where the user tracks progress.

It would include:

Current status badge

Progress bar (if the backend provides percentage)

A logs section (collapsible)

Retry button (if the job fails)

Cancel option (if still processing)

If partial results are available (for example, summary is ready but highlights are still generating), I would show the available content immediately instead of waiting for everything to complete.

I think showing partial output improves user trust.

4. Results Screen

When the job is completed successfully, I would show:

Markdown preview of the summary

Highlights with clickable timestamps

Download buttons (Summary.md and all assets as ZIP)

While rendering markdown, I would make sure to sanitize the content to prevent any XSS issues.

UI States Handling

I would handle the following states:

loading

queued

processing

partial output

success

failed

During processing, action buttons would be disabled to prevent duplicate requests.

If the user refreshes the page, the current job state should be restored instead of resetting.

API Calling Strategy

Since this is a long-running task, I would use polling by default.

After creating the job, I would:

Poll the job status every 5 seconds

Stop polling when the job reaches success or failed state

Use AbortController to stop polling if the user navigates away

If the backend supports Server-Sent Events (SSE), I would prefer using that for real-time updates. But polling would be my initial implementation because it is simpler and reliable.

For error handling:

Retry failed network requests up to 3 times

Use exponential backoff

Show user-friendly error messages

Caching Strategy

To balance performance and data freshness, I would:

Cache:

Job list (short TTL, around 30 seconds)

Job detail (short TTL if processing)

Final results (longer TTL, around 24 hours)

I would use in-memory caching for fast updates and possibly IndexedDB for storing completed results.

If the job status changes, I would invalidate the job detail cache to avoid stale UI.

Debugging & Observability

If a job appears stuck in processing, from the frontend side I would:

Check network polling frequency

Display correlation ID in the UI

Show last API response timestamp

Log errors centrally

I would also add a small “Report Issue” button that sends:

Job ID

Correlation ID

Browser information

Current job status

This would help the support team debug issues faster.

Final Thoughts

For this platform, I believe the most important part is handling async jobs in a clear and reliable way.

The frontend should:

Clearly show job status

Handle retries safely

Avoid stale data

Show partial results when possible

My focus would be on making the async experience feel transparent and trustworthy for the user.

---

## **Problem 2: LinkedIn Automation Platform (Frontend System Design)**

**Goal:** Connect LinkedIn → persona setup → draft preview → approve → schedule → posting history. [READ MORE ABOUT THE PROJECT](./linkedin-automation.md)

**Your solution must include**

* **Screens:** Connect, Persona editor, Drafts (3 variants), Approval, Scheduler, Post history
* **Form UX:** persona inputs validation, topic input rules, guardrails for scheduling
* **API calling:** draft generation request lifecycle, optimistic UI vs strict confirmation
* **Caching:** drafts caching, schedule list caching, refetch triggers after approval/post
* **Debugging:** how you surface posting failures to user and capture details for support

**Your Solution for problem 2:**

You need to put your solution here.

---

## **Problem 3: DOCX Template → Bulk Generator (Frontend System Design)**

**Goal:** Upload template → review fields → single generate → bulk via CSV → ZIP download + per-row report. [READ MORE ABOUT THE PROJECT](./docs-template-output-generation.md)

**Your solution must include**

* **Screens:** Template upload, Field review/editor, Single fill form, Bulk upload, Bulk run status, Report table, Downloads
* **Field UI:** field types (text/number/date), required/default, inline validation
* **Bulk UX:** CSV upload constraints, mapping UI (optional), progress + partial success
* **Browser caching:** template metadata caching, field schema caching, bulk report pagination caching
* **Downloads:** safe download UX (signed URL flow assumed), progress indicator

**Your Solution for problem 3:**

You need to put your solution here.

---

## **Problem 4: Character-Based Video Series Generator (Frontend System Design)**

**Goal:** Define characters once → create episode from story → view episode package (script/scenes/assets/render plan). [READ MORE ABOUT THE PROJECT](./char-based-video-generation.md)

**Your solution must include**

* **Screens:** Character library, Relationship editor, Episode creator, Episode detail (scenes), Asset gallery
* **Consistency UX:** show “locked character profile” per episode, version badges
* **API calling:** long-running generation job UI (progress, resume)
* **Caching:** character library caching, episode package caching, asset thumbnails caching

**Your Solution for problem 4:**

You need to put your solution here.

---

## **Cross-Cutting** 

Answer these in **bullet points** (max 1 page total):

1. **Frontend stack choice**

* EDIT YOUR ANSWER HERE: Framework (Next.js/Vue/etc), state management, router, UI kit, why.
  `<EDIT YOUR ANSWER HERE>`

2. **API layer design**

* Fetch/Axios choice, typed client generation (OpenAPI), error normalization, retries, request dedupe, abort controllers.
  `
  <EDIT YOUR ANSWER HERE>`

3. **Browser caching plan**

* What you cache (GET responses, derived state), where (memory, IndexedDB, localStorage), TTL/invalidation rules.
* How you handle “job status updates” without stale UI.
  `
  <EDIT YOUR ANSWER HERE>`

4. **Debugging & observability**

* Error boundaries, client-side logging approach, correlation id propagation, “report a problem” payload.
* How you would debug: slow uploads, failed downloads, intermittent 500s.
  `
  <EDIT YOUR ANSWER HERE>`

5. **Security basics**

* Token storage approach, CSRF considerations (if cookies), XSS avoidance for markdown rendering, safe file download patterns.
  ` A<EDIT YOUR ANSWER HERE>`
