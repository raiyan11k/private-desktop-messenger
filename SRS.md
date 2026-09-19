PRIVATE DESKTOP MESSENGER
Software Requirements Specification (SRS)
Version: 2.0
Document Type: Master Product & Engineering Specification
Target Platform: Windows Desktop
Initial Users: 5–10 users
Target Infrastructure Cost: $0/month
Development Model: Incremental AI-assisted development
________________________________________
1. DOCUMENT PURPOSE
This document is the single source of truth for the development of the Private Desktop Messenger.
The application is a private, lightweight, real-time Windows desktop instant-messaging application inspired by the interaction model and nostalgic desktop experience of classic PC messengers such as Garena's old social/chat client.
The application must NOT be developed as a browser-based messenger.
The actual messenger must be installed and operated as a standalone Windows desktop application.
A separate, simple public website will exist only to explain the application and allow users to download the desktop installer.
Development will be performed incrementally using GitHub Copilot or another AI coding assistant. The AI assistant must follow this SRS and the individual development instructions provided after the SRS.
________________________________________
2. PRODUCT CONCEPT
The system consists of two separate products:
2.1 Public Landing Website
A simple one-page website that:
•	Explains what the application is.
•	Shows the major features.
•	Displays screenshots/visual previews.
•	Provides a Windows download button.
•	Provides basic installation instructions.
•	Shows current version information.
•	May provide changelog/release information.
•	May provide basic system requirements.
•	May provide support/contact information.
The website does NOT provide the actual messaging functionality.
Users do not need to open the website to chat.
________________________________________
3.2 Desktop Messenger
The desktop messenger is the actual product.
Users:
1.	Download the installer from the website.
2.	Install the application.
3.	Launch the application from Windows.
4.	Create an account or log in.
5.	Use the messenger directly from the desktop.
The application must operate independently of a browser.
The application must feel like a traditional Windows instant-messaging client rather than a website wrapped inside a browser.
________________________________________
3. PRODUCT PHILOSOPHY
The application should prioritize:
1.	Security
2.	Reliability
3.	Desktop-native user experience
4.	Simplicity
5.	Low operating cost
6.	Performance
7.	Nostalgic/classic messenger experience
8.	Additional features
The application should remain lightweight and practical.
The first version is intended for a small private community of approximately 5–10 users, but the architecture must NOT hard-code this number.
________________________________________
4. TECHNOLOGY STACK
4.1 Desktop Application
Use:
•	Electron
•	React
•	TypeScript
•	Tailwind CSS
Electron provides:
•	Native desktop application packaging
•	Windows application windows
•	Multiple chat windows
•	Window positioning
•	Window resizing
•	Minimize/maximize/close
•	System tray integration where appropriate
•	Desktop notifications
•	Desktop-level behavior
React provides the application UI.
TypeScript is mandatory.
Tailwind CSS is preferred for styling.
________________________________________
4.2 Backend
Use Supabase for:
•	Authentication
•	PostgreSQL database
•	Realtime communication
•	File storage
Do NOT introduce a custom backend unless the SRS explicitly requires one.
________________________________________
4.3 Landing Website
Use:
•	Next.js
•	React
•	TypeScript
•	Tailwind CSS
Host the landing website using Cloudflare Pages or another genuinely free static/web hosting option.
The landing website and desktop application are separate projects or clearly separated application packages within the repository.
________________________________________
4.4 Desktop Distribution
The desktop application should eventually produce a Windows installer.
Preferred output:
•	.exe installer
The installer should install the application normally on Windows.
The application should have:
•	Application name
•	Application icon
•	Version number
•	Installer
•	Uninstaller
The final packaging strategy should be chosen based on the Electron ecosystem and free tooling.
No paid packaging service is required.
________________________________________
5. COST REQUIREMENT
The target operating cost is:
$0/month
The system should use free tiers wherever possible.
Expected infrastructure:
•	Cloudflare Pages/free web hosting for landing page.
•	Supabase free tier for backend.
•	GitHub for source code.
•	Free/open-source development tooling.
However, the SRS must NOT claim that third-party free tiers are guaranteed to remain free forever.
The architecture must therefore minimize:
•	Database usage
•	Storage usage
•	File size
•	Realtime traffic
•	Bandwidth
•	Unnecessary API requests
The application must enforce reasonable limits.
________________________________________
6. V1 NON-GOALS
The following are explicitly OUT OF SCOPE for V1:
•	Voice calls
•	Video calls
•	Screen sharing
•	Large group chat
•	Public social feed
•	Public posts
•	Payments
•	Advertising
•	Cryptocurrency
•	AI chatbot
•	Native Android application
•	Native iOS application
•	Federation
•	Self-hosted infrastructure
•	Mandatory end-to-end encryption
Voice/video should NOT be added simply because the architecture could technically support them.
The primary goal is a lightweight private desktop messenger.
________________________________________
7. AUTHENTICATION
Users must be able to:
•	Register
•	Log in
•	Log out
•	Reset password
•	Maintain a persistent account
Authentication must use Supabase Auth.
The application must NEVER manually store plaintext passwords.
Possible registration fields:
•	Email
•	Password
•	Display name
Authentication errors should be presented clearly.
Sessions should persist securely according to Supabase/Electron best practices.
________________________________________
8. PUBLIC USER ID
Every account must have a unique public user ID.
Example:
RH-48291
or another suitable format.
The public user ID:
•	Must be unique.
•	Must remain stable.
•	Can be shared with other users.
•	Can be used to search for friends.
•	Must NOT expose internal database identifiers unnecessarily.
Users should be able to find another user using their public ID.
________________________________________
9. USER PROFILE
Each user profile should support:
•	Avatar/profile picture
•	Display name
•	Public user ID
•	Status message
•	Online status
•	Account creation date
Users can edit:
•	Display name
•	Avatar
•	Status message
The profile UI should feel appropriate for a classic desktop messenger.
________________________________________
10. PRESENCE
Users should have presence states:
•	Online
•	Away
•	Offline
Presence should primarily use Supabase Realtime rather than repeatedly writing heartbeat records to the database.
The UI should show presence indicators beside friends.
Example:
🟢 Online
🟡 Away
⚪ Offline
Presence should update without requiring the user to refresh the application.
________________________________________
11. FRIEND SYSTEM
Users can:
•	Search users by public ID.
•	Send friend requests.
•	Accept requests.
•	Reject requests.
•	Remove friends.
•	Block users.
Friendship states:
•	PENDING
•	ACCEPTED
•	REJECTED
•	BLOCKED
•	REMOVED
The UI should contain a dedicated friend list.
Possible sections:
•	Friends
•	Pending Requests
•	Blocked Users
The friend list should show:
•	Avatar
•	Display name
•	Online status
•	Optional status message
•	Unread message indicator
________________________________________
12. MAIN DESKTOP APPLICATION UI
The main application must have a dedicated desktop messenger window.
It should NOT resemble a generic website.
The UI should resemble a classic PC instant messenger.
Suggested structure:
┌──────────────────────────────────────────────────────────┐
│  APP NAME                                  ─  □  X       │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────┐   Display Name                                 │
│  │ AVA  │   Online                                       │
│  └──────┘                                                │
│                                                          │
├──────────────────────────────────────────────────────────┤
│  FRIENDS                                                 │
│                                                          │
│  🟢 Friend One                                           │
│  🟢 Friend Two                                           │
│  🟡 Friend Three                                         │
│  ⚪ Friend Four                                           │
│                                                          │
├──────────────────────────────────────────────────────────┤
│  Friends    Requests    Settings                         │
└──────────────────────────────────────────────────────────┘
The exact design is not fixed.
The AI developer should build a polished original UI that captures the desktop instant-messenger feel.
________________________________________
13. GARENA-INSPIRED DESIGN DIRECTION
The application is inspired by the old Garena PC social/chat experience.
This means the design should capture characteristics such as:
•	Compact desktop layout
•	Friend-centric navigation
•	Small profile/avatar area
•	Online status indicators
•	Floating chat windows
•	Multiple simultaneous conversations
•	Window focus/z-index behavior
•	Nostalgic instant-messenger interaction
•	Chat sounds
•	Nudge functionality
•	Desktop notifications
•	Custom chat backgrounds
•	Lightweight UI
•	Strong visual distinction between online/offline users
However:
DO NOT copy Garena's proprietary assets.
Do not copy:
•	Garena logos
•	Garena trademarks
•	Proprietary source code
•	Copyrighted sounds
•	Copyrighted UI assets
•	Proprietary artwork
The application must have its own:
•	Name
•	Logo
•	Icons
•	Sounds
•	Graphics
•	Visual identity
The goal is to reproduce the type of experience, not illegally reproduce the original product.
________________________________________
14. POPUP CHAT WINDOWS
This is one of the most important features.
Opening a friend's chat should create a dedicated chat window/panel.
It should behave like a desktop messenger window.
Example:
┌────────────── Chat: Alex ─────────────────┐
│                                     ─ □ X │
├───────────────────────────────────────────┤
│                                           │
│ Alex: Hey!                                │
│                                           │
│                       You: Hey! 👋         │
│                                           │
│ Alex: Are you online?                     │
│                                           │
├───────────────────────────────────────────┤
│                                           │
│ Type a message...                   😊 📎 │
│                                           │
├───────────────────────────────────────────┤
│  Nudge                                    │
└───────────────────────────────────────────┘
Chat windows must support:
•	Open
•	Close
•	Minimize
•	Resize
•	Move
•	Focus
•	Bring to front
•	Multiple simultaneous windows
Example:
┌──────── Main Messenger ────────┐

