# family-knowledge


Product Requirements Document (PRD)
Home Database App for Family Knowledge, Asset Management, and AI-Enhanced Documentation
1. Overview
The Home Database App is a locally hosted, user-friendly application designed to centralize family knowledge, asset management, life memories, operational documentation, and property management, with a strong emphasis on enabling the primary user to expand documentation using AI. It acts as a robust system for tracking household items (e.g., appliances, tools, vehicles), equipment rentals (e.g., Bobcat), maintenance logs, family memories, documentation, and property maps (e.g., 80-acre property), all interconnected through automated backlinking. Key features include quick data capture, fully automated interconnected notes, automated uploads, natural language querying and documentation expansion via a local LLM, and offline functionality. The app must be easy to back up, allow remote access, and prioritize minimal mobile browsing with rapid data entry, serving as the primary user’s ultimate system for AI-driven documentation.
2. Goals and Objectives
	•	Centralize Knowledge: Consolidate all family data in one accessible place, replacing scattered notes and chats, to serve as a single system for documentation.
	•	Quick Capture: Enable rapid data entry, especially on mobile, to log details like equipment rentals, project outcomes, memories, and property notes without friction.
	•	Interconnected Notes (Fully Automated): Automatically backlink entities (e.g., linking a Bobcat rental to a tree-clearing project) using AI-driven keyword matching, OCR, image analysis, and transcription, inspired by Reflect.
	•	Automated Uploads: Support AI-powered processing of receipts, photos, and voice memos, inspired by Ramp, to minimize manual work and feed into documentation expansion.
	•	AI-Driven Documentation Expansion: Leverage a local LLM to expand sparse notes into detailed documentation (e.g., turning “Bobcat brought down a tree” into a full incident report), fulfilling the primary user’s strength in using AI for documentation.
	•	Offline Functionality: Ensure the app works locally without internet, with data stored on a home server.
	•	Backup and Portability: Provide easy backup and restore to physical drives for system migration.
	•	Remote Access: Enable access from anywhere, even if the home server is down, via a cloud sync option.
	•	Natural Language Querying: Integrate a local LLM for querying data and generating expanded documentation (e.g., “Expand my notes on the Bobcat rental”).
	•	User-Friendly Experience: Ensure the app is intuitive for all family members, with minimal mobile browsing.
	•	Property Management: Support spatial data (e.g., maps of an 80-acre property) with annotated notes for quick reference.
3. User Personas
	•	Primary User (You): Tech-savvy family member skilled at expanding documentation with AI, seeking a system to organize and amplify data (e.g., turning quick notes into detailed records for future decisions like Bobcat purchases or property management).
	•	Secondary Users (Family Members): Less tech-savvy users who need a simple interface to log memories, maintenance, property notes, or view information, with minimal mobile browsing.
	•	External Users (Extended Family, Helpers): Occasional users who may need remote access to documentation, property maps, or memories, with read-only or limited write access.
