# Grilli - Restaurant Website (Fixed + MongoDB Backend)

Built and maintained by **Dhruv Jain** (jaindhruv1923@gmail.com).

A fully working restaurant website with a live table reservation system backed by MongoDB.

## Folder Structure

```
grilli-website/
├── frontend/              → the website (HTML, CSS, JS, images)
│   ├── index.html
│   ├── favicon.svg
│   └── assets/
│       ├── css/style.css
│       ├── css/chefs.css         (new - styles for the Our Chefs section)
│       ├── js/script.js          (original template scripts - slider, navbar, etc.)
│       ├── js/reservation.js     (new - sends booking form to the backend)
│       └── images/
├── backend/                → Node.js + Express + MongoDB API
│   ├── server.js
│   ├── package.json
│   ├── .env.example
│   ├── config/db.js
│   ├── models/Reservation.js
│   └── routes/reservations.js
└── README.md
```

## What Was Fixed

1. **"Find A Table"** and **"Book A Table"** buttons had `href="#"` (dead links) — now link to `#reservation`.
2. **"Contact"** nav/footer link had `href="#"` — now links to `#reservation` (where the contact info and form are).
3. The **reservation section had no `id`** at all, so nothing could ever link to it. Added `id="reservation"`.
4. **Home / Menus / About Us** footer links were also dead `href="#"` — pointed to their real sections.
5. Found a real bug: the **guest-count dropdown and the time dropdown both had `name="person"`**, so only one value would ever be captured on submit. Renamed the time dropdown to `name="time"`.
6. **"Our Chefs"** — this was fully missing before (the original template never had this section or any chef photos). Built a brand new **Our Chefs** section from scratch: 4 chef cards in a responsive grid, linked from both the nav bar and footer (`#chefs`). Hover (or focus, for keyboard users) any card to reveal their **years of experience** and **cuisine specialty** as an overlay. Chef photos are free-to-use (no attribution required) images hotlinked from Unsplash — this needs an internet connection to load; swap in your own local images under `frontend/assets/images/` and update the `src` in `index.html` if you want it fully offline.
7. The **booking form now actually works** — it submits to the backend via `fetch`, saves the reservation to MongoDB, and shows a live success/error message on the page (no page reload, no more "goes nowhere").

## How To Run It

### 1. Install MongoDB (pick one)
- **Local**: install MongoDB Community Server and run it (`mongod`), OR
- **Cloud (easier, free)**: create a free cluster at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register), get your connection string.

### 2. Configure the backend
```bash
cd backend
cp .env.example .env
```
Open `.env` and set `MONGODB_URI` to your local or Atlas connection string.

### 3. Install & run
```bash
cd backend
npm install
npm start
```

### 4. Open the site
Go to **http://localhost:5000** in your browser. The backend serves the frontend directly, so everything — including the reservation form — works from this single URL.

> If you just want to preview the design without the backend, you can still open `frontend/index.html` directly in a browser — but the "Book A Table" form won't save anywhere without the backend running.

## API Endpoints

| Method | Endpoint                 | Description                    |
|--------|---------------------------|---------------------------------|
| POST   | `/api/reservations`       | Create a new reservation        |
| GET    | `/api/reservations`       | List all reservations           |
| GET    | `/api/reservations/:id`   | Get a single reservation        |
| PATCH  | `/api/reservations/:id`   | Update status (confirm/cancel)  |
| DELETE | `/api/reservations/:id`   | Delete a reservation            |

## Notes

- The original design/template is based on work by [codewithsadee](https://github.com/codewithsadee/grilli), used under the MIT license (see LICENSE).
- The MongoDB backend, the entire "Our Chefs" section, the reservation form wiring, and all navigation/link fixes were built by **Dhruv Jain** (jaindhruv1923@gmail.com) on top of that base template.