│ Friends                        │
│                                │
│ 🟢 Alex                        │
│ 🟢 John                        │
│ 🟡 Mike                        │

└────────────────────────────────┘

      ┌──── Chat: Alex ─────┐
      │                     │
      │ Hello!              │
      └─────────────────────┘

                  ┌──── Chat: John ────┐
                  │                    │
                  │ Hey!               │
                  └────────────────────┘
Clicking a chat should bring that chat window to the front.
Each window should have its own:
•	Conversation
•	Scroll state
•	Input state
•	Unread state
•	Position
•	Size
Window positions/sizes may be persisted locally or per user where appropriate.
________________________________________
15. CHAT WINDOW BEHAVIOR
Chat windows should support:
Move
User can drag the title bar.
Resize
User can resize using window edges/corners.
Minimize
The chat disappears from the main visible area but remains open.
Close
The window closes, but the conversation remains stored.
Focus
Clicking the window brings it to the front.
Multiple windows
Multiple chats may remain open simultaneously.
Unread state
If a message arrives in an inactive/minimized chat:
•	Show unread indicator.
•	Highlight the relevant chat.
•	Optionally play a sound.
•	Optionally show desktop notification.
________________________________________
16. PRIVATE MESSAGING
V1 supports private 1-to-1 text conversations.
Users can:
•	Send messages
•	Receive messages
•	View conversation history
•	Scroll through messages
•	Send emoji
•	Send images
•	See message timestamps
•	See typing indicators
•	See read status
Messages should be delivered in real time.
Refreshing the application should NOT be required.
________________________________________
17. MESSAGE MODEL
Suggested message fields:
•	id
•	conversation_id
•	sender_id
•	body/content
•	message_type
•	attachment_path
•	created_at
•	updated_at
•	deleted_at
Message types may include:
•	TEXT
•	IMAGE
•	SYSTEM
Additional types can be introduced only when required.
________________________________________
18. MESSAGE STATUS
Messages should support:
•	Sending
•	Sent
•	Delivered
•	Read
•	Failed
The UI should provide appropriate feedback.
For example:
You: Hello          ✓
You: Are you there? ✓✓
The exact iconography can be designed later.
________________________________________
19. MESSAGE ORDERING AND REALTIME RELIABILITY
Realtime events may arrive:
•	Out of order
•	More than once
•	After reconnection
The client must handle this safely.
The application must:
•	Avoid duplicate messages.
•	Correctly order messages.
•	Reconcile local optimistic messages with server messages.
•	Recover after temporary network loss.
•	Resynchronize conversation state after reconnecting.
Do not assume realtime delivery is perfectly reliable.
________________________________________
20. TYPING INDICATOR
When a user is typing:
Alex is typing...
Typing state must be:
•	Realtime
•	Temporary
•	Debounced/throttled
•	NOT stored permanently in the messages table
Typing events should automatically expire.
________________________________________
21. EMOJI
Users should be able to send Unicode emoji.
A simple emoji selector may be provided.
The implementation should avoid unnecessary heavy dependencies where practical.
________________________________________
22. IMAGE AND SCREENSHOT SHARING
Users can send images through chat.
Supported formats:
•	JPEG
•	PNG
•	WebP
Recommended maximum file size:
5 MB
Images should be uploaded to Supabase Storage.
The database should store the storage reference/path rather than unnecessarily duplicating the image.
The UI should support:
•	Image preview
•	Sending
•	Receiving
•	Opening a larger image view
•	Appropriate loading/error states
Storage must be protected by appropriate Supabase policies.
________________________________________
23. DESKTOP SCREENSHOT EXPERIENCE
Because this is a desktop messenger, screenshot sharing should feel natural.
The implementation should consider support for:
Ctrl+V image paste
For example:
1.	User takes a screenshot.
2.	Screenshot is copied to clipboard.
3.	User focuses the chat input.
4.	User presses Ctrl+V.
5.	The application detects the image.
6.	The image is shown as a preview.
7.	User sends it.
This can be implemented after the basic image upload system is stable.
________________________________________
24. NUDGE SYSTEM
The messenger should have a classic instant-messenger-style Nudge feature.
A Nudge is a temporary realtime event.
When User A nudges User B:
•	User B's active chat window shakes briefly.
•	A nudge sound plays if sounds are enabled.
•	A visual effect is displayed.
•	The event is NOT stored as a normal message.
Example:
        ┌─────────────────────────┐
        │                         │
        │     Alex sent a Nudge!  │
        │                         │
        └─────────────────────────┘

             ← SHAKE →