4. Use Cases
Below are the key use cases, updated to emphasize your motivation for AI-driven documentation expansion and the system’s role in supporting it.
4.1 Equipment Rental Tracking (Bobcat Example)
	•	Scenario: You rented a Bobcat from Action Rents for $2000 for a week to clear trees on your 80-acre property. The Bobcat brought down a tree, and you want to log the model, cost, performance, and issues as a quick note, then use AI to expand it into detailed documentation for future reference (e.g., deciding to rent again or buy your own).
	•	Requirements:
	◦	Quick Capture:
	▪	Mobile app allows rapid entry of rental details (vendor, cost, duration, model) via a form with minimal fields (e.g., “Action Rents, $2000, 1 week”).
	▪	Voice memo upload (e.g., “The Bobcat worked well but brought down a tree—check the model”) with automatic transcription.
	▪	Photo upload (e.g., receipt, Bobcat in action) with OCR to extract data (e.g., model, cost).
	▪	Texting integration: Text a receipt photo or voice memo to a Twilio number, and the app logs it under “Bobcat Rental.”
	◦	Data Storage:
	▪	Store rental as an “Item” with category “Rental Equipment” in the Items table.
	▪	Log sparse details (e.g., “Brought down a tree”) in the description or Logs table.
	▪	Store related files (receipts, photos, voice memos) in Supabase Storage, linked via the Files table.
	◦	Interconnected Notes (Fully Automated):
	▪	Automatically backlink to a “Tree Clearing Project” (stored as a Documentation entry) by matching keywords (e.g., “tree clearing” in transcription).
	▪	Automatically backlink to related entities (e.g., “Property Map” documentation) by AI-driven context analysis.
	◦	AI-Driven Documentation Expansion:
	▪	Use the local LLM to expand sparse notes (e.g., “Brought down a tree”) into detailed documentation:
	▪	User query: “Expand my notes on the Bobcat rental.”
	▪	LLM output: “On 2023-10-16, we rented a Bobcat from Action Rents for $2000 for one week to clear trees on our 80-acre property. During operation, the Bobcat inadvertently brought down a tree due to stability issues with the model (TBD). This suggests checking the model’s specifications for stability before future rentals or purchases.”
	▪	Save expanded documentation as a Documentation entry (e.g., “Bobcat Rental Report”), automatically backlinked to the rental item.
	◦	Automated Uploads:
	▪	Texting a receipt triggers OCR to extract data (e.g., model, cost), auto-creates an Items entry, and backlinks to related entities.
	▪	Texting a voice memo triggers transcription, logs it, and prompts the LLM to expand it into detailed documentation.
	◦	Retrieval:
	▪	Search for “Bobcat” to retrieve the rental, expanded report, and backlinked entities.
	▪	LLM query: “What issues did we have with the Bobcat?” → “The Bobcat brought down a tree due to stability issues, as detailed in the ‘Bobcat Rental Report’ from 2023-10-16.”
4.2 Property Management (80-Acre Property Map)
	•	Scenario: You own an 80-acre property and want to maintain a map with quick notes (e.g., “Tree clearing area,” “Bobcat incident”) that AI can expand into detailed documentation for reference when getting help or planning future projects.
	•	Requirements:
	◦	Quick Capture:
	▪	Mobile app allows rapid entry of property notes (e.g., “Tree Clearing Area: Cleared 2 acres”) with optional coordinates.
	▪	Photo upload (e.g., map of the property) with image analysis to identify features (e.g., “trees”).
	▪	Voice memo upload (e.g., “This is where the Bobcat brought down a tree”) with transcription.
	▪	Texting integration: Text a map photo or voice memo to auto-log it under “Property Notes.”
	◦	Data Storage:
	▪	Store property notes as Documentation entries with category “Property Management.”
	▪	Store maps in Supabase Storage (file_category = “map”), with metadata (e.g., coordinates) in the content field as JSON.
	◦	Interconnected Notes (Fully Automated):
	▪	Automatically backlink to “Bobcat Rental” (item) and “Tree Clearing Project” (documentation) by matching keywords (e.g., “Bobcat,” “tree clearing”).
	▪	Automatically backlink map annotations to related notes by AI-driven context analysis.
	◦	AI-Driven Documentation Expansion:
	▪	Use the local LLM to expand sparse notes (e.g., “Tree Clearing Area: Cleared 2 acres”) into detailed documentation:
	▪	User query: “Expand my notes on the tree clearing area.”
	▪	LLM output: “The ‘Tree Clearing Area’ on our 80-acre property spans 2 acres at coordinates (lat: 40.7128, lng: -74.0060). On 2023-10-16, we cleared this area using a Bobcat rented from Action Rents for $2000. The process was effective but included an incident where the Bobcat brought down a tree, indicating potential stability concerns.”
	▪	Save expanded documentation as a Documentation entry, automatically backlinked to the map and “Bobcat Rental.”
	◦	Automated Uploads:
	▪	Texting a map photo triggers image analysis, creates a Documentation entry, and backlinks to related entities.
	▪	Texting a voice memo triggers transcription, logs it, and expands it into detailed documentation.
	◦	Retrieval:
	▪	Mobile app shows a “Property” section with a tappable map icon, displaying the map with annotations.
	▪	LLM query: “Where did the Bobcat incident happen?” → “The Bobcat incident occurred at the ‘Tree Clearing Area’ (lat: 40.7128, lng: -74.0060), detailed in the expanded documentation from 2023-10-16.”
4.3 Life Memories (Daughter’s First Bike Ride)
	•	Scenario: Capture a memory of your daughter’s first bike ride with a quick note, then use AI to expand it into a detailed story.
	•	Requirements:
	◦	Quick capture via mobile app (e.g., “She rode without training wheels!”).
	◦	Automatic backlink to “Bike” (item) by matching keywords.
	◦	AI expansion: “Expand my memory of her bike ride” → “On 2023-10-16, our daughter achieved a milestone by riding her bike without training wheels for the first time. It happened on the driveway, and she was thrilled!”
	◦	Automated upload via texting (e.g., text a photo to auto-create a memory).
4.4 Item Maintenance Logs (Leather Shoes, Tesla)
	•	Scenario: Track maintenance with quick notes (e.g., “Cleaned shoes with Saphir”), then use AI to expand it into a detailed log.
	•	Requirements:
	◦	Quick capture via mobile app (text, receipt photo).
	◦	Automatic backlink to “Shoe Care Guide” (documentation) by matching keywords.
	◦	AI expansion: “Expand my shoe maintenance note” → “On 2023-10-16, I cleaned my leather shoes using Saphir Renovateur, following the ‘Shoe Care Guide.’ The process restored the leather’s shine.”
	◦	Automated upload via texting (e.g., text a receipt to auto-create a log).
4.5 Family Documentation (Home Server, Ubiquiti)
	•	Scenario: Document systems with quick notes (e.g., “Restart Ubiquiti via admin panel”), then use AI to expand it into a full guide.
	•	Requirements:
	◦	Quick capture via mobile app.
	◦	Automatic backlink to “Ubiquiti Router” (item) by matching keywords.
	◦	AI expansion: “Expand my Ubiquiti note” → “To restart the Ubiquiti router, log into the admin panel at 192.168.1.1, navigate to Settings > System, and click Reboot. This resets the system without losing settings.”
5. Functional Requirements
5.1 Data Storage
	•	Entities: (Unchanged from previous PRD, see Section 5.1)
	•	Storage: Use Supabase PostgreSQL and Storage.
5.2 Quick Capture
	•	Mobile App:
	◦	Rapid entry forms with minimal fields (e.g., for rentals: vendor, cost; for property notes: title, details).
	◦	Voice memo recording with automatic transcription (local Whisper).
	◦	Photo/receipt/map upload with AI analysis (OCR, image analysis).
	◦	One-tap “Save” to store data and trigger automatic backlinking and AI expansion prompts.
	•	Texting Integration:
	◦	Twilio phone number for texting uploads, processed by AI to create entries and backlinks.
5.3 Interconnected Notes (Fully Automated)
	•	Automatic Backlinking:
	◦	Keyword Matching: Search entity fields for keywords and context (e.g., “Bobcat” links to “Bobcat Rental”).
	◦	OCR Matching: Extract keywords from receipts/maps (e.g., “Action Rents” links to “Bobcat Rental”).
	◦	Image Analysis Matching: Identify features in photos (e.g., “trees” links to “Tree Clearing Project”).
	◦	Transcription Matching: Extract keywords from voice memos (e.g., “bike” links to “Bike”).
	◦	AI Context Analysis: Use the local LLM to infer deeper connections (e.g., “tree clearing” and “Bobcat” in a note link to both “Tree Clearing Project” and “Bobcat Rental”).
	◦	Storage: Store backlinks in the Backlinks table, created automatically by AI.
	◦	Display: Show backlinks on entity pages using shadcn (web) or React Native (mobile).
	•	Network View:
	◦	Web: Visualize backlinks with react-force-graph.
	◦	Mobile: Show backlinks as a tappable list.
