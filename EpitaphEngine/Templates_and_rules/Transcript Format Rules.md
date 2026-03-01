## Transcript Format Rules

_(Cold, procedural, and structured. Used for interrogations, post-incident questioning, or internal security interviews.)_

---

### **1. Header Structure**

- Always start with **institutional metadata block**:
    ```
    :: TRANSCRIPT RECORD: [TYPE]
    :: FILE ID: [#ID-CODE]
    :: SUBJECT: [Full name, role, location if needed]
    :: INTERVIEWER: [Full name, role]
    :: LOCATION: [Interview room or environment]
    :: RECORD TYPE: [Full/Partial – Audio Only/Video Available]
    ```
- Keep it **ALL CAPS** for the header labels, followed by the relevant data in sentence case.
- Purpose: makes it feel like an official extract from a larger archive.

---

### **2. Timestamp Placement**

- Format: `[HH:MM:SS]` at the start of each exchange or significant pause.
- Timestamps are **monotonic** (always moving forward, no rewinds).
- If multiple lines occur in rapid succession within the same second, they share the timestamp.

---

### **3. Speaker Tagging**

- All **speaker names in FULL CAPS** followed by a colon:
    ```
    CPT. VOSS:
    MIRELLE:
    ```
- Always list the speaker’s **rank/title if applicable** on first appearance.
- If the same speaker continues without interruption, keep their tag — this format is **more rigid** than Audio Log A, so no dropping tags mid-conversation.

---

### **4. Continuations & Asides**

- Use `(cont’d)` if a speaker resumes after being interrupted:
    ```
    MIRELLE (cont’d):
    ```
- Short clarifications for tone or delivery in parentheses:
    - `(hesitant)`
    - `(overlapping)`
    - `(under breath)`

---

### **5. Sound Cues**

- Place **environmental or notable sounds** in square brackets on their own line or inline:
    ```
    [chair creaks]
    MIRELLE: I didn’t do anything.
    ```
- Keep descriptions concise and neutral — this is a **security transcript**, not creative prose.

---

### **6. Tone & Voice**

- Dialogue should remain **grounded, controlled, and procedural**.
    - The _interviewer_ asks short, direct questions.
    - The _subject_ may be emotional, but avoid long monologues — keep it to natural responses.
- Let worldbuilding slip in subtly through **questions and casual references** (“hydroponics corridor,” “deck six”).

---

### **7. Ending the Record**

- Always close with:
    ```
    :: END RECORD
    ```    
- Optional: if the transcript cuts abruptly or data is missing, note it:
    ```
    :: END RECORD – FILE INCOMPLETE
    ```

---

## **Example**

```
:: TRANSCRIPT RECORD: INTERVIEW/OBSERVATION
:: FILE ID: #092-ACT/DELTA-RED
:: SUBJECT: Mirelle Karr – Biological Technician
:: INTERVIEWER: CPT. Elen Voss (Security Oversight)
:: LOCATION: Processing Cell 03
:: RECORD TYPE: Partial – Audio Only

[00:00:02] CPT. VOSS:
State your name for the record.

[00:00:04] MIRELLE:
Mirelle Karr. Technician, deck six.

[00:00:09] CPT. VOSS:
Are you aware of why you’ve been detained?

[00:00:12] MIRELLE:
Because of what happened in the hydroponics corridor. But I didn’t—

[00:00:15] CPT. VOSS:
One step at a time.

[00:00:22] MIRELLE:
Yes. I mean—kind of. I was there, but it wasn’t a breach.

[00:00:28] MIRELLE (cont’d):
I heard someone. Talking. It sounded like me.

[00:00:35] MIRELLE (cont’d):
It was my voice, I swear. But it said things I didn’t say.

[00:00:39] CPT. VOSS:
We’ll come back to that.

:: END RECORD
```