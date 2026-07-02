# Debug Session: sitemap-gsc

Status: OPEN

Problem:
- Google Search Console nu accepta sitemap-ul.

Initial hypotheses:
- H1: Exista mismatch intre `www` si non-`www`.
- H2: Certificatul SSL pentru `www` este invalid sau incomplet.
- H3: Proprietatea GSC folosita nu corespunde cu URL-urile din sitemap.
- H4: Serverul raspunde cu redirect-uri sau header-e neacceptate pentru `sitemap.xml`.
- H5: Fisierele locale corectate nu sunt publicate pe hosting.

Evidence log:
- `https://solomoncarassistance.it/` raspunde `200 OK` de la GitHub Pages.
- `https://solomoncarassistance.it/sitemap.xml` raspunde `200 OK` cu `Content-Type: application/xml`.
- Continutul live al sitemap-ului foloseste `https://solomoncarassistance.it/`.
- `https://solomoncarassistance.it/robots.txt` declara corect `Sitemap: https://solomoncarassistance.it/sitemap.xml`.
- `https://www.solomoncarassistance.it/` si `https://www.solomoncarassistance.it/sitemap.xml` esueaza la handshake SSL cu eroare `SEC_E_WRONG_PRINCIPAL`.
- `http://www.solomoncarassistance.it/` face `301` catre `http://solomoncarassistance.it/`.
- Nu exista fisier `CNAME` in proiect, desi site-ul este servit de GitHub Pages.

Current conclusion:
- Root cause probabil: configuratie incompleta pentru custom domain / certificatul TLS pe `www` in GitHub Pages sau DNS `www` incorect.

Next steps:
- Inspectez raspunsurile live pentru homepage, sitemap si robots.
- Verific redirect-urile, content-type si certificatul pentru `www` si non-`www`.
- Verific daca exista fisiere/config de hosting care pot explica problema.
