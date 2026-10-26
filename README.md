# PawPal — Pet Grooming Voice Assistant

PawPal is a voice-enabled prototype for booking, rescheduling, or cancelling a pet-grooming appointment. Its conversation brain is deterministic Python code; it does not use an LLM to decide what the caller wants or what to do next. The React page displays both the conversation and the backend's decision state. Availability and customer data are fake and held in memory.

The available slots are a fixed demo schedule, not a live calendar. Booking a slot does not reserve it or remove it for another session. Conversation and booking state are held in the backend process's memory only; there is no database, and restarting the backend clears the in-memory state.

## Run locally

Requirements: Python 3.10+ and Node.js 20+.

### Backend

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload
```

The API runs at `http://127.0.0.1:8000`; its health check is `http://127.0.0.1:8000/api/health`.

### Frontend

In a second terminal, from the repository root:

```powershell
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite (usually `http://localhost:5173`). The frontend proxies `/api` calls to the backend.

## Tests and build

```powershell
cd backend
python -m pytest
```

In a separate terminal:

```powershell
cd frontend
npm run build
```

## Try the demo

The opening message now shows what details to provide and an example. Type or click **Speak** and say a message such as `Full grooming appointment` or `Book a bath for Luna Saturday at 10 AM`. A broader request such as `Spa for my pet Tyler` starts a booking, remembers Tyler's name, and asks which supported grooming service you mean rather than guessing. Recognized speech is sent automatically; the browser asks for microphone permission if needed. PawPal asks for any missing details and, with **Replies on**, speaks its responses. Complete the owner name with `My name is Maya`. PawPal reads the details back and waits for `Yes` before booking; repeated confirmations like `Yes, yes` are accepted too. Say `Actually, make it Saturday at 2 PM` to correct the details and hear a new confirmation, or say `No` to abandon the draft without booking. `Saturday at 10 AM` is a sample available slot; `Monday at 10 AM` demonstrates unavailable-slot handling. After booking, try `Please reschedule to Tuesday at 2 PM`; the change also requires confirmation. To correct an existing booking, say `My pet's name is Paul`, then confirm with `Yes`; `No` keeps the previous details. `Cancel my appointment` requires a separate yes/no confirmation, while `No thanks, bye` closes politely without cancelling the booking.

Browser speech recognition support varies. Use a current browser that supports the Web Speech API and run on `localhost` or HTTPS. Typed chat remains available if speech input is unsupported or microphone permission is denied.

## Project notes

- [DESIGN.md](./DESIGN.md) describes the use case and deterministic conversation flow.
- [AI_USAGE.md](./AI_USAGE.md) documents AI assistance and the limits on available token records.
- No secrets, real customer details, external AI services, or real booking integrations are used.

## Fork and submit the assessment

**Repository:** https://github.com/savvpro/savvpro-test-voice-agent

---

### Step 1: Fork the Repository

1. Go to the repository: https://github.com/savvpro/savvpro-test-voice-agent
2. Click the **Fork** button in the top-right corner.
3. This will create a copy of the repository in your GitHub account.

---

### Step 2: Clone Your Fork

1. Open your forked repository in your GitHub account.
2. Click the green **Code** button and copy the URL.
3. Run the following commands:

```bash
git clone https://github.com/your-username/savvpro-test-voice-agent.git
cd savvpro-test-voice-agent
```

---

### Step 3: Read the Task

Open and read **TASK.md** carefully before writing any code.

- TASK.md URL: https://github.com/savvpro/savvpro-test-voice-agent/blob/main/TASK.md

---

### Step 4: Create a New Branch

Branch pattern: `candidate-<your-github-username>`

```bash
git checkout -b candidate-<your-github-username>
```

**Example:**
```bash
git checkout -b candidate-johndoe
```

---

### Step 5: Complete the Task

Build the full application on your branch.

---

### Step 6: Push Your Branch

```bash
git add .
git commit -m "feat: complete voice-agent assessment"
git push origin candidate-<your-github-username>
```

---

### Step 7: Create a Pull Request

1. Go to your **forked** repository on GitHub (`https://github.com/your-username/savvpro-test-voice-agent`).
2. Click **Compare & pull request** (GitHub will show this banner after you push your branch).
3. Ensure the following settings in the PR form:
   - **Base repository:** `savvpro/savvpro-test-voice-agent` ← the original repo
   - **Base branch:** `main`
   - **Head repository:** `your-username/savvpro-test-voice-agent` ← your fork
   - **Compare branch:** `candidate-<your-github-username>`
4. Use the title: `feat: complete voice-agent assessment`
5. Submit the pull request.

> 💡 **Tip:** If you don't see the banner, go to the original repo (`savvpro/savvpro-test-voice-agent`), click the **Pull requests** tab, then click **New pull request** → **compare across forks**.

---

> ⚠️ **Important:** No submissions will be accepted after the deadline.