Recommended anti-spam cooldown:
5–10 seconds per sender/recipient pair.
The cooldown can be adjusted during development.
Browser autoplay restrictions are less relevant because the messenger is a desktop application, but audio failures must still be handled gracefully.
Use an original application-owned sound.
Do not use copyrighted Garena sound effects.
________________________________________
25. CHAT BACKGROUNDS
Users can customize the background of individual conversations.
Options:
•	Default
•	Light
•	Dark
•	Custom image
Custom image formats:
•	JPEG
•	PNG
•	WebP
Recommended maximum:
5 MB
The background preference should be associated with:
•	User
•	Conversation
One user's background choice must NOT automatically change another user's background.
________________________________________
26. NOTIFICATIONS
The desktop application should support:
In-app notifications
•	New message
•	Friend request
•	Nudge
Windows desktop notifications
Where supported:
•	New message
•	Friend request
•	Other important events
Users should be able to configure:
•	Notifications enabled/disabled
•	Message sounds
•	Nudge sounds
•	Friend request notifications
________________________________________
27. SYSTEM TRAY
A system tray experience may be implemented.
Potential behavior:
•	Minimize application to tray.
•	Tray icon indicates application is running.
•	Clicking tray icon restores the application.
•	Right-click provides basic actions:
o	Open
o	Settings
o	Exit
This feature should be implemented only after the core messenger is stable.
________________________________________
28. DATABASE ARCHITECTURE
Suggested tables:
profiles
•	id
•	public_user_id
•	display_name
•	avatar_url
•	status_message
•	created_at
•	updated_at
friendships
•	id
•	requester_id
•	receiver_id
•	status
•	created_at
•	updated_at
conversations
•	id
•	type
•	created_at
•	updated_at
V1 conversation type:
PRIVATE
conversation_members
•	conversation_id
•	user_id
•	joined_at
messages
•	id
•	conversation_id
•	sender_id
•	body
•	message_type
•	attachment_path
•	created_at
•	updated_at
•	deleted_at
user_settings
•	user_id
•	notification_enabled
•	sound_enabled
•	theme
•	updated_at
chat_settings
•	user_id
•	conversation_id
•	background_type
•	background_path
•	window_width
•	window_height
•	window_position_x
•	window_position_y
•	updated_at
The exact schema may be adjusted when implementation begins, but unnecessary tables should not be created.
________________________________________
29. DATA RETENTION
Messages should automatically expire after:
30 days
Attachments associated with expired messages should also be deleted.
Cleanup must be:
•	Safe
•	Idempotent
•	Repeatable
•	Resistant to partial failures
The system must not leave large amounts of abandoned image data in storage.
The implementation must consider whether cleanup is performed through:
•	Supabase scheduled functions
•	Database jobs
•	Edge Functions
•	Another free-tier-compatible mechanism
The selected approach must not introduce unnecessary paid infrastructure.
________________________________________
30. SECURITY
Supabase Row Level Security is mandatory.
Users must only be able to:
•	Access their own profile.
•	Access profiles that are appropriate for public discovery.
•	Access friendships involving themselves.
•	Access conversations they belong to.
•	Read messages from conversations they belong to.
•	Create messages as themselves.
•	Modify/delete only messages they are authorized to modify.
•	Access authorized files.
The system must prevent users from manipulating IDs to access another user's private conversation.
________________________________________
31. STORAGE SECURITY
Storage policies must prevent unauthorized access to private attachments.
Do not make private chat images globally public unless there is a specific security justification.
Storage references should be handled securely.
________________________________________
32. SECRETS
Never place:
•	Supabase service-role keys
•	Private API keys
•	Database passwords
•	Server secrets
inside the client application source.
Public configuration may use appropriate public Supabase credentials.
Environment files must not be committed.
Include:
.env.example
The actual .env file must be ignored by Git.
________________________________________
33. VALIDATION AND LIMITS
The application should enforce sensible limits.
Recommended:
•	Message length: 4,000 characters.
•	Image upload: 5 MB.
•	Chat background: 5 MB.
•	Reasonable friend request rate.
•	Reasonable nudge rate.
•	Reasonable message sending rate.
•	Reasonable upload rate.
Limits should exist both for usability and to protect free-tier infrastructure.
________________________________________
34. PERFORMANCE
The application should feel responsive on normal Windows PCs.
Requirements:
•	Avoid unnecessary database queries.
•	Avoid polling where realtime is appropriate.
•	Use pagination for message history.
•	Recommended initial history page: 50 messages.
•	Lazy-load older messages.
•	Avoid loading entire conversations unnecessarily.
•	Compress/limit uploaded images where appropriate.
•	Prevent duplicate realtime subscriptions.
•	Clean up listeners when chat windows close.
•	Avoid memory leaks from multiple chat windows.
________________________________________
35. NETWORK RESILIENCE
The application must handle:
•	Temporary internet loss.
•	Supabase reconnects.
•	Application reconnecting after sleep.
•	Realtime subscription failures.
•	Failed messages.
•	Failed uploads.
The UI should clearly indicate when appropriate:
•	Connecting
•	Offline
•	Reconnecting
Messages should not silently disappear.
________________________________________
36. DESKTOP RESPONSIVENESS
The primary target is Windows desktop.
The UI does not need to behave like a mobile website.
However, the application should remain usable at:
•	1280×720
•	1366×768
•	1920×1080
Small application windows should degrade gracefully.
________________________________________
37. THEMES
At minimum:
•	Light theme
•	Dark theme
Potential future themes:
•	Classic
•	Custom
•	Seasonal
Theme selection should not require rebuilding the application.
________________________________________
38. SETTINGS
The application should eventually contain settings for:
Account
•	Display name
•	Avatar
•	Password/account actions
Appearance
•	Light/dark theme
•	Chat background preferences
Notifications
•	Notifications on/off
•	Message sound
•	Nudge sound
•	Friend request notifications
Privacy
•	Blocked users
•	Other privacy controls
Application
•	Version
•	Logout
•	Exit
________________________________________
39. ADMIN CAPABILITY
A simple administrator capability may be added later.
Potential abilities:
•	View user accounts
•	Disable abusive accounts
•	Manage basic system configuration
Admins must NOT automatically receive access to private messages unless the product explicitly introduces a legitimate moderation policy and appropriate authorization.
Admin authorization must be server-side.
________________________________________
40. LANDING WEBSITE
The public website should be intentionally simple.
Suggested sections:
Hero
Application name + short description.
Example:
A private desktop messenger built for fast, simple conversations.
Buttons:
•	Download for Windows
•	Learn More
Features
Show:
•	Private messaging
•	Friends
•	Realtime chat
•	Popup chat windows
•	Nudge
•	Image sharing
•	Custom backgrounds
•	Desktop notifications
Screenshots
Show the actual application UI.
Installation
Simple 3-step explanation:
1.	Download
2.	Install
3.	Log in and start chatting
System Requirements
Basic Windows requirements.
Version
Example:
Version 1.0.0
Footer
Basic copyright/project information.
The landing page should NOT contain the actual messenger.
________________________________________
41. INSTALLER EXPERIENCE
The Windows installer should:
•	Install the application.
•	Create Start Menu entry.
•	Optionally create desktop shortcut.
•	Provide uninstaller.
•	Preserve appropriate user settings during normal updates where possible.
The installer should be tested on a clean Windows environment before release.
________________________________________
42. AUTO UPDATE
Automatic application updates are optional for the first release.
If implemented later, the system must use a free and secure update mechanism.
Do not introduce a paid update infrastructure.
________________________________________
 
