# Product Requirements Document (PRD)
## Home Database App for Family Knowledge, Asset Management, and AI-Enhanced Documentation

### 1. Overview
The **Home Database App** is a locally hosted, user-friendly application designed to centralize **family knowledge, asset management, life memories, operational documentation, and property management**, with a strong emphasis on **AI-powered documentation expansion**. 

It serves as a **robust system** for tracking:
- **Household items** (appliances, tools, vehicles)
- **Equipment rentals** (e.g., Bobcat)
- **Maintenance logs**
- **Family memories**
- **Property maps** (e.g., 80-acre property)
- **Documentation of systems and operations**

The system enables **automated backlinking** between entries, **quick data capture**, **AI-enhanced documentation**, **natural language queries**, and **offline functionality**. It must be **easy to back up, allow remote access**, and **prioritize rapid data entry** over extensive mobile browsing.

---

### 2. Goals and Objectives
- **Centralize Knowledge:** Replace scattered notes and chats with a single, structured system.
- **Quick Capture:** Enable rapid data entry on mobile (text, voice, photos).
- **Interconnected Notes (Automated):** AI-powered backlinking between related entries.
- **Automated Uploads:** AI-powered processing of receipts, photos, and voice memos.
- **AI-Driven Documentation Expansion:** Convert sparse notes into detailed records.
- **Offline Functionality:** Works **without** internet, stored on a home server.
- **Backup & Portability:** Easy migration via external storage.
- **Remote Access:** Optional cloud sync for access from anywhere.
- **Natural Language Querying:** Use a local LLM to search and expand records.
- **User-Friendly Experience:** Minimal mobile browsing, focus on **quick data entry**.
- **Property Management:** Support for maps, annotated notes, and spatial data.

---

### 3. User Personas
- **Primary User (You):** Tech-savvy, skilled at using AI to expand documentation.
- **Secondary Users (Family Members):** Less tech-savvy; need an easy way to log/view info.
- **External Users (Helpers, Extended Family):** Occasional access with limited permissions.

---

### 4. Use Cases

#### **4.1 Equipment Rental Tracking (Bobcat Example)**
- **Scenario:** You rent a Bobcat for $2000 to clear trees. The machine brings down a tree. You want to log the **cost, performance, issues**, and **expand notes** for future reference.
- **Features:**
  - **Quick Capture:** Text input, voice memo, photo upload.
  - **Automated Backlinking:** Links rental to "Tree Clearing Project."
  - **AI Expansion:** Converts "Brought down a tree" into a full **rental incident report**.
  - **Retrieval:** Search "Bobcat" to see rental, logs, and related records.

#### **4.2 Property Management (80-Acre Property Map)**
- **Scenario:** Maintain a map with quick notes like **"Tree clearing area"**, later expanded into detailed records.
- **Features:**
  - **Quick Capture:** Mobile entry for notes, images, and voice memos.
  - **Map Storage:** Annotated maps with coordinates.
  - **Automated Backlinking:** Connects to rentals, projects, incidents.
  - **AI Expansion:** Converts **"Tree Clearing Area: 2 acres cleared"** into a **detailed project log**.

#### **4.3 Life Memories (Daughter’s First Bike Ride)**
- **Scenario:** Capture quick memory ("She rode without training wheels!") and expand it into a **detailed story**.
- **Features:**
  - **Quick Capture:** Text, photo, voice note.
  - **AI Expansion:** Converts short notes into **detailed memory logs**.
  - **Automated Uploads:** Text a photo to auto-create an entry.

#### **4.4 Item Maintenance Logs (Leather Shoes, Tesla)**
- **Scenario:** Track maintenance with **quick notes**, later expanded via AI.
- **Features:**
  - **Quick Capture:** Mobile text, receipt photo.
  - **Automated Backlinking:** Links notes to **maintenance guides**.
  - **AI Expansion:** Converts "Cleaned shoes with Saphir" into a **detailed log**.

#### **4.5 Family Documentation (Home Server, Ubiquiti)**
- **Scenario:** Log system processes with **quick notes**, later expanded into guides.
- **Features:**
  - **Quick Capture:** Short notes, photo uploads.
  - **AI Expansion:** Converts "Restart Ubiquiti via admin panel" into a **full restart guide**.