5.4 AI-Driven Documentation Expansion
	•	Expansion Workflow:
	◦	User captures a sparse note (e.g., “Bobcat brought down a tree”).
	◦	Option to trigger expansion via a button (web: shadcn ; mobile: React Native ) or LLM query (e.g., “Expand my Bobcat note”). 
	◦	Local LLM processes the note, pulling context from related entities (via backlinks) and generating detailed documentation.
	◦	Save expanded documentation as a new Documentation entry, automatically backlinked to the original entity.
	•	Examples:
	◦	Input: “Cleaned shoes with Saphir.”
	◦	Expanded Output: “On 2023-10-16, I cleaned my leather shoes using Saphir Renovateur, a premium leather conditioner, as recommended in the ‘Shoe Care Guide.’ The process involved applying the product with a cloth, restoring the leather’s shine.”
	◦	Saved as: Documentation entry titled “Shoe Cleaning Log,” backlinked to “Leather Shoes” (item).
5.5 Automated Uploads
	•	Texting Workflow:
	◦	Text a receipt, photo, voice memo, or map to the Twilio number.
	◦	Backend uses AI (OCR, image analysis, transcription) to extract data, create entries, and backlink to related entities.
	◦	LLM optionally expands the entry into detailed documentation (e.g., a texted receipt becomes a full maintenance log).
	◦	Logs actions in Logs and sends confirmation texts.
	•	App Workflow:
	◦	Direct uploads in the mobile app use the same AI processing logic.
5.6 Property Management (Maps and Notes)
	•	Map Storage: Store maps in Supabase Storage, with metadata in Documentation as JSON.
	•	Map Annotations: Use AI to extract annotations from uploaded maps, store as Documentation entries, and backlink to related entities.
	•	Map Display: Web (react-leaflet), Mobile (react-native-maps) with tappable annotations.
	•	Quick Reference: Mobile home screen “Property” section with one-tap map access.
5.7 Offline Functionality
	•	Local Supabase hosting and mobile app caching for offline use.
5.8 Backup and Portability
	•	Script to dump DB and Storage files, restorable on another machine.
5.9 Remote Access
	•	Hybrid local/cloud approach with Supabase sync and authentication.
5.10 Natural Language Querying
	•	Local LLM (Ollama) for querying and expanding documentation.
5.11 User-Friendly Experience
	•	Web and mobile UIs prioritize quick capture and minimal browsing, with AI handling complexity.
6. Non-Functional Requirements
	•	Performance: Quick capture <10s, LLM queries/expansions <5s, map display <3s.
	•	Scalability: Support 10 users, thousands of entities.
	•	Security: RLS, JWT, encryption.
	•	Reliability: Offline functionality, automated backups.
7. Technical Stack
	•	Unchanged from previous PRD, with added emphasis on AI tools (Whisper, Tesseract.js, TensorFlow.js, Ollama).
8. Success Metrics
	•	AI Expansion: 80% of sparse notes expanded into detailed documentation within 6 months.
	•	Quick Capture: 90% of entries logged in <10s.
	•	Automation: 50% of uploads processed automatically with 90% backlinking accuracy.
	•	Retrieval: 90% of LLM queries accurate in <5s.
	•	Offline Usage: 100% core functionality offline.
	•	Backup: Weekly backups successful.
9. Risks and Mitigations
	•	Risk: AI backlinking or expansion is inaccurate.
	◦	Mitigation: Add a review queue for AI-generated backlinks/documentation, refine keyword matching and LLM prompts.
	•	Risk: LLM expansion overwhelms storage.
	◦	Mitigation: Limit expansion frequency, store only approved expansions.
10. Timeline and Milestones
	•	Month 1: Set up project (web, mobile, Supabase, Twilio, AI tools).
	•	Month 2: Implement core storage and quick capture.
	•	Month 3: Add Documentation, Memories, MaintenanceLogs, Property Management with automatic backlinking.
	•	Month 4: Implement automated uploads and AI expansion.
	•	Month 5: Integrate LLM, map display, and test offline functionality.
	•	Month 6: Deploy, test, set up backups, conduct family testing.
	•	Month 7: Polish UI, refine AI features, finalize system.
11. Appendix
	•	Example AI Expansion for Bobcat:
	◦	Input: Logs: "Brought down a tree—check model stability"
	◦	Expanded Output: Documentation: "Bobcat Rental Incident Report", content: "On 2023-10-16, during a tree-clearing project on our 80-acre property, the Bobcat rented from Action Rents for $2000 brought down a tree unexpectedly. This incident suggests potential stability issues with the model (TBD), which should be reviewed before future rentals or purchases."