43. APPLICATION STRUCTURE
A recommended repository structure:
project-root/

├── desktop/
│   ├── electron/
│   ├── src/
│   │   ├── components/
│   │   │   ├── chat/
│   │   │   ├── friends/
│   │   │   ├── profile/
│   │   │   ├── notifications/
│   │   │   └── ui/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── lib/
│   │   │   ├── supabase/
│   │   │   ├── realtime/
│   │   │   └── utilities/
│   │   ├── types/
│   │   └── styles/
│   ├── public/
│   │   ├── sounds/
│   │   └── backgrounds/
│   └── package.json
│
├── website/
│   ├── app/
│   ├── components/
│   ├── public/
│   └── package.json
│
├── supabase/
│   ├── migrations/
│   ├── functions/
│   └── seed/
│
├── SRS.md
├── README.md
├── .gitignore
└── .env.example
The exact structure may change if the AI developer has a strong technical reason.
Do not reorganize the entire repository without a reason.
________________________________________
44. TESTING REQUIREMENTS
The project must eventually include:
Unit testing
For:
•	Utilities
•	Validation
•	Message state
•	Window state
•	Formatting
Integration testing
For:
•	Authentication
•	Friend system
•	Conversations
•	Messages
•	Realtime
•	Storage
UI testing
For:
•	Login
•	Friend list
•	Chat windows
•	Sending messages
•	Image sharing
•	Nudge
•	Settings
Security testing
Verify:
•	RLS
•	Authentication boundaries
•	Conversation access
•	Storage access
•	ID manipulation protection
Performance testing
Test:
•	Multiple open chat windows
•	Multiple realtime subscriptions
•	Large conversation history
•	Reconnection
•	Image uploads
________________________________________
45. DEVELOPMENT RULES FOR AI CODING AGENTS
This section is extremely important.
The AI coding agent must follow the SRS.
The SRS is the product's source of truth.
However, the agent must NOT attempt to implement everything at once.
Development will happen through individual instructions.
When receiving a development instruction:
1.	Read the relevant SRS sections.
2.	Inspect the existing repository.
3.	Understand the current implementation.
4.	Implement ONLY the requested phase/feature.
5.	Avoid unrelated refactoring.
6.	Do not implement future features prematurely.
7.	Run appropriate validation.
8.	Fix errors caused by the implementation.
9.	Report what changed.
10.	Report tests/checks performed.
11.	Report remaining limitations.
12.	Commit the work when instructed or when repository workflow permits.
________________________________________
46. AI AGENT HARD CONSTRAINTS
The AI agent MUST NOT:
•	Convert the project into a browser-only messenger.
•	Replace Electron with a normal web application.
•	Add voice/video in V1.
•	Add paid infrastructure.
•	Disable Supabase RLS.
•	Put service-role keys in the frontend.
•	Commit secrets.
•	Hard-code user accounts.
•	Hard-code the initial 5–10 users.
•	Remove authentication for convenience.
•	Bypass security to make development easier.
•	Replace Supabase without explicit instruction.
•	Introduce unnecessary dependencies.
•	Rewrite working code unnecessarily.
•	Implement all phases in one instruction.
•	Copy proprietary Garena assets.
•	Use copyrighted Garena sounds.
•	Claim internet latency can be guaranteed.
•	Assume realtime events can never duplicate.
•	Store temporary typing/nudge events permanently without a specific reason.
________________________________________
47. AI AGENT DEVELOPMENT BEHAVIOR
When an instruction is ambiguous:
•	Prefer the architecture in this SRS.
•	Preserve existing working functionality.
•	Make the smallest reasonable implementation.
•	Ask for clarification only when the ambiguity would materially change architecture or behavior.
The AI agent should explain significant architectural decisions.
________________________________________
48. DEVELOPMENT PHASES
Development should happen in the following order.
Phase 1 — Project Foundation
•	Repository structure
•	Electron application
•	React
•	TypeScript
•	Tailwind
•	Basic Electron window
•	Development scripts
•	Environment configuration
•	Basic landing website
•	Git configuration
•	Documentation
NO messaging yet.
________________________________________
Phase 2 — Supabase Foundation
•	Supabase project connection
•	Client configuration
•	Environment variables
•	Basic database migration structure
•	Secure configuration
NO complete authentication yet unless specifically requested.
________________________________________
Phase 3 — Authentication
•	Registration
•	Login
•	Logout
•	Session persistence
•	Password recovery
________________________________________
Phase 4 — Profiles
•	Profile creation
•	Public user ID
•	Display name
•	Avatar
•	Status message
________________________________________
Phase 5 — Friend System
•	Search by public ID
•	Friend requests
•	Accept
•	Reject
•	Remove
•	Block
________________________________________
Phase 6 — Conversations
•	Conversation creation
•	Conversation membership
•	Private 1-to-1 conversations
•	Conversation retrieval
________________________________________
Phase 7 — Realtime Messaging
•	Sending messages
•	Receiving messages
•	Optimistic UI
•	Message status
•	Message ordering
•	Reconnection
•	Duplicate prevention
________________________________________
Phase 8 — Presence and Typing
•	Online
•	Away
•	Offline
•	Typing indicators
________________________________________
Phase 9 — Desktop Chat Windows
•	Popup chat windows
•	Move
•	Resize
•	Minimize
•	Close
•	Focus
•	Multiple windows
•	Z-index
•	Window state
This phase is particularly important to the product identity.
________________________________________
Phase 10 — Nudge
•	Nudge event
•	Chat shake
•	Sound
•	Visual feedback
•	Cooldown
________________________________________
Phase 11 — Image Sharing
•	Upload
•	Preview
•	Send
•	Receive
•	Open image
•	Storage security
________________________________________
Phase 12 — Chat Backgrounds
•	Default
•	Light
•	Dark
•	Custom background
•	Per-conversation preferences
________________________________________
Phase 13 — Notifications
•	Desktop notifications
•	Sounds
•	Notification settings
________________________________________
Phase 14 — Screenshot Paste
•	Clipboard image detection
•	Ctrl+V
•	Image preview
•	Upload/send
________________________________________
Phase 15 — System Tray
•	Tray icon
•	Minimize to tray
•	Restore
•	Exit
________________________________________
Phase 16 — Message Retention
•	30-day message deletion
•	Attachment cleanup
•	Idempotent cleanup
________________________________________
Phase 17 — Settings
•	Account
•	Appearance
•	Notifications
•	Privacy
•	Blocked users
•	Application information
________________________________________
Phase 18 — Testing & Security Audit
•	Unit tests
•	Integration tests
•	UI tests
•	RLS tests
•	Storage security
•	Authentication security
•	Realtime reliability
•	Performance testing
________________________________________
Phase 19 — Production Build
•	Windows installer
•	Application icon
•	Versioning
•	Production environment
•	Production Supabase configuration
________________________________________
Phase 20 — Landing Website & Distribution
•	Final screenshots
•	Download button
•	Version information
•	Installation guide
•	System requirements
•	Release information
________________________________________
49. DEFINITION OF DONE
V1 is considered complete when:
•	The Windows application installs successfully.
•	Users can create accounts.
•	Users can log in.
•	Profiles work.
•	Public IDs work.
•	Friend system works.
•	Private conversations work.
•	Realtime messages work.
•	Message history works.
•	Typing indicators work.
•	Presence works.
•	Multiple popup chat windows work.
•	Windows can be moved/resized/minimized/closed.
•	Nudge works.
•	Image sharing works.
•	Chat backgrounds work.
•	Notifications work.
•	30-day retention works.
•	Security policies are verified.
•	RLS is enabled.
•	Storage policies are verified.
•	No secrets are committed.
•	The application can be packaged into a Windows installer.
•	The landing website can distribute the installer.
•	The project remains within the intended free-tier architecture under the expected small user base.
________________________________________
50. FINAL ARCHITECTURAL PRINCIPLE
The system should remain:
A real Windows desktop messenger with a small download website — NOT a website pretending to be a desktop messenger.
The core experience should be:
Website
   ↓
Download Windows Installer
   ↓
Install
   ↓
Launch Desktop Messenger
   ↓
Login
   ↓
Friend List
   ↓
Open Friend
   ↓
Floating Chat Window
   ↓
Real-time Conversation
The desktop application is the actual product.
The website is only the public entry point and download portal.
________________________________________
51. AI DEVELOPMENT WORKFLOW
The master SRS should be given to the AI coding agent first.
After the agent has read and understood it, development instructions should be given individually.
The recommended workflow is:
SRS.md
   ↓
Prompt 1
   ↓
Implement Phase 1
   ↓
Test
   ↓
Commit
   ↓
Prompt 2
   ↓
Implement next feature
   ↓
Test
   ↓
Commit
   ↓
Prompt 3
   ↓
...
The AI agent should never assume that receiving the SRS means it has permission to implement every feature immediately.
Each individual development instruction grants scope for that specific task.
________________________________________
52. CHANGE CONTROL
If a future requirement conflicts with this SRS:
1.	Identify the conflict.
2.	Explain the affected architecture.
3.	Do not silently change major architecture.
4.	Update the SRS when a decision is finalized.
5.	Continue development using the updated SRS as the new source of truth.
The SRS should remain synchronized with the actual product.
________________________________________
END OF SRS