---

### 5. Functional Requirements

#### **5.1 Data Storage**
- Uses **Supabase PostgreSQL** and **Supabase Storage**.

#### **5.2 Quick Capture**
- **Mobile App:**
  - **Minimal data entry** (predefined fields, voice memos, photos).
  - **One-tap save**, triggers **automatic backlinking** and **AI expansion**.
- **Texting Integration:**
  - Users **text receipts, photos, or voice memos** to an **AI-powered Twilio number**.

#### **5.3 Interconnected Notes (Automated Backlinking)**
- **AI-Powered Keyword Matching:** Detects connections between entities.
- **OCR & Image Analysis:** Extracts text from receipts and photos.
- **Transcription Matching:** Extracts keywords from voice memos.
- **Graph View:** Web visualization using **react-force-graph**.

#### **5.4 AI-Driven Documentation Expansion**
- **Expansion Workflow:**
  1. User captures **sparse note** (e.g., "Bobcat brought down a tree").
  2. **LLM generates detailed documentation** with context from backlinks.
  3. **Expanded log is saved** as a new entry.
- **Example:**
  - **Input:** "Cleaned shoes with Saphir."
  - **Expanded Output:** "On 2023-10-16, I cleaned my leather shoes using Saphir Renovateur, following the ‘Shoe Care Guide.’"

#### **5.5 Automated Uploads**
- **Texting Workflow:**
  - User **texts a receipt, voice memo, or photo**.
  - AI extracts data, **creates entries, adds backlinks**.
  - AI optionally **expands into full documentation**.

#### **5.6 Property Management (Maps & Notes)**
- **Storage:** Maps stored in Supabase, metadata as JSON.
- **Annotations:** AI extracts and backlinks **key locations**.
- **Map Display:** **react-leaflet** (web), **react-native-maps** (mobile).

#### **5.7 Offline Functionality**
- **Local Supabase hosting**, **mobile app caching**.

#### **5.8 Backup and Portability**
- **Script-based backups** (DB & Storage), **external drive support**.

#### **5.9 Remote Access**
- Hybrid **local/cloud sync** using **Supabase authentication**.

#### **5.10 Natural Language Querying**
- Uses **local LLM (Ollama)** to query and expand documentation.

#### **5.11 User-Friendly Experience**
- **Quick capture first**, AI **handles complexity** in the background.

---

### 6. Non-Functional Requirements
- **Performance:** Quick capture <10s, AI expansions <5s, map display <3s.
- **Scalability:** Supports **10 users, thousands of entities**.
- **Security:** RLS, JWT authentication, encrypted storage.
- **Reliability:** Works **fully offline**, automated weekly backups.

---

### 7. Technical Stack
- **Supabase PostgreSQL**
- **Whisper (transcription)**
- **Tesseract.js (OCR)**
- **TensorFlow.js (image analysis)**
- **Ollama (local LLM)**

---

### 8. Success Metrics
- **80%** of notes expanded into detailed documentation.
- **90%** of entries logged in <10s.
- **50%** of uploads automatically processed with **90% backlinking accuracy**.
- **100%** core functionality **available offline**.

---

### 9. Risks and Mitigations
- **Risk:** AI backlinking is inaccurate → **Mitigation:** Review queue for AI-generated backlinks.
- **Risk:** LLM-generated expansions overwhelm storage → **Mitigation:** User approval required before saving.

---

### 10. Timeline and Milestones
- **Month 1:** Set up Supabase, Twilio, and AI tools.
- **Month 2:** Implement quick capture.
- **Month 3:** Add documentation, memories, maintenance logs.
- **Month 4:** Automate uploads & AI expansion.
- **Month 5:** Integrate LLM, test offline mode.
- **Month 6:** Deploy & test with family.

---

### 11. Appendix
- **Example AI Expansion for Bobcat:**
  - **Input:** "Brought down a tree—check model stability"
  - **Expanded Output:** "On 2023-10-16, the rented Bobcat unexpectedly brought down a tree, suggesting potential stability concerns with the model."