# 🧠 מערכת אחזור מבוססת חיפוש סמנטי – ארכיטקטורה מוצעת

מטרת המערכת היא לאפשר למשתמשים לאחזר כתבות ותחקירים ממיליוני מקורות באינטרנט, על בסיס **משמעות**, ולא רק מילות מפתח. לשם כך נדרשת מערכת מודולרית, גמישה וניתנת לשדרוג בקלות.

---

## 🧱 רכיבי המערכת המרכזיים

- **Frontend**: ממשק משתמש אינטראקטיבי (לדוגמה React).
- **API / Backend**: שכבת תיווך, ניהול שאילתות, קישור בין שכבות.
- **מנוע חיפוש סמנטי**: מבצע המרת שאילתה לוקטור והשוואה לוקטורים של כתבות.
- **Vector DB**: מאחסן embedding-ים של כל כתבה.
- **Metadata Store**: שומר נתונים על הכתבות (כותרת, מחבר, תאריך).
- **Text Embedding Service**: ממיר טקסט לווקטור סמנטי.
- **Pipeline לעיבוד נתונים**: אוסף כתבות, מנקה, ממיר ומעדכן את בסיסי הנתונים.

---

## 🗺️ תרשים ארכיטקטורה

```mermaid
graph TD
    UI[Frontend<br>(React/Vue)]
    API[API Gateway<br>(FastAPI/Node.js)]
    SEM[Semantic Search Engine<br>(FAISS/Elastic)]
    VDB[Vector DB<br>(Weaviate/Pinecone)]
    MDB[Metadata DB<br>(PostgreSQL/MongoDB)]
    EMB[Text Embedding Service<br>(SBERT/OpenAI)]
    PIPE[News Ingestion Pipeline<br>(Scraper → Cleaner → Embedder)]

    UI --> API
    API --> SEM
    API --> MDB
    SEM --> VDB
    SEM --> EMB
    PIPE --> EMB
    PIPE --> VDB
    PIPE --> MDB
