## **AUDIO LOG – Sentence-Per-Line, Flow-Based Timestamps**

### **1. Header Structure**

- Always start with:
```
ARCHIVE LOG – ANALOG RECORDING UNIT [unique 2 digit 1-100 + A-Z]
TITLE: [title of the log]
OPERATOR: [prefix + first name + last name]
ENTRY NO.: [3 digit number]
DATE: [current date]
DEVICE: Compact Cassette Vox Logger
RUN TIME: ~[total time of log]
```
    
- Keep **rank/title** if relevant (military, corporate, academic, etc.).
    
- Device names should feel era-appropriate (“Wrist Assist MK. II,” “Cassette Node,” “Voxclip Unit”).
    

---

### **2. Timestamp Philosophy – “Anchoring Moments”**

- Format: `[HH:MM:SS]` — always left-aligned.
    
- A **timestamp covers a continuous moment** of speech and/or sound until a natural break occurs.
    
- Start a **new timestamp** when:
    
    1. A noticeable pause, gap, or time skip occurs (e.g., “signal dropout,” silence, implied break).
        
    2. A **major** sound cue punctuates the moment (door slam, crash, burst of static).
        
    3. The subject’s tone or context clearly shifts.
        
- Never break mid-sentence for a timestamp.
    
- **Each sentence is on its own line** under the same timestamp.
    
- Think of timestamps like paragraph breaks — they chunk the flow for readability, not for every breath.
    

---

### **3. Speaker Tagging**

- First line after a timestamp always starts with:
    
    ```
    SPEAKER:
    ```
    
    (e.g., `CONRAD:`)
    
- Same speaker under the same timestamp:  
    No need to repeat the name unless the timestamp changes.
    
- After a sound cue inside the same timestamp:  
    Resume without repeating the speaker name.
    

---

### **4. Sound Cue Rules**

- Always **own line** — no attaching to dialogue text.
    
- **Format:** `[description of sound]`
    
- **Personal sound cues** use the speaker’s name in CAPS:  
    `[CONRAD chuckles]`  
    `[MAHONEY coughs]`
    
- **Environmental/neutral sounds** have no name:  
    `[static]`  
    `[deep inhale]`
    
- If a sound cue is big enough to break the scene’s flow, it triggers a **new timestamp**.
    
- If part of the same moment, it stays inside the current timestamp block.
    

---

### **5. Interruptions**

- Always on their own line:
    
    - Sharp cut: `—`
        
    - Trailing off: `...`
        
- If the cut or pause is significant enough to change the moment, create a **new timestamp** after it.
    

---

### **6. Tone & Voice**

- Dialogue should be **natural and unpolished** — slang, filler words, stumbles, and tangents are welcome.
    
- Worldbuilding emerges in passing, not as exposition dumps.
    
- Characters should feel like they’re talking to themselves or to a familiar audience, not narrating for a reader.
    

---

### **7. Ending the Log**

- Always close with either:
    
    ```
    [HH:MM:SS]
    [log ends]
    ```
    
- Or for abrupt/corrupted endings:
    
    - `[recording cuts out]`
        
    - `[data fragment terminates]`
        
