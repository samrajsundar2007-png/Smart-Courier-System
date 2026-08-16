# 📦 Smart Courier System

A single-page, browser-based courier booking & tracking counter — book parcels, generate tracking IDs and receipts, track shipments by ID, and manage a live manifest of all shipments. Built entirely in vanilla HTML, CSS, and JavaScript with a warm "postal counter" visual theme (kraft paper, parcel tags, postmark stamp).

---

## ✨ Features

### 📮 Book Parcel
- Capture sender & receiver details (name, mobile, address)
- Product name + parcel description
- Courier type toggle — **Normal** or **Express**, each with its own pricing
- Live delivery charge calculation based on weight and courier type
- Payment method selection — Cash, UPI, Net Banking, or Pay on Delivery (auto-sets payment status: paid up front vs. pending)
- On booking: generates a unique tracking ID (`COUR-1001`, `COUR-1002`, …), a 4-digit secure OTP, and a parcel-tag-style receipt with a barcode graphic

### 🔍 Track Parcel
- Look up any parcel by tracking ID
- Visual stepper showing shipment progress: **Booked → In-Transit → Out for Delivery → Delivered**
- Full shipment details: sender/receiver, address, status badge, payment badge, amount

### 🗂️ Manifest
- Table view of all booked shipments
- Filter by status (All / Booked / In-Transit / Out for Delivery / Delivered)
- Live count of shipments matching the current filter
- Per-shipment **Update** action opens a modal to change status and mark payment as paid (auto-marks Pay-on-Delivery parcels as paid when marked Delivered)

### 📊 Header Stats
- Live counts: total parcels, payments pending, parcels delivered

---

## 💰 Pricing Logic

| Courier type | Base charge | Per-kg rate |
|---|---|---|
| Normal | ₹50 | ₹20/kg |
| Express | ₹150 | ₹50/kg |

Charge = `base + (weight × per-kg rate)`, rounded down to the nearest rupee.

---

## 📋 Prerequisites

None — no build tools, no dependencies, no backend. Just a modern web browser.

---

## 🚀 Running it

Since it's a single static HTML file, you can either:

**Option 1 — Open directly**
Just double-click `smart-courier-system.html` (or open it via `File → Open` in your browser).

**Option 2 — Serve locally** (recommended for consistent font loading)
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000`.

---

## 🗂️ Project Structure

```
.
├── smart-courier-system.html   # Entire app — HTML, CSS, and JS in one file
└── README.md                   # This file
```

---

## ⚠️ Important — Read Before Relying On This

This is a **frontend-only demo/prototype**. A few things to know:

- **No persistence.** All shipment data lives in a JavaScript object (`couriers`) in memory. The footer even says it: *"SESSION DATA · RESETS ON PAGE RELOAD."* Refreshing the page wipes everything.
- **No backend / database.** There's no server-side storage, so this isn't suitable for real courier operations as-is — it's a UI/UX prototype or a starting point for a full-stack build.
- **No real payment processing.** Payment method selection just sets a display label and status (`PAID` / `PENDING`) — no actual payment gateway is integrated.
- **No authentication.** Anyone with the page open can book, track, and update any shipment.
- **Tracking IDs are sequential and predictable** (`COUR-1001`, `COUR-1002`, ...) rather than random/secure — fine for a demo, but you'd want unguessable IDs (and probably to keep the OTP server-side) for a real system.

---

## 🛣️ Ideas for Improvement

- [ ] Add a backend (Node/Express, Django, or FastAPI) + database (PostgreSQL/MongoDB) for real persistence
- [ ] Add user authentication for counter staff, with role-based access
- [ ] Integrate a real payment gateway (Razorpay, Stripe, etc.) for UPI/net banking/card payments
- [ ] Move OTP generation and validation to the backend rather than generating and displaying it client-side
- [ ] Add SMS/email notifications to sender & receiver at each status change
- [ ] Add search/export (CSV/PDF) for the manifest
- [ ] Add multi-branch/multi-counter support with a shared shipment database

---

## 📄 License

MIT License — free to use, modify, and distribute.
