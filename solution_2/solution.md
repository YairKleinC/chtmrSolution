#  מערכת אחזור מבוססת חיפוש סמנטי – ארכיטקטורה מוצעת

מטרת המערכת היא לאפשר למשתמשים לאחזר כתבות ותחקירים ממיליוני מקורות באינטרנט, על בסיס **משמעות**, ולא רק מילות מפתח. לשם כך נדרשת מערכת מודולרית, גמישה וניתנת לשדרוג בקלות.

---

##  רכיבי המערכת המרכזיים

- **Frontend** – ממשק משתמש אינטראקטיבי (React או Vue)
- **API / Backend** – תיווך בין השכבות, ניהול שאילתות
- **Semantic Search Engine** – המרת שאילתה לוקטור והשוואה לוקטורים של כתבות
- **Vector DB** – מאגר של embedding-ים ווקטוריים
- **Metadata DB** – בסיס נתונים לעובדות כמו כותרת, מחבר, תאריך
- **Embedding Service** – ממיר טקסטים לוקטורים סמנטיים
- **Pipeline לעיבוד כתבות** – Scraper → Cleaner → Embedder → Indexer

---

## 🗺️ תרשים ארכיטקטורה

```mermaid
graph TD
    UI[Frontend]
    API[API Gateway]
    SEARCH[Semantic Search Engine]
    VDB[Vector Database]
    MDB[Metadata Database]
    EMB[Embedding Service]
    PIPE[Ingestion Pipeline]

    UI --> API
    API --> SEARCH
    API --> MDB
    SEARCH --> VDB
    SEARCH --> EMB
    PIPE --> EMB
    PIPE --> VDB
    PIPE --> MDB
