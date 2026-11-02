# WinG Group Website

Static multi-page website for **WinG Group**, a Germany-based company for global staffing and recruitment (Engineering, IT, Healthcare, Ausbildung) and IT consulting and solutions.

Plain HTML, CSS and a few lines of JavaScript. No build step and no framework. Served by nginx in Docker.

## Quick start

### With Docker

```bash
docker compose up -d --build
```

Open <http://localhost:8080>.

To stop and remove it:

```bash
docker compose down
```

To change the port, edit `ports` in `docker-compose.yml` (default `8080:80`).

### Without Docker

Open `site/index.html` in a browser, or serve the folder:

```bash
cd site
python3 -m http.server 8080
```

## Project structure

```
.
├── Dockerfile            # nginx:alpine image serving ./site
├── docker-compose.yml    # container "wing-website", port 8080 -> 80
├── nginx.conf            # gzip and static asset caching (7 days)
└── site/
    ├── index.html        # Home
    ├── job.html          # For Candidates: Looking for a Job
    ├── vocational.html   # For Candidates: Looking for a Vocational Training
    ├── recruit-talent.html     # For Employers: Recruit Top Talent
    ├── hire-apprentices.html   # For Employers: Hire Apprentices & Trainees
    ├── it-solutions.html # IT Solutions & Services
    ├── partnerships.html # Partnerships
    ├── who-we-are.html   # Our Company: Who we are
    ├── contact.html      # Contact us (also used for "Submit your CV")
    ├── *.html            # "Read more" pages with the full text of each section
    ├── style.css
    ├── site.js           # mobile menu and contact form
    ├── logo.png
    └── img/              # optimized photos
```

## Site map

| Menu | Page |
|---|---|
| Home | `index.html` |
| For Candidates | `job.html`, `vocational.html`, Submit your CV (`contact.html?topic=cv`) |
| For Employers | `recruit-talent.html`, `hire-apprentices.html` |
| IT Solutions & Services | `it-solutions.html` |
| Partnerships | `partnerships.html` |
| Our Company | `who-we-are.html` |
| Contact us | `contact.html` |

Each main page shows a short text per section with a **Read more** link to a separate page with the full content.

## Notes

- **Contact form:** the form has no backend. On submit it opens the visitor's email app with a prepared message to `Contact@winggroup.de`. For CV submissions the visitor attaches the file in the email. To receive messages directly, connect the form to a form service or your own backend.
- **Fonts:** Outfit and Source Sans 3 are loaded from Google Fonts. The site falls back to system fonts if they are blocked. For GDPR-strict setups, self-host the fonts and remove the Google Fonts links from the HTML files.
- **HTTPS and domain:** the container only serves HTTP. Put it behind a reverse proxy (Traefik, Caddy, Nginx Proxy Manager) for a domain and TLS.
- **Updating content:** edit the HTML files in `site/` directly, then rebuild with `docker compose up -d --build`. Images and CSS are cached for 7 days, so force-refresh the browser (Ctrl+F5) after a change.

## Contact

WinG Group · Dresden, Germany
Email: Contact@winggroup.de · Phone: +49 1515 88 60008
