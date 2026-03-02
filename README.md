# Prezziario Lombardia - WebApp

WebApp Blazor WebAssembly per la ricerca e navigazione delle voci del prezziario delle Opere ed Opere Elettromeccaniche della Regione Lombardia.

## 🚀 Caratteristiche Principali

- **Navigazione TreeView**: Esplora la struttura gerarchica su 11+ livelli
- **Ricerca Avanzata**: Cerca per codice voce, descrizione o dagli ultimi livelli
- **Dettaglio Completo**: Visualizza tutte le informazioni della voce incluse le risorse
- **Performance Ottimizzate**: Caricamento lazy e paginazione per gestire file XML grandi (120+ MB)
- **Architettura Moderna**: Blazor WebAssembly + ASP.NET Core Web API + SQLite

## 📖 Utilizzo

### Home Page
Landing page con introduzione e link alle funzionalità principali.

### TreeView
Navigazione gerarchica interattiva:
- Click su un nodo per espandere il livello successivo
- Caricamento lazy dei dati
- Fino a 11 livelli gerarchici
- Click su una voce finale per visualizzare i dettagli

### Ricerca
Ricerca avanzata con:
- **Ricerca standard**: Per codice voce o descrizione
- **Ricerca dagli ultimi livelli**: Trova voci usando pattern negli ultimi livelli (es: "9721" trova "L9721")
- **Paginazione**: Risultati organizzati in pagine
- Click su una card per visualizzare i dettagli

### Dettaglio Voce
Visualizzazione completa con:
- Informazioni principali (prezzo, unità di misura, ecc.)
- Declaratoria completa
- Tabella risorse con materiali e manodopera
- Percorso gerarchico completo
- Calcolo totali

## 🏗️ Architettura Tecnica

### Backend (Server)
- **Framework**: ASP.NET Core Web API .NET 10
- **Database**: SQLite con Entity Framework Core
- **Parser XML**: Parsing incrementale con `XmlReader` per file grandi
- **API**: RESTful endpoints con Swagger documentation
- **CORS**: Configurato per Blazor WebAssembly

### Frontend (Client)
- **Framework**: Blazor WebAssembly .NET 10
- **UI**: Bootstrap 5 + Bootstrap Icons
- **Componenti**: Riutilizzabili e modulari
- **Routing**: Blazor Router con parametri
- **HTTP**: HttpClient con error handling

### Shared
- **DTOs**: Modelli condivisi tra client e server
- **Serializzazione**: System.Text.Json

## 📊 Performance

- **File XML**: Supporta file fino a 120+ MB
- **Parsing**: Incrementale con batch processing (100 voci per batch)
- **Database**: Indici ottimizzati per ricerche su codici e livelli
- **Lazy Loading**: Caricamento on-demand dei nodi TreeView
- **Paginazione**: Massimo 50-100 risultati per pagina

## 🔌 API Endpoints

### GET /api/prezziario/tree
Ottiene i nodi root del TreeView.

### GET /api/prezziario/tree/{level}/{code}
Ottiene i figli di un nodo specifico.

### POST /api/prezziario/search
Esegue una ricerca con filtri.

**Request Body:**
```json
{
  "searchTerm": "string",
  "searchFromEnd": false,
  "level": null,
  "pageNumber": 1,
  "pageSize": 50
}
```

### GET /api/prezziario/voce/{codiceVoce}
Ottiene i dettagli di una voce specifica.

### GET /api/prezziario/initialize
Inizializza il database dal file XML.

### GET /api/prezziario/status
Verifica se il database è inizializzato.

## 🧪 Testing

Per testare l'applicazione:

```bash
# Build del progetto
dotnet build

# Test delle API (richiede server in esecuzione)
curl https://localhost:7151/api/prezziario/status
curl https://localhost:7151/swagger
```

## 📝 Note Implementative

### Gestione File XML Grandi
Il parser utilizza `XmlReader` per parsing incrementale, salvando i dati in batch per evitare problemi di memoria.

### Primo Avvio
All'avvio l'applicazione crea automaticamente il database SQLite. Il caricamento dei dati XML deve essere fatto manualmente tramite l'endpoint `/initialize`.

### Sicurezza
- HTTPS enabled by default
- CORS configurato per origini specifiche
- Input validation sui parametri API

## 🔮 Possibili Miglioramenti Futuri

- [ ] Cache in-memory lato server per query frequenti
- [ ] Export risultati ricerca (Excel, CSV)
- [ ] Confronto tra voci
- [ ] Storico modifiche prezzi
- [ ] Autenticazione/autorizzazione
- [ ] Dark mode
- [ ] Progressive Web App (PWA)
- [ ] Grafici e statistiche

## 📄 Licenza

Questo progetto è rilasciato sotto licenza MIT.

## 👥 Contributi

Contributi, issues e feature requests sono benvenuti!

## 📧 Contatti
