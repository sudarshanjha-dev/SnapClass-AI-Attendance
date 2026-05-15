# SnapClass — AI-Powered Attendance System

> Take attendance in seconds, not minutes. No roll calls, no paper sheets.

SnapClass is a full-stack AI attendance system that lets teachers mark attendance using **face recognition** from a class photo or **voice biometrics** by having students say "Present". Built with Streamlit and Supabase, it works entirely from a browser — no app installation needed.

🌐 **Live App:** [snap-attendance.streamlit.app](https://snap-attendance.streamlit.app)
🖥️ **Landing Page:** [snap-class-landing-page-psi.vercel.app](https://snap-class-landing-page-psi.vercel.app)
📦 **Landing Page Repo:** [SnapClass-Landing-Page](https://github.com/sudarshanjha-dev/SnapClass-Landing-Page)

---

## Features

**For Teachers**
- Face ID attendance — upload a single class photo and the system identifies every student automatically
- Voice ID attendance — students say "Present" one by one; the system matches their voice biometrics
- QR code course enrollment — generate a QR code for any course and share it with students
- Attendance dashboard — view records, confidence scores, and export as CSV

**For Students**
- Enroll via QR code in seconds
- Register face and voice biometrics once during onboarding
- Track your own attendance across all enrolled subjects from a personal dashboard

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend / App | Streamlit |
| Face Recognition | `face_recognition` (Dlib + HOG) |
| Voice Biometrics | Resemblyzer + Librosa |
| Database & Auth | Supabase (PostgreSQL) |
| QR Code Generation | Segno |
| Image Processing | Pillow, NumPy |
| ML Utilities | scikit-learn, pandas |

---

## Project Structure

```
SnapClass-AI-Attendance/
├── app.py                  # Entry point — routing between home, teacher, student screens
├── requirements.txt
└── src/
    ├── screens/
    │   ├── home_screen.py          # Login / landing
    │   ├── teacher_screen.py       # Teacher dashboard
    │   └── student_screen.py       # Student dashboard
    └── components/
        └── dialog_auto_enroll.py   # QR-based auto enrollment dialog
```

---

## Getting Started

### Prerequisites

- Python 3.9+
- A [Supabase](https://supabase.com) project with the required tables set up
- CMake installed (required for `dlib`)

### Installation

```bash
# Clone the repo
git clone https://github.com/sudarshanjha-dev/SnapClass-AI-Attendance.git
cd SnapClass-AI-Attendance

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
# Create a .env file or set Streamlit secrets:
# SUPABASE_URL = your_supabase_url
# SUPABASE_KEY = your_supabase_anon_key
```

### Run locally

```bash
streamlit run app.py
```

The app will open at `http://localhost:8501`

---

## How It Works

**Face ID Attendance**
1. Teacher uploads a class photo
2. `face_recognition` detects and encodes all faces in the image
3. Encodings are compared against stored student face embeddings in Supabase
4. Matched students are marked present with a confidence score

**Voice ID Attendance**
1. Each student records a short voice clip saying "Present"
2. `Resemblyzer` generates a speaker embedding (d-vector) from the audio
3. The embedding is compared against the student's stored voice profile using cosine similarity
4. Students above the similarity threshold are marked present

**QR Enrollment**
1. Teacher creates a course and generates a QR code via `Segno`
2. Student scans QR → redirected to app with `?join-code=` query parameter
3. App auto-triggers enrollment dialog on login

---

## Environment Variables

Create a `.streamlit/secrets.toml` file:

```toml
SUPABASE_URL = "https://your-project.supabase.co"
SUPABASE_KEY = "your-anon-key"
```

---

## Screenshots


<img width="732" height="622" alt="Screenshot 2026-05-15 174750" src="https://github.com/user-attachments/assets/f030cc16-ce0a-4280-840e-2128b6a2f2b5" />
<img width="808" height="545" alt="Screenshot 2026-05-15 174657" src="https://github.com/user-attachments/assets/c7814693-57d2-42df-977a-898f0d32d8cb" />
<img width="748" height="607" alt="Screenshot 2026-05-15 181634" src="https://github.com/user-attachments/assets/05424c50-0d7d-416a-9d0d-91ed86888750" />
<img width="718" height="803" alt="Screenshot 2026-05-15 180820" src="https://github.com/user-attachments/assets/a3f8f46f-a4d4-46b0-8f26-2a310377cd83" />


---

## Future Improvements

- [ ] Add liveness detection to prevent photo spoofing
- [ ] Email/SMS alerts for low attendance
- [ ] Export attendance reports as PDF
- [ ] Admin panel for institution-level management
- [ ] Mobile-optimised UI

---

## Author

**Sudarshan Jha**
[GitHub](https://github.com/sudarshanjha-dev) · [LinkedIn](https://www.linkedin.com/in/sudarshan-jha-67aa281b9/)

---

## License

This project is open source and available under the [MIT License](LICENSE).
