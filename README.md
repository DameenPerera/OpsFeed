OPS FEED
Operational Task Feed Management System
README  •  System Documentation  •  v1.0


1. Overview
Ops Feed is a client-side web application designed for operational task tracking across branches. Inspired by social media feed interfaces, it allows staff to create posts — each representing a set of tasks tied to a specific branch, date, relevant officer, and priority level.

The system runs entirely in the browser with no server, no installation, and no internet connection required after the initial load. All data is stored persistently using IndexedDB inside the browser.

App Name	Ops Feed

Version	1.1.0

Type	Client-side Web Application (Single HTML File)

Database	IndexedDB via Dexie.js

Compatibility	Chrome, Firefox, Edge on Windows 7 and above

Installation	None required — open the .html file in a browser


2. Key Features

Feature	Description
Social Feed	Posts appear in a scrollable feed, newest first, similar to a social media timeline.
Post Tagging	Each post is tagged with Branch Name, Relevant Officer, Date, and Priority (High/Low).
Task Checklist	One post contains one or more tasks. Each task can be marked complete or incomplete.
Task Progress	A progress bar and count show how many tasks are completed per post.
Comments	Each post supports exactly one comment with optional image or file attachments.
Filter & Sort	Filter posts by branch, officer, date range, priority, and completion status.
Live Stats	Dashboard counts show total posts, total tasks, completed, and uncompleted tasks.
Dark / Light Mode	Light mode is the default. Toggle to dark mode with the theme button.
Zero Install	Runs as a single .html file — no server, no setup, no dependencies to install.
Data Export	Export all posts as a JSON backup file. Reimport to restore data.


3. How to Use
3.1  Opening the App
•	Locate the file OpsFeed.html on your computer.
•	Double-click the file to open it in your default browser.
•	No internet connection is required after the first load.
•	The app loads instantly with an empty feed on first use.

3.2  Creating a Post
•	Click the New Post button at the top of the feed.
•	Fill in the following fields:
◦	Branch Name — the branch this post relates to (required)
◦	Relevant Officer — the officer responsible (required)
◦	Date — defaults to today's date (required)
◦	Priority — select High (red) or Low (green)
•	Add tasks one by one using the task input field. At least one task is required.
•	Click Post to save. The post appears instantly at the top of the feed.

3.3  Managing Tasks
•	Each task inside a post has a checkbox.
•	Click the checkbox to toggle a task between complete and incomplete.
•	Completed tasks show with strikethrough text and a muted color.
•	The progress bar and counter update instantly.
•	All changes are saved automatically to IndexedDB.

3.4  Adding a Comment
•	Each post allows exactly one comment.
•	Click Add Comment below a post.
•	Type your comment text in the textarea.
•	Optionally attach images or files (stored as base64 in the database).
•	Files over 5MB will show a size warning.
•	Attached images appear as thumbnails — click to enlarge.
•	Non-image files appear as download links with a file icon.
•	You can edit or delete a comment after posting it.

3.5  Filtering Posts
•	Use the filter panel (sidebar on desktop, drawer on mobile) to narrow the feed.
•	Available filters:
◦	View: All Tasks / Uncompleted (at least one task pending) / Completed (all tasks done)
◦	Branch — filter by a specific branch name
◦	Relevant Officer — filter by officer name
◦	Priority — All / High / Low
◦	Date Range — from date to date
◦	Sort — Newest First / Oldest First / Priority / Most Tasks
•	Filters apply in real time. No submit button needed.
•	Click Clear Filters to reset all filters.

3.6  Deleting a Post
•	Click the trash icon on the top right of a post card.
•	A confirmation dialog appears before deletion.
•	Deletion is permanent and removes the post and its comment from IndexedDB.


4. Data Storage
4.1  How Data is Stored
Ops Feed uses IndexedDB, a built-in browser database, managed through the Dexie.js library. Data is stored locally inside your browser profile and persists between sessions. No data is ever sent to any server.

4.2  Database Structure

