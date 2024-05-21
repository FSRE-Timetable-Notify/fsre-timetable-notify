# FSRE Timetable Notify

Ovaj projekt je napravljen u svrhu praćenja promjena online rasporeda na FSRE-u.

Trenutne funkcije uključuju:
- Mobile push notifikacije u vezi promjena rasporeda
- Offline podrška (nećete propustiti promjene čak ako niste spojeni na internet dok se promjena detektirala)
- Web UI kao alternativa postojećem pregledu rasporeda
- Promjena jezika (trenutno podržani jezici su Engleski i Hrvatski)
- Selekcija studija za kojeg želimo dobivati obavijesti
- Mogućnost primanja obavijesti za više studija
- Povijest obavijesti
- Pregled obavijesti (je li predmet dodan ili skinut sa rasporeda, kada se promjena detektirala, itd.)
- Navigacija kroz tjedne
- Moguće self-hostanje
- Mogućnost izmjene intervala promjene (trenutno svakih 15 minuta)

## Tehničke informacije

### Backend

Backend server je implementiran u Java Spring Bootu. Koristi MariaDB bazu podataka u produkciji, a H2 bazu prilikom testiranja.
Projekt je Dockeriziran no može se i lokalno pokrenuti.

Neke informacije:
- Pravovremenost je važna značajka ovog projekta, pa se koriste Spring Events, Firebase Cloud Messaging, i cron jobovi
- Definicije o rasporedu sati (nazivi predmeta, profesora, itd.) se dohvaćaju jedanput prilikom paljenja aplikacije
- Raspored je keširan za trenutni i sljedeći tjedan (u trenutku paljenja aplikacije) za sve studije (trenutno 27)
- Potpuna Swagger dokumentacija (requests, responses, exceptions, HTTP status codes, itd.)
- Dokumentiran način rada u README fileu
- Koristi se najnovija Java LTS verzija (21) što uključuje značajke poput records, a i druge moderne značajke poput Optional klase

### Web

Web aplikacija je React SPA implementirana putem Vite bundlera. Za UI se koristi ShadCN i TailwindCSS.
Projekt je kompatibilan sa Bun runtimeom, koji je puno brži od Node.js i omogućava brže build times.

Neke informacije:
- Potpuno responzivan dizajn
- Dark i light teme
- Moderan dizajn i paleta boja
- Napredne mogućnosti: prikaz više predmeta unutar istog vremenskog raspona, navigacija po tjednima i studijima, pregled detaljnih informacija
- Error handling sustav koji ne skriva ništa od korisnika

### Mobile

Mobilna aplikacija je izrađena u Flutter-u i najkompleksniji je dio ovog projekta.
Koristi Flutter BLoC i BLoC arhitekturu, a glavni cilj prilikom izrade je bio snižavanje mogućnosti pogrešaka.
Aplikacija je jednostavna i služi za registriranje subskripcija na FCM kao i za pregled povijesti notifikacija.

Neke informacije:
- Podržana 2 jezika (hrvatski i engleski)
- Light i dark teme
- Mogućnost selekcije i pretraživanja studija na koji se želimo pretplatiti
- Mogućnost slušanja promjena sa više studija
- Navigacija po tjednima
- Upravljanje sa poviješču (osvježavanje povijesti da bi se UI ažurirao, brisanje povijesti za pojedini studij/tjedan, brisanje čitave povijesti)