Feature	Description
Database Name	TaskFeedDB
posts store	Holds all posts: id, branch, relevantOfficer, date, priority, createdAt, tasks[]
comments store	Holds all comments: id, postId, text, attachments[], createdAt
tasks (embedded)	Stored as an array inside each post: { id, text, completed }
attachments	Stored as base64 data URLs inside the comment record

4.3  Backup and Restore
•	Use the Export button to download all data as a .json file.
•	Store this file safely as your backup.
•	Use the Import button to restore data from a previously exported JSON file.
•	Importing replaces all current data — back up before importing.

4.4  Data Limitations
•	IndexedDB capacity: typically 50MB–1GB+ depending on the browser and device.
•	Attached files and images are stored as base64, which increases size by ~33%.
•	Avoid attaching files over 5MB to keep the database performant.


5. Technical Details
5.1  Technology Stack

Feature	Description
HTML5	Structure and semantic markup
CSS3	Styling, layout (Grid + Flexbox), CSS variables for theming
Vanilla JavaScript (ES6+)	All logic, interactivity, and database operations
IndexedDB	Persistent client-side database built into the browser
Dexie.js (CDN)	Lightweight wrapper library for IndexedDB — the only external dependency
No frameworks	No React, Vue, Bootstrap, or jQuery — pure HTML/CSS/JS

5.2  Browser Compatibility
•	Google Chrome 57+ — Recommended
•	Mozilla Firefox 51+
•	Microsoft Edge 79+
•	Internet Explorer — Not supported (IE does not support modern IndexedDB)

Note: The app requires an internet connection on first open to load Dexie.js from the CDN. After that, it works fully offline.

5.3  File Structure
The entire application is contained in a single file:

    OpsFeed.html
This file includes all HTML markup, CSS styles, and JavaScript logic inline. No additional files, folders, or server configuration is required.


6. Post Structure
Each post in Ops Feed contains the following information:

Feature	Description
Branch Name	The branch or department the post is associated with.
Relevant Officer	The name of the officer or staff member responsible.
Date	The operational date for the post (not the creation timestamp).
Priority	High (red badge) or Low (green badge) — indicates urgency.
Tasks	One or more tasks, each with a text description and completion status.
Comment	One optional comment with text and optional file/image attachments.
Timestamp	Auto-generated creation time shown as relative time (e.g. '2 hours ago').


7. Theme & Display
•	Light Mode is the default theme with white backgrounds and dark text.
•	Dark Mode uses deep gray backgrounds with soft white text.
•	Toggle between modes using the sun/moon icon button in the top navigation bar.
•	The selected theme is saved to localStorage and restored on next visit.
•	All colors are defined as CSS variables for clean, consistent theming.


8. Troubleshooting

Feature	Description
App shows blank screen	Make sure you are using Chrome or Firefox. IE is not supported.
Data not saving	Check that your browser allows IndexedDB for local files (file://).
Dexie.js not loading	Ensure you have an internet connection on first load to fetch the CDN script.
Attachments not showing	Files over 5MB may fail to encode. Use smaller files.
Data lost after reinstall	Data is tied to your browser profile. Export a backup before reinstalling.
Filter not working	Click Clear Filters and reapply. Ensure the date range is valid.


9. Glossary

Feature	Description
Post	A feed entry created by a user, containing metadata tags and a task list.
Task	A single action item within a post. Can be marked complete or incomplete.
Relevant Officer	The staff member named on a post as responsible.
Branch	The branch or location the post is tagged to.
Priority	The urgency level of a post — High or Low.
Comment	A single note attached to a post, supporting text and file attachments.
IndexedDB	A browser-native database used to store all app data locally.
Dexie.js	A JavaScript library that simplifies working with IndexedDB.
Base64	An encoding method used to store files as text strings in the database.
Dark Mode	An alternate color theme using dark backgrounds for low-light use.



Ops Feed — Operational Task Feed Management System
Version 1.0  •  Client-Side  •  Zero Installation Required
Made by Damien Perera. All rights reserved.
