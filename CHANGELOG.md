# Changelog — Opera Persa

Registro delle versioni del progetto (sito + dati RDF). Copre l'intero progetto; per lo storico delle sole modifiche
allo schema dell'ontologia, vedi anche il commento "STORICO VERSIONI" in `grafo_eco/ontologia_eco.ttl`.

## 2026-10-21 (78) — Supplementi accorpati alla testata: Cacopedia → Alfabeta, supplemento a Media Forum → Media Forum

Backup `20261021-2230` (suffisso `_supplementi`: `Articoli.xlsx` anche in `sorgenti/backup/`, i due CSV di `dati_estratti/tutto/` anche in `tutto/backup/`, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`, `grafo_dati.json`, `istanze_espresso.ttl`, `indici_volumi.csv`, CHANGELOG, Word, `dati_rdf/`). mtime di `Articoli.xlsx` 15:08, nessuna modifica di altre sessioni.
- **Su richiesta**, sul modello dei supplementi de L'Espresso (testata unificata, «(supplemento)» nel numero). Fonte `sorgenti/Articoli.xlsx`, foglio journal_article, 6 righe: i 5 articoli di *Cacopedia - Supplemento di Alfabeta, n. 38/39* (1982: «Come falsificare Eraclito», «Il novissimo Melzi d'Eril», «La mappa dell'impero uno a uno», «L'Anopticon», «Il teorema degli 800 colori») → Rivista «Alfabeta», Numero «38/39 (supplemento)»; l'articolo «Gli aspetti sociologici: la marmellata radiofonica…» (1981) da «supplemento a Media Forum» → Rivista «Media Forum», Numero «75 (supplemento)». ACNP: link invariati (Cacopedia aveva già quello di Alfabeta).
- **Rigenerazione**: `aggiorna_da_articoli.py` (dry run: 12 MODIFICATO, 0 nuovi; poi `--applica`), poi catena completa. Alfabeta passa da 15 a 20 articoli, «Media Forum» è una testata con 1 articolo, la testata «Cacopedia» non esiste più (nodi 2780 → 2779, archi 3183). Nel sito: «Alfabeta, 1982, n. 38/39 (supplemento), p. 7».
- **Layout**: gli ID dei nodi sono cambiati, quindi `posizioni_iniziali.js` ricalcolato nel cloud (57 s; 604 nodi vista «tutti», 189 «ristampe») e copiato sul Mac.
- **Invariato**: in `indici_volumi.csv` (riga di «Il secondo diario minimo») la testata come indicata nell'indice stampato resta «Cacopedia – Supplemento di Alfabeta» (è la fonte dell'indice, non la testata normalizzata).
- **Nota**: il registro `aggiornamento_da_articoli_20261021.csv` ha lo stesso nome di giorno e viene sovrascritto a ogni esecuzione: ora contiene solo queste 12 righe, non più le 1106 modifiche di rubrica della voce (73) (che restano documentate dal CHANGELOG e dai backup).
- **Word**: paragrafo sulle varianti di testata (cap. dati) aggiornato.

## 2026-10-21 (77) — Indici: aggiornamento dal ritocco in `Indice.xlsx` («Opera aperta» 1962)

Backup `20261021-2034` (suffisso `_aggiorna_indici`: `Indice.xlsx` e `Estratti.xlsx` anche in `sorgenti/backup/`, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`, `grafo_dati.json`, `istanze_espresso.ttl`, `indici_volumi.csv`, CHANGELOG, Word, `dati_rdf/`). mtime di `Indice.xlsx` 20:32 (modificato da te dopo l'ultima mia sessione); `Articoli.xlsx` ed `Estratti.xlsx` invariati.
- **Modifica rilevata** (confronto cella per cella con il backup delle 17:12): unica differenza di contenuto, foglio «Opera aperta (1962)», cella A3: «Introduzione alla I edizione» → «Introduzione». Le edizioni 1966 e 1976 conservano il loro titolo.
- **Rigenerazione**: `importa_indici.py` → `genera_rdf.py` → `importa_indici.py` → `genera_rdf.py` → `genera_dati_sito.py`. `indici_volumi.csv`: una sola riga cambiata (Opera aperta 1962, posizione 1); 593 voci in 15 libri; nodi 2780 e archi 3183 invariati, `posizioni_iniziali.js` non ricalcolato.
- **Correzione di un mio errore**: nella voce (74) rinominando i fogli «La bustina di Minerva» in `Indice.xlsx` ed `Estratti.xlsx` openpyxl li aveva chiamati «La bustina di minerva1» (il vecchio nome esisteva ancora, senza distinguere maiuscole). Ora i fogli si chiamano «La bustina di minerva». Nessun effetto sui dati (l'indice del libro è letto dal CSV).

## 2026-10-21 (76) — Tolto dal sito l'avviso «[dato ricostruito da Excel - da verificare]»

Backup `20261021-1727` (suffisso `_senza_avviso_excel`: `genera_dati_sito.py`, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `grafo_dati.json`, CHANGELOG, Word, `dati_rdf/`).
- **Su richiesta**: l'avviso compariva nel tooltip di 36 articoli il cui numero o pagina era stato ricostruito da una data anomala di Excel. Ora non si mostra più.
- **Come**: `genera_dati_sito.py` non aggiunge più la riga al tooltip (dati.js rigenerato, 0 occorrenze). Il dato resta marcato nel grafo (`eco:numeroRicostruitoDaData`, `eco:paginaRicostruitaDaData`) e nel campo `dato_ricostruito` di `dati.js`, per uso interno. Nodi 2780, archi 3183 invariati; `posizioni_iniziali.js` non toccato.
- **Word**: paragrafo «Dati ricostruiti da un'anomalia di Excel» aggiornato (l'avviso non è più sul sito).

## 2026-10-21 (75) — «La struttura assente»: l'anno nella scheda segue l'edizione scelta

Backup `20261021-1720` (suffisso `_anno_edizione`: `index.html`, CHANGELOG, Word).
- **Problema**: scegliendo l'edizione 1980 la scheda mostrava ancora «Anno di pubblicazione: 1968» (anno del nodo unico).
- **Correzione** (`index.html`, `disegnaDettaglioLibro`): per i libri con più indici per edizione l'anno mostrato è quello dell'edizione selezionata (`edizioneIndiceAttiva`); per gli altri libri resta l'anno del libro. Il nodo nel grafo e il suo pannello restano al 1968.
- **Verifica Playwright**: La struttura assente 1968 → «1968», clic su 1980 → «1980»; Diario minimo 1966 → «1966»; nessun errore JS. Dati non toccati.
- **Nota**: editore e città sono gli stessi per le due edizioni (Bompiani, Milano); il link OPAC SBN è unico.

## 2026-10-21 (74) — Libro «La bustina di minerva» (2000): «m» minuscola

Backup `20261021-1712` (suffisso `_libro_minerva`: `Articoli.xlsx`, `Indice.xlsx`, `Estratti.xlsx` anche in `sorgenti/backup/`, `index.html`, CHANGELOG, Word, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`, `importa_indici.py`, `genera_rdf.py`, `ontologia_eco.ttl`, `istanze_espresso.ttl`, `grafo_dati.json`, i CSV di `dati_estratti/`, `dati_rdf/`).
- **Su richiesta**: anche il titolo del libro del 2000 ha la «m» minuscola, come la rubrica (73).
- **Fonti**: `raccolte_eco.csv`, `classificazione_libri.csv`, `ristampe_aggiunte.csv`, `articoli_riviste_tutte.csv` (colonna `ristampa_in_volume_raw`, 142 righe), `importa_indici.py` (tabella `FOGLI` e `CSV_INDICI`), `note_oscurate.md`; `sorgenti/Indice.xlsx` (foglio e cella A1 «La bustina di minerva») e `sorgenti/Estratti.xlsx` (foglio e riga nel foglio «Indice»). Il nome del file `Indice_La_bustina_di_Minerva_ordine_libro.csv` e l'URI `libro-la-bustina-di-minerva` non cambiano.
- **Rigenerazione**: `indici_volumi.csv` (vecchio titolo nella prima colonna) aggiustato con una sostituzione provvisoria per sbloccare `genera_rdf.py`, poi catena completa: 593 voci in 15 libri, nodi 2780, archi 3183 invariati; `posizioni_iniziali.js` non ricalcolato.
- **Invariati (storici)**: i registri `report_estrazione.txt`, `indici_volumi_report.txt`, `correzioni_applicate_agli_excel_20261016.csv`, `aggiornamento_da_articoli_20261021.csv` e le voci precedenti di questo CHANGELOG.
- **Word**: titolo del libro aggiornato nei paragrafi dei capitoli (non nel cap. 20 né nei paragrafi 506/507).

## 2026-10-21 (73) — Rubrica «La bustina di minerva»: «m» minuscola ovunque

Backup `20261021-1707` (suffisso `_rubrica_minerva`: `Articoli.xlsx` anche in `sorgenti/backup/`, `index.html`, CHANGELOG, Word, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`, `genera_rdf.py`, `ontologia_eco.ttl`, `istanze_espresso.ttl`, `grafo_dati.json`, `indici_volumi.csv`, i quattro CSV di `dati_estratti/tutto/`, `dati_rdf/`).
- **Fonte**: `sorgenti/Articoli.xlsx`, colonna «Rubrica» (fogli journal_article e newspaper_article): 1106 celle «La bustina di Minerva» → «La bustina di minerva» (nessuna variante diversa trovata).
- **Rigenerazione**: `aggiorna_da_articoli.py --applica` ha riportato le 1106 modifiche (solo `MODIFICATO`, 0 nuovi) in `articoli_riviste_tutte.csv`, colonna `rubrica`; poi `genera_rdf.py` → `importa_indici.py` → `genera_rdf.py` → `genera_dati_sito.py`. L'etichetta della risorsa `eco:Rubrica` e il campo `rubrica` degli articoli in `dati.js` sono ora in minuscolo; l'URI (`rubrica-la-bustina-di-minerva`) non cambia. Nodi 2780 e archi 3183 invariati; `posizioni_iniziali.js` non ricalcolato (ID e archi uguali).
- **Testi**: esempi di rubrica in `index.html` (Home e timeline 1985), commenti in `ontologia_eco.ttl` (copiati in `dati_rdf/`), `genera_rdf.py`, `estrai_tutto.py`; Word, paragrafo sulla proprietà `eco:rubrica`.
- **Invariato**: il **libro** «La bustina di Minerva» (raccolta, 2000) mantiene la «M» maiuscola, così come le sue ristampe e le colonne `ristampa_in_volume_raw`/`altre_ristampe_raw`.

## 2026-10-21 (72) — «La struttura assente»: edizione 1968 (un solo libro, due indici)

Backup `20261021-1702` (suffisso `_struttura_assente`: `Indice.xlsx` anche in `sorgenti/backup/`, `index.html`, `genesi.html`, `importa_indici.py`, `genera_rdf.py`, `genera_dati_sito.py`, `ontologia_eco.ttl`, `libro_indice.rq`, `raccolte_eco.csv`, `classificazione_libri.csv`, `indici_volumi.csv` e report, `istanze_espresso.ttl`, `grafo_dati.json`, `dati.js`, `query_esempio.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`, `dati_rdf/`, CHANGELOG, Word). Catena rigenerata: `genera_rdf.py` → `importa_indici.py` → `genera_rdf.py` → `genera_dati_sito.py` (errore finale di Playwright atteso).
- **Modello (su richiesta)**: nel grafo il nodo è uno solo, «La struttura assente», anno 1968 (prima edizione), senza distinzione fra edizioni: i rapporti fra gli articoli sono gli stessi. Le due edizioni sono due **indici** dello stesso libro. Id dei nodi, nodi (2780) e archi (3183) identici a prima; `posizioni_iniziali.js` non toccato (stessi id, stesso hash).
- **Fonte**: `sorgenti/Indice.xlsx`, nuovo foglio «La struttura assente (1968)», copia del foglio «La struttura assente» (edizione 1980) senza la riga «Prefazione» (nel 1968 non c'è); intestazione A1 «La struttura assente (1968)». Foglio 1980 non modificato.
- **Dati**: `raccolte_eco.csv` (titolo «La struttura assente», anno 1968, nota aggiornata), `classificazione_libri.csv` (stessa chiave). `importa_indici.py`: tabella `EDIZIONI_FOGLI` (foglio → anno) e nuova colonna `edizione` in `indici_volumi.csv`; le posizioni ripartono da 1 in ogni edizione. `genera_rdf.py`: la voce porta `eco:edizioneIndice` (URI delle voci 1980 invariati). Voci d'indice: 587 → 593 (6 nuove, edizione 1968).
- **Ontologia 1.10**: nuova proprietà `eco:edizioneIndice` (xsd:gYear, dominio `eco:VoceIndice`); `libro_indice.rq` e `genera_dati_sito.py` la portano in `DATI.indici[libro][i].edizione`.
- **Raccolte** (`index.html`): il pulsante dell'edizione 1968 (prima spento) è ora cliccabile e acceso di default quando si apre «La struttura assente»; accanto c'è il 1980. Cambiando edizione cambia l'indice (1968: 6 voci; 1980: 7, con la «Prefazione»). `EDIZIONI_NON_CARICATE` svuotata. Nelle schede dei capitoli presenti in entrambe le edizioni, «Ripubblicato anche in: La struttura assente (Milano: Bompiani, 19xx)» rimanda all'altra edizione, come per Diario minimo.
- **Focus sull'opera** (`genesi.html`): un capitolo presente in più edizioni conta una volta sola.
- Verifica Playwright (`file://`): pulsanti 1968\* / 1980; indici di 6 e 7 voci; collegamento fra le due edizioni nei capitoli «Il segnale e il senso» e «La struttura assente»; nessun collegamento sulla «Prefazione»; Diario minimo invariato; nessun errore JS.
- Word: ontologia 1.10 (cap. 4.3 e tabella delle versioni), 593 voci (cap. 5 e 12.4 e tabella di evoluzione), elenco delle voci d'indice; descrizione dei pulsanti d'edizione in 12.4.

## 2026-10-21 (71) — «Focus sull'opera»: tolta la nota «Capitolo tratto da un contributo pubblicato originariamente in un volume collettivo…»

Backup `20261021-1612` (suffisso `_note_volume`: `genesi.html`, CHANGELOG, Word). Solo `genesi.html` (visualizzazione) e Word; nessun dato toccato.
- `genesi.html`: nelle schede dei capitoli senza articolo la nota «Capitolo tratto da un contributo pubblicato originariamente in un volume collettivo (dati bibliografici riportati sotto), non in un periodico: per questo non è collegato a un fabio:JournalArticle.» (17 capitoli nei dati) non compare più, per nessun libro (`NOTA_VOLUME_COLLETTIVO`). I dati del volume restano nei campi «Tratto da» e «Curatori/autori»; le altre note (inedito, «Non abbiamo informazioni sulla versione originale…», fonte citata nell'indice) restano.
- Verifica Playwright (`file://`): aperte le 37 schede di capitoli senza articolo delle 15 raccolte, nessuna contiene più la nota; nessun errore JS.
- Word: cap. 12.5 aggiornato.

## 2026-10-21 (70) — «Focus sull'opera»: i capitoli senza articolo vengono sempre dall'indice del volume

Backup `20261021-1609` (suffisso `_capitoli_da_indice`: `genesi.html`, CHANGELOG, Word). Solo `genesi.html` (visualizzazione) e Word; nessun dato, Excel o altro file toccato (nodi 2780, archi 3183).
- **Problema**: il focus leggeva i capitoli senza articolo da `capitoli_non_collegati` del libro, una lista che non coincideva con l'indice. In *La bustina di Minerva* le quattro voci «Inedito / N.D.» (Kosovo, Dell'importanza delle lettere maiuscole, L'Opus Dei smentisce che io sia l'Anticristo!, Come scrivere bene) comparivano, in *Apocalittici e integrati* no («La musica e la macchina», «Sulla fantascienza» e altre mancavano).
- **Regola (ora uguale per tutte le raccolte)**: `capitoliSenzaArticolo(ed)` in `genesi.html` prende dall'indice (`DATI.indici`, la fonte della sezione Raccolte) ogni voce senza articolo collegato, introduzioni escluse. Volume d'origine indicato → «noto solo da un volume»; voce inedita → «inedito»; altrimenti → «senza fonte individuata». `capitoli_non_collegati` arricchisce soltanto la scheda (note) ed è il ripiego per i libri senza indice.
- **Effetto per raccolta** (voci senza articolo, prima → ora): *Apocalittici e integrati* 4 → 7 (+ le 2 voci senza fonte, + «La struttura del cattivo gusto», + il titolo del volume, «La musica, la radio e la televisione» al posto di «La radio e la televisione»; «Prefazione» ora «inedito» come nell'indice; «Valori estetici e cultura di massa», che non è nell'indice, non compare più); *Diario minimo (1975)* 0 → 1 («Nota all'edizione 1975», inedito); *La struttura assente (1980)* 3 → 4 («La frontiera semiologica», inedito); *Le poetiche di Joyce* 0 → 1 («Ulysses», inedito); *Opera aperta (1976)* 1 → 2 («Opera aperta: il tempo, la società», inedito); *La bustina di Minerva* 5 → 4 («La peste dello straccio» ha un articolo collegato ed era un doppione). Invariate: Dalla periferia dell'impero 5, Il costume di casa 5, La definizione dell'arte 5, Opera aperta (1966) 1, Pape Satàn Aleppe 2, Diario minimo (1963, 1966), Opera aperta (1962), Sette anni di desiderio (0).
- Verifica Playwright (`file://`): in tutte le 15 raccolte il numero di capitoli senza articolo mostrati coincide con quello dell'indice, nessun errore JS; controllato a vista il focus di *Apocalittici e integrati*.
- Word: cap. 12.5 («Capitoli senza articolo») aggiornato allo stato attuale.

## 2026-10-21 (69) — «Focus sull'opera»: gli estratti non compaiono mai

Backup `20261021-1602` (`backup_genesi_…html`, `backup_CHANGELOG_…md`, `backup_Opera_Persa_Documentazione_Tecnica_…docx`). Solo `genesi.html` (visualizzazione) e Word; nessun dato, Excel o altro file toccato (nodi 2780, archi 3183).
- `genesi.html`: nel diagramma a imbuto entrano solo le ristampe (`isVersionOf`); gli archi `estrattoDi` sono ignorati. Tolti l'imbuto rovesciato dei soli estratti, la freccia tratteggiata rosa, la voce di legenda «articolo estratto dal libro», il testo d'aiuto dedicato e lo stile fucsia delle voci. Stessa regola nel codice non raggiungibile per le edizioni multiple.
- Il focus riguarda solo le raccolte: le edizioni con `tipo_libro` diverso da «raccolta» (7 romanzi, 5 non raccolta) sono scartate e, se si apre l'indirizzo a mano, compare «Nessuna opera trovata per questo indirizzo.». Dalla sezione Raccolte non erano comunque raggiungibili.
- Effetto sui dati mostrati: in Apocalittici e integrati spariscono dal focus i 4 articoli collegati come estratto; nelle altre raccolte nulla cambia.
- Verifica Playwright (`file://`, vis-network 9.1.9 in locale): 15 raccolte senza errori JS e senza la parola «estratto» in pagina; 12 libri non raccolta → messaggio di opera non trovata. `node --check` del blocco script superato.
- Word: cap. 12.5 aggiornato allo stato attuale.

## 2026-10-21 (68) — La pagina principale si chiama ora `index.html`

Backup `20261021-1238` (suffisso `_rinomina_index`: pagina principale, `index.html` precedente, `genesi.html`, `stile.css`, `note_oscurate.md`, `genera_dati_sito.py`, `precalcola_layout.js`, README del precalcolo, CHANGELOG, Word). Nessun dato, Excel o sorgente toccato.
- Rinominato con `git mv` il file della pagina principale in `index.html` (contenuto invariato, salvo 2 righe di riferimenti); il vecchio `index.html`, che era solo un reindirizzamento, è sostituito. La pagina si apre così direttamente all'indirizzo della cartella del sito, senza passaggi intermedi.
- Riferimenti aggiornati: `genesi.html` (14 righe, forma unica `index.html` / `index.html?tab=…` / `index.html?articolo=…`), `stile.css` (1), `note_oscurate.md` (1), `genera_dati_sito.py` (3), `precalcola_layout.js` (4: ora apre `index.html`), README del precalcolo (10), Word (6 paragrafi).
- Il file di reindirizzamento `visualizzazione.html` (poche righe, conservava `?tab=…#…`) è stato creato e poi eliminato, su richiesta, nello stesso giorno: il vecchio indirizzo `…/visualizzazione.html` ora non è più raggiungibile. Copia del vecchio contenuto in `backup/backup_visualizzazione_20261021-1238_rinomina_index.html`.
- `posizioni_iniziali.js` non toccato: ricalcolato in prova, le coordinate risultano identiche (cambia solo la riga d'intestazione, che citerà `index.html` al prossimo precalcolo).
- Verificato con Playwright (copia servita in locale e `file://`): apertura diretta, tutte le schede, `?tab=`, Indietro/refresh, link di `genesi.html`, vecchio indirizzo → nuovo (prova fatta prima di eliminare il reindirizzamento).

## 2026-10-21 (67) — Documentazione: nuova presentazione e frasi tolte

Backup `backup_visualizzazione_20261021-1147.html` (e `backup_CHANGELOG_20261021-1147.md`). Solo testo della scheda «Documentazione» in `visualizzazione.html`.
- «Che cos'è Opera Persa»: la presentazione è sostituita dal testo con le tre domande (riviste e quotidiani, articoli, capitoli dei libri); resta la frase «Si rivolge a…».
- Tolte le frasi sui dati non riscontrati sugli originali e sull'abbinamento dei nuovi articoli, le voci «Ristampe da note libere», «Numeri e pagine ricostruiti» e «Note editoriali complesse», e «, senza modificare i dati» da «Note mostrate e nascoste».

## 2026-10-21 (66) — Word: documentazione ristrutturata (stato attuale, non cronaca)

Backup `backup/backup_Opera_Persa_Documentazione_Tecnica_20261021-1143_prima_riscrittura.docx` (e CHANGELOG, stesso stampo). Solo il Word; nessun dato e nessun file del sito toccato.
- **Archivio**: `archivio_documentazione/Opera_Persa_Registro_modifiche_20261021.docx` conserva per intero il vecchio capitolo 18 (77 voci) e l'elenco degli errori reali trovati dai controlli (già 14.2).
- **Capitolo 18** ora «Evoluzione del progetto in breve»: una tabella di tappe, con rinvio a CHANGELOG.md e all'archivio.
- **Capitolo 12** riscritto al presente, per sezione del sito (Vista a grafo, Articoli, Raccolte, Focus sull'opera, Linea del tempo, Interroga e Documentazione, scelte comuni): da circa 6.700 a circa 3.500 parole, senza date nei titoli. Ogni capitolo 1-12, 14 e 16 si apre con «In questo capitolo»; 14.2 e 16 riscritti come regole; 17.5 e 17.6 aggiornati.
- **Affermazioni superate corrette**: libri 15/5/7 (non 18/6/7) e 27 libri, 31 capitoli non collegati (non 43), 117 riviste con 111 ACNP, 587 voci d'indice in 15 volumi (non 423 in 6), nodi 2780, `Articoli.xlsx`/`Indice.xlsx`/`Estratti.xlsx` al posto di `Dataset completo.xlsx`, sei pseudonimi (non quattro), Wikidata come pilota già eseguito, tabella delle versioni dell'ontologia senza rimandi al capitolo 18, rimando VoID corretto (13.5), cartelle d3-force e `Indice.xlsx` non più «di stato incerto». Il capitolo 20 resta com'è, con introduzione che lo qualifica come testo storico della scheda.
- **Regola stabile (vale per le prossime sessioni)**: il Word descrive solo lo stato attuale, in tempo presente; quando il progetto cambia si riscrive il capitolo interessato, senza aggiungere voci di cronaca né un capitolo 18.n. La cronologia sta solo in CHANGELOG.md.

## 2026-10-21 (65) — Scheda «Documentazione» riscritta in forma sintetica

Backup `20261021-1136` (`visualizzazione.html`, `stile.css`, CHANGELOG, Word). Solo testo e presentazione; nessun dato toccato.
- `visualizzazione.html`: il contenuto della scheda «Documentazione» passa da circa 6.100 parole (24 sezioni) a circa 1.400 parole visibili: Che cos'è Opera Persa, Che cosa contiene, Come usare il sito, Da dove vengono i dati, Come sono organizzati i dati, Limiti noti e sviluppi previsti, Scarica e riusa, due sezioni a comparsa «Approfondimenti tecnici», Come citare e licenza, Glossario. Rimosse storia delle modifiche, nomi di funzioni e affermazioni non più vere (vedi sotto). Conteggi sempre dai dati (`data-conteggio`, nuovi: `n-articoli`, `anno-min`, `anno-max`); il collegamento a «Interroga (SPARQL)» passa dalla scheda senza ricaricare la pagina (`data-vai-tab`).
- `stile.css`: stile di `details.approfondimento` e del glossario nella scheda, tabelle che a capo su schermo stretto, padding ridotto sotto 640 px (nessun colore nuovo).
- Archivio: `archivio_documentazione/documentazione_estesa_20261021.html` (copia autonoma del testo precedente, apribile con doppio clic). Il Word resta il documento completo (capitolo 20 = testo precedente; capitolo 18.77 = questa modifica).
- Affermazioni della vecchia scheda non più vere e non riportate: sei raccolte con indice (ora tutte le 15), Indice_integrazione_20261016.xlsx (non esiste più), 44 capitoli non collegati nel grafo (ora 31), 2248/366 righe di Excel (ora 2247/375 articoli), «14 libri e edizioni» con indice, versioni dell'ontologia 1.6/1.7 (la corrente è 1.9), `report_estrazione.txt` come log dei dati finali (non aggiornato dopo le integrazioni), nascosti Secondo diario minimo, Sugli specchi, Le forme del contenuto.
- Verifica Playwright: nessun errore in console, conteggi compilati, 2 sezioni a comparsa che si aprono e chiudono, link ai 6 file di dati e a Interroga, nessun overflow a 390 px.

## 2026-10-21 (64) — Word: nuovo capitolo 20 con la documentazione del sito

Backup `backup/backup_Opera_Persa_Documentazione_Tecnica_20261021-1126.docx` (e `backup_CHANGELOG_20261021-1126.md`). Solo `Opera_Persa_Documentazione_Tecnica.docx`: aggiunto in coda il capitolo **«20. Documentazione del sito (testo della scheda «Documentazione»)»** (anche nell'indice), che riporta per intero e senza tagli il testo della scheda «Documentazione» di `visualizzazione.html` al 21 ottobre 2026 (8 sezioni, tabelle dei vocabolari, dei file scaricabili e delle varianti di nome, esempio di codice Python; i numeri sono quelli calcolati dal sito in quella data). Serve a conservare nel Word la versione estesa, comprese le guide per ricercatori (Protégé, SPARQL, riuso dei dati) e l'elenco dei file, prima di una eventuale riscrittura più breve della scheda del sito. Nessun altro capitolo modificato; sito, dati e codice non toccati.

## 2026-10-21 (63) — «Volume a parte» in Raccolte, tassello «Opera aperta (1962)» in Le poetiche di Joyce, ordine dei tasti

Backup `20261021-1119` (`visualizzazione.html`, `genesi.html`, CHANGELOG, Word). Solo visualizzazione; nessun dato toccato (nodi 2780, archi 3183).
- `visualizzazione.html`: tabella `VOLUMI_RISTAMPATI_A_PARTE` (libro consultato → volume a parte); nelle schede di Raccolte di Opera aperta (1962) «Le poetiche di Joyce» esce da «Ripubblicato anche in:» e va in «Capitolo ristampato in un volume a parte:». Il campo «Ripubblicato anche in:» sparisce se non restano altri volumi. Altrove (indici di Opera aperta 1966/1976, Articoli, grafo, Linea del tempo) nulla cambia.
- `genesi.html`: tabella `PASSAGGI_VIA_VOLUME` (Le poetiche di Joyce → via Opera aperta (1962)): riga a sé fra articoli e volume, frecce articoli → tassello → volume, pannello con link al focus di Opera aperta (1962), paragrafo in sidebar e voce di legenda solo per questo focus.
- Raccolte: «Ordina per anno» prima di «Ordina per titolo».
- Verifica Playwright: 27 diagrammi, 0 righe miste, nessun errore JS; schede di Opera aperta (1962) controllate.

## 2026-10-21 (62) — Rivista «Comics» (Bordighera): numero 1 per i due articoli del 1965

Backup `backup_Articoli_20261021-0833.xlsx` (in `backup/` e `sorgenti/backup/`), `posizioni_iniziali` `20261021-0834`, CHANGELOG e Word `20261021-0835`.
- `sorgenti/Articoli.xlsx`, foglio `journal_article`: celle `G430` («Il fumetto intellettuale») e `G431` («Il linguaggio e il fumetto») da vuote a `1` (Numero). Nessun'altra cella modificata.
- Eseguiti `aggiorna_da_articoli.py --applica`, la catena RDF/dati e il ricalcolo di `posizioni_iniziali.js`; nodi e archi invariati (2780/3183). Le schede dei due articoli riportano «n. 1».

## 2026-10-21 (61) — «La bustina di Minerva»: l'Introduzione in cima all'indice

Backup `backup_Indice_20261021-0825.xlsx` (in `backup/` e `sorgenti/backup/`), `posizioni_iniziali` `20261021-0827`, CHANGELOG e Word `20261021-0830`.
- `sorgenti/Indice.xlsx`, foglio «La bustina di Minerva»: la riga «Introduzione» (tipologia Introduzione) spostata dalla riga 18 alla riga 3 (prima riga di dati); le righe 3-17 scendono alle 4-18. Nessun'altra cella modificata.
- Rigenerati `indici_volumi.csv` (Introduzione = posizione 1, «Migrazioni» = 2), RDF, `dati.js` (2780 nodi, 3183 archi invariati) e `posizioni_iniziali.js`. Nessuna modifica a `visualizzazione.html`.
- Le introduzioni degli altri volumi non sono state spostate.

## 2026-10-21 (60) — Le due notazioni dei capitoli passano dall'indice al «Focus sull'opera»

Backup stampo `20261021-0811` (`genesi.html`, `visualizzazione.html`, `stile.css`, CHANGELOG, Word). Correzione al punto 2 della voce (58): le notazioni «capitolo noto solo da un volume» e «capitolo senza fonte individuata» andavano nel «Focus sull'opera», non nell'indice di Raccolte.
- `genesi.html`: i capitoli senza articolo hanno due stili in palette terracotta (`COL_IMB.ncVolume` #ec9a76, bordo tratteggiato; `COL_IMB.ncSenza` #a8502d, bordo punteggiato) e due voci di legenda; il testo inedito scritto per la raccolta («Valori senza campioni») resta grigio con la sua voce («capitolo inedito»). Criterio: volume originale noto → «solo da un volume»; altrimenti «senza fonte individuata».
- `visualizzazione.html`: `CAPITOLI_NOTAZIONI.attive = false`: nessun segno né legenda nell'indice di Raccolte (il codice resta, `true` per riattivarlo). Testo di Documentazione aggiornato.
- Verifica Playwright: 27 diagrammi, 0 righe miste, nessun errore JS; indice di Raccolte senza segni.
- **Ritocco (stessa data, backup `20261021-0817_colori`)**: colori resi ben distinti (capitolo da volume: salmone chiaro #f2b8a0, bordo tratteggiato; capitolo senza fonte: rosso-mattone vivo #e0451a, bordo punteggiato); legenda: «Fonte dell'articolo: intervento in volume» (capitolo da volume) e «Fonte dell'articolo: intervento in testata periodica» (articolo ristampato, ex «articolo ristampato nel libro (da rivista a libro)»).
- **Ordine in fondo (backup `20261021-0818_ordine_nc`)**: i capitoli senza articolo chiudono la serie in tre gruppi di righe separati: prima quelli noti solo da un volume, poi l'inedito, per ultimi (proprio alla fine dell'imbuto) quelli senza fonte individuata. Verifica: 27 diagrammi, 0 righe miste; *Dalla periferia dell'impero* 17→18 righe, *Il costume di casa* 20→21.
- **Capitoli da volume in ordine cronologico (backup `20261021-0821_volume_cronologico`)**: i capitoli noti solo da un volume si dispongono nel tempo insieme agli articoli, per anno del volume originale (`anno_volume_originale`); nello stesso anno vengono dopo gli articoli e possono affiancarsi a essi (sempre solo anno uguale sulla stessa riga). Restano in coda soltanto quelli senza anno noto (i tre capitoli de *La struttura assente*), poi l'inedito e, per ultimi, i capitoli senza fonte. Verifica: 27 diagrammi, 0 righe miste, anni crescenti, nessun errore JS.

## 2026-10-21 (59) — «Focus sull'opera»: righe per anno nel diagramma a imbuto

Backup stampo `20261021-0758` (`genesi.html`, CHANGELOG, Word). Solo `genesi.html` (`disegnaGenesiImbuto`).
- **Problema**: le voci erano disposte per posizione (riga = i / colonne), quindi anni diversi finivano sulla stessa riga (es. in *Dalla periferia dell'impero* «Il cogito interruptus», Quindici 1967, accanto a «Verso un nuovo medioevo», L'Espresso Colore 1972) e l'asse degli anni mostrava solo l'anno della prima voce.
- **Regola**: una riga contiene solo voci dello stesso anno; anni in ordine cronologico dall'alto in basso, senza righe vuote per gli anni senza articoli (1967, poi 1972 subito sotto); più voci dello stesso anno si affiancano fino al numero di colonne, poi vanno a capo prima dell'anno seguente (ordine `chiaveData`); i capitoli senza data chiudono la serie in righe proprie, mai miste con voci datate; vale anche per l'imbuto rovesciato dei soli estratti. Le righe con meno voci della griglia sono centrate. `yLibro`, `yFine`, contorno, asse degli anni (anno solo sulla prima riga di ciascun anno), altezza e inquadratura derivano dal nuovo numero di righe.
- **Colonne**: come prima 1 (fino a 10 voci), 2 (fino a 30), 3 (oltre), ma mai più del massimo numero di voci di uno stesso gruppo-anno (o del gruppo dei capitoli senza data), per non avere colonne sempre vuote. Nessun libro ha cambiato numero di colonne.
- **`disegnaGenesi` a più edizioni**: non è raggiungibile dal sito (ogni pulsante «Focus sull'opera» passa sempre `libro`); resta solo per vecchi indirizzi senza `libro` e non è stata modificata.
- **Testo**: «Come leggere questa vista» e aiuto dei soli estratti aggiornati.
- **Verifica Playwright** (coordinate y dei nodi): 27 diagrammi, righe con anni diversi 48 → 0, anni sempre crescenti, nessuna riga vuota fra anni, capitoli senza data mai mescolati (prima 2 casi), nessun errore JS. Altezza dei casi più lunghi: *Il costume di casa* 1334 → 1556 px (17→20 righe), *Dalla periferia dell'impero* 1112 → 1334 (14→17), *Pape Satàn Aleppe* 4442 → 4812, *La bustina di Minerva* 3776 → 4072.

## 2026-10-21 (58) — Note filologiche, notazioni dei capitoli, campi N.D., rubrica, recensioni, spirale

Backup stampo `20261021-0743` (`visualizzazione.html`, `stile.css`, `genesi.html`, CHANGELOG, Word; `sorgenti/backup/backup_Articoli_20261021-0743.xlsx`). Un solo intervento in nove punti.
1. **Note filologiche**: nei box (grafo, Articoli, Raccolte, Linea del tempo) restano solo le note brevi «Ristampato in …/anche in …» (≤100 caratteri), tutto il resto oscurato in sola visualizzazione. Regola in un solo punto: `NOTE_CONFIG` (+ `tipoNota`, `notaVisibile`) in `visualizzazione.html`. Su 60 note nei dati: 5 visibili, 55 oscurate; elenco completo in `note_oscurate.md` (nuovo). Nessun dato toccato.
2. **Raccolte, due notazioni** (terracotta: cerchio chiaro «capitolo noto solo da un volume» = 15 capitoli; quadratino mattone «capitolo senza fonte individuata» = 12) con legenda sotto «Indice»; configurazione `CAPITOLI_NOTAZIONI`. Non marcati i 3 capitoli con rivista nota ma articolo fuori dataset («I modi della moda culturale», «La bistecca e la politica», «Un consuntivo metodologico»): in attesa di decisione.
3. **Capitoli con tutto N.D.** (11): un solo «N.D.» con lo stile di «Inedito».
4. **Rubriche**: corretta la cella H39 del foglio `newspaper_article` di `sorgenti/Articoli.xlsx` («La voce umana», il manifesto, 12/11/1972): «Sceneggiature per la controinformazione» → «Un film alla settimana: sceneggiature per la controinformazione». Catena rigenerata: la rubrica ha 5 articoli (4+1), la vecchia voce non compare più; nodi 2780, archi 3183 invariati.
5. **Linea del tempo**: 1964 ora «Pubblica «Apocalittici e integrati».» (la dicitura «analisi della cultura di massa» non compariva altrove).
6. **Spirale** di apertura dei gruppi per anno gialla (`--articolo-rist`, solo `#network-loading.attesa-gruppo`); il caricamento iniziale resta invariato.
7. **Opera recensita** (253 record, titolo e autore già separati nei dati): titolo in corsivo senza caporali + campo «Autore dell'opera recensita:» (solo presentazione).
8. **Campi N.D.** omessi nei box (148 occorrenze nelle schede dei capitoli: Co-autore 32, Note 28, Pagine 17, Numero 14, Titolo 12, Rivista 11, Tipo 11, Data 11, A cura di 5, Anno 4, Pubblicato in 3); `colonneHTML` ricompone le colonne senza vuoti.
9. **Segnalazioni** (nessuna correzione applicata): vedi riepilogo in chat.
Verifica Playwright: 283 box articolo e 58 schede di capitolo cambiati, tutti per i motivi sopra; nessun errore in console; nodi/archi invariati; `posizioni_iniziali.js` ricalcolato.

## 2026-10-21 (57) — Vista a grafo: gruppi per anno aperti coerenti con ricerca, filtri e selezione

Backup `backup/backup_visualizzazione_20261020-2330.html` (anche CHANGELOG e Word, stesso stampo). Solo `visualizzazione.html`.
- **Causa**: il gestore `doubleClick` aggiungeva nodi/archi con lo stile di base e richiamava solo `riapplicaEvidenziazioneSelezione()`, non `applicaVisibilitaEStile()`. Dopo una ricerca, gli archi nuovi restavano grigi/arancioni (invece di rosa/lilla) e, cercando un libro, comparivano articoli esclusi (6 nel caso «Il costume di casa»); identico in «Solo ristampe».
- **Correzione**: (1) dopo `nodesDS.add/edgesDS.add` e l'aggiornamento di `clusterInfoCorrente`, il doppio clic richiama `applicaVisibilitaEStile()` prima di `riapplicaEvidenziazioneSelezione()`; (2) `applicaVisibilitaEStile()` chiama `spegniEvidenziazioneClick()` all'inizio e `riapplicaEvidenziazioneSelezione()` alla fine; (3) `let evidenziazioneClickAttiva/nodoSelezionatoId` spostate prima di `applicaVisibilitaEStile` (nessun rischio TDZ). Risolto così anche il difetto 2 (stato «stantio» con opacità 0.15), già segnalato nella voce (precedente) come «NON modificato».
- **Verifica Playwright** (stato hidden/colore/borderWidth/opacity dopo l'azione identico a quello dopo `applicaVisibilitaEStile()`): scenari a–g tutti a zero differenze (prima della correzione: a 28/37 e 20/51 archi errati, b 6 articoli esclusi visibili, c 22, d 28/20, f 12 nodi/17 archi, g stato stantio). Chiusura gruppi invariata, nessun errore JS.
- **Tempi**: gestore doppio clic 44 → 99 ms; apertura completa del gruppo 2478 → 2525 ms (+2%).

## 2026-10-20 (56) — «Focus sull'opera»: diagramma a imbuto

Backup stampo `20261020-2144` (`genesi.html`, `stile.css`, CHANGELOG, Word). Solo `genesi.html` (nuova funzione `disegnaGenesiImbuto`, usata quando il diagramma ha una sola edizione, cioè sempre dal sito): articoli e capitoli in alto, in ordine cronologico dall'alto verso il basso, a righe da sinistra a destra su 1 colonna (fino a 10 voci), 2 (fino a 30) o 3 (oltre); contorno a imbuto che converge sul libro in basso, con asse degli anni a sinistra. I capitoli senza data (senza fonte periodica individuata) chiudono la serie, con bordo tratteggiato grigio. Per romanzi e libri non raccolta (solo estratti) l'imbuto è rovesciato: libro in alto, articoli sotto, freccia tratteggiata rosa dal libro agli articoli. Colori coerenti con il sito: libro arancione, ristampa gialla, estratto fucsia, rivista in azzurro corsivo (seconda riga di ogni riquadro, con l'anno); spariscono i nodi-fonte (triangoli e esagoni) e le frecce una per voce. Legenda e testo «Come leggere questa vista» riscritti. Testato con Playwright su Opera aperta (1962), Il costume di casa (3 colonne), Dalla periferia dell'impero, Baudolino e Il nome della rosa.

## 2026-10-20 (55) — «Focus sull'opera»: un diagramma per ogni edizione

Backup stampo `20261020-2132` (`genesi.html`, `visualizzazione.html`, `stile.css`, CHANGELOG, Word). `genesi.html`: se l'indirizzo contiene il parametro `libro` (sempre presente dal bottone «Focus sull'opera» di Raccolte), il diagramma mostra soltanto quell'edizione (per esempio Opera aperta 1962, 1966 e 1976 hanno tre diagrammi distinti, come Diario minimo 1963/1966/1975), senza catena cronologica fra edizioni né nodi condivisi; il sottotitolo riporta l'edizione («Opera aperta (1962) - …») e il testo «Come leggere questa vista» è riscritto. Il vecchio diagramma con più edizioni resta solo come ripiego per indirizzi senza `libro`. Nessun dato rigenerato. Testato con Playwright (Opera aperta, Diario minimo).

## 2026-10-20 (54) — «Tutti gli articoli»: ordinamento solo per anno o titolo

Backup stampo del 20/10/2026 (sera). Solo `visualizzazione.html` (`campiOrdinaDisponibili`, `disegnaOrdinaArticoli`): nella sezione Articoli, modalità «Tutti gli articoli», l'elenco si ordina soltanto per «anno» (predefinito) o «titolo»; tolti «periodico» e «rubrica», che restano dove hanno senso (dentro un periodico o una rubrica). Testato con Playwright.

## 2026-10-20 (53) — Rivista «Paragone. Letteratura»

Backup stampo `20261020-2043`. Il titolo della rivista «Paragone (Forse paragone letteratura?)» (1 articolo, 1999) è uniformato alla notazione ACNP «Paragone. Letteratura»: corretto alla fonte in `Articoli.xlsx` (foglio journal_article, colonna Testata, cella E1768) e, prima, nella colonna `rivista` di `articoli_riviste_tutte.csv` (così `aggiorna_da_articoli.py` non lo tratta come riga nuova); `aggiorna_da_articoli.py --applica` ha rigenerato `riviste_tutte.csv` (link ACNP invariato). Rigenerati RDF e sito (33.535 triple, 2.780 nodi, 3.183 archi, invariati); `posizioni_iniziali.js` ricalcolato. Nessuna altra occorrenza del vecchio titolo (verificato su dati, RDF, sito, Word, CHANGELOG).

## 2026-10-20 (52) — Raccolte ordinate per anno, arco estratto rosa, «Ricerca più approfondita» nascosta, «Ospitata su»

Backup stampo `20261020-1542`. Solo `visualizzazione.html` e `stile.css`, nessun dato rigenerato. (1) Raccolte: ordinamento predefinito «per anno» (`ordinaLibriPer`). (2) Arco «Estratto (da libro a rivista)» (vista a grafo e legenda): da giallo a rosa chiaro `#f0abfc` (`COLORI.arco_estratto`, `--arco-estratto`), tinta più luminosa del fucsia `#d946ef` dei nodi estratto, per restare leggibile sul fondo scuro e coerente con la palette (giallo = ristampa, fucsia/rosa = estratto). (3) Sezione «Ricerca più approfondita» della Vista a grafo nascosta (`display:none`; i filtri restano nel codice con tutto selezionato). (4) Articoli › Rubriche: sotto il titolo di una rubrica la riga «Ospitata su: [rivista]», in una fascia apposita (`#elenco-ospitata`): «Ospitata su:» e, sulla stessa riga, il nome della rivista come semplice link sottolineato (nessuna forma a pulsante) verso la sua scheda; più riviste separate da virgole. Testato con Playwright.

## 2026-10-20 (51) — Introduzioni non cliccabili, note de «La struttura assente», legenda del grafo, box nota tolti

Backup stampo `20261020-1522`. (1) `importa_indici.py`: nota del gruppo «volume» (colonna S di `Indice.xlsx`) usata come nota delle righe «Ristampa di un volume» senza nota propria («Dispense scritti per gli studenti della Facoltà di Architettura dell'Università di Firenze» per i tre capitoli de «La struttura assente (1980)»); le note delle righe riunite in una voce con più articoli si conservano («Modelli e strutture»: «Ristampa parziale»). (2) Stato `introduzione` esteso a «Nota introduttiva», e (elenco `INTRODUZIONI_NON_APRIBILI`) alla «Nota introduttiva» de «La definizione dell'arte» e all'«Introduzione» di «Sette anni di desiderio» (in Excel «Inedito»); nuove «Introduzione» di Il costume di casa, La bustina di Minerva, Pape Satàn Aleppe già riconosciute (tipologia «Introduzione»). (3) `visualizzazione.html`: box `ristampe-libro-nota` («Note / altre edizioni citate nella fonte») sempre nascosto in Raccolte. (4) Tolta alla fonte (`Articoli.xlsx`, JA0069 «Poetica ed estetica in James Joyce», Altre ristampe) la dicitura su Tel Quel; svuotato `titolo_capitolo` «Finnegans Wake» di JA0273 in `ristampe_aggiunte.csv` (non compare più nell'indice di Opera aperta). (5) Legenda Vista a grafo: «Estratto (da libro a rivista)» al posto di «Anticipazione»; «Ristampa (da rivista a libro)»; testo della scheda Documentazione allineato. Rigenerato (triple 33.535, nodi 2.780, archi 3.183); `posizioni_iniziali.js` ricalcolato nel container cloud. Word: capitolo 18.64 (e spostati al posto giusto i capitoli 18.58–18.63, che erano finiti nell'indice iniziale), tabella 1.1 aggiornata.

## 2026-10-20 (50) — Nulla oltre la morte di Eco; La struttura assente 1968/1980; linea del tempo

Backup stampo `20261020-1441`. (1) Tolti gli articoli successivi al 19 febbraio 2016 (14 righe: NA0354-NA0366 e JA2214 «Conclusioni sul complotto…», *Query* 2017) da `Articoli.xlsx` (righe spostate verso l'alto, tabelle ridotte a A3:J378 e A3:L2250), dai quattro CSV (`aggiorna_da_articoli.py --applica`, ID in `RIGHE_RIMOSSE_CONSAPEVOLMENTE`; registro `aggiornamento_da_articoli_20261020.csv`). Nel grafo (filtro `ANNO_MASSIMO` = 2016) uscivano già quelli dal 2017: ora sono fuori anche i due del Corriere della Sera del 21 febbraio 2016. «Pape Satàn Aleppe» (2016) resta. (2) `visualizzazione.html`: tabella `EDIZIONI_NON_CARICATE` = {La struttura assente: 1968}: nell'elenco l'anno è 1968, nella scheda pulsante «1968» spento (`.btn-edizione:disabled`) e «1980» attivo. `importa_indici.py`: «Prefazione»/«Introduzione» senza tipologia e senza dati = stato `introduzione` (non apribili). (3) Linea del tempo (`BIOGRAFIA_ECO`): tolte le frasi su crisi religiosa/RAI (1954), Fenomenologia di Mike Bongiorno (1961), Kazimierz (1966, voce intera), labirinti (1980), cronache/personal computer (1983), Interpretation and Overinterpretation (1992, voce intera), Fiji (1994), Istanbul (2000), social network (2015), ultimi scritti/Sorella Morte/tumore al pancreas (2016). Totali: nodi 2.780, archi 3.183, triple 33.515, quotidiani 375; `posizioni_iniziali.js` ricalcolato (2026-10-20T14:43Z); 15 query ok. Word: 18.63, tabella 1.1.

## 2026-10-20 (49) — «Le forme del contenuto» nascosto; nuovi indici; ritocchi alla sezione Raccolte

Backup stampo `20261020-1425` (anche `dati_rdf/backup/`, `ontologia_eco.ttl`). (1) «Le forme del contenuto» in `LIBRI_NASCOSTI` (`genera_rdf.py`): fuori da grafo e Raccolte; rimane in `Indice.xlsx`, `raccolte_eco.csv`, `classificazione_libri.csv` ed `Estratti.xlsx` (non toccati). (2) `Indice.xlsx` (sola lettura): «La struttura assente» → «La struttura assente (1980)» (`raccolte_eco.csv`: titolo_visualizzato, anno 1980, nota; `classificazione_libri.csv`; `FOGLI_DEFINITIVO`); «Le poetiche di Joyce» aggiunto a `FOGLI_DEFINITIVO`; nuove voci di Opera aperta 1962/1966/1976. `capitoli_non_collegati.csv`: «Lo Zen e l'Occidente» da Opera aperta 1962 a 1966 e 1976, +3 capitoli «Appunti per una semiologia delle comunicazioni visive» (La struttura assente). `ristampe_aggiunte.csv`: JA0406 «Modelli e strutture» → La struttura assente; JA0273 → Le poetiche di Joyce. (3) Nuovo stato `introduzione` (`importa_indici.py`, `genera_rdf.py`, ontologia): tipologia «Introduzione» = voce non apribile; riga con sola voce d'indice e tipologia vuota = `inedito-nd`. (4) `visualizzazione.html`/`stile.css`: tolta la colonna «N.» dell'indice; voci `introduzione` con hover ma senza box (`.voce-non-apribile`, cursore normale); pulsante dell'edizione anche per una sola edizione («1980»); testi della scheda Documentazione. (5) Controllo ristampe: scollegato JA0307 «R. Bayer storico dell'estetica» da «La definizione dell'arte» (`ristampa_in_volume_raw` svuotato in `articoli_riviste_tutte.csv`); negli altri libri con indice i collegamenti coincidono con gli indici. (6) Libri 27 (15 raccolte, 5 non raccolta, 7 romanzi), indici caricati 15 libri/584 voci; nodi 2.782 (-1), archi 3.185 (-1), triple 33.543; `posizioni_iniziali.js` ricalcolato (2026-10-20T14:32Z); 15 query ok. Word: 18.62, tabella 1.1. Da confermare: editore/città dell'edizione 1980 di La struttura assente (assunti uguali al 1968).

## 2026-10-20 (48) — Sospeso il nodo del libro «Postille a Il nome della rosa»

Backup stampo `20261020-1215`. Su richiesta dell'utente il libro «Postille a Il nome della rosa» (Bompiani 1984) non è più un nodo, per ora. La sua riga è passata da `estratti_libri.csv` a `estratti_libri_sospesi.csv` (nuovo file, per ripristinarla); tolta la riga da `classificazione_libri.csv` (che dà errore se contiene titoli senza libro); `Estratti.xlsx` non toccato (contiene ancora la riga). L'articolo «Postille al Nome della rosa» (JA0914) resta collegato solo a «Il nome della rosa (1985)» (ristampa). `visualizzazione.html`: nella scheda Documentazione i due esempi che citavano il libro sono ora «Verso una civiltà della visione?» (più raccolte) e «Il nome della rosa (1985)». Libri 28 (16 raccolte, 5 non raccolta, 7 romanzi); nodi 2.783 (-1), archi 3.186 (-1), triple 33.373 (-12); `posizioni_iniziali.js` ricalcolato (2026-10-20T12:16Z, 610 nodi nella vista «tutti»); 15 query ok. Word: capitolo 18.61, tabella 1.1 e paragrafi sulle categorie dei libri.

## 2026-10-20 (47) — Link ACNP della rivista «Genius»

Backup stampo `20261020-0125`. Su richiesta dell'utente il link ACNP della rivista «Genius : vivere la civiltà elettronica, scoprire la nuova intelligenza» (1 articolo, JA0933) è ora https://acnpsearch.unibo.it/journal/72710 (prima .../971251): corretto in `Articoli.xlsx` (cella e collegamento ipertestuale) e nei CSV intermedi `articoli_riviste_tutte.csv` e `riviste_tutte.csv`. Catena rigenerata: nodi 2.784, archi 3.187, triple 33.385 (invariati); `posizioni_iniziali.js` ricalcolato (2026-10-20T01:26Z); 15 query ok.

## 2026-10-20 (46) — Titolo «Intervento in "cinema e letteratura"» (JA0276) e pagine di JA0005

Backup stampo `20261020-0106`. Su decisione dell'utente: (1) il titolo giusto dell'articolo di *Film Selezione* 13/14 (1962) è «Intervento in "cinema e letteratura"» (prima «Intervento»), corretto in `Articoli.xlsx` e nel CSV intermedio `articoli_riviste_tutte.csv` (allineato prima di rigenerare, per non creare un nuovo ID); (2) le pagine di «Funzioni e limiti di una sociologia dell'arte» (JA0005) sono 317-325 (in `Articoli.xlsx` era «317-25», letto come 25-317): corrette in `Articoli.xlsx` e nel CSV. (3) Su segnalazione dell'utente: l'articolo «[recensione senza titolo]» di *Filosofia*, 30 aprile 1956, pp. 376-381 (JA0009) era già nel dataset (con nota di ristampa: unito a «Necessità e possibilità delle strutture musicali», ristampato come «Note sui limiti dell'estetica») ma non collegato al libro, quindi la riga dell'indice risultava «non abbinata» (errore mio): aggiunto in `ristampe_aggiunte.csv`; ora la voce «Note sui limiti dell'estetica» riunisce JA0009 e JA0159. Resta non abbinata la riga 16 («Necessità e possibilità nelle strutture musicali», di nuovo Filosofia 1956 pp. 376-381, cioè lo stesso JA0009 già usato); JA0008 (stessa data, pp. 376-380) non toccato. Nessun articolo nuovo; nodi 2.784, archi 3.187 (+1), triple 33.385; `posizioni_iniziali.js` ricalcolato (2026-10-20T01:08Z); 15 query ok. Resta una discrepanza solo nel report: la cella delle pagine in `Indice.xlsx` (foglio «La definizione dell'arte», riga 6) dice ancora «317-25»; il file era aperto dall'utente (file di blocco `~$Indice.xlsx`), quindi non l'ho modificato.

## 2026-10-19 (45) — Indice di «La definizione dell'arte» rivisto; Times Literary Supplement come contributo in volume

Backup stampo `20261019-1812` (`sorgenti/backup/`, `grafo_eco/backup/`, `dati_estratti/backup/`, `tutto/backup/`, `dati_rdf/backup/`, `backup/`). L'utente ha modificato solo il foglio «La definizione dell'arte» di `Indice.xlsx` (24 voci). (1) La voce «Un consuntivo metodologico» (articolo «The Analysis of Structure», *The Times Literary Supplement*, 1963, pp. 755-756) è in lingua inglese: nessun nodo rivista/articolo, trattata come contributo in volume (riga in `capitoli_non_collegati.csv`, solo fonte citata). (2) `capitoli_non_collegati.csv`: aggiunti «Il problema dell'opera aperta» (Sansoni, Firenze 1961), «I colori del ferro» (Italsider, Genova 1963) e il Times; aggiornato «La ricerca interdisciplinare»; rimossi «Introduzione» (confluita in «Arte programmata», JA0289: dati del volume ora in `articoli_volume_originale.csv`) e la voce del Dizionario Bompiani, non più nell'indice. (3) `importa_indici.py`: le righe senza titolo d'indice, tipologia e titolo dell'articolo vengono ignorate e segnalate come `[RIGA IGNORATA]` (due residui nel foglio). (4) Corretto il refuso «[ntervento senza titolo]» → «[intervento senza titolo]» (JA0013) in `Articoli.xlsx` e nel CSV intermedio. (5) Nessun articolo nuovo (`aggiorna_da_articoli.py`: 0 nuovi). Rigenerata la catena: nodi 2.784, archi 3.186, triple 33.393 (+35); `posizioni_iniziali.js` ricalcolato (18:14); 15 query su 15 ok. Word: capitolo 18.58, tabella 1.1 (triple). Da confermare con l'utente: JA0307 «R. Bayer storico dell'estetica» collegato al libro ma tolto dall'indice; due righe Filosofia 1956 (pp. 376-381) non abbinate; titolo «Intervento in "cinema e letteratura"» (dataset: «Intervento»); pagine «317-25».

## 2026-10-19 (44) — Titolo «Cultura come spettacolo» (JA2252) deciso dall'utente

Backup stampo `20261019-1631`. Su decisione dell'utente il titolo giusto dell'articolo di *La Società. Quaderni* n. 2 (1980) è «Cultura come spettacolo», in tutte le fonti: corretto in `Articoli.xlsx` (JA2252, era «Cultura come spettacolo?»), in `Indice.xlsx` (foglio *Sette anni di desiderio*, cella C37) e nella nota di `ristampe_aggiunte.csv`. Per conservare l'ID l'abbinamento è stato riallineato nel CSV intermedio prima di rilanciare `aggiorna_da_articoli.py`; registro del 19/10 integrato con la riga di modifica. Catena rigenerata, posizioni ricalcolate (611 «tutti», 192 «ristampe»), 15 query ok. Totali invariati. Word: capitolo 18.57. Chiude la questione in sospeso della voce 43.

## 2026-10-19 (43) — Confronto con `Confronto.xlsx`: due articoli nuovi (Repubblica e La Società)

Backup stampo `20261019-1624` (`sorgenti/backup/`, `tutto/backup/`, `backup/`). Confrontato il file dell'utente (journal 2.249, newspaper 386) con `Articoli.xlsx`: aggiunti «...Ma il moto esiste? Proviamo a camminare» (La Repubblica, 21/3/1978, p. 13 → NA0389) e «Il play-boy, l'autonomo e le macchine dell'oblio» («La Società», n. 24, maggio-giugno 1979, pp. 73-79 → JA2253; rivista nuova, ACNP 57347). Aggiunto il link ACNP (57348) a «La Società. Quaderni» (JA2252). **Non importato**: «Che bell'errore!» (L'Espresso, 3/3/2016), duplicato escluso da `RIGHE_EXCEL_ESCLUSE`. **In sospeso (da chiedere)**: titolo di JA2252, «Cultura come spettacolo?» (indice/dataset) contro «La società come spettacolo?» (Confronto.xlsx). Registro `aggiornamento_da_articoli_20261019.csv` unito (una prova intermedia aveva assegnato per errore JA2253/NA0389 a un articolo poi escluso: ripulita, ID senza buchi). Totali: 2.247 articoli di rivista, 377 di quotidiano (2.624), 117 riviste (111 ACNP), 14 quotidiani, 2.784 nodi, 3.186 archi, 33.358 triple. Posizioni ricalcolate nel cloud (611 «tutti», 192 «ristampe»), 15 query ok. Word: capitolo 18.56, tabella 1.1, paragrafo ACNP (111 su 117; «6 riviste senza collegamento»).

## 2026-10-19 (42) — «Cultura come spettacolo» (Sette anni di desiderio) e nuova rivista «La Società. Quaderni»

Backup stampo `20261019-1618` in `sorgenti/backup/`, `dati_estratti/backup/`, `tutto/backup/`, `backup/` (CHANGELOG, Word, posizioni_iniziali). Unica novità in `Indice.xlsx`: il capitolo «Cultura come spettacolo» (prima N.D.) ha ora la fonte «Cultura come spettacolo?», *La Società. Quaderni: politica cultura economia*, n. 2, aprile-maggio 1980, pp. 27-29. Aggiunto ad `Articoli.xlsx` (`journal_article`, tabella A3:L2250 → JA2252; data testuale «aprile-maggio 1980», senza giorno; rivista senza link ACNP) e collegato in `ristampe_aggiunte.csv`; `capitoli_non_collegati.csv` da 27 a 26 righe. Registro `aggiornamento_da_articoli_20261019.csv` ricomposto (le righe NA0381-NA0388 della voce 41 erano state sovrascritte e sono state rimesse). Totali: 2.246 articoli di rivista, 376 di quotidiano (2.622), 116 riviste (109 ACNP), 14 quotidiani, 2.781 nodi, 3.184 archi, 33.335 triple. Posizioni ricalcolate nel cloud (608 «tutti», 192 «ristampe»), 15 query ok. Word: capitolo 18.55, tabella 1.1 e frase sui collegamenti ACNP (109 delle 116).

## 2026-10-19 (41) — Nuovi dati degli indici: otto articoli di Repubblica in «Sette anni di desiderio»

Backup in `sorgenti/backup/` (Articoli, Indice), `dati_estratti/backup/` (ristampe_aggiunte, capitoli_non_collegati), `tutto/backup/`, `backup/` (CHANGELOG, Word, posizioni_iniziali), stampo `20261019-1555`. Letti i cambiamenti di `Indice.xlsx`: *Sette anni di desiderio* ora 45 voci (nuova «Introduzione», inedito; nuovo capitolo «TV: la trasparenza perduta» = rielaborazione di «Stravideo», JA0916; otto capitoli N.D. collegati a articoli de La Repubblica → NA0381-NA0388); *Dalla periferia dell'impero*: quattro Corriere da «in rivista» a «in quotidiano», «Dopo i poeti» ora contributo in volume. Aggiunti ad `Articoli.xlsx` (`newspaper_article`, tabella A3:J390) gli otto articoli: due con titolo non noto (indice N.D.) registrati come «[titolo non noto]», pagine vuote; «Gli amici della "pravda"» (14/15 maggio 1978) datato 15/5/1978 (ultimo giorno, come L'Unità: da confermare). `ristampe_aggiunte.csv` +9 righe; `capitoli_non_collegati.csv` da 35 a 27 righe. Catena rigenerata. Totali: 2.245 articoli di rivista, 376 di quotidiano (2.621), 115 riviste, 14 quotidiani, 2.779 nodi, 3.182 archi, 33.330 triple. Posizioni ricalcolate nel cloud (606 «tutti», 190 «ristampe»), 15 query ok. Word: capitolo 18.54 e tabella 1.1.

## 2026-10-19 (40) — Raccolte: anno a sinistra dei titoli nell'elenco dei libri

Backup `backup/backup_visualizzazione_20261019-1205.html`, `backup_stile_20261019-1205.css`, CHANGELOG, Word. Nell'elenco libri di «Raccolte» ogni voce ha ora l'anno prima del titolo (colonna fissa, cifre tabulari, tono sommesso); per i libri con più edizioni vale l'anno della prima edizione. `visualizzazione.html`: nuova funzione `riempiVoceLibro()` usata in `disegnaElencoLibri()`; `stile.css`: regole `.libro-voce` (flex), `.libro-anno`, `.libro-titolo`. Entrambe le parti sono marcate `[ANNO-LIBRI]`. **Per annullare**: ripristinare i due backup citati sopra. Nessun dato modificato. Word: capitolo 18.53.

(Nota: il file di prova `visualizzazione_prova_articoli.html` della voce 39 è stato eliminato dall'utente.)

## 2026-10-19 (39) — File di prova: pagina «Articoli» con fascia di ricerca in alto

Backup `backup/backup_CHANGELOG_…`. Creato `visualizzazione_prova_articoli.html` (copia di `visualizzazione.html` con il solo layout di «Articoli» ripensato; stili in un blocco `<style>` interno, `stile.css` e `visualizzazione.html` non toccati): versione snella: una sola riga in alto con selettore a tre voci (Articoli/Rubriche/Periodici) e barra di ricerca, titolo e conteggio tolti dalla fascia, legenda spostata nell'intestazione dell'elenco, ricerca per anno tolta dall'interfaccia (campi nascosti, nessun filtro attivo), sotto l'elenco e la scheda come prima. Solo prova: il sito pubblicato non cambia, nessun dato modificato.

## 2026-10-18 (38) — Linea del tempo: fasce colorate come nella sezione Articoli

Backup `backup/backup_visualizzazione_…`, `backup_stile_…`, CHANGELOG, Word. Nell'elenco articoli della «Linea del tempo» (anno → rivista) le voci ora hanno le stesse fasce della sezione Articoli: giallo = raccolto in volume, fucsia = estratto (riempimento tenue + banda a sinistra, hover più intenso, voce attiva con velo terracotta). `stile.css`: nuove regole `.timeline-articolo-voce.ripubblicato/.estratto` (+ hover/attivo/espansa) che riusano le variabili dell'elenco; rimossa la vecchia banda sottile `--ristampa-segno` delle voci. `visualizzazione.html`: classe `estratto` assegnata alle voci e legenda sopra la lista. Nessun dato modificato: non serve rigenerare né ricalcolare le posizioni. Word: capitolo 18.52.

## 2026-10-18 (37) — Nuovo articolo dall'indice di *Apocalittici e integrati*

Backup `sorgenti/backup/backup_Articoli_…`, `dati_estratti/backup/backup_ristampe_aggiunte_…`, `tutto/backup/`, `backup/` (CHANGELOG, Word, posizioni_iniziali). Nuova voce in `Indice.xlsx`: capitolo «I nichilisti fiammeggianti» (prima N.D.) = Corriere della Sera, 14 aprile 1963, p. 8. Aggiunto l'articolo ad `Articoli.xlsx` (`newspaper_article`, tabella ora A3:J382 → NA0380) e collegato al capitolo in `ristampe_aggiunte.csv`. Catena rigenerata; registro `aggiornamento_da_articoli_20261018.csv` unificato. Totali: 2.245 articoli di rivista, 368 di quotidiano (2.613), 115 riviste, 14 quotidiani, 2.771 nodi, 3.165 archi, 33.296 triple. Posizioni ricalcolate nel cloud (598 «tutti», 183 «ristampe»), 15 query ok. Word: capitolo 18.51 e tabella 1.1.

## 2026-10-18 (36) — Date in conflitto risolte e nuovo articolo del Corriere della Sera

Backup `sorgenti/backup/backup_Articoli_…` e `backup_Indice_…`, `tutto/backup/`, `dati_estratti/backup/backup_ristampe_aggiunte_…`, `backup/backup_CHANGELOG_…`, `backup/backup_Opera_Persa_Documentazione_Tecnica_…`, `backup/backup_posizioni_iniziali_…`. Su indicazione dell'utente: «Il vecchio pessimismo dei nuovi filosofi» resta 27 luglio 1977 (nessuna modifica); «Forse l'Italia è il migliore dei mondi possibili» corretto al 28 maggio 1976 (era 1978) in `Articoli.xlsx` e nell'indice di *Dalla periferia dell'impero* in `Indice.xlsx` (ID NA0372 invariato; nota in `ristampe_aggiunte.csv` allineata); intervento su L'Unità «Informazione e politica» (NA0151) datato 24 febbraio 1995 (ultimo giorno dell'intervallo 22-24); aggiunto «L'atomica e la cultura» (Corriere della Sera, 10 marzo 1963, p. 8 → NA0379; tabella `newspaper_article` ora A3:J381). Catena rigenerata; registro `aggiornamento_da_articoli_20261018.csv` unificato. Totali: 2.245 articoli di rivista, 367 di quotidiano (2.612), 115 riviste, 14 quotidiani, 2.770 nodi, 3.163 archi, 33.289 triple. Posizioni iniziali ricalcolate nel cloud (598 nodi «tutti», 182 «ristampe»), 15 query ok. Word: capitolo 18.50 e tabella 1.1.

## 2026-10-18 (35) — Confronto con `sorgenti/new_newspaper_article.csv`: due articoli del Corriere della Sera aggiunti

Backup `sorgenti/backup/backup_Articoli_…`, `dati_estratti/backup/backup_opera_recensita_…`, `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su richiesta dell'utente, confronto del CSV (377 articoli di quotidiano; codifica Windows-1252) con i dati per testata e data: 372 sono doppioni, 5 no. Aggiunti a `Articoli.xlsx` (foglio `newspaper_article`, tabella ora A3:J380) due articoli nuovi del Corriere della Sera: «I comunisti fra antemarcia e cacciatori di streghe» (15/1/1977, pp. 1-2 → NA0377) e «[recensione senza titolo]» (21/7/1963, p. 7 → NA0378, recensione de «Il robot e il minotauro» di Roberto Vacca, aggiunta a `opera_recensita.csv`). Non toccati, in attesa di decisione dell'utente: «Il vecchio pessimismo dei nuovi filosofi» (CSV 25/7/1977; indice di *Sette anni di desiderio* e dati 27/7/1977) e «Forse l'Italia è il migliore dei mondi possibili» (CSV 28/5/1976; indice di *Dalla periferia dell'impero* e dati 28/5/1978, anno impossibile per un libro del 1977); non incorporato l'intervento su L'Unità «22-23-24-feb-1995» (non Corriere, data non riconducibile a un giorno). Totali: articoli di quotidiano 366 (2.611 articoli in tutto), nodi 2.769, archi 3.162, triple 33.279. `posizioni_iniziali.js` ricalcolato (599 nodi «tutti», 183 «ristampe»); 15 query ok.

## 2026-10-18 (34) — Altri tre articoli del Corriere della Sera in «Dalla periferia dell'impero»

Backup `sorgenti/backup/backup_Articoli_…` e `backup_Indice_…`, `dati_estratti/backup/` (ristampe_aggiunte, capitoli_non_collegati), `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su richiesta dell'utente, che ha aggiornato `Indice.xlsx` (nuova voce «Lettera dal ponto», inserita in testa all'indice di *Dalla periferia dell'impero*, che passa a 42 voci): aggiunti a `Articoli.xlsx` (foglio `newspaper_article`, tabella ora A3:J378) «Lettera dalla periferia dell'impero» (24/4/1976, pp. 1-2 → NA0374, capitolo «Lettera dal ponto»), «Il nudo tranquillo sui giornali e in Tv» (14/1/1976, p. 3, rubrica «quando dire è fare» → NA0375, capitolo «Troubadours for Men only») e «Sentire due campane» (31/1/1976, p. 3, rubrica «quando dire è fare» → NA0376). Collegati con `ristampe_aggiunte.csv`; tolti da `capitoli_non_collegati.csv` i due capitoli già elencati (da 37 a 35). Totali: articoli di quotidiano 364 (2.609 articoli in tutto), nodi 2.767, archi 3.160, triple 33.259. `posizioni_iniziali.js` ricalcolato (599 nodi «tutti», 183 «ristampe»); 15 query ok.

## 2026-10-17 (33) — Altri tre articoli del Corriere della Sera in «Dalla periferia dell'impero»

Backup `sorgenti/backup/backup_Articoli_…` e `backup_Indice_…`, `dati_estratti/backup/` (ristampe_aggiunte, capitoli_non_collegati), `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su richiesta dell'utente, che ha aggiornato di nuovo `Indice.xlsx`: aggiunti a `Articoli.xlsx` (foglio `newspaper_article`, tabella ora A3:J375) «Dialogo in treno sui destini elettorali» (16/6/1976, pp. 1-2 → NA0371, capitolo «Dialogo in treno ovvero la Viaggiatrice Calva»), «Forse l'Italia è il migliore dei mondi possibili» (28/5/1978, pp. 1-2 → NA0372, «Il migliore dei mondi possibili») ed «Eversione e spiazzamento» (23/4/1976, p. 3, rubrica «quando dire è fare» → NA0373). Collegati con `ristampe_aggiunte.csv`; tolti da `capitoli_non_collegati.csv` (da 40 a 37). La modifica alla riga 30 di *Sette anni di desiderio* (voce 32), cancellata dal salvataggio di Excel dell'utente, è stata reinserita. Totali: articoli di quotidiano 361 (2.606 articoli in tutto), nodi 2.764, archi 3.154, triple 33.233. `posizioni_iniziali.js` ricalcolato (599 nodi «tutti», 183 «ristampe»); 15 query ok.

## 2026-10-17 (32) — Data di «Gli orfani del sessantotto» = 1980; «Il silenzio è di piombo» vale un solo capitolo di Sette anni di desiderio

Backup `sorgenti/backup/backup_Articoli_…` e `backup_Indice_…`, `tutto/backup/backup_articoli_riviste_tutte_…`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. (1) Su richiesta dell'utente, la data di «[Intervento senza titolo]» (L'Espresso n. 8, Tic & Tabù; ripubblicato come «Gli orfani del sessantotto») corretta da 1990-02-24 a 1980-02-24 in `Articoli.xlsx`. (2) Confronto fra l'OCR de L'Espresso n. 13 del 2 aprile 1978 (`_testo-ocr-pulito`) e il PDF del libro: «Il silenzio è di piombo» (pp. 13-15) coincide con il solo capitolo «C'è un'informazione oggettiva?»; il capitolo «La falsificazione e il consenso» riprende invece «Questo articolo, forse, è falso» (pp. 65-68, già nel dataset). Corretti `ristampa_in_volume_raw` di JA0763 (ora solo «C'è un'informazione oggettiva?») e JA0765 (ora «La falsificazione e il consenso») in `articoli_riviste_tutte.csv`; riga 30 di `Indice.xlsx` (Sette anni di desiderio) aggiornata a titolo «Questo articolo, forse, è falso» e pagine 65-68. Sette anni di desiderio: 0 voci non abbinate. Archi 3.148, triple 33.229; `posizioni_iniziali.js` ricalcolato (598 nodi «tutti», 182 «ristampe»); 15 query ok.

## 2026-10-17 (31) — Tre articoli del Corriere della Sera aggiunti (indici di «Dalla periferia dell'impero» e «Sette anni di desiderio»)

Backup `sorgenti/backup/backup_Articoli_…`, `dati_estratti/backup/backup_ristampe_aggiunte_…` e `backup_capitoli_non_collegati_…`, `grafo_eco/backup/backup_importa_indici_…`, `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su richiesta dell'utente, che ha aggiornato `Indice.xlsx` individuando tre articoli del Corriere della Sera non presenti in «Articoli»: aggiunti a `Articoli.xlsx` (foglio `newspaper_article`, tabella ora A3:J372) «Al congresso dc: la sintassi del disprezzo» (24/3/1976, pp. 1-2 → NA0368, capitolo «La sintassi del disprezzo»), «Il vecchio pessimismo dei nuovi filosofi» (27/7/1977, p. 3 → NA0369, «I nuovi filosofi») e «La comunicazione «sovversiva» nove anni dopo il Sessantotto» (25/2/1977, p. 3 → NA0370, «Anno nove»). Collegati ai libri con tre righe di `ristampe_aggiunte.csv`; i tre capitoli tolti da `capitoli_non_collegati.csv` (da 43 a 40, altrimenti comparivano due volte). `importa_indici.py`: le celle Data in formato data di Excel sono ora lette come «24 marzo 1976» (prima davano «formato non riconosciuto»). Totali: articoli di quotidiano 358 (2.603 articoli in tutto), nodi 2.761, archi 3.147, triple 33.231. `posizioni_iniziali.js` ricalcolato (598 nodi «tutti», 182 «ristampe»); 15 query ok.

## 2026-10-17 (30) — Raccolte: il titolo dell'articolo originale porta alla sua scheda in «Articoli»

Backup `backup/backup_visualizzazione_…`, CHANGELOG, Word. Su richiesta dell'utente, nelle schede dell'indice di un libro (sezione Raccolte) il titolo dell'articolo originale è ora un collegamento (`campiArticoloHTML`, opzione `slotFissi`; gestore in `attivaEspansioneInlineVoce`) che apre la scheda dell'articolo nella pagina «Articoli» con la funzione `vaiAArticolo`, la stessa del bottone «Vai alla scheda dell'articolo» della Vista a grafo (periodico di appartenenza, articolo evidenziato). Vale anche per i capitoli che riprendono più articoli (un collegamento per ciascun titolo). Nessuna modifica ai dati. Provato con Playwright su *Pape Satàn Aleppe*: il clic porta alla scheda giusta, nessun errore in console. Aggiornata la scheda Documentazione.

## 2026-10-17 (29) — Tolta la rivista «SubStance» e il suo articolo

Backup `sorgenti/backup/backup_Articoli_…`, `grafo_eco/backup/backup_aggiorna_da_articoli_…`, `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su richiesta dell'utente (rivista in lingua inglese, non di interesse) tolti la rivista «SubStance» e il suo unico articolo, «Intervento» (1985): riga rimossa da `Articoli.xlsx` (spostamento manuale delle righe per non rompere i link ipertestuali, tabella ora A3:L2249) e registrata in `RIGHE_RIMOSSE_CONSAPEVOLMENTE`. Totali: articoli di rivista 2.245, quotidiano 355 (2.600 in tutto), riviste 115 (109 con ACNP), nodi 2.758, archi 3.141, triple 33.228. `posizioni_iniziali.js` ricalcolato (598 nodi «tutti», 180 «ristampe»); 15 query ok.

## 2026-10-17 (28) — «Res publica»: tolto il collegamento ACNP errato

Backup `sorgenti/backup/backup_Articoli_…`, `tutto/backup/`, `backup/backup_posizioni_iniziali_…`, CHANGELOG, Word. Su segnalazione dell'utente, la rivista «Res publica» (un solo numero, 1979; articolo «Ultime notizie») aveva il collegamento ACNP di L'Espresso (journal/53484): errato, la rivista non ha scheda ACNP. Tolto in `Articoli.xlsx` (cella e link ipertestuale); le riviste con ACNP passano da 111 a 110 su 116. Rigenerati CSV, RDF e dati del sito; `posizioni_iniziali.js` ricalcolato (600/180 nodi), 15 query ok.

## 2026-10-17 (27) — Rivista «Op. cit.» rinominata col titolo ACNP

Backup `sorgenti/backup/backup_Articoli_…`, `backup_Indice_…`, `backup/backup_visualizzazione_…`, `tutto/backup/`. Su richiesta dell'utente la rivista «Op. cit.» ha ora il titolo ufficiale ACNP «Op. Cit. : selezione della critica d'arte contemporanea», cambiato alla fonte in `Articoli.xlsx` (2 articoli: «Analisi componenziale di un segno architettonico» e «Chi ha paura del cannocchiale?») e in `Indice.xlsx` (Le forme del contenuto), e nella tabella delle normalizzazioni di `visualizzazione.html`. CSV, RDF e dati del sito rigenerati (nodi 2.760, archi 3.142). Le modifiche a «Recensione», «Pensare la guerra» e «Op. cit.» avevano reso obsoleto `posizioni_iniziali.js` (il sito ricadeva sul calcolo dal vivo e il grafo risultava disordinato): ricalcolato in cloud e riportato sul Mac.

## 2026-10-16 (26) — «Pensare la guerra» (La Rivista dei libri, 1991): tolto il numero

Backup `sorgenti/backup/backup_Articoli_…`, `tutto/backup/`, CHANGELOG, Word. Su richiesta dell'utente (dati non sicuri) svuotato in `Articoli.xlsx` il Numero («1/4»); restano mese «ottobre» e pagine 9-11. Dati del sito rigenerati (nodi 2.760, archi 3.142).

## 2026-10-16 (25) — «Recensione» (La Rivista dei libri, 1991): solo l'anno

Backup `sorgenti/backup/backup_Articoli_…`, `tutto/backup/`, CHANGELOG, Word. Su richiesta dell'utente, di questa recensione si sa solo l'anno: in `Articoli.xlsx` sono stati svuotati Numero («1, 7, ottobre 1991») e Data 2 («ottobre»); restano titolo, anno e rivista. CSV e dati del sito rigenerati (nodi 2.760, archi 3.142, triple invariati; layout invariato). «Pensare la guerra» (1991) non è stato toccato.

## 2026-10-16 (24) — Tolto dal sito l'articolo «La musica e la macchina» (1963)

Backup `sorgenti/backup/backup_Articoli_…`, `grafo_eco/dati_estratti/tutto/backup/`, `backup/backup_posizioni_iniziali_…`, `…_CHANGELOG_…`, Word. Su richiesta dell'utente l'articolo «La musica e la macchina» (1963, senza testata) è stato tolto perché non ci sono informazioni su di esso: riga rimossa da `sorgenti/Articoli.xlsx` (spostamento manuale delle righe per non rompere i link ipertestuali), registrata in `RIGHE_RIMOSSE_CONSAPEVOLMENTE` di `aggiorna_da_articoli.py`, CSV e grafo rigenerati con la catena completa. La voce omonima dell'indice di *Apocalittici e integrati* (inedito/N.D., da `Indice.xlsx`) resta, perché è una voce dell'indice del libro e non un articolo. Totali: articoli di rivista 2.246, quotidiano 355 (2.601 in tutto), nodi 2.760, archi 3.142, triple 33.243. `posizioni_iniziali.js` ricalcolato (600 nodi «tutti», 180 «ristampe»); 15 query di esempio ok.

## 2026-10-16 (23) — Nascosti dal grafo e da Raccolte «Il secondo diario minimo» e «Sugli specchi e altri saggi»

Backup `…_20261016-15xx` (`genera_rdf.py`, `visualizzazione.html`, `posizioni_iniziali.js`, `CHANGELOG.md`, Word). Su richiesta dell'utente, finché i dati bibliografici non sono verificati, i due libri non sono più nel grafo né nella sezione Raccolte, ma **non sono stati cancellati da nessuna fonte** (restano in `Indice.xlsx`, `indici_volumi.csv`, `raccolte_eco.csv`, `ristampe_aggiunte.csv`). Meccanismo: elenco `LIBRI_NASCOSTI` in `genera_rdf.py` (filtra le raccolte, le ristampe aggiunte a mano e le voci d'indice; i riferimenti in «Altre ristampe» restano come nota libera dell'articolo). Per rimetterli basta toglierli dall'elenco e rigenerare. Risultato: 2761 nodi e 3142 archi (prima 2763 e 3205), 29 libri (16 raccolte + 6 non raccolta + 7 romanzi), 14 indici in Raccolte (prima 16). `posizioni_iniziali.js` ricalcolato nella sessione con browser: vista «Tutti» 600 nodi, vista «Ristampe» 180. Verifica su pagina vera: 2602 articoli · 116 riviste · 14 quotidiani, 15 query SPARQL ok, console senza errori né avvisi. Aggiornato il testo della scheda Documentazione e il Word (cap. 1.1 e 18.37).

## 2026-10-16 (22) — Pagine di «Industria e repressione sessuale in una società padana» allineate in `Indice.xlsx`

Backup `sorgenti/backup/backup_Indice_…`. Su richiesta dell'utente (i dati dei vari Excel devono restare coerenti) le pagine 54-142 sono diventate 142-154 nelle tre schede di Diario minimo (1963, 1966, 1975) di `Indice.xlsx`, come in `Articoli.xlsx`. Rigenerato: le tre schede non hanno più discrepanze; nodi (2763) e archi (3205) invariati, quindi `posizioni_iniziali.js` resta valido. «Recensione» (La Rivista dei libri, 1991): per ora prevale «ottobre» (data testuale in `Articoli.xlsx` e nel CSV da «aprile» a «ottobre»; il Numero «1, 7, ottobre 1991» resta); la versione definitiva è ancora da decidere. Verifica su pagina vera ripetuta: Home 2602 articoli · 116 riviste · 14 quotidiani, 15 query SPARQL ok, console senza errori né avvisi di disallineamento, scheda Documentazione con il testo nuovo.

## 2026-10-16 (21) — `sorgenti/Articoli.xlsx` diventa la fonte di articoli e riviste (al posto di `Dataset completo.xlsx`)

Backup (tutti `…_20261016-14xx/15xx`): `Articoli.xlsx`, i quattro CSV di `dati_estratti/tutto/`, `estratti_libri.csv`, `ristampe_aggiunte.csv`, `genera_rdf.py`, `estrai_tutto.py`, `visualizzazione.html`, `posizioni_iniziali.js`, `precalcola_layout.js`, `CHANGELOG.md`.

**Come funziona ora.** Nuovo script `grafo_eco/aggiorna_da_articoli.py` (passo 0 della catena: `aggiorna_da_articoli.py` → `genera_rdf.py` → `importa_indici.py` → `genera_rdf.py` → `genera_dati_sito.py`). Legge i fogli `journal_article` e `newspaper_article` di `Articoli.xlsx` e li abbina agli articoli già nei CSV **per titolo, anno, testata e data, non per posizione** (1. chiave esatta; 2. titolo+anno; 3. anno+testata+data; a parità di chiave si sceglie la riga con le stesse pagine). Gli ID esistenti non vengono mai rinumerati; gli articoli nuovi prendono ID nuovi in coda (assert che l'ID non sia usato in nessun altro file); una riga dei CSV senza più corrispondenza nell'Excel viene tolta solo se elencata in `RIGHE_RIMOSSE_CONSAPEVOLMENTE` e se nessun file la cita. Per le righe abbinate vale l'Excel; restano i campi che l'Excel non ha più (`ristampa_in_volume_raw`, `ristampato_in_raw`, congelati: le ristampe vengono da `Indice.xlsx`) e i flag «ricostruito da data» se il valore non è cambiato. Registro delle differenze: `dati_estratti/tutto/aggiornamento_da_articoli_20261016.csv`. `estrai_tutto.py` è marcato STORICO – NON RIESEGUIRE. `Dataset completo.xlsx` spostato in `sorgenti/backup/`. Il foglio `book_chapter` non esiste più in `Articoli.xlsx`: nessuno script lo leggeva (l'estrazione lo escludeva già), cambia solo il testo della scheda Documentazione.

**Correzioni all'Excel decise dall'utente.** «Pensare la guerra» (Numero 1/4, Pagina 9-11) e «Recensione» (Numero «1, 7, ottobre 1991») della Rivista dei libri: tenuti i valori del sito e riscritti in `Articoli.xlsx`. «Lettura del Paradiso» (La Repubblica, 2000): testata «La Repubblica (6.9.2000)» → «La Repubblica». Quattro articoli di Rinascita (1963) avevano i numeri 39, 40, 46, 47 nella colonna Rubrica: spostati in una nuova colonna «Numero» del foglio `newspaper_article` (nel CSV nuova colonna `numero`, in `genera_rdf.py` emessa come `prism:number`, come per le riviste). Le due «[recensione senza titolo]» di Filosofia (1956) restano abbinate in base alle pagine (quella che finisce a 381 è la ristampata).

**Supplementi.** «Intervento in "Hanno scritto di Snoopy"» diventa un normale articolo di Linus (Numero «33 (supplemento)»); il nodo «Ali baba, Supplemento al n. 33 di Linus» è sparito. «Il computer da scrivere…», «Il grande caldo» e «Questo secolo è stato un infarto» nel file avevano tre riviste-supplemento: ora rivista L'Espresso, Numero «45 (supplemento)», «3 (supplemento)», «11 (supplemento)», come «Aiuto! Mi sono perduto tra i fogli».

**Dati nuovi.** 21 articoli: 19 dell'Almanacco del bibliofilo (nuova rivista, con link ACNP), «Valori estetici e cultura di massa» (nuova rivista Quaderni di San Giorgio, 1966), «Una storia della scienza» (Rassegna medica e culturale, 1963), «Totalitarismo "fuzzy" e Ur-Fascismo» e «Omicidio a Chicago» (La Rivista dei libri). Tolto il doppione «Quelle parole ridotte a brandelli» del 3 giugno 2002 (resta quello del 21 giugno). Dati cambiati (vale `Articoli.xlsx`): pagine e numero di «Superman coltiva la nostra pigriza»; pagine di «Industria e repressione sessuale in una società padana» (142-154; `Indice.xlsx` dice ancora 54-142: la differenza compare come discrepanza nelle tre schede di Diario minimo); pagine di «Anno Duemila: ora è il mondo laico a temere l'Apocalisse»; rubrica «Letture e idee» di «Pochi clamori tra la Bormida e il Tanaro»; «Altre ristampe» di «Come si comportano gli eroi della pubblicità televisiva» e «Abbicì o doremì»; titoli senza pseudonimo per «Siamo tutti registi» e «Il mistero Gomulka» (pseudonimi già gestiti da `articoli_titolo_pseudonimo.csv`); data testuale (aprile/ottobre) per le due recensioni del 1991.

**Nuovi collegamenti (certi).** «La peste dello straccio» (Almanacco del bibliofilo n. 10, 2000) ↔ voce omonima di *La bustina di Minerva* (riga in `ristampe_aggiunte.csv`, perché il nuovo articolo non ha colonna di ristampa); «Valori estetici e cultura di massa» ↔ estratto di *Apocalittici e integrati* (riga in `estratti_libri.csv` e voce in `ESTRATTI_VERI` di `genera_rdf.py`). `Estratti.xlsx` e `Indice.xlsx` non toccati.

**Risultato.** Articoli di rivista 2247 (+21 nuovi, −1 sopra il 2016 come prima), quotidiani 355, 116 riviste (+2 nuove, −1 Ali baba), 14 quotidiani, 2763 nodi e 3205 archi nel grafo RDF (prima 2742 e 3183). Indici e Raccolte invariati tranne la voce della Bustina e l'estratto di Apocalittici. `posizioni_iniziali.js` ricalcolato nella sessione con browser: vista «Tutti» 602 nodi, vista «Ristampe» 199 nodi. Verifica su pagina vera (Chromium): console senza errori né avvisi di disallineamento, Home 2602 articoli · 116 riviste · 14 quotidiani, tutte le 15 query di esempio SPARQL eseguite. Corretto anche un difetto latente di `precalcola_layout.js` (il timeout passato a `waitForFunction` era di 30 secondi invece di 15 minuti).

## 2026-10-16 (20) — Tolto il doppione «La presentazione» (JA0673)

Backup `…_20261016-1520`. JA0673 «La presentazione» (L'Espresso, 9 marzo 1975) era un doppione di JA0672 (stessa data e pagina, senza numero); nel nuovo `Articoli.xlsx` c'è una sola riga. Tolto da `articoli_riviste_tutte.csv` (2227 righe) e L'Espresso da 1625 a 1624 articoli in `riviste_tutte.csv`. Nessun altro file lo richiamava. Grafo: 2742 nodi, 3183 archi. `posizioni_iniziali.js` ricalcolato (580 / 197 nodi).

## 2026-10-16 (19) — Titolo «La saggezza delle democrazie»

Backup `…_20261016-1510`. Scelto dall'utente il titolo di `Articoli.xlsx` («La saggezza delle democrazie», Alfabeta, 1983) al posto di «…della democrazia»: corretto in `articoli_riviste_tutte.csv`, in `Dataset completo.xlsx` e nel sito (rigenerato). Nessun nodo o arco cambia (2743 / 3184); le posizioni iniziali del grafo restano valide (nessun avviso di mancata corrispondenza).

## 2026-10-16 (18) — Colonna «Pseudonimo» in Articoli.xlsx; tolto «Intervento» (Alfabeta2, 2011)

Backup `…_20261016-1450` (Articoli.xlsx, articoli_riviste_tutte.csv, riviste_tutte.csv, dati.js, posizioni_iniziali.js, CHANGELOG). (1) `sorgenti/Articoli.xlsx`: nuova colonna «Pseudonimo» (subito dopo «N. Cognome.», in entrambi i fogli), compilata dalle indicazioni di `articoli_titolo_pseudonimo.csv`: Siamo tutti registi (Lia Quilici), Il mistero Gomulka (Telesio Malaspina), Novantanove proverbi strutturalisti (Anonimo Ginevrino), Due inediti di Dedalus (Dedalus), La notizia Findus e La natura? Là in fondo a destra (Dedalus). Titoli ripuliti dalla dicitura «[con lo pseudonimo …]» per i primi due. Verificato: nessun'altra cella alterata. (2) Su richiesta («le info di Articoli sono quelle aggiornate») eliminato dal CSV l'articolo JA2065 «Intervento» (Alfabeta2, 2011-07-04): `articoli_riviste_tutte.csv` 2228 righe, Alfabeta2 da 4 a 3 articoli in `riviste_tutte.csv`. Grafo: 2743 nodi, 3184 archi (−1 articolo, −1 arco). (3) `posizioni_iniziali.js` ricalcolato (580 nodi vista completa, 197 ristampe). `articoli_titolo_pseudonimo.csv` resta in uso dallo script finché l'estrazione non passa da Articoli.xlsx.

## 2026-10-16 (17) — Correzioni dei CSV riportate in `Dataset completo.xlsx` e `Articoli.xlsx`

Backup `sorgenti/backup/backup_Dataset completo_20261016-1430.xlsx`, `backup_Articoli_20261016-1415.xlsx` e `…-1430_prima_correzioni.xlsx`. Elenco cella per cella in `grafo_eco/dati_estratti/tutto/correzioni_applicate_agli_excel_20261016.csv` (627 modifiche). Abbinamento righe Excel-CSV per titolo, anno, testata e data (non per posizione). (1) Corretti i titoli già corretti nei CSV (Il mito di «Superman», Intervento in «Discussione», Il teorema degli 800 colori, classification of signs, Anno Duemila…, Strategia del desiderio). (2) «La musica e la macchina»: rivista, numero e ristampa svuotati. (3) JA0782: rivista «L'Espresso», numero «25 (supplemento)». (4) Numeri doppi con la barra (es. 5/6) e celle di numero e pagina che Excel aveva trasformato in date, riscritte come testo. (5) Varianti di testata unificate (Il manifesto, L'Unità, La Stampa, L'Espresso Colore, Op. cit., Il Contemporaneo - Rinascita). (6) Dataset completo: campi «Ristampa in volume» / «Ristampato in» allineati al CSV (423 celle, compreso «nuovo medioevo»). (7) Articoli: svuotato «Altre ristampe» dell'articolo di Alfabeta2 (richiesta del 2026-10-07). (8) Eliminata la riga JA2213 «Che bell'errore!» (2016) da entrambi i file. (9) Ripristinata in Articoli, foglio quotidiani, la colonna «Titolo dell'opera», scomparsa dopo la pulizia delle colonne. NON applicato: le tre unificazioni automatiche dei supplementi dell'Espresso (JA1054, JA1173, JA1280), le correzioni di titolo con pseudonimo (JA0570, JA0511: l'informazione sullo pseudonimo non ha una colonna) e le differenze in cui l'Excel risulta più recente del CSV (elenco in chat).

## 2026-10-16 (16) — `sorgenti/Articoli.xlsx` ridotto alle colonne usate dal sito

Backup `sorgenti/backup/backup_Articoli_20261016-1415.xlsx`. Nel nuovo `Articoli.xlsx` (fogli `journal_article`, `newspaper_article`) sono state eliminate tutte le colonne non usate dal sito, comprese «Ristampa in volume» (riviste) e «Ristampato in volume» (quotidiani), perché le ristampe effettive sono nell'Excel Indice. Restano: riviste = Titolo, Anno, N. Cognome. (co-autori), Rivista, ACNP, Numero, Data, Data 2, Pagina, Rubrica, Altre ristampe; quotidiani = Titolo, Anno, N. Cognome. (co-autori), Quotidiano, Data, Pagina, Rubrica, Titolo dell'opera (recensione). Verificato cella per cella: nessun valore alterato nelle colonne tenute. Nessuno script lo legge ancora (l'estrazione parte dai CSV): da collegare in un passaggio successivo.

## 2026-10-16 (16) — `sorgenti/Articoli.xlsx` ridotto alle colonne usate dal sito

Backup `sorgenti/backup/backup_Articoli_20261016-1415.xlsx`. Nel nuovo `Articoli.xlsx` (fogli `journal_article`, `newspaper_article`) sono state eliminate tutte le colonne non usate dal sito, comprese «Ristampa in volume» (riviste) e «Ristampato in volume» (quotidiani), perché le ristampe effettive sono nell'Excel Indice. Restano: riviste = Titolo, Anno, N. Cognome. (co-autori), Rivista, ACNP, Numero, Data, Data 2, Pagina, Rubrica, Altre ristampe; quotidiani = Titolo, Anno, N. Cognome. (co-autori), Quotidiano, Data, Pagina, Rubrica, Titolo dell'opera (recensione). Verificato cella per cella: nessun valore alterato nelle colonne tenute. Nessuno script lo legge ancora (l'estrazione parte dai CSV): da collegare in un passaggio successivo.

## 2026-10-16 (15) — Refuso «nuovo medioevo» corretto ovunque; posizioni iniziali del grafo ricalcolate

Backup `…_20261016-1400/1410`. (1) Il titolo «Verso un nuovo medioevo» (ristampa di «Il medioevo è già cominciato») aveva un refuso nel campo ristampa del dataset (`articoli_riviste_tutte.csv`) e nell'Excel Indice: corretto in entrambi e rigenerato tutto. (2) `posizioni_iniziali.js` ricalcolato (vista tutti 581 nodi, vista ristampe 197) nel container con Chromium, dopo il caricamento di «Dalla periferia dell'impero».

## 2026-10-16 (14) — «Dalla periferia dell'impero» caricato dall'Excel Indice

Backup `…_20261016-1330/1345/1350`. (1) Aggiunto il foglio «Dalla periferia dell'impero» a `FOGLI_DEFINITIVO` in `importa_indici.py`: 41 voci (31 ristampe, 10 inedito/N.D.), 30 articoli già collegati al libro e tutti abbinati; nessun articolo nuovo da collegare (le voci N.D. non hanno dati per essere cercate; «Il pubblico fa male alla televisione?» è un contributo in volume, non nel dataset). Le sei differenze sono solo di formato delle pagine (Excel «104-114, 207» / dataset «104-207»): il dataset resta la fonte. Grafo invariato: 2744 nodi, 3185 archi; indici 16. (2) Uniformata la vista all'indice di Costume/Diario minimo: tolto il riquadro «Note / altre edizioni citate nella fonte» dal libro (`raccolte_eco.csv`, colonna `note_ricerca`: conteggi 30/41 ora ricavabili dall'indice); le osservazioni editoriali sono passate nella colonna Note delle righe dell'Excel (e quindi nelle schede dei capitoli): «La sintassi del disprezzo» (fonte «da definire»), «Verso un nuovo medioevo» (refuso del titolo corretto in «nuovo» nel dataset e nell'Excel), «I fratelli del Libero Festival» (attribuzione «probabile»), «Dopo i poeti» (atti di convegno o volume collettivo). (3) Documentazione: 16 libri.

## 2026-10-16 (13) — «Ristampa parziale» per «Verso una civiltà della visione?»; Excel rinominati «Indice» ed «Estratti»

Backup `…_20261016-1255`. (1) L'articolo «Verso una civiltà della visione?» (Pirelli 1961) è stato diviso tra «Diario minimo» (1963, 1966, 1975) e «Apocalittici e integrati»: la dicitura è ora uniforme, «Ristampa parziale» (senza pagine), in `articoli_riviste_tutte.csv` («(ristampa parziale)»), in `ristampe_aggiunte.csv` e nella colonna Note dell'Excel per le 4 voci; uniformata anche «Tre recensioni anomale» (Diario minimo 1975). (2) `sorgenti/Indice_definitivo_Raccolte_20261016.xlsx` → `sorgenti/Indice.xlsx` (aggiornati importa_indici.py e Documentazione); `sorgenti/estratti.xlsx` → `sorgenti/Estratti.xlsx` (nessuno script lo leggeva per nome). Grafo invariato: 2744 nodi, 3185 archi.

## 2026-10-16 (12) — Excel definitivo degli indici come UNICA fonte di `importa_indici.py`

Backup `…_20261016-1105/1120` (Excel definitivo, importa_indici.py, indici_voci_aggiunte.csv, CHANGELOG, visualizzazione.html, Word). (1) `importa_indici.py` legge ora SOLO `sorgenti/Indice_definitivo_Raccolte_20261016.xlsx` (19 colonne per foglio, lettura per posizione) per i 15 libri/edizioni elencati in `FOGLI_DEFINITIVO`; per caricare un altro foglio (es. «Cinque scritti morali») basta aggiungere una riga a quel dizionario. Le vecchie fonti restano disponibili solo con `--vecchie-fonti`. Nuova opzione `--prova` (scrive in file di prova, non tocca `indici_volumi.csv`). (2) Verifica di non perdita: confronto campo per campo tra il CSV precedente e quello rigenerato dall'Excel (620 voci): titolo d'indice, stato, id articolo, coautore, pseudonimo, nota, volume indicato, numero capitolo, pagine volume, verifica dataset: 0 differenze. Grafo invariato: 2744 nodi, 3185 archi, 15 indici, 620 voci. (3) Nel foglio «La bustina di Minerva» la tipologia della voce «La peste dello straccio» era «N.D.» pur avendo una testata: corretta in «Articolo in rivista». (4) `indici_voci_aggiunte.csv` svuotato (la «Nota all'edizione 1975» è ora nell'Excel). (5) Spostati in `sorgenti/_da_eliminare/`: `Indice_integrazione_20261016.xlsx`, `Indice_aggiornato_20261013.xlsx`, `Il_costume_di_casa_indice.csv`, `Indice_La_bustina_di_Minerva_ordine_libro.csv`; in `dati_estratti/_da_eliminare/` i file di prova.

## 2026-10-16 (11) — Indici di altri sette volumi dal secondo Excel; 59 nuove ristampe; Excel definitivo a 20 fogli

Backup `…_20261016-*` (importa_indici.py, indici_volumi.csv e report, ristampe_aggiunte.csv, capitoli_non_collegati.csv, visualizzazione.html, CHANGELOG.md, Word). (1) `importa_indici.py` legge anche `sorgenti/Indice_integrazione_20261016.xlsx` (foglio con colonna «Fonte originale» e gruppo «contributo in volume», letto per nome di colonna: `FOGLI_INTEGRAZIONE`): Il secondo diario minimo (70 voci), Sette anni di desiderio (43), La definizione dell'arte (21), Opera aperta 1962/1966/1976 (7/6/7), La struttura assente (2), Sugli specchi e altri saggi (24). Celle con più articoli separati da «;» -> una voce con più articoli; titolo d'indice N.D. -> titolo dell'articolo; «Verifica incrociata con Dataset UE» non va nel sito: conservata nella nuova colonna `verifica_dataset_ue` di `indici_volumi.csv`; `data_parziale` ora legge anche «27/10/1974» e toglie le parentesi. Diario minimo, Dalla periferia, Apocalittici, Bustina, Costume di casa e Pape non toccati. (2) `ristampe_aggiunte.csv` +59 righe (54 Secondo diario minimo, 5 Sugli specchi; corrispondenza esatta titolo+testata+numero+anno; archi 3126 -> 3185; nodi invariati, posizioni iniziali non rigenerate). (3) JA0317 «La musica e la macchina» scollegata dal libro (già nella voce 10). (4) `sorgenti/Indice_definitivo_Raccolte_20261016.xlsx` rigenerato: 20 fogli (anche Dall'albero al labirinto e Cinque scritti morali, non presenti nel sito; Dalla periferia dall'Excel definitivo dell'utente). (5) Documentazione del sito aggiornata (elenco dei 15 libri con indice; secondo Excel). Word: 18.34 (e spostati 18.32-18.33 nel posto giusto, prima del capitolo 19). Gli script leggono ancora i vecchi file in `sorgenti/`: non eliminarli finché non passano al nuovo.

## 2026-10-16 (10) — «La musica e la macchina» scollegata dal libro; «Dalla periferia dell'impero» nell'Excel dal file definitivo

(1) `articoli_riviste_tutte.csv`: svuotato `ristampa_in_volume_raw` di «La musica e la macchina» (1963): l'articolo non è più collegato a «Apocalittici e integrati» (archi 3127 → 3126); la voce d'indice resta tutta N.D. (autore compreso). L'articolo resta nel dataset come nodo senza rivista, da completare. Dati rigenerati dai CSV. (2) `Indice_definitivo_Raccolte_20261016.xlsx`: il foglio «Dalla periferia dell'impero» riprende per intero le righe del file definitivo fornito dall'utente (il sito non è ancora allineato: sarà aggiornato su richiesta). Posizioni iniziali del grafo non rigenerate.

## 2026-10-16 (9) — Excel definitivo degli indici delle Raccolte

Nuovo file `sorgenti/Indice_definitivo_Raccolte_20261016.xlsx`: un foglio per ciascun libro/edizione della sezione Raccolte (18 fogli), con le stesse 19 colonne e gli stessi colori del modello fornito (Indice, Tipologia, dati dell'articolo originale, dati del contributo in volume). Generato dai dati del sito (`dati.js`: indici dei volumi, articoli collegati, capitoli non collegati); per i libri senza indice completo le righe sono gli articoli collegati più i capitoli non collegati. Nessun dato del sito o del dataset modificato.

## 2026-10-15 (8) — Schede dei capitoli ordinate; divisore fra articoli; tolto l'avviso «data di Excel» (9) Schede dei capitoli (Raccolte): due colonne con lato fisso per ogni campo (sinistra: Titolo, Autore, Rivista/Quotidiano, Numero; destra: Tipo, Co-autore, Data, Pagine; per i contributi in volume sinistra: Pubblicato in, Editore, Anno, Note; destra: A cura di, Luogo, Pagine, Altre ristampe). Se un dato manca si salta e i campi sotto salgono (nessun vuoto); i campi aggiuntivi (Rubrica, Ripubblicato in, Note…) su tutta la larghezza. Verificato su 5 volumi: ogni etichetta sempre nella stessa colonna. (10) «La musica e la macchina»: la voce d'indice non è più abbinata all'articolo del dataset (rimossa la regola «fonte N.D. = articolo senza testata» di `importa_indici.py`): la scheda riporta N.D. per tutti i dati dell'Excel; l'articolo resta nel grafo, collegato al libro. Nella scheda fonte lo pseudonimo «N.D.» non compare più fra parentesi. (11) La rubrica nelle schede degli articoli è cliccabile e porta alla stessa rubrica in Articoli → «Per rubrica» (`vaiARubrica`, `impostaVistaRubrica`, stato di cronologia «rubrica»).

Backup `…_20261015-2339` (visualizzazione.html, stile.css, CHANGELOG.md, Word). (1) Schede dei capitoli (Raccolte): resta la disposizione su due colonne (metà e metà); stesso ordine dei campi in ogni scheda (Titolo, [Tipo, Autore], Co-autore, Rivista, Data, Numero, Pagine); nella scheda fonte «Pagina» -> «Pagine» e Data prima di Numero.
(2) Fra gli articoli di «Appunti sulla televisione» c'è un divisore (`.divisore-articoli`). (3) In quella scheda non compaiono più «Ripubblicato anche in» (Diario minimo) e «Nota ristampa»: dati invariati, solo non mostrati (opzione `senzaRistampe`). (4) Eliminato in tutto il sito l'avviso «un dato (numero o pagina) è stato ricostruito da una data spuria di Excel»;
i dati restano marcati nel grafo (`eco:numeroRicostruitoDaData`, `eco:paginaRicostruitaDaData`) e in `anomalie_da_verificare.csv`; aggiornato il paragrafo della Documentazione. Dati e layout invariati.

## 2026-10-15 (7) — «Appunti sulla televisione» in una sola voce; collegamenti per Corriere/SIPRA/Pirelli; numeri con la barra

Backup `…_20261015-2327`. (1) Un capitolo che riprende più articoli è ora UNA voce d'indice: `importa_indici.py` riunisce le righe consecutive dell'Excel con lo stesso titolo in indice (`id_articolo` = «ID1;ID2;ID3»), `genera_rdf.py` scrive un `eco:articoloCorrispondente` per articolo,
`genera_dati_sito.py` aggiunge `articoli` alla voce (ordine cronologico) e la scheda mostra in fila i dati di ciascun articolo. (2) Nuovi collegamenti in `ristampe_aggiunte.csv` (il dataset non si modifica): «Incontro a Grosseto» e «Televisione: gli effetti e i rimedi» (SIPRA) e «Verso una civiltà della visione?» (Pirelli) -> capitolo «Appunti sulla televisione»;
«Da Pathmos a Salamanca» (Corriere della Sera, 1963); «La canzone di consumo» (Marcatré, 1964; stesso testo del capitolo uscito come prefazione a «Le canzoni della cattiva coscienza»). (3) Numeri di fascicolo doppi sempre con la barra: 36 valori del dataset (`articoli_riviste_tutte.csv`) da «5-6» a «5/6»,
e lettura dell'Excel normalizzata (`numero_con_barra`). Gli altri libri cambiano solo in 8 valori `excel_numero`. (4) `posizioni_iniziali.js` rigenerato. Totali: 2744 nodi, 3127 archi.

## 2026-10-15 (6) — Correzioni alla fonte, indice di «Apocalittici e integrati» riletto, posizioni iniziali, Excel «estratti»

Backup `…_20261015-2111`. (1) NA0002: «Stretegia del desiderio» -> «Strategia del desiderio» (`articoli_quotidiani_tutti.csv`, `ristampe_da_verificare.csv`); la riga dell'indice ora si collega. (2) Rimossa la rivista «La Rassegna (forse La rassegna musicale?)» da `riviste_tutte.csv`
e `articoli_riviste_tutte.csv`: «La musica e la macchina» (JA0317) resta senza rivista, link ACNP e numero (l'Excel dice N.D.). (3) L'Excel dell'indice è cambiato (due gruppi di colonne): `importa_indici.py` lo legge con la stessa funzione di «Il costume di casa»
(`FOGLI_GRUPPI`, `leggi_gruppi_righe`); sostituita la logica dei contributi in volume da `capitoli_non_collegati.csv` introdotta in (5) del giorno; una riga con fonte N.D. si abbina a un articolo del dataset senza testata e di pari titolo. (4) Scollegati da «Apocalittici e integrati» perché assenti
dall'indice: «Superman coltiva la nostra pigriza», «Fumetti e cultura», «Ma Superman a cosa serve?» (campo di ristampa svuotato alla fonte; i nodi restano). (5) `posizioni_iniziali.js` rigenerato (cloud, Chromium). Totali: 2744 nodi, 3122 archi. (6) `sorgenti/estratti.xlsx` arricchito con le
informazioni dell'Excel allegato (provenienza, tipo, evidenza OCR, verifica, file OCR) e 5 righe in più (3 nuovi fogli); non letto da nessuno script. Word: 18.30 e 18.31.

## 2026-10-15 (5) — «Apocalittici e integrati»: indice del volume e collegamento degli estratti

Backup `…_20261015-2300`. (1) Indice: `importa_indici.py` legge ora anche il foglio «Apocalittici e integrati» di `sorgenti/Indice_aggiornato_20261013.xlsx` (14 righe: 10 ristampe collegate ad articoli del dataset, 4 contributi in volume
con i dati di `capitoli_non_collegati.csv`, 1 riga non abbinata); stesso comportamento di Il costume di casa / Pape Satàn Aleppe. «Quaderni di San Giorgio» non esiste ancora come rivista: solo il titolo del contributo
(«Valori estetici e cultura di massa») è nella nota di `raccolte_eco.csv`, senza nodi né archi. (2) Estratti: 3 nuove righe in `estratti_libri.csv` (JA0331, JA0339, JA0462) -> 3 archi `eco:estrattoDi` verso il libro già esistente
(sezione 7 di `genera_rdf.py` riusa il nodo; `ESTRATTI_VERI` esteso). Nodi invariati; archi 3123 -> 3126. `posizioni_iniziali.js` non rigenerato. Documentazione: card aggiornata. `sorgenti/Indice.xlsx` spostato in `sorgenti/_da_eliminare/`.

## 2026-10-15 (4) — Colore dei libri: di nuovo tutti arancioni; legenda «Libro»

Backup `…_20261015-2153` (visualizzazione.html, stile.css, CHANGELOG.md, Word). Su richiesta esplicita annullata la distinzione di colore della voce (3): tutti i 31 libri tornano arancioni
(`COLORI.libro`, `--libro`); rimossi `--libro-altro` e `COLORI.libro_altro` e la scelta per `tipo_libro` in `styleNodo`. Legenda: una sola riga, «Libro» (al posto di «Raccolta di Eco» e «Romanzo o
altro libro»); tolto il paragrafo sui due colori dalla scheda Documentazione. Invariati titoli corretti, statistiche della sidebar (`aggiornaStatisticheGrafo`), dati e layout. Word: 18.29 e frase
corretta in 12.2.

## 2026-10-15 (3) — Titoli di due articoli di «Archivio di filosofia»; colore dei libri non raccolta; statistiche della sidebar sempre aggiornate

Backup `…_20261015-2131` (visualizzazione.html, stile.css, CHANGELOG.md, Word, dati.js, grafo_completo_ttl.js, query_esempio.js, `grafo_eco/grafo_dati.json`,
`grafo_eco/istanze_espresso.ttl`, `grafo_eco/dati_estratti/tutto/articoli_riviste_tutte.csv`, cartella `backup/dati_rdf_20261015-2131`). **Titoli**, corretti alla fonte
(`articoli_riviste_tutte.csv`) e propagati con `genera_rdf` → `importa_indici` → `genera_rdf` → `genera_dati_sito`: JA0274 «Il mito di Superman e la dissoluzione del tempo» →
«Il mito di «Superman» e la dissoluzione del tempo»; JA0275 «Discussione» → «Intervento in "Discussione"» (virgolette dritte, come gli altri «Intervento in "…"», per esempio JA0350 e
JA0400). Nessun'altra occorrenza dei due titoli nei CSV sorgente (i titoli simili in `ristampe_da_verificare.csv` e `note_editoriali_lunghe.csv` riguardano altri articoli, JA0002 e JA0006, e
non sono stati toccati). Nodi e archi invariati (2745; `partOf` 2584, `isVersionOf` 529, `estrattoDi` 10); 31.895 triple. Il precalcolo del layout non è stato rilanciato (nessun nodo né arco
cambia): `posizioni_iniziali.js` non toccato. **Colore dei libri:** i 13 libri che non sono raccolte (7 romanzi, 6 «non raccolta») sono verde oliva `#7d8f1c` (`--libro-altro` in
`stile.css`, `COLORI.libro_altro`), scelto per distanza percettiva (CIELAB ≥ 39) da tutti gli altri colori del grafo, evidenziazioni comprese; le 18 raccolte restano arancioni, come gli archi di
Ristampa. Decisione in `styleNodo`, da `tipo_libro`. Legenda: «Raccolta di Eco» e «Romanzo o altro libro» al posto di «Libro (raccolta di Eco)»; aggiornata la scheda Documentazione;
`genesi.html` invariata. **Statistiche della sidebar:** nuova `aggiornaStatisticheGrafo` (nodi non nascosti; archi non nascosti con entrambi gli estremi visibili, la condizione con cui
vis-network li disegna), chiamata da `applicaVisibilitaEStile`, dall'apertura di un riquadro-anno e da `chiudiGruppiRivista` (prima restava ferma: 583 nodi anche con un gruppo di 6 articoli
aperto, invece di 588). Verifica con Playwright contro il conteggio indipendente di vis-network (iniziale 583/587; un gruppo aperto 588/593; due 637/643; richiusi 632/637 e 583/587; con un
filtro attivo 587/584, 582/578, 583/587): sempre uguale; 18 libri arancioni e 13 oliva contati dai dati; console senza errori. **Non applicato (in attesa di decisione):** nascondere
esplicitamente gli archi del riquadro all'apertura di un gruppo e ripristinarli alla chiusura; a schermo non cambia nulla (vis-network non disegna un arco il cui nodo è nascosto), cambierebbe lo
stato interno usato dalla mappa dei vicini e dall'evidenziazione. Aggiornati Word (12.2, 18.28) e scheda Documentazione.

## 2026-10-15 (2) — Apertura dei gruppi per anno: niente nodi nascosti, spirale più grande che blocca il grafo

Backup `…_20261015-1315` (visualizzazione.html, stile.css, CHANGELOG.md, Word). **Corretta la modifica precedente:** i nuovi articoli non sono più
tenuti `hidden` durante l'attesa (nascondeva anche gli archi): compaiono subito vicino al riquadro con `sparpagliamentoDeterministico`, visibili e
con tutti i loro archi (Ristampa, Estratto, verso i libri), poi parte `animaNodiVerso` invariato; rimossi `membriInAttesaDiPosizione` e
`rivelaMembriGruppo`. **Spirale:** 68 px, tratto 6 px, colore `--accento-testo` su traccia `--bordo`, scritta «Sto disponendo gli articoli… attendi
un momento» (15 px, 600) su fondo semitrasparente, centrata in `#network-area`; velo leggero (`--bg` al 35 %) con i nodi e gli archi sotto ben
visibili. **Blocco dell'interazione:** durante l'attesa l'overlay ha `pointer-events:auto` e `z-index:30` (sopra toolbar e pannello dettagli):
click, doppi click, trascinamenti e zoom sul grafo non passano; fuori dall'attesa (e in dissolvenza di uscita) non intercetta nulla. Non resta mai
bloccato: tolto a fine apertura, in caso di errore nella promise, a cambio vista e, come salvaguardia, dopo 20 s (`LIMITE_SICUREZZA_ATTESA_MS`).
Invariati ritardo di comparsa (150 ms), dissolvenza, `aria-live`, `prefers-reduced-motion` e contatore `apertureGruppoInCorso`. **Archi:** verificato che
nessun arco venga nascosto o reso trasparente all'apertura; trovato e corretto un errore preesistente alla richiusura: se, a gruppo aperto, un
filtro o una ricerca rivalutava il grafo, gli archi del riquadro (box → rivista/libro) restavano `hidden` anche dopo la richiusura (5 archi persi
nel caso provato); ora `chiudiGruppiRivista` li rivaluta con la stessa regola di `applicaVisibilitaEStile`. Aggiornati scheda Documentazione e Word
(12.2, 18.27). Dati non toccati.

## 2026-10-15 — Indicatore di attesa all'apertura di un gruppo per anno; controllo generale del grafo

Backup `…_20261015-1258` (visualizzazione.html, stile.css, CHANGELOG.md, Word). **Apertura di un riquadro-anno:** i nuovi articoli entrano nel
dataset nascosti (`hidden:true`) e compaiono solo quando `ricalcolaMembriApertiRivista` ha restituito le posizioni finali, poi `animaNodiVerso`
li dispone (niente più pallini ammucchiati durante l'attesa; fisica, parametri Barnes-Hut e calcolo delle posizioni invariati). Durante l'attesa
compare, dopo 150 ms, l'overlay esistente `#network-loading` in versione «leggera» (classe `.attesa-gruppo`: trasparente, `pointer-events:none`,
spinner più piccolo, scritta «Sto disponendo gli articoli…» poi ripristinata a «Sto disponendo il grafo…»; `role="status"`, `aria-live="polite"`;
con `prefers-reduced-motion` lo spinner non ruota); sparisce con dissolvenza di 220 ms quando tutte le aperture in corso sono concluse (contatore
dedicato + identificativo di generazione, azzerato da cambio vista/ricostruzione del dataset). Robustezza: errore nella promise → nodi mostrati e
indicatore nascosto; filtri/ricerca durante l'attesa non rivelano i nodi in anticipo (`membriInAttesaDiPosizione`); chiusura o cambio vista durante
l'attesa senza nodi fantasma. `animaNodiVerso` ha un callback facoltativo `alInterruzione`: prima, se un'altra animazione la superava, `alTermine`
non veniva mai chiamata (contatore `apertureGruppoInCorso` bloccato, chiusura di un gruppo lasciata a metà); ora l'apertura porta i nodi alla
posizione finale e la chiusura si completa. **Controllo generale:** nodi 2745 (rivista 116, quotidiano 14, libro 31, articolo 2584) e archi 3123
(`partOf` 2584, `isVersionOf` 529, `estrattoDi` 10) senza archi orfani né duplicati né nodi isolati; stili e colori di nodi/archi coerenti con
legenda e CSS; `posizioni_iniziali.js` valido (583 e 187 nodi, hash corrispondenti, nessun avviso in console); filtri, ricerca, dettagli, tooltip,
trascinamento, «Ripristina disposizione», «Centra» e apertura/chiusura gruppi verificati con Playwright, senza errori. Rimosso codice morto
(`disponiSuCerchio`, `PREFISSO_ID_LIBRI`). Aggiornati scheda Documentazione e Word (12.2, 18.27). Dati non toccati.

## 2026-10-14 (pomeriggio, 6) — Costume di casa: nota ridondante di «La generazione di Nettuno»

Backup `…_20261014-1645`. Svuotata, nella copia `sorgenti/Il_costume_di_casa_indice.csv`, la cella Note di «La generazione di Nettuno» («in N. Balestrini et al.,
Gruppo 63…»), ridondante con i dati del volume; la scheda mostra Note: N.D. Dati rigenerati; nodi e archi invariati (2745, `partOf` 2584,
`isVersionOf` 529, `estrattoDi` 10). Word 18.26.

## 2026-10-14 (pomeriggio, 5) — Costume di casa: nota eliminata, «Altre ristampe»

Backup `…_20261014-1638`. `raccolte_eco.csv`: campo «Note / altre edizioni citate nella fonte» di Il costume di casa svuotato (il riquadro non
compare). Scheda dell'indice di «Ciò che non sappiamo della pubblicità televisiva»: prima il volume («Pubblicato in», ecc.), poi
«Altre ristampe:» con la rivista «Video» cliccabile (`altreRistampeIndiceHTML`). Grafo e conteggi invariati (2745 nodi, `partOf` 2584,
`isVersionOf` 529, `estrattoDi` 10). Aggiornati scheda Documentazione e Word (12.2, 18.25).

## 2026-10-14 (pomeriggio, 4) — Regola per gli inediti; contributo in volume con articolo; titolo di JA0344

Backup `…_20261014-1634`. Regola per tutti i capitoli inediti: la scheda dell'indice riporta solo «Inedito» (`campiVoceIndiceHTML` la
controlla per prima; «Valori senza campioni» non ha più né nota né dati di fonte). «Ciò che non sappiamo della pubblicità televisiva»
(contributo in volume e ristampa in comune con l'articolo JA0545 di «Video»): le proprietà del volume si scrivono anche con
l'articolo e la scheda dell'indice mostra il contributo in volume; il collegamento nel grafo è invariato. Titolo di
«Neocapitalismo e letteratura»: completato nella copia del CSV sorgente («Intervento in “10 domande su «Neocapitalismo e
Letteratura»”», come nel dataset, che non cambia): nessuna discrepanza residua per il Costume di casa. Nodi 2745, `partOf` 2584,
`isVersionOf` 529, `estrattoDi` 10 invariati. Aggiornati scheda Documentazione e Word (12.2, 18.24).

## 2026-10-14 (pomeriggio, 3) — Indice del volume anche per «Il costume di casa»

Backup `…_20261014-1621`. Nuovo sorgente `sorgenti/Il_costume_di_casa_indice.csv` (49 capitoli, ordine del file, copia fedele
dell'allegato; codifica Windows-1252, non Mac Roman). `importa_indici.py`: formato «gruppi» (due gruppi di colonne letti per
posizione, senza colonna N.), lettura UTF-8 o Windows-1252, nuove colonne `volume_indicato` e `tipologia` in `indici_volumi.csv`,
«N.D.»/celle vuote non sono discrepanze, intervalli di mesi confrontati sull'anno; righe degli altri libri invariate. Sito: stesso
codice di Diario minimo, Pape e Bustina; `campiFonteIndiceHTML` mostra «Informazioni sul contributo originale» (Pubblicato in,
A cura di, Editore, Luogo, Anno, Pagine, N.D. dove manca) per i capitoli in volume senza articolo; `titoloRigaUguale` ignora ogni
tipo di virgolette e apostrofi. Ontologia 1.9: sei proprietà `eco:titoloVolumeIndicato`, `curatoreVolumeIndicato`,
`editoreVolumeIndicato`, `luogoVolumeIndicato`, `annoVolumeIndicato`, `paginaVolumeIndicato`. «Dedalus» aggiunto per NA0016 e
NA0015 (`articoli_titolo_pseudonimo.csv`: articoli con pseudonimo 4 → 6). `raccolte_eco.csv`: nota del volume aggiornata (link OPAC
invariato). Nessun nodo o arco nuovo: nodi 2745, `partOf` 2584, `isVersionOf` 529, `estrattoDi` 10; voci d'indice 374 → 423 in 6 libri.
Aggiornati scheda Documentazione e Word (18.23).

## 2026-10-14 (pomeriggio, 2) — Titoli di capitolo con virgolette interne; layout rigenerato

Backup `…_20261014-1411`. `estrai_titolo_capitolo` (`genera_rdf.py`) non scrive più `eco:titoloCapitolo` quando il titolo ha
virgolette interne (il titolo giusto è quello dell'indice): spariscono da tutte le schede «I», «Mamma, che cosa vuol dire “fratello»
(Bustina) e «“Cagü!» (Pape); altri 417 titoli invariati. `posizioni_iniziali.js` rigenerato con `precalcola_layout.js`
(«Tutti» 583 nodi, «Solo ristampe» 187): nessun avviso in console. Nodi 2745, `partOf` 2584, `isVersionOf` 529 invariati.
Chiude la segnalazione del 13 ottobre (sera, 6).

## 2026-10-14 (pomeriggio) — Bustina: link OPAC, nota tolta, notazione di MicroMega

Backup `…_20261014-1357`. `raccolte_eco.csv`: nuovo link OPAC SBN per La bustina di Minerva e campo «Note / altre edizioni citate
nella fonte» svuotato. Riga N. 11 del CSV sorgente e nota di `ristampe_aggiunte.csv`: rivista «MicroMega : le ragioni della sinistra»,
numero «3» (come nel dataset); il rapporto degli indici non segnala più divergenze per la Bustina. Rigenerato con
genera_rdf → importa_indici → genera_rdf → genera_dati_sito. Nodi 2745, `partOf` 2584, `isVersionOf` 529 invariati. Nella vista
«Solo ristampe» i nodi sono 187 (non più 185): articolo JA2219 + la sua rivista MicroMega. Aggiunto 18.21 al Word.

## 2026-10-14 — Indice del volume anche per La bustina di Minerva

Backup `…_20261014-1343`. Nuova fonte `sorgenti/Indice_La_bustina_di_Minerva_ordine_libro.csv` (148 capitoli, N. 1..148,
ordine del file); `importa_indici.py` la legge per nome di colonna e scrive le righe in `indici_volumi.csv` (nuova colonna
`fonte_indicata`), senza toccare Diario minimo e Pape. Il codice del sito è lo stesso (`disegnaIndiceVolume`,
`campiVoceIndiceHTML`, `attivaEspansioneInlineVoce`); nuova `campiFonteIndiceHTML` per le voci senza articolo: mostra sempre
Titolo, Rivista / Testata, Numero, Data, Pagina, Note, con «N.D.» dove manca il dato; `htmlTestataFonteIndice` (testo semplice)
è il punto per un futuro collegamento (caso N.136, L'Almanacco del Bibliofilo, solo testo). Ontologia 1.8: cinque proprietà
`eco:titoloOriginaleIndicato/testataIndicata/numeroIndicato/dataIndicata/paginaIndicata`. Nuovo `dati_estratti/ristampe_aggiunte.csv`
(sezione 5ter di `genera_rdf.py`): JA2219 → La bustina di Minerva come ristampa (+1 `isVersionOf`: 529; nodi 2745 e `partOf` 2584
invariati); tolta da `capitoli_non_collegati.csv` la riga «Su un processo» (44 → 43). Voci d'indice: 374 in 5 libri. Aggiornati
scheda Documentazione, Word (18.20), `raccolte_eco.csv` (nota). Segnalato: il layout «Ristampe» di `posizioni_iniziali.js`
(non toccato) non corrisponde più ai nodi della vista (187 vs 185).

## 2026-10-13 (sera, 6) — «Titolo del capitolo» non più ripetuto nelle schede delle Raccolte

Solo aspetto (`visualizzazione.html`); nessun dato toccato. Backup `…_20261013-2008`. In `campiArticoloHTML` il campo
«Titolo del capitolo» (sezione Raccolte) si mostra solo se differisce dal titolo della riga cliccata: mai nelle tabelle degli
altri libri, nell'indice solo se il titolo nei dati è diverso (nuova `titoloRigaUguale`, opzione `titoloRiga` passata da
`campiVoceIndiceHTML`). Resta in un solo caso su 223 voci con articolo: «I "dottori" del triennio», dove il dato è sbagliato
(`TITOLO_CAPITOLO_RE` in `genera_rdf.py` si ferma alla prima virgoletta interna: 5 titoli troncati o assenti). Non corretto,
in attesa di decisione. Articoli, Timeline e pannello del grafo invariati.

## 2026-10-13 (sera, 5) — La legenda delle fasce passa nella colonna a sinistra

Solo aspetto (`visualizzazione.html`, `stile.css`). Backup `…_20261013-2005`. Il blocco `#elenco-legenda` non sta più tra
«Ordina per» e le righe: è una sezione «Legenda» della colonna di sinistra, tra «Cerca per titolo» e «Anno», con le due voci
in verticale. Stessa logica di visibilità (nascosta nell'elenco dei periodici/rubriche) e stesse variabili CSS.

## 2026-10-13 (sera, 4) — Legenda delle fasce colorate nell'elenco Articoli

Solo aspetto (`visualizzazione.html`, `stile.css`). Backup `…_20261013-1958` (visualizzazione, stile, CHANGELOG, Word).
Nuovo blocco `#elenco-legenda` tra «Ordina per» e le righe: «Articolo raccolto in volume» (giallo) e «Articolo estratto»
(fucsia), con campioni che usano le stesse variabili delle fasce (`--intensita-fascia-articolo`, `--larghezza-banda-articolo`).
Mostrata solo quando l'elenco articoli è visibile (in `disegnaTabella`, insieme a `#elenco-lista`). Nessun dato toccato.

## 2026-10-13 (sera, 3) — Titolo «Indice» nelle Raccolte, fasce colorate nell'elenco Articoli

Solo aspetto e testo (`visualizzazione.html`, `stile.css`). Backup prima di modificare:
`backup_visualizzazione_20261013-1952.html`, `backup_stile_20261013-1952.css`, `backup_CHANGELOG_20261013-1952.md`
(più il backup del Word, `backup_Opera_Persa_Documentazione_Tecnica_20261013-1952.docx`). Nessuna modifica a dati, RDF,
grafo, posizioni, Timeline, tabelle delle Raccolte, pannello del grafo.

**Raccolte.** Il titoletto sopra l'elenco dei capitoli dice solo «Indice» per tutti i libri (testo fisso nell'HTML; eliminato il
codice dei conteggi in `disegnaIndiceVolume` e `disegnaDettaglioLibro`). Stile: da 12,5 px / 400 / `--testo-sec` a
`--fs-titolo-indice` 18,5 px / 600 / `--testo`, padding 18px 22px 12px.

**Articoli.** Righe `.riga-art`: fascia intera gialla (`.ripubblicato`, `--articolo-rist`) o fucsia (`.estratto`,
`--articolo-estratto`, nuova classe aggiunta in `disegnaTabella`). Variabili in `:root`: `--intensita-fascia-articolo` (.20),
`--larghezza-banda-articolo` (3px), `--articolo-rist-rgb`, `--articolo-estratto-rgb`, `--testo-sec-fascia` (#d6cfc2, riga di meta
sulle righe colorate/selezionate per il contrasto AA). Hover = 1,5 × intensità; selezionata = velo terracotta + contorno +
banda del colore del tipo. `--ristampa-segno` resta (usata dalla Timeline).

## 2026-10-13 (sera, 2) — Altri tre pseudonimi d'articolo, anno non più doppio in «Ripubblicato anche in»

Backup fatti prima di modificare (`backup_<nome>_20261013-1912.<ext>`, nelle cartelle `backup/` del progetto, di
`grafo_eco/`, `grafo_eco/dati_estratti/`, più `backup/dati_rdf_20261013-1912`). NON modificati: `sorgenti/`,
`posizioni_iniziali.js`, `genesi.html`, l'ontologia (resta 1.7). dati.js, grafo_dati.json e RDF solo rigenerati.

**Pseudonimi.** Aggiunte tre righe a `grafo_eco/dati_estratti/articoli_titolo_pseudonimo.csv`, stesso meccanismo del caso
JA0570: JA0511 «Il mistero Gomulka [con lo pseudonimo di Telesio Malaspina]» → titolo «Il mistero Gomulka», Autore
`Umberto Eco [Telesio Malaspina]`; JA0598 «Novantanove proverbi strutturalisti» (Il Caffè 1972) → Autore
`Umberto Eco [Anonimo Ginevrino]`; JA0259 «Due inediti di Dedalus» (Il Verri 1961) → Autore `Umberto Eco [Dedalus]`
(per questi due il titolo non conteneva parentesi e resta invariato). Lasciato intatto, su richiesta, il caso del libro
«Filosofi in libertà» (1992). Rigenerata la catena (genera_rdf → importa_indici → genera_rdf → genera_dati_sito):
rispetto a prima cambiano solo label/tooltip di JA0511 e il campo `pseudonimo` dei tre nodi; nodi 2745, archi invariati,
indici invariati, 15 query SPARQL OK. `ristampe_da_verificare.csv` non contiene il titolo di JA0511: nessuna modifica.

**«Ripubblicato in / anche in» ed «Estratto da».** L'etichetta del libro finiva con l'anno e la parentesi bibliografica lo
ripeteva («Diario minimo (1966) (Milano: Mondadori, 1966)»). Nuova funzione `etichettaLibroSenzaAnnoRipetuto` in
`visualizzazione.html`: toglie l'anno finale dall'etichetta quando la parentesi con editore e anno è presente; ora
«Diario minimo (Milano: Mondadori, 1966)», cliccabile solo «Diario minimo». Vale per tutte le schede articolo.

## 2026-10-13 (serata) — Schede dei capitoli più essenziali, «Ripubblicato anche in» cronologico, titolo e pseudonimo di JA0570, ontologia 1.7

Backup fatti prima di modificare (`backup_<nome>_20261013-1802.<ext>`, nelle cartelle `backup/` del progetto, di
`grafo_eco/`, `grafo_eco/queries/`, `grafo_eco/dati_estratti/`, più `backup/dati_rdf_20261013-1802`). NON modificati:
`sorgenti/` (Excel solo letti), `posizioni_iniziali.js`, `genesi.html`. dati.js, grafo_dati.json e RDF solo rigenerati.

**Sezione Raccolte (`visualizzazione.html`).** (1) «Titolo in indice» eliminato da tutte le schede; rimossa la funzione
`titoloConfrontabile`, che serviva solo a quel confronto (causa: confrontava solo minuscole, apostrofi, virgolette,
trattini, spazi e punteggiatura finale, non accenti né punteggiatura interna; 63 capitoli su 226 lo mostravano:
10 differenze solo ortografiche, 9 sottotitoli, 9 varianti lievi, 35 titoli davvero diversi). (2) Virgolette caporali tolte dal
«Titolo» delle schede (voci d'indice, capitoli non collegati) e dal «Titolo del capitolo» nelle schede delle altre
raccolte; restano nell'elenco, in Articoli, nel pannello del grafo e in «Pubblicato originariamente in:» e
«Opera recensita:». (3) «Ripubblicato anche in:» in ordine cronologico (`ordinaLibriPerAnno`: anno numerico, poi
titolo con `localeCompare("it")`, senza anno in fondo), solo con `escludiLibro`.

**JA0570 «Siamo tutti registi» e pseudonimi.** Nuovo `dati_estratti/articoli_titolo_pseudonimo.csv` (id,
titolo_atteso, titolo_corretto, pseudonimo, nota), letto da `genera_rdf.py` (sezione 1ter): corregge il titolo e
scrive `eco:pseudonimo` caso per caso, con controllo sul titolo atteso (lo script si ferma se non corrisponde); nessuna
regola automatica; sopravvive a una nuova estrazione. Ontologia 1.7: `eco:pseudonimo` ha dominio VoceIndice o
JournalArticle. `queries/articoli.rq`: OPTIONAL su `eco:pseudonimo`; `dati.js`: campo `pseudonimo` sui nodi-articolo;
`campiArticoloHTML`: «Autore: Umberto Eco [Lia Quilici]» in tutte le schede articolo. Tolto il campo «Pseudonimo:» dalla scheda
del capitolo (se l'Excel degli indici indica uno pseudonimo e l'articolo non ne ha, si usa quello della voce: nessun caso
oggi). `ristampe_da_verificare.csv`: titolo ripulito (la riga porta un id, JA0031, che non corrisponde a JA0570).
`indici_volumi.csv`: l'abbinamento di JA0570 passa a «rivista+numero+data+titolo», sparisce la segnalazione di titolo
diverso (una segnalazione in meno nel rapporto).

**Documentazione.** Scheda del sito (Raccolte, nuovo paragrafo sugli pseudonimi), Word (capitolo 5, 12.2, diagramma dei dati,
versione 1.7, nuova sezione 18.14).

**Verifica (Playwright + oxigraph).** 226 schede dei quattro indici (16+17+17+176) senza «Titolo in indice», senza
caporali, con «Titolo»; «Ripubblicato anche in:» in ordine crescente in 46 schede; otto schede a caso di Opera aperta e
La bustina di Minerva; JA0570 in nodo, tooltip, ricerca, elenco, timeline, scheda e pannello; nodi (2745), archi
(2584/528/10), indici e posizioni identici; 15 query SPARQL senza errori; console pulita.

**Da decidere / segnalato.** Rapporto sugli altri casi di pseudonimia (JA0511, Dedalus, Anonimo Ginevrino ecc.) e sulle
indicazioni di «altri autori» presenti nell'Excel ma non estratte: consegnato, nessun dato toccato.

## 2026-10-13 (tarda sera) — Tre categorie di libri (ontologia 1.6), etichette della legenda, schede dei capitoli, «Nota all'edizione 1975»

Backup fatti prima di modificare (`backup_<nome>_20261013-1735.<ext>`, nelle cartelle `backup/` del progetto, di
`grafo_eco/`, `grafo_eco/queries/`, `grafo_eco/dati_estratti/` ecc.) per ogni file toccato. NON modificati: Excel e
`sorgenti/`, `posizioni_iniziali.js`, `dati.js`/`grafo_dati.json`/RDF a mano (solo rigenerati).

**Tre categorie di libri.** Nuovo `dati_estratti/classificazione_libri.csv` (titolo_libro, categoria): unico punto in
cui si decide la categoria di ciascuno dei 31 libri. 7 romanzi (Il nome della rosa 1980 e 1985, Il pendolo di
Foucault, La misteriosa fiamma della regina Loana, Baudolino, Il cimitero di Praga, L'isola del giorno prima), 6 non
raccolta (Storia della bellezza, Storia della bruttezza, Storia delle terre e dei luoghi leggendari, Il problema
estetico in San Tommaso, La ricerca della lingua perfetta nella cultura europea, Postille a Il nome della rosa),
18 raccolte. «Numero zero» non esiste nei dati e non è stato creato. Ontologia 1.6: `eco:LibroEstratto` sostituita da
`eco:Romanzo` e `eco:LibroNonRaccolta`; `eco:tipoLibro` = «romanzo» / «non raccolta» / «raccolta»; STORICO VERSIONI
aggiornato. `genera_rdf.py` valida le categorie (errore su valori non validi o titoli doppi, avviso per i libri senza
riga, che finiscono in «raccolta»), genera le note automatiche per categoria e stampa i conteggi. Sito:
`LIBRI_ESCLUSI_DA_RACCOLTE` eliminata, `libroInRaccolte` controlla `tipo_libro === "raccolta"`; pannello del libro con
tre etichette di tipo; `genesi.html`, `queries/libri.rq`, `queries/libro_indice.rq`, SPIEGAZIONI in
`genera_dati_sito.py` e Documentazione aggiornati. Nodi, archi, colori e posizioni invariati (2745 nodi; partOf 2584,
isVersionOf 528, estrattoDi 10). La riga di legenda «Libro (raccolta di Eco)» NON è stata toccata.

**Legenda (solo etichette).** Articolo ripubblicato → «Articolo raccolto in volume»; Articolo estratto → «Estratto»;
Ristampa (…) → «Ristampa»; Estratto (da volume a rivista) → «Anticipazione»; «Articolo» invariato. Colori, forme e
stili invariati, nomi tecnici invariati. «Anticipazione» compare solo in legenda e nel nuovo paragrafo «Come leggere
la legenda della Vista a grafo» (Documentazione e Word).

**Raccolte.** Elenco dei capitoli (`#tabella-indice`, `#tabella-ristampe`) da 13,5 px a 15 px (+11 %) con la variabile
`--fs-elenco-capitoli` in `stile.css`; colonne N. (56 px) e Pagine (76 px) strette; scheda in linea alla stessa
dimensione. Schede dei capitoli: «Informazioni sull'articolo originale»; «Titolo» (+ «Titolo in indice:» se diverso);
«Ripubblicato anche in:» ed «Estratto da:» senza l'edizione consultata (parametro opzionale `escludiLibro` di
`campiArticoloHTML`: Articoli, pannello del grafo e Timeline restano «Ripubblicato in:»). Nuovo stato di voce
«inedito» (distinto da «inedito-nd») e voce «Nota all'edizione 1975» in prima posizione in Diario minimo (1975), da
`dati_estratti/indici_voci_aggiunte.csv`, unita da `importa_indici.py` a ogni esecuzione; non è nodo, arco né
conteggio del grafo; intestazione «Indice del volume: 17 capitoli». `indici_volumi.csv`: 226 voci (16 + 17 + 17 + 176).

**Documentazione.** Scheda del sito, `genesi.html` e Word (nuove sezioni nel capitolo 5, 12.2 e 18.13; tabelle, catena
dei dati, versione 1.6) allineati.

**Verifica (Playwright + oxigraph).** Conteggi per categoria 7/6/18; grafo e posizioni invariati; elenco Raccolte di
18 libri; `genesi.html` per romanzo, non raccolta e raccolta con più edizioni; legenda; valori CSS prima/dopo con
schermate a ~1280 e ~400 px; «Ripubblicato anche in:» su tutti i capitoli dei quattro indici e su un campione di
altre raccolte; Articoli e pannello invariati; Diario minimo (1975) con 17 voci; 15 query SPARQL senza errori.

**Da decidere / segnalato.** (1) `posizioni_iniziali.js` RIGENERATO su richiesta (17:46, `precalcola_layout.js`, backup `backup_posizioni_iniziali_20261013-1735.js`): vista «Tutti» 583 nodi, vista «Ristampe» 185 nodi; la pagina non segnala più il layout non valido. (2) Testi
della Vista a grafo che dicono ancora «ripubblicato»/«estratto» (pannello «Articoli ripubblicati:», «Nota ristampa:»,
«Nota (estratto):», «Ripubblicato in:», «Estratto da:»). (3) Note bibliografiche nei dati che nominano il volume
consultato (JA0594, JA0620, JA0914, JA0849, JA0545): non riscritte. (4) A 400 px la pagina ha già uno scorrimento
orizzontale (673 px) anche prima di questa modifica.

## 2026-10-13 (sera) — Indice del volume per Diario minimo e Pape Satàn Aleppe, Appendice e «pubblicatoIntegralmenteSu» rimosse, ontologia 1.5

Backup fatti prima di modificare (`backup_<nome>_20261013-1650.<ext>`, nelle cartelle `backup/` del progetto, di
`grafo_eco/queries/`, `grafo_eco/dati_estratti/` ecc.) per ogni file toccato. NON modificati: Excel e `sorgenti/`
(`Indice_aggiornato_20261013.xlsx` è solo letto), `posizioni_iniziali.js`, le altre CSV.

**Dati alla fonte (CSV in `grafo_eco/dati_estratti/`).**
- `articoli_rivista_correlata.csv`: «La scolastica» (Alfabeta n. 48, JA0913) NON è un'anticipazione delle Postille;
  era l'unica riga: il file è stato ritirato (copia in `dati_estratti/backup/`). `estratti_libri.csv`: dalla nota di
  JA0914 tolto solo il frammento sull'anticipazione JA0913. «La scolastica» resta un normale articolo (solo `partOf`).
- `estratti_libri.csv`: «Il nome della rosa (1985)» ora porta `id_articolo = JA0914` con nota di ristampa (il saggio
  è stato ripubblicato nella 6ª edizione del romanzo, 1985); colonna `contiene_come_appendice` eliminata.
  JA0914 ha quindi DUE archi `prism:isVersionOf` (Postille a Il nome della rosa; Il nome della rosa 1985). L'elenco
  `ESTRATTI_VERI` (10 estratti) non è stato toccato.
- `raccolte_eco.csv`: `link_opac` dei tre Diario minimo (1963, 1966, 1975) sostituiti con i link esatti forniti
  (Pape Satàn Aleppe invariato); `note_ricerca` svuotata per Diario minimo 1963/1966/1975 e Pape Satàn Aleppe
  (il riquadro «Note / altre edizioni citate nella fonte» sparisce solo per questi quattro).
- NUOVO `indici_volumi.csv` (+ `indici_volumi_report.txt`): 225 voci d'indice in 4 libri (16 + 17 + 16 + 176),
  generato da `grafo_eco/importa_indici.py` (NUOVO) dall'Excel `sorgenti/Indice_aggiornato_20261013.xlsx`. Colonne
  `numero_capitolo` e `pagine_volume` vuote (da compilare a mano nel CSV; l'importatore le conserva alle esecuzioni
  successive). Il rapporto elenca 7 discrepanze Excel/dataset e nessuna riga non abbinata.

**Modello.** Rimossi: `eco:pubblicatoIntegralmenteSu` (arco `correlataRivista`, campo
`pubblicato_integralmente_titolo`, testo «Testo integrale uscito su:») e la relazione Appendice (`frbr:part` fra due
libri: `appendici_pendenti`, `libro_appendici.rq`, relative sezioni in genera_rdf.py, genera_dati_sito.py, genesi.html,
Documentazione e query d'esempio). `frbr:part` resta solo per `eco:CapitoloNonCollegato`. Le relazioni di riuso
restano due (`prism:isVersionOf`, `eco:estrattoDi`). Nuova classe `eco:VoceIndice` (9 proprietà: `nelIndiceDi`,
`posizioneInIndice`, `titoloInIndice`, `statoVoce`, `numeroCapitolo`, `pagineNelVolume`, `articoloCorrispondente`,
`coautore`, `pseudonimo`): una voce d'indice NON è un nodo né un arco del grafo visivo. Ontologia 1.5 con voce nello
STORICO VERSIONI.

**Pipeline e sito.** `genera_rdf.py` (sezione 8: voci d'indice), nuova query `queries/libro_indice.rq`
(commentata, inserita in `query_esempio.js` con spiegazione), `genera_dati_sito.py` scrive `DATI.indici[idLibro]`.
`visualizzazione.html`: pallini estratti a dimensione 12 come i ripubblicati (`styleNodo`); nelle Raccolte, per i
libri con `DATI.indici` l'indice del volume («Indice del volume: N capitoli», colonne N. / Titolo del capitolo /
Pagine, senza ordinamento) sostituisce la tabella degli articoli; click su una riga = espansione in linea con la
scheda del capitolo (Ristampa con tutti i dati dell'articolo, oppure «Inedito / N.D.»); gli altri libri sono
invariati. Scheda Documentazione aggiornata; `stile.css`: regole `#tabella-indice`.

**Verifica (Playwright + oxigraph).** 2745 nodi; archi `partOf` 2584, `isVersionOf` 528 (527 + 1), `estrattoDi` 10,
nessun `correlataRivista`/`contieneAppendice`; 10 estratti a dimensione 12 (anche con clic e box-anno aperti);
posizioni dei nodi invariate; indici di 16/17/16/176 righe nell'ordine dell'Excel con titoli = colonna `Indice`;
«Twitto dunque sono» e «Postilla» = Inedito / N.D.; «Tre recensioni anomale» (1975) = Parziale ristampa; link OPAC
identici ai forniti; altre raccolte invariate con riquadro note presente; `genesi.html` aperta per libri con e senza
indice; 15 query SPARQL senza errori.

**Da decidere / segnalato.** (1) `posizioni_iniziali.js` NON toccato: l'arco JA0914 → Il nome della rosa (1985)
aggiunge il nodo del romanzo alla vista «Ristampe» (184 → 185 nodi) e ne invalida l'hash; la pagina avvisa in console
e calcola quella disposizione nel browser (la vista «Tutti» resta valida). Rigenerarlo è una decisione dell'utente.
(2) Le note dei libri «Postille a Il nome della rosa» e «Il nome della rosa (1985)» contengono ancora la parola
«appendice» come descrizione editoriale (non come relazione). (3) JA0914 ha due note di ristampa (quella delle
Postille e quella del 1985).

## 2026-10-13 — Modello a due relazioni di riuso (Ristampa, Estratto), terminologia "estratto", nuovo colore, ontologia 1.4

Backup fatti prima di modificare (`backup_<nome>_20261013-1545.<ext>` in `backup/`) per ogni file toccato:
`visualizzazione.html`, `stile.css`, `genesi.html`, `grafo_eco/genera_rdf.py`, `grafo_eco/genera_dati_sito.py`,
`grafo_eco/ontologia_eco.ttl`, le query `.rq` ritoccate, `CHANGELOG.md`, `Opera_Persa_Documentazione_Tecnica.docx`
e gli output rigenerati. NON modificati: i dati sorgente (CSV, Excel, `dati_estratti/`), `posizioni_iniziali.js`
(il layout non è stato né toccato né ricalcolato; l'hash dei nodi resta valido).

**Modello.** Oltre all'appartenenza articolo → testata (`frbr:partOf`, archi `partOf`, articolo-rubrica: invariata),
fra pubblicazioni diverse restano soltanto due relazioni: (1) **Ristampa** = `prism:isVersionOf`, da rivista a volume
o da rivista a un'altra rivista (la seconda forma è prevista ma oggi senza istanze; per estenderla a articolo →
articolo servirebbero istanze reali, non inventate); (2) **Estratto** = `eco:estrattoDi`, da volume a rivista (il
volume è la fonte). `contieneAppendice` e `correlataRivista` escono dal modello e dal grafo (non più emesse).

**Cosa è cambiato.**
- `visualizzazione.html`: legenda (tolte le righe "Gruppo per anno con ripubblicazioni", "Anticipazione uscita
  integralmente altrove" e "Appendice"; rinominate "Ristampa (da rivista a volume, o da rivista a rivista)" ed
  "Estratto (da volume a rivista)"; aggiunta "Articolo estratto" dopo "Articolo ripubblicato"); codice morto
  rimosso (`idsAppendicePropagati`, rami di `stileArco` per i due archi tolti); `COLORI.articolo_estratto`;
  scheda Documentazione riscritta sul modello a due relazioni; l'informazione `correlataRivista` resta nella
  scheda dell'articolo come "Testo integrale uscito su:".
- `stile.css`: `--articolo-estratto:#d946ef`; rimossi `--evidenzia-indiretto`, `.linea-puntinata`,
  `.linea-tratteggiata-libro`.
- Terminologia: "anticipazione/anticipare" → "estratto" in HTML, `genesi.html`, script Python, query, ontologia,
  testi delle query d'esempio (ripetuti con grammatica adattata, nessuna sostituzione automatica).
- `ontologia_eco.ttl`: versione 1.4 con voce nello STORICO (le voci precedenti invariate); commenti dei termini
  riscritti. Nomi tecnici (`eco:estrattoDi`, `eco:LibroEstratto`, `eco:tipoLibro`) invariati.
- Pipeline rigenerata: `dati.js`, `grafo_dati.json`, `istanze_espresso.ttl`, `grafo_completo_ttl.js`,
  `query_esempio.js` (rigenerato dallo script, non modificato a mano), `dati_rdf/*`.

**Nodo senza articoli.** Togliere `contieneAppendice` avrebbe isolato "Il nome della rosa (1985)" (e invalidato
l'hash del layout): il nodo resta e, nelle viste, segue la regola dei libri senza articoli collegati.

**Verifica (Playwright + oxigraph).** Conteggi: 2584 articoli, 2584 partOf, 527 isVersionOf, 10 estrattoDi,
31 libri, 116 riviste, 14 quotidiani; archi totali −2 (i due tolti); posizioni identiche; nessun arco
`contieneAppendice`/`correlataRivista`; i 10 articoli estratti nel nuovo colore, anche con nodo selezionato;
legenda controllata nei due sensi; 15 query SPARQL eseguite senza errori; console pulita.

**Da decidere / segnalato.** Codice dell'Appendice fuori dalla legenda (es. in `genesi.html`) non toccato, in
attesa di indicazioni. Le note dei CSV contengono ancora la parola "Anticipazione" (10 casi): finché i CSV non
vengono modificati, resta nei dati generati. L'articolo `correlataRivista` (JA0913 "La scolastica") risulta su
Alfabeta n. 48, non su L'Espresso.

## 2026-10-12 — Sezione "Raccolte": l'elenco mostra solo le raccolte curate da Eco

Modifica di sola visualizzazione in `visualizzazione.html`. Backup fatto prima di modificare, con la convenzione
d'uso (`backup_<nome>_20261012-1707.<ext>`): `visualizzazione.html`, `CHANGELOG.md` e
`Opera_Persa_Documentazione_Tecnica.docx`. NON modificati: dati (`dati.js`, `grafo_dati.json`, RDF, CSV), script
Python, ontologia, `posizioni_iniziali.js`, `stile.css`, le altre sezioni. Nessuna rigenerazione della pipeline.

**Regola.** Costante unica `LIBRI_ESCLUSI_DA_RACCOLTE` (riga ~3577, blocco "SCHERMATA 3: RISTAMPE"): insieme di id
con un commento in italiano per ciascuno. I 12 titoli richiesti sono 13 nodi (Il nome della rosa ha due edizioni,
1980 e 1985): Baudolino, Il cimitero di Praga, Il nome della rosa (1980 e 1985), Il pendolo di Foucault, Il problema
estetico in San Tommaso, L'isola del giorno prima, La misteriosa fiamma della regina Loana, La ricerca della lingua
perfetta nella cultura europea, Postille a Il nome della rosa, Storia della bellezza, Storia della bruttezza,
Storia delle terre e dei luoghi leggendari. La regola NON si basa su `tipo_libro`: per aggiungere o togliere
un'eccezione si cambia una riga. La legge la funzione `libroInRaccolte(id)` (riga ~3596).

**Dove è applicata.**
- `disegnaElencoLibri` (~3638): l'elenco parte da `TUTTI_LIBRI.filter(libroInRaccolte)`. Intestazione "Libri (N)",
  ricerca, ordinamento e raggruppamento per edizioni (`baseOperaLibro`) lavorano su questo elenco, quindi i conteggi
  restano calcolati e coerenti (nessun numero scritto a mano).
- Schede articolo (`campiArticoloHTML`, ~886; usata sia in Articoli sia nel pannello del grafo): per "Ripubblicato
  in:" ed "Estratto da:" la nuova `htmlTitoloLibroCollegato` (~3604) dà il link `data-vai-libro` solo per le vere
  raccolte; per i libri esclusi il titolo è testo semplice, con lo stesso aspetto del resto del campo.
- Pannello di un nodo-libro nella Vista a grafo (`mostraDettagli`, ~971): il pulsante "Vedi la scheda completa" è
  nascosto per i libri esclusi, invariato per le raccolte.
- `libroAttivo`: `vaiALibro` (~3918), `ripristinaStato` (tasto Indietro) e il deep-link a fine script (~4199)
  ignorano un libro escluso; la selezione iniziale parte dall'elenco filtrato. Un deep-link verso un libro escluso
  apre la sezione senza libro selezionato e senza voci di cronologia verso di esso.

**Il problema estetico in San Tommaso.** Nei dati è un nodo `libro` con `tipo_libro = "raccolta"` (non
"estratto") collegato da due archi `isVersionOf` ad articoli del 1956 su "Filosofia". Michele ha confermato che NON
è una raccolta ma un saggio a sé, in cui Eco ha fatto confluire, rielaborandoli, alcuni articoli: va quindi trattato
come saggio e la classificazione "raccolta" nei dati è un'anomalia (nel CSV `raccolte_eco.csv` ha una riga come
"raccolta propria di Eco" e `genera_rdf.py` applica il default "raccolta"). Nel sito è già escluso da Raccolte;
nei dati non è stato toccato nulla, da correggere a monte (CSV/script) quando vorrai.

**Verifica (Playwright/Chromium, pagina vera, 34 controlli, tutti superati).** Elenco mostrato = elenco atteso
calcolato da `DATI` (14 voci, stampati entrambi; prima erano 26); nessuno dei 12 titoli presente; ogni voce ed
edizione si apre senza errori; nel grafo i 13 nodi esclusi sono presenti, visibili, cliccabili, con pannello
corretto e senza pulsante verso Raccolte (prima c'era); `network.getPositions()` identico a prima per tutti i
583 nodi, stessi nodi e 587 archi, stessa evidenziazione al click; tutti i 2584 articoli: nessun link verso libri
esclusi (13 casi in testo semplice, link intatti per le raccolte); deep-link, `vaiALibro`, `ripristinaStato`
sicuri; console pulita.

**Documentazione.** Nuova sotto-sezione "La sezione Raccolte: quali libri elenca" in fondo al paragrafo 12.2.

**Da segnalare, NON modificato.**
- Testo di aiuto della sezione e legenda del grafo ("Libro (raccolta di Eco)") lasciati come sono.
- Il contatore in home "N libri con ristampe" (`nLibriRistampa`) conta ancora anche Postille e Il problema estetico
  (hanno archi `isVersionOf`) e può quindi essere maggiore del numero di voci in Raccolte.
- Nel codice resta un ramo per l'etichetta "estratto" ormai non raggiungibile dall'elenco.

## 2026-10-12 — Vista a grafo: articoli ripubblicati gialli con un nodo selezionato; il clic su un box-anno non fa più perdere la selezione

Due interventi richiesti sull'evidenziazione al click di un nodo (`visualizzazione.html`). Backup fatto prima di
modificare, con la convenzione d'uso (`backup_<nome>_20261012-1538.<ext>`): `visualizzazione.html`, `CHANGELOG.md`
e `Opera_Persa_Documentazione_Tecnica.docx`. `stile.css` NON modificato (la riga di legenda usa variabili CSS e
stile inline già esistenti). Nessuna modifica a dati (`dati.js`, `grafo_dati.json`, RDF), script Python,
`posizioni_iniziali.js`, fisica o disposizione: solo colore, bordo e opacità dei nodi.

- **1. Ripubblicati gialli nello stato "nodo cliccato"**: in `evidenziaNodoCliccato` (circa riga 2390) lo stile dei
  nodi illuminati in modo indiretto è ora deciso dalla nuova `stileNodoIlluminatoIndiretto(n)` (circa riga 2286). Un
  nodo-articolo nell'insieme `ponte` o `collegati` con `raw.ripubblicato` vero resta `COLORI.articolo_rist` (giallo,
  come la legenda), con opacity 1 e `borderWidth` 3; gli articoli non ripubblicati restano `COLORI.evidenziaIndiretto`
  (viola). Invariati: libri (ambra), riviste/quotidiani, nodo cliccato (rosa) e nodi sfumati (opacity 0.15, colore di
  partenza non toccato). Vale per ogni rivista/quotidiano cliccato e anche cliccando un libro con articoli vicini.
- **1. Box-cluster chiusi: nessun bordo giallo (rifinitura del 12 ottobre, ore 15:53)**: in un primo momento un box
  con almeno un membro ripubblicato aveva il bordo giallo (colore `{background, border}` calcolato da
  `clusterInfoCorrente`); esteticamente non piaceva ed è stato TOLTO. Rimosso il ramo `raw.group === "cluster"` di
  `stileNodoIlluminatoIndiretto` (con il calcolo "il box contiene membri ripubblicati", che non serviva ad altro) e
  la frase del commento che lo descriveva. Un box illuminato torna come nelle versioni precedenti: riempimento viola
  `COLORI.evidenziaIndiretto`, `borderWidth` 3, nessuna distinzione grafica fra box con e senza ripubblicati.
  `calcolaStatoBoxCluster` (stati di ricerca e filtro dei box) non è stato toccato. Backup della rifinitura:
  `backup_visualizzazione_20261012-1553.html`, `backup_CHANGELOG_20261012-1553.md`,
  `backup_Opera_Persa_Documentazione_Tecnica_20261012-1553.docx`.
- **1. Legenda**: aggiunta UNA riga dopo "Gruppo per anno (doppio click)" (riga 142), "Gruppo per anno con
  ripubblicazioni (nodo selezionato)", con un quadratino viola (`--evidenzia-indiretto`) e bordo giallo
  (`--articolo-rist`). NOTA: era stata aggiunta per spiegare il bordo giallo dei box, ora eliminato; per richiesta
  esplicita ("tutto il resto invariato") la riga è stata lasciata com'è, ma descrive un segnale che non esiste più:
  da decidere se toglierla (basta cancellare la riga 142 di `visualizzazione.html`).
- **2. Selezione che sopravvive al click su un box-anno**: nuova variabile `nodoSelezionatoId` (riga 2254) con l'ultimo
  nodo non-cluster cliccato. In `network.on("click")` (circa riga 2554) un click su un nodo con `raw.group ===
  "cluster"` non chiama né `evidenziaNodoCliccato` né `mostraDettagli`: illuminazione, colori e scheda dei dettagli
  restano identici; senza selezione non si accende nulla. Poiché vis-network ha comunque selezionato il box, la
  selezione corretta viene ripristinata con `network.selectNodes([nodoSelezionatoId])` (o `network.unselectAll()` se
  non c'è selezione): scelta più semplice che funziona, il contorno di selezione non resta sul box.
- **2. Quando la selezione si azzera**: nuova `azzeraSelezioneClick()` (riga 2257, imposta `nodoSelezionatoId = null`
  e chiama `spegniEvidenziazioneClick()`), usata dal click sul canvas vuoto, da `naviga()` quando si lascia la Vista a
  grafo (riga 765) e da `ricostruisciDataset()` (riga 1621: cambio vista Tutti/Ristampe, filtri che ricostruiscono il
  dataset). Un click su un altro nodo non-cluster sposta la selezione su quello.
- **2. Doppio click su box-anno e sulla testata**: la nuova `riapplicaEvidenziazioneSelezione()` (riga 2268) richiama
  `evidenziaNodoCliccato(nodoSelezionatoId)` se c'è una selezione, DOPO `nodesDS.add/remove/update` e dopo
  l'aggiornamento di `clusterInfoCorrente` (da cui dipende `idVisualizzatoPerArticolo`): in apertura (`network.on
  ("doubleClick")`, circa riga 2523) e a fine animazione in `chiudiGruppiRivista` (circa riga 2453). In
  `chiudiGruppiRivista` ho tolto lo `spegniEvidenziazioneClick()` iniziale, così l'illuminazione resta accesa durante
  l'animazione di richiusura e non lampeggia; il doppio click di apertura mantiene il suo spegni iniziale (è
  sincrono con la ri-evidenziazione, nessun fotogramma intermedio). Se il nodo selezionato non esiste più o è nascosto
  (es. un articolo selezionato i cui gruppi vengono richiusi), la selezione si azzera e la scheda dei dettagli si
  chiude, come cliccando sul canvas vuoto.
- **Difetto trovato dalla verifica e corretto (doppio click)**: il parametro `params.nodes` del doppio click di
  vis-network contiene la SELEZIONE corrente, non il nodo sotto il puntatore. Dopo il ripristino della selezione, il
  doppio click su un box-anno veniva letto come doppio click sulla rivista selezionata (il gruppo non si apriva), e
  senza selezione `params.nodes` era vuoto (il box non si apriva affatto). `network.on("doubleClick")` ora ricava il
  nodo da `network.getNodeAt(params.pointer.DOM)` (circa riga 2480).
- **Verifica**: Playwright (Chromium) sulla pagina vera, stili letti dal DataSet, 54 controlli, tutti superati
  (dopo la rifinitura sul bordo dei box: con L'Espresso selezionato i box con e senza ripubblicati hanno stesso colore
  e stesso `borderWidth`, e gli articoli ripubblicati restano gialli dopo l'apertura di un gruppo).
  L'Espresso, La Repubblica (quotidiano) e *Baudolino* (libro): colori/opacità/bordi di ogni nodo illuminato e
  sfumato; click su box-anno (anche di un'altra testata, sfumato) con colori, opacità, scheda e selezione vis-network
  identici a prima; doppio click di apertura (articoli già gialli/viola, resto sfumato, selezione intatta), due
  gruppi aperti di seguito e richiusura con doppio click sulla rivista; senza selezione, click su box-anno senza
  effetto e doppio click che apre il gruppo senza illuminare nulla; canvas vuoto, cambio scheda, cambio vista
  (Ristampe e ritorno), click su un altro nodo; nessun errore o avviso in console; `network.getPositions()` identica
  prima e dopo i click e dopo il ritorno alla vista "Tutti" (nessun nodo preesistente mosso dall'apertura, oltre
  all'assestamento già previsto dei membri).
- **Segnalato, poi corretto il 2026-10-21 (57)**: `applicaVisibilitaEStile` (filtri e ricerca) riscrive colore e
  bordo di tutti i nodi con lo stile di base e quindi, con un nodo selezionato, spegne l'illuminazione (il nodo
  cliccato perde il rosa, i nodi viola tornano al colore normale) lasciando però l'opacità 0.15 sugli altri nodi e
  `evidenziazioneClickAttiva`/`nodoSelezionatoId` impostati (stato "stantio"). Verificato cambiando un filtro con
  L'Espresso selezionato. Un nuovo click su un nodo, o un doppio click su un box-anno (che ora richiama
  `riapplicaEvidenziazioneSelezione`), la riaccende. Se si vuole, la correzione naturale è richiamare
  `riapplicaEvidenziazioneSelezione()` alla fine di `applicaVisibilitaEStile`.
- **Documentazione**: `Opera_Persa_Documentazione_Tecnica.docx`, capitolo 12.2: nel capitolo non esisteva nessun
  paragrafo sull'evidenziazione al click, quindi ho aggiunto una nuova sottosezione "Evidenziazione al click su un
  nodo (aggiornata il 12 ottobre 2026)" dopo "Apertura di un gruppo per anno", con lo stesso stile delle altre
  (meccanismo, i due cambiamenti, il difetto del doppio click, riquadro "In parole semplici" con il limite noto sui
  filtri). La scheda "Documentazione" del sito non è stata toccata.

## 2026-10-07 — Ordinamenti sensati in Articoli; limite ANNO_MASSIMO=2016

Due interventi richiesti: (A) controlli di ordinamento nella sezione Articoli, che mostravano spesso voci senza
senso (es. "periodico" dentro un periodico, dove è identico per tutti gli articoli); (B) eliminazione dal sito
degli articoli posteriori al 2016 (dal 2017 in poi), nella pipeline di generazione, senza toccare i CSV originali.
Backup fatto prima di modificare, con la convenzione d'uso (`backup_<nome>_20261007-1430.<ext>`):
`visualizzazione.html`, `genera_rdf.py`, `dati.js`, `posizioni_iniziali.js`, `grafo_completo_ttl.js`,
`query_esempio.js`, `CHANGELOG.md`, `grafo_dati.json` e `grafo_eco/istanze_espresso.ttl`, più una copia
completa della cartella `dati_rdf/` precedente (`dati_rdf_20261007-1430/`).

- **A. Elenco periodici/rubriche — tre ordinamenti invece di due, nessuno dei due col senso della direzione**:
  aggiunta una terza voce "data" (anno del primo articolo del periodico/rubrica nell'intervallo di anni scelto,
  a parità il nome) accanto a "nome" (alfabetico italiano) e "numero di articoli" (default, decrescente come
  prima); i tre controlli hanno ora lo stesso aspetto e comportamento di quelli già usati per gli articoli
  (link di testo, voce attiva evidenziata, clic ripetuto = inverte il verso, freccia ↑/↓), prima assenti per
  periodici/rubriche.
- **A. Elenco articoli dentro un periodico/rubrica/"tutti" — solo i campi che possono davvero cambiare l'ordine**:
  "data" e "titolo" (alfabetico italiano) sempre presenti; "periodico" e "rubrica" compaiono solo se, fra gli
  articoli effettivamente mostrati, quel campo assume almeno due valori diversi — quindi spariscono da soli
  dentro un singolo periodico (periodico sempre uguale) o dentro una rubrica di un solo periodico (periodico
  sempre uguale) o con una sola rubrica (rubrica sempre uguale), e restano con una sola voce utile quando serve.
  Lo stato di ordinamento attivo è globale: se il campo attivo smette di essere disponibile cambiando modo o
  categoria, si ricade su "data" crescente invece di lasciare un ordinamento nascosto; l'elenco si aggiorna
  anche cambiando l'intervallo di anni. Nessun nuovo colore: riuso di `--accento`, `--accento-testo`,
  `--separatore` e delle scale `--fs-*`/`--sp-*` già esistenti. Raccolte, Linea del tempo, grafo e SPARQL non
  toccati.
- **B. ANNO_MASSIMO = 2016, filtro nella pipeline non nei dati**: aggiunta in `grafo_eco/genera_rdf.py` una
  costante unica `ANNO_MASSIMO = 2016` che scarta gli articoli con anno > 2016 appena letti dai CSV, prima di
  costruire il grafo RDF; `genera_dati_sito.py` e gli script collegati (`dati.js`, `grafo_completo_ttl.js`,
  `query_esempio.js`) ereditano il filtro perché leggono dal grafo già filtrato. I CSV di
  `grafo_eco/dati_estratti/` NON sono stati toccati (restano gli originali, con tutti gli articoli): per tornare
  indietro basta cambiare `ANNO_MASSIMO` e rieseguire `genera_rdf.py` → `genera_dati_sito.py` (vedi nota in
  `grafo_eco/dati_estratti/tutto/report_estrazione.txt`).
- **B. 12 articoli esclusi, nessun nodo orfano**: 1 di rivista (JA2214, QUERY, "Conclusioni sul complotto: da
  Popper a Dan Brown", 2017) e 11 di quotidiano fra il 2017 e il 2025 (Corriere della Sera, La Repubblica,
  LaRepubblica.it, QUERY) — numero confermato sui CSV prima di scrivere il codice. Nessuno era ripubblicato in
  volume né richiamato da altre righe (estratti, capitoli, correlazioni, recensioni): nessuna ristampa o estratto
  orfano. Le quattro testate coinvolte conservano tutte almeno un articolo (rispettivamente 1, 70, 210 e 3):
  nessun nodo periodico/quotidiano eliminato — restano 116 riviste e 14 quotidiani, invariati. Le rubriche non
  corrono mai questo rischio (i loro nodi esistono solo fra gli articoli già filtrati).
- **B. Rigenerazione completa**: `dati_rdf/` (ttl, rdf, nt, jsonld), `dati.js`, `grafo_completo_ttl.js`,
  `query_esempio.js` rigenerati da `genera_rdf.py` → `genera_dati_sito.py`. Articoli di rivista 2229→2228, di
  quotidiano 367→356, totale 2596→2584 (116 riviste e 14 quotidiani invariati); 2745 nodi e 3123 archi nel grafo
  del sito. `posizioni_iniziali.js` ricalcolato a convergenza vera con Chromium/Playwright (il Mac di questo
  progetto non può scaricare Chromium: eseguito in una sessione Claude con accesso a un browser, come da
  procedura già descritta per la cartella `grafo_eco/layout_iniziale/`) — vista "tutti" passata da 595 a 583
  nodi (-12, coerente con gli articoli esclusi), vista "ristampe" invariata a 184 nodi (nessuno dei 12 articoli
  esclusi vi compariva). Numeri di Home, Articoli e Documentazione non richiedono modifiche manuali: sono tutti
  calcolati dal vivo dal front-end a partire da `dati.js`, compreso "Intervallo disponibile", ora 1952–2016
  ovunque. Aggiunta una nuova sezione datata in `Opera_Persa_Documentazione_Tecnica.docx` (18.10) e una nota in
  `report_estrazione.txt`.
- **Verifica**: Playwright (console senza errori; nessun avviso di ripiego nel calcolo della disposizione del
  grafo — il precalcolo corrisponde ai dati rigenerati; anno massimo 2016 in Articoli, Linea del tempo e nel
  grafo stesso; nessuna query SPARQL può restituire un anno superiore, il dato non esiste più nel grafo); tutti
  i casi di ordinamento richiesti provati singolarmente: elenco periodici e rubriche nei tre criteri con
  inversione; un periodico con una sola rubrica; un periodico con più rubriche (es. L'Espresso, dove
  data/titolo/rubrica compaiono e periodico no); una rubrica con un solo periodico (solo data/titolo); una
  rubrica con più periodici; "Tutti gli articoli" (tutti e quattro i criteri).

## 2026-10-07 — Palette terracotta, separatori più quieti, segno "ripubblicato" discreto

Richiesto di sostituire l'accento verde-acqua (che accostato al giallo delle ristampe e al blu dei vecchi pulsanti
di Articoli non convinceva) con una terracotta, e di ridurre l'evidenza dei separatori dorati. Lavoro limitato a
`stile.css`; nessuna modifica a dati, grafo, JavaScript, `visualizzazione.html` o `genesi.html`. Backup fatto
prima di modificare (`backup/backup_stile_20261007-1413.css`, più i due HTML della stessa ora).

- **Accento terracotta**: `--accento` #3f7078 → #a8502d (riempimenti, con testo bianco sopra: 5,45:1),
  `--accento-testo` #64a0a8 → #ec9a76 (testo e link su fondo scuro: 6,75-8,27:1 su sfondo e pannelli),
  `--accento-rgb` aggiornata di conseguenza (le sfumature tenui di riga evidenziata/hover ne derivano). Un solo
  accento ovunque, come già deciso; l'alone della Home passa da un grigio-verde (#1f2c2e) a un bruno caldo (#2c1f17).
- **Separatori**: il `--bordo` precedente (#766a4f) aveva una dominante ocra, che accanto all'oro delle ristampe
  creava l'effetto di "tante linee dorate". Ora i bordi di pulsanti, campi e schede sono un marrone neutro
  (`--bordo` #6b6256, 2,5-3,1:1) e le sole linee di separazione fra righe, sezioni e colonne (23 regole
  `border-bottom/top/right`) usano una nuova `--separatore` (#443c33, 1,4-1,7:1), volutamente quieta.
- **Segno "ripubblicato"**: la barra gialla a sinistra di righe e tabelle (`.riga-art`, `.timeline-articolo-voce`,
  `tbody tr` in Raccolte) passa da 3px del giallo pieno a 2px dello stesso giallo al 45% (`--ristampa-segno`,
  nuova, solo interfaccia). `--articolo-rist` resta identica per la legenda e i nodi del grafo.
- **Invariati di proposito**: tutti i colori funzionali del grafo (`--rivista`, `--libro`, `--articolo`,
  `--articolo-rist`, `--cluster`, `--evidenzia*`, `--quotidiano`), i pallini colorati accanto ai titoli di sezione
  e i puntini della Home.
- **Verifica**: lette a schermo, con Chromium, tutte le schermate (Home, grafo, Articoli, Raccolte, Linea del
  tempo, Documentazione, SPARQL) e la cornice di `genesi.html` (barra, sidebar; il grafo di una singola opera non è stato aperto); nessun errore JavaScript (restano solo le richieste ai font
  online, bloccate nell'ambiente di prova); il grafo si apre con la disposizione precalcolata di sempre.

## 2026-10-07 — Design system unificato: stesso linguaggio visivo su tutte le schermate

Richiesto di dare coerenza grafica a tutto il sito (Home, Vista a grafo, Articoli, Raccolte, Linea del tempo,
Documentazione, Interroga/SPARQL, genesi.html): i pulsanti di Articoli erano blu e a tutta larghezza, diversi da
quelli verde-acqua di Raccolte, dalle schede-anno/frecce della Linea del tempo e dalle pillole di SPARQL. Lavoro
limitato a `stile.css`, `visualizzazione.html` e `genesi.html` — nessuna modifica a dati, grafo o JavaScript (vedi
sotto). Backup dei tre file fatto prima di modificarli, con la convenzione d'uso (`backup_<nome>_20261007-1354.<ext>`).

- **Un solo accento in tutto il sito**: eliminate le tre variabili `--accento-tutti`, `--accento-periodico`,
  `--accento-rubrica` (il blu di Articoli) — tutti gli stati selezionato/attivo/hover/focus, su ogni schermata,
  usano ora `--accento` (riempimenti) e una nuova `--accento-testo` (testo e link, variante più chiara per
  restare leggibile su fondo scuro). Il pallino colorato (`.puntino-sezione`) accanto al titolo di ogni
  schermata resta invariato come riferimento di orientamento — è l'unico posto dove compaiono colori diversi
  per sezione.
- **Contrasto verificato per calcolo, non a occhio** (script Python, formula di luminanza relativa WCAG):
  `--accento` usato come colore di testo era circa 3,3:1 sul fondo scuro, sotto la soglia di 4,5:1 richiesta per
  il testo normale. Introdotta `--accento-testo` (stessa tinta, più chiara) per testo/link, lasciando `--accento`
  per i riempimenti con testo bianco sopra. Risultati finali (tutti sopra soglia):
  testo principale su fondo 15,73:1; testo secondario su fondo 7,13:1; testo principale sui pannelli
  12,84-14,20:1; testo secondario sul pannello scuro 5,82:1; `--accento-testo` su fondo/pannelli 5,09-6,24:1;
  testo bianco sul riempimento `--accento` 5,53:1. Il bordo (`--bordo`) è stato schiarito da un valore
  praticamente invisibile (~1,3:1 sui pannelli) a uno chiaramente percepibile (2,82-3,11:1), sufficiente per un
  elemento puramente decorativo/di separazione che non deve soddisfare il rapporto riservato al testo.
- **Scale ridotte in `:root`**: una scala tipografica a 6 livelli (`--fs-titolo-grande` 22px fino a
  `--fs-minuscolo` 11px, nessun carattere sotto 12px per contenuti importanti), una scala di spaziature
  (`--sp-1`…`--sp-6`) e una scala di raggi (`--radius-sm/md/pill`), applicate al posto dei valori in px sparsi
  nel file su titoli, campi di ricerca, pulsanti, tabelle, legenda, schede.
- **Componenti unificati**: pulsante primario/secondario (`.btn`, `.btn-hero`), pillola-filtro con stato attivo
  (fusi in un'unica regola `.btn-edizione, .sparql-esempio-btn` — prima duplicati quasi identici), voce di
  elenco selezionabile, scheda, campo di ricerca, titolo di sezione, tabella: stessa resa su ogni schermata. I
  pulsanti "Modalità" di Articoli (`#schermata-elenco .btn.attivo[data-modo]`) sono stati consolidati da sei
  regole quasi duplicate a una sola basata sull'attributo `data-modo`, già usato dal JavaScript e non toccato.
  Aggiunto uno stato `:focus-visible` coerente (contorno `--accento-testo`, 2px) su tutta la famiglia di
  pulsanti/pillole/schede, per un focus da tastiera sempre visibile e identico ovunque.
- **Colori "funzionali" del grafo non toccati e non più sfruttati per l'interfaccia**: dove un elemento di
  interfaccia riusava una variabile del grafo (`.link-acnp-periodico` e l'hover di `.link-articolo`/
  `#elenco-torna` leggevano `--rivista`; `.avviso` leggeva `--libro`), è stata introdotta una variabile
  separata (`--accento`/`--accento-testo` per i link, una nuova `--avviso` dedicata) invece di cambiare il
  colore del grafo. `--rivista`, `--libro`, `--articolo`, `--articolo-rist`, `--cluster`, `--evidenzia` e le
  altre variabili "funzionali" restano identiche ai valori precedenti.
- **`genesi.html`**: il suo `<style>` locale (forme della legenda, override dei link delle schede, regole di
  `#genesi-vuoto`/`#network`) è stato spostato in `stile.css` in una sezione dedicata — nessuna riga di
  JavaScript toccata, stesso risultato visivo verificato a schermata.
- **Stili inline ripetuti spostati in `stile.css`**: le righe "Anno — anno" di Vista a grafo e Articoli (classe
  `.riga-intervallo-anni`/`.separatore-intervallo` al posto dello style inline ripetuto due volte), i
  `border-bottom:none` di alcune sezioni (classe `.sezione--senza-bordo`), e i due stili inline su
  `#anno-range-label` ed `#elenco-titolo-corrente`, ora in CSS. Nessun id, classe o attributo `data-*` usato dal
  JavaScript è stato rimosso o rinominato (`.attivo`, `.aperta`, `modo-tutti/rivista/rubrica`, `data-tab`,
  `data-modo`, `data-vai`, `data-conteggio` tutti invariati).
- **Dati, grafo e logica non modificati**: `dati.js`, `grafo_completo_ttl.js`, `posizioni_iniziali.js`,
  `query_esempio.js`, `dati_rdf/`, `grafo_eco/`, `sorgenti/` e tutto il JavaScript (query SPARQL, filtri,
  ordinamenti, ricerca, disposizione del grafo) non sono stati toccati. Verificato con Playwright: screenshot
  di tutte le 16 schermate/stati (prima e dopo), zero errori in console in entrambi i casi, nessun avviso di
  ripiego nel calcolo della disposizione del grafo (il precalcolo in `posizioni_iniziali.js` resta allineato ai
  dati), conteggio e posizione dei nodi della Vista a grafo e di genesi.html identici prima e dopo.

## 2026-10-07 — Vista a grafo più affollata del solito: causa e correzione (precalcolo disallineato + disposizione iniziale non riproducibile)

Segnalato che la Vista a grafo, alla "Tutti gli articoli", appariva più affollata e confusa del solito
all'apertura. Diagnosi fatta SENZA modificare nulla (Chromium/Playwright, console, confronto quantitativo), poi
corretta solo dopo aver riportato la causa.

- **Causa principale**: `posizioni_iniziali.js` era stato rigenerato alle 09:58, con i dati di allora (583 nodi
  per la vista "tutti"), ma la correzione delle liste filtro checkbox fatta subito dopo, nella stessa mattinata
  (vedi la voce precedente in questo changelog), ha cambiato quali nodi entrano in quella vista, portandoli a
  595. Il controllo di corrispondenza fra `posizioni_iniziali.js` e i dati attuali (numero di nodi + hash) se n'è
  accorto correttamente e ha fatto scattare, come previsto, il ripiego nel browser (150 iterazioni invece delle
  20000 del precalcolo offline) — ma quel ripiego produce, con centinaia di nodi, un risultato oggettivamente
  più compatto e affollato: misurato, il riquadro occupato dalla disposizione era circa un decimo dell'area di
  un precalcolo a convergenza vera, la distanza media fra un nodo e il suo vicino più prossimo meno della metà
  (77px contro 173-177px), e il 52,6% dei nodi aveva un altro nodo a meno di 60px di distanza (contro lo 0% di
  ogni precalcolo storico confrontato). Non era quindi un'impressione: il sito stava davvero mostrando, in
  silenzio, il meccanismo di ripiego invece di quello preferito.
- **Causa secondaria, indipendente**: `calcolaDisposizione()` non fissava mai `layout.randomSeed`, quindi
  vis-network partiva ogni volta da posizioni iniziali casuali diverse. Misurato: due aperture indipendenti
  della stessa identica pagina, con gli stessi identici dati, spostavano lo stesso nodo in media di oltre
  1000px (fino a 3163px) fra una disposizione finale e l'altra. Non è mai stata la causa dell'affollamento (la
  fisica arriva comunque a un vero equilibrio quando le è permesso), ma spiega perché anche un precalcolo
  corretto e ben assestato cambia comunque aspetto ad ogni rigenerazione, pur senza che i dati cambino.
- **Escluso come causa**: i parametri della fisica (`gravitationalConstant`, `springLength`, `springConstant`,
  `avoidOverlap`, `damping`) e la logica di raggruppamento (`clusterizzaEPrepara`) sono risultati identici,
  confrontando byte per byte `visualizzazione.html` con i backup disponibili (a parte l'unica rinomina già
  documentata di un tipo di arco, non collegata a questo problema).

**Correzione**: aggiunta una costante `SEME_DISPOSIZIONE = 1946`, passata come `layout.randomSeed` nelle opzioni
di `calcolaDisposizione()` in `visualizzazione.html` — un solo punto di modifica che vale sia per il precalcolo
offline sia per il ripiego nel browser, dato che entrambi passano da quella stessa funzione. Nessun altro
parametro toccato. Rigenerato poi `posizioni_iniziali.js` con `precalcola_layout.js` contro i dati attuali:
vista "tutti" ora a 595 nodi (allineata), vista "ristampe" invariata a 184 (era già allineata, non interessata
dalla correzione delle liste filtro). Non si tratta di un difetto nell'ordine dei passi dentro
`precalcola_layout.js` o `genera_dati_sito.py` (quest'ultimo richiama già in automatico il precalcolo ogni volta
che rigenera `dati.js`): il problema è che una modifica fatta a mano al codice di `visualizzazione.html` che
cambia la composizione di una vista, come la correzione delle liste filtro di questa stessa mattinata, non passa
da quello script e quindi non fa scattare da sola una rigenerazione. Aggiunto un avviso esplicito su questo in
`grafo_eco/layout_iniziale/README.md` ("Attenzione — quando NON basta aver rigenerato dati.js").

**Verificato dopo la correzione**: confrontando il nuovo precalcolo con tre versioni storiche a convergenza vera
(24/9 e due del mattino del 7/10), i valori sono praticamente indistinguibili — riquadro occupato 10634×10630
(storici: 9452-10625 di lato), vicino medio 174px (storici: 173-177px), 0% di nodi affollati in tutti i casi,
arco medio 330px (storici: 328-338px). In console: nessun avviso di disallineamento per nessuna delle due viste,
nessun errore. Il grafo resta perfettamente fermo all'apertura (0px di movimento osservato in 2 secondi senza
interazione). Ricerca, filtri rivista/quotidiano/libro, intervallo anni e passaggio "Solo ristampe" verificati
tutti ancora funzionanti, invariati.

**File modificati**: `visualizzazione.html` (backup pre-modifica in `backup/`), `posizioni_iniziali.js`
(rigenerato; il precedente, disallineato, è comunque conservato tra i backup di questa stessa mattinata),
`grafo_eco/layout_iniziale/README.md` (backup pre-modifica in `backup/`; aggiunta la nota sul seme fisso e
l'avviso sul disallineamento silenzioso dopo una modifica al codice).


## 2026-10-07 — il refresh (F5/Cmd+R) resta sulla scheda corrente; la scheda dettagli del grafo sparisce cambiando sezione

Due correzioni distinte in `visualizzazione.html`, segnalate insieme.

- **Refresh**: ricaricare la pagina riportava sempre alla Home, anche stando su "Articoli" o con un
  periodico/libro/articolo aperto - solo il tasto/gesto "indietro" del browser ripristinava correttamente lo
  stato. Causa: il ramo finale dello script, che legge lo stato salvato da "pagehide" in `sessionStorage`
  (`operaPersaStatoTorno`) quando non c'è nessun parametro esplicito nell'indirizzo, controllava solo
  `navEntries[0].type === "back_forward"`, escludendo il caso "reload" dello stesso identico meccanismo -
  `history.state` non si può usare qui perché `history.replaceState({tab:"home"}, "")`, eseguito ad ogni
  caricamento, lo sovrascrive sempre a `{tab:"home"}` prima che questo ramo venga raggiunto: da qui la scelta,
  già presente per "indietro", di leggere da `sessionStorage` invece che da `history.state`. Corretto estendendo
  la condizione anche a `"reload"`: il refresh ora legge lo stesso stato salvato e chiama `ripristinaStato()`
  esattamente come "indietro". Un'apertura nuova (scheda o finestra appena aperta, tipo di navigazione
  "navigate") continua a mostrare la Home come prima; il parametro `?tab=`/`?articolo=`/`?libro=` nell'indirizzo
  resta prioritario su entrambi i meccanismi, invariato.
- **Scheda dettagli nella Vista a grafo**: il pannello `#dettagli` (aperto cliccando un nodo rivista/quotidiano/
  libro/articolo) vive fuori dai contenitori `.schermata` della pagina, quindi non si nascondeva da solo
  cambiando sezione - restava visibile, con l'ultimo nodo cliccato ancora evidenziato nel grafo sottostante,
  anche su "Articoli" o "Raccolte". Corretto in `vaiA(tab)`, il punto unico di cambio schermata (usato da
  `naviga`, `vaiAPeriodico`, `vaiALibro`, `vaiAArticolo`, da "indietro"/"avanti" e dall'apertura via URL): quando
  si lascia la Vista a grafo, il pannello viene nascosto e l'evidenziazione del nodo cliccato spenta
  (`spegniEvidenziazioneClick()`); tornando sul grafo la scheda resta chiusa finché non si clicca di nuovo un
  nodo. Il comportamento della scheda dentro la Vista a grafo (chiusura con la ×, cambio vista Completa/Solo
  ristampe, ricerca) non è stato toccato.

**Verificato** (Chromium/Playwright): refresh su ciascuna delle sei schede (Articoli, Raccolte, Linea del tempo,
Documentazione, Interroga SPARQL, Vista a grafo) resta sulla stessa scheda; refresh con un periodico aperto in
Articoli riapre lo stesso periodico; un'apertura da zero (nuova scheda, nessun parametro nell'indirizzo) mostra
la Home; `?tab=grafo` nell'indirizzo apre direttamente il grafo anche a una nuova apertura. Nella Vista a grafo:
cliccato un nodo la scheda compare, passando ad Articoli sparisce, tornando al grafo resta chiusa, ricliccando un
nodo riappare. Verificato anche che "indietro" da `genesi.html` (aperta nella stessa scheda cliccando "Vai alla
genesi dell'opera" su un libro con più edizioni) continua a riportare al libro di provenienza in Raccolte, come
prima di questa modifica. Nessun errore reale in console.

**File modificati**: `visualizzazione.html` (backup pre-modifica in `backup/`). Verificato che il documento Word
(capitolo 12.4, sul tasto "Indietro") non descrive da nessuna parte il comportamento precedente del refresh:
nessuna correzione necessaria lì.


## 2026-10-07 — liste filtro Rivista/Quotidiano/Libro generate da dati.js invece che scritte a mano (MicroMega e Il Venerdì di Repubblica non apparivano nella Vista a grafo)

**Causa**: i checkbox delle sezioni "Rivista", "Quotidiano", "Libro" sotto "Ricerca più approfondita" (Vista a
grafo) erano scritti a mano nell'HTML invece di essere generati dai dati, esattamente come i contatori "(116)"
"(14)" "(31)" nelle intestazioni delle stesse sezioni e alcuni numeri nella scheda Documentazione. La lista delle
riviste era rimasta a 115 voci (ne mancavano quindi 2): non comprendeva "MicroMega : le ragioni della sinistra" e
"Il Venerdì di Repubblica", le due riviste aggiunte il 7 ottobre con i 17 articoli nuovi (vedi voce precedente).
`applicaVisibilitaEStile()` nasconde dalla Vista a grafo ogni rivista/quotidiano/libro il cui checkbox non risulta
tra quelli selezionati: una rivista assente dalla lista non è mai "selezionata", quindi lei e tutti i suoi articoli
restavano sempre nascosti, qualunque fosse lo stato dei filtri - anche trovandola con il campo Ricerca (la Ricerca
mostra il suggerimento, perché legge `DATI.nodes` direttamente, ma selezionarlo non bastava a farlo comparire nel
grafo, perché il filtro per lista restava a monte). Confermato che il resto del sito non aveva lo stesso problema:
la scheda Articoli costruisce il suo elenco di periodici direttamente dai dati (non da una lista scritta a mano),
quindi mostrava già correttamente le due riviste.

**Correzione**: le tre liste di checkbox sono ora generate a runtime da `DATI.nodes` (stessa struttura/classi di
prima, stesso ordine alfabetico italiano, tutte pre-selezionate come prima), prima di qualunque listener o disegno
del grafo - un nodo rivista/quotidiano/libro aggiunto in futuro comparirà quindi da solo nella lista, senza bisogno
di toccare l'HTML. Lo stesso principio è stato esteso ai numeri scritti a mano trovati nell'audit (vedi sotto):
ora calcolati da `DATI.nodes` tramite `<span data-conteggio="...">`, sul modello già in uso per `#stat-art-riviste`
e per le dimensioni dei file scaricabili. Questo fa sparire da solo anche "L'Espresso (supplemento)", che era
rimasto come checkbox orfano in quella lista (nessun nodo corrispondente nei dati, essendo già stato ricondotto a
"L'Espresso" il 7 ottobre - vedi voce precedente): non è stato quindi rimosso con una modifica a sé, ma generando
le liste dai dati scompare automaticamente, perché assente da `DATI.nodes`. Aggiunte anche le due voci di legenda
che mancavano per i tipi di arco `correlataRivista` e `contieneAppendice` (1 solo arco ciascuno nel grafo attuale,
quindi passati finora inosservati): avevano già uno stile proprio in `stileArco()`, solo la legenda non li citava.

**Audit completo svolto prima di correggere** (confronto a stringa esatta fra `DATI.nodes`/`DATI.edges` e ogni
lista/numero scritto a mano nel sito, come richiesto): nessun'altra lista di checkbox era disallineata (quotidiani
e libri corrispondevano già esattamente, 14 e 31); nessun arco punta a un nodo inesistente, nessun nodo duplicato,
nessun articolo senza rivista/quotidiano, nessun nodo isolato; tutti e 5 i tipi di arco presenti nel grafo
(`partOf`, `isVersionOf`, `estrattoDi`, `correlataRivista`, `contieneAppendice`) hanno già uno stile esplicito in
`stileArco()` (nessuno finisce silenziosamente nel default); l'intervallo dello slider "Anno" nella Vista a grafo e
nella scheda Articoli copre già tutto il dataset (1952–2025), calcolato dai dati e non scritto a mano; il
raggruppamento per anno/rivista nella Vista a grafo copre correttamente tutti gli articoli (nessuno sfugge al
cluster o al nodo singolo); la Ricerca (`CANDIDATI_RICERCA`) è già generata da `DATI.nodes`, quindi già copriva
(e continua a coprire) tutte le riviste/quotidiani/libri, compresi quelli aggiunti oggi; `genesi.html` e
`query_esempio.js` non contengono liste o numeri scritti a mano legati ai dati. `grafo_dati.json` e
`istanze_espresso.ttl` sono stati controllati in parallelo a `dati.js`: nessuna traccia residua di "L'Espresso
(supplemento)" in nessuno dei due, né in alcun CSV, né nel documento Word (a parte le note storiche sulla sua
unificazione, volutamente non toccate).

**Due punti segnalati, non corretti - in attesa di una decisione**:
1. La schermata "Linea del tempo" copre solo gli anni 1952–2016 (`ANNI_TIMELINE`, intervallo scritto a mano con un
   commento che lo giustifica esplicitamente "fino alla morte di Eco"). Il dataset contiene però 12 articoli
   datati dopo il 2016 (`JA2214`, `NA0356`-`NA0366`, 2017-2025: pubblicazioni postume ORIGINALI, non ristampe,
   stesso caso già riconosciuto come eccezione alla regola "dopo il 2016 = ristampa" nella schermata Articoli il
   6-7 ottobre). Questi 12 articoli non sono quindi raggiungibili dalla Linea del tempo, pur comparendo
   correttamente nella Vista a grafo e nella scheda Articoli. Non corretto perché tocca una scelta di raggio
   d'azione dichiarata esplicitamente nel codice, non un semplice disallineamento meccanico.
2. `posizioni_iniziali.js`: era allineato ai dati di oggi SOLO nel senso che era stato calcolato con la stessa
   lista di checkbox ancora incompleta (583 nodi nella vista "tutti"); con le liste ora generate dai dati, la vista
   "tutti" include le due riviste aggiunte e i loro articoli/gruppi (595 nodi) e la disposizione precalcolata non
   corrisponde più (il sito stampa in console l'avviso già previsto per questo caso e ricalcola la disposizione nel
   browser - il sito resta quindi funzionante, solo più lento al primo caricamento di quella vista). La vista "Solo
   ristampe" (184 nodi) non è invece interessata: nessuno dei nuovi articoli ha ristampe o estratti. Non rigenerato:
   in attesa dell'ok esplicito, come richiesto.

**Verificato** (Chromium/Playwright, copia di verifica con la sola libreria vis-network locale, file originale sul
Mac non toccato da questo passaggio): le liste ora contano esattamente 116/14/31 voci, identiche a `DATI.nodes`;
"L'Espresso (supplemento)" assente da ogni lista e da ogni ricerca; MicroMega, Il Venerdì di Repubblica, Liberal e
Alfabeta2 tutti presenti, selezionati e NON nascosti nella Vista a grafo, oltre che trovabili e selezionabili dalla
Ricerca. Test sistematico su tutti i nodi di `DATI`: le 116+14+31 = 161 riviste/quotidiani/libri sono tutti
cercabili (`CANDIDATI_RICERCA`) e tutti visibili a filtri predefiniti (0 mancanti, 0 nascosti); tutti i 2596
articoli sono raggiungibili, singolarmente o come membri di un gruppo-anno visibile (0 irraggiungibili). "Seleziona
tutto"/"Nessuno" e la ricerca per-lista funzionano sulle liste generate; lo slider "Anno" copre 1952–2025; la vista
"Solo ristampe" passa correttamente a 184 nodi e torna a 595 nella vista "Tutti". Nessun errore reale in console
(solo l'avviso atteso su `posizioni_iniziali.js`, punto 2 sopra, e un blocco di rete del tutto estraneo al sito,
dovuto all'ambiente di verifica isolato senza accesso a Google Fonts).

**File modificati**: `visualizzazione.html` (generazione dinamica delle tre liste filtro; contatori e numeri della
scheda Documentazione calcolati da `<span data-conteggio="...">`; due voci di legenda aggiunte), `stile.css` (due
nuove classi CSS per le linee di legenda aggiunte). Backup pre-modifica in `backup/` per entrambi. Nessuna modifica
ai dati (`dati.js`, CSV, TTL), a `estrai_tutto.py`, a `genera_rdf.py`/`genera_dati_sito.py`, a `genesi.html`, a
`query_esempio.js`, né a `posizioni_iniziali.js` (vedi punto 2 sopra).


## 2026-10-07 — tre correzioni: query d'esempio, ricerca, "L'Espresso (supplemento)"

Tre segnalazioni distinte nella stessa richiesta, trattate separatamente qui sotto.

- **Query d'esempio "Articoli di un anno preciso"** (scheda Documentazione, SPARQL): confrontava `?anno` con la
  stringa `"1975"`, ma `prism:publicationDate` è tipizzato `xsd:gYear` (vedi voce precedente) - il confronto di
  tipo falliva silenziosamente e la query restituiva sempre 0 righe, qualunque anno. Corretto aggiungendo il
  prefisso `xsd:` e scrivendo il confronto come `?anno = "1975"^^xsd:gYear`, sia in `query_esempio.js` sia nella
  sua fonte in `genera_dati_sito.py` (altrimenti una rigenerazione futura avrebbe riportato il bug). Verificato:
  la query ora restituisce 40 articoli per il 1975 (prima: 0). Problema preesistente, non introdotto dalla
  revisione di ieri/oggi.
- **Ricerca nella Vista a grafo**: segnalato che digitando "micromega" o i nomi dei nodi aggiunti oggi non
  compariva nulla. Verificato il codice (`mostraSuggerimentiRicerca()`): il confronto è già case-insensitive e,
  testato direttamente sul file appena aggiornato, trova correttamente tutti i nuovi nodi digitando il nome in
  qualunque maiuscole/minuscole - non è stato quindi modificato codice che, alla verifica, già funziona. Causa più
  probabile: il browser aveva in cache la versione di `dati.js` precedente all'aggiornamento di oggi (file locale
  di quasi 3 MB caricato con un semplice `<script src>`, senza alcun meccanismo che forzi il browser a notare che
  è cambiato) - un ricaricamento completo della pagina dovrebbe risolverlo.
- **"L'Espresso (supplemento)"** era rimasta come rivista a sé stante (1 solo articolo, JA0782 "Aiuto! Mi sono
  perduto tra i fogli", 1978), invece di essere ricondotta a "L'Espresso" come già fatto per altre 3 varianti
  dello stesso tipo durante l'estrazione originale (supplementi del 1978, 1980 e 1990). Corretto allo stesso
  modo: rivista di JA0782 cambiata in "L'Espresso" direttamente in `articoli_riviste_tutte.csv` (nessun ID
  rinumerato), `riviste_tutte.csv` rigenerato per intero - L'Espresso passa da 1624 a 1625 articoli, il totale
  delle riviste da 117 a 116. Per non perdere l'informazione che quell'uscita era su un supplemento, il campo
  "numero" dello stesso articolo è stato annotato come "25 (supplemento)" invece di 25 (solo testo nel campo
  esistente: nessuna nuova proprietà RDF né modifica di schema per un caso isolato). Resa durevole anche per una
  futura ri-estrazione completa: aggiunta una quarta voce `"l'espresso (supplemento)"` → `"L'Espresso"` in
  `REDIREZIONI_SPECIALI` (`estrai_tutto.py`).
- Rigenerato con `genera_rdf.py` → `genera_dati_sito.py`; `posizioni_iniziali.js` ricalcolato con Chromium.
  Documentazione aggiornata di conseguenza nella scheda Documentazione del sito e nel documento Word (capitoli
  6.3, 13.3, 17.1): "117 riviste" → "116", "112 delle 117" → "111 delle 116".
- Verificato: 2757 nodi / 3135 archi, 28727 triple identiche nei 4 formati RDF; le 10 query della pipeline e le
  15 query di esempio del sito (compresa quella corretta sopra) tutte eseguite senza errori; "L'Espresso
  (supplemento)" assente da ogni ricerca e da ogni file generato; nessun warning di disallineamento del
  precalcolo della disposizione; nessun errore reale in console.

## 2026-10-07 — 17 articoli nuovi da MicroMega, Il Venerdì di Repubblica, Liberal, Alfabeta2 e La Repubblica

Su richiesta diretta: confrontato il `Dataset UE.xlsx` aggiornato sulla Scrivania (fogli `journal_article` e
`newspaper_article`, con la stessa pulizia di `sheet_to_df()` in `estrai_tutto.py`) con tutti i dati già presenti
sul sito, per titolo e - dove il titolo non bastava a riconoscere la stessa riga - anche per rivista+data o
rivista+numero+anno, per trovare gli articoli non ancora estratti. Trovati 17 articoli nuovi, più del previsto
(si pensava a 2-3 riviste): elenco completo mostrato e portata della modifica confermata prima di procedere.

- **6 articoli su MicroMega : le ragioni della sinistra** (nodo rivista nuovo, non c'era prima) e **4 su Il
  Venerdì di Repubblica** (nodo nuovo anche questo).
- **3 articoli in più su Liberal : un incontro tra cattolici e laici** (nodo già esistente, da 1 a 4 articoli) e
  **3 in più su Alfabeta2** (nodo già esistente, da 1 a 4 articoli).
- **1 articolo in più su La Repubblica** (quotidiano, nodo già esistente, da 216 a 217 articoli).
- Nuovi ID assegnati in append dopo il massimo esistente (`JA2215`-`JA2230`, `NA0367`), **non** per posizione nel
  foglio Excel: nessun ID esistente rinumerato, stessa logica già usata per l'esclusione di `JA2213` del 6
  ottobre. `estrai_tutto.py` non è stato rieseguito (il suo percorso `SRC` resta non aggiornato all'Excel di
  oggi): le righe sono state aggiunte a mano ad `articoli_riviste_tutte.csv`/`articoli_quotidiani_tutti.csv`,
  come già fatto per l'aggiunta del 24 settembre. `riviste_tutte.csv` e `quotidiani_tutti.csv` rigenerati per
  intero dai CSV di dettaglio (tabelle puramente derivate, stessa tecnica già sicura in uso).
- Su richiesta esplicita, **non riportato** il campo "Altre ristampe" ("Bentornata Realtà") per l'articolo
  Alfabeta2 "Ci sono delle cose che non si possono dire. Di un realismo negativo" (2012).
- **3 correzioni di titolo** di articoli già esistenti, emerse durante il confronto (probabilmente corrette da
  Michele nel suo Excel, non nuovi articoli), applicate su richiesta: `JA0895` "Teorema degli 800 colori" →
  "Il teorema degli 800 colori"; `JA0945` "...classification ofsigns" → "...classification of signs" (spazio
  mancante); `JA1556` "Intervento" → "Anno Duemila: ora è il mondo laico a temere l'Apocalisse" (titolo vero al
  posto di un segnaposto generico, rivista Liberal).
- Rigenerato con `genera_rdf.py` → `genera_dati_sito.py`; `posizioni_iniziali.js` ricalcolato in una sessione con
  Chromium (il Mac non ce l'ha) e riportato nella cartella principale.
- **Documentazione aggiornata di conseguenza**: nella scheda Documentazione del sito, "115 riviste" → "117"
  (due punti), "le altre 113" → "le altre 115", "110 delle 115 riviste" (copertura ACNP) → "112 delle 117", e il
  contatore della sezione "Rivista" nella Vista a grafo, "(115)" → "(117)" (era un numero scritto a mano nell'
  HTML, non calcolato: controllato con grep, non c'erano altri punti dello stesso tipo rimasti indietro). I
  conteggi "2214/366 righe grezze" descrivono il foglio Excel di una specifica estrazione passata, non il totale
  attuale: lasciati invariati, come deciso per lo stesso caso il 6 ottobre.
- Verificato: 2758 nodi / 3135 archi (2229 articoli di rivista + 367 di quotidiano, 117 riviste, 14 quotidiani, 31
  libri invariati); 28731 triple, stesso numero esatto nei 4 formati RDF; le 10 query della pipeline e le 15 query
  di esempio del sito tutte eseguite senza errori; nessun warning di disallineamento del precalcolo della
  disposizione; ricerca nella Vista a grafo riconosce correttamente MicroMega e Il Venerdì di Repubblica come
  RIVISTA; nessun errore reale in console su `visualizzazione.html` e `genesi.html` (non toccato, non impattato:
  nessuno dei nuovi articoli ha relazioni di ristampa/estratto).
- **Segnalato, non corretto** (fuori dalla richiesta): la query di esempio "Articoli di un anno preciso" (SPARQL,
  scheda Documentazione) confronta `?anno` con la stringa `"1975"`, ma `prism:publicationDate` è tipizzato
  `xsd:gYear`: il confronto di tipo fallisce silenziosamente e la query restituisce sempre 0 righe, anche
  sull'anno giusto - un problema preesistente, non introdotto da questa modifica.

## 2026-10-06 — Riordino della cartella di progetto: backup in sottocartelle dedicate, sorgenti Excel separate

Su richiesta diretta. Nessun file del sito toccato (`visualizzazione.html`, `genesi.html`, `dati.js`,
`posizioni_iniziali.js`, `grafo_completo_ttl.js`, `query_esempio.js`, `stile.css` restano in radice, caricati
con percorso relativo com'era già) - solo file non referenziati da nessuno script spostati.

- Rimossi i backup ormai superati di `visualizzazione.html` (24-25 settembre: tre dello stesso giorno 24, uno
  del 25) e di `stile.css` (24 settembre): a troppe revisioni di distanza, con le modifiche già interamente
  documentate qui sopra. Rimossa anche `grafo_eco/__pycache__/` (cache Python, si rigenera da sola).
- Tutti i `backup_*` rimasti (di oggi) spostati in una cartella `backup/` dedicata, creata in ognuna delle
  quattro cartelle dove prima si accumulavano mescolati ai file veri: la radice del progetto,
  `grafo_eco/`, `grafo_eco/dati_estratti/`, `grafo_eco/dati_estratti/tutto/`. In quest'ultima, in particolare, i
  backup mescolati ai CSV della pipeline erano un rischio concreto, non solo un disordine: un futuro script che
  elencasse quella cartella per leggere "tutti i CSV" li avrebbe presi per dati veri.
- `Dataset completo.xlsx` e `Indice.xlsx` spostati in una nuova cartella `sorgenti/`: non sono letti da nessuno
  script della pipeline attuale (il riferimento diretto all'Excel è solo in `estrai_tutto.py`, non più eseguito
  di routine - vedi sopra), solo citati per nome in qualche punto di testo, quindi lo spostamento non richiede
  nessuna modifica al codice.
- **Per le prossime sessioni**: i nuovi backup pre-modifica vanno fatti dentro la cartella `backup/` più vicina
  al file toccato (quella della stessa cartella, non quella di radice), non più nella cartella principale
  mescolati ai file attivi.

## 2026-10-06 — Rimosse le frecce sugli archi ristampa/estratto, introdotte per errore nella revisione precedente

Su segnalazione diretta: la revisione di oggi (vedi la voce sopra) aveva aggiunto `arrows:"to"`/`arrows:"from"` ai
due tipi di arco in `stileArco()` (`visualizzazione.html`), senza che fosse richiesto - la direzione era già
leggibile dal tipo di linea (piena arancione = ristampa, tratteggiata = estratto) e non doveva comparire nessun
triangolino. Backup fatto prima della correzione (`backup_visualizzazione_20261006-2236.html`).

- Rimossa la proprietà `arrows` da entrambi i `return` di `stileArco()` (tipi `isVersionOf` ed `estrattoDi`):
  colore, spessore, opacità e tratteggio di ogni tipo di arco restano identici a prima. Verificato con grep
  ("arrows", "arrowStrikethrough", "scaleFactor") che non ci sia nessun altro punto del file - impostazioni
  globali del network, legenda, evidenziazione/ricerca/hover/selezione/trascinamento
  (`applicaVisibilitaEStile`), reti temporanee per il calcolo dell'apertura dei gruppi - che reintroduca una
  freccia, né sugli archi aggregati sul riquadro-anno né su quelli del singolo articolo (entrambi passano dalla
  stessa funzione, quindi un'unica correzione li copre tutti e due).
- Commenti nel codice e legenda riscritti per descrivere la direzione a parole invece che nominare una freccia:
  "Ristampa in volume (dalla rivista al libro)", "Estratto (dal libro alla rivista)".
- `genesi.html` non toccato, come richiesto: lì le frecce restano, scelta volutamente diversa per quella pagina.
- Verificato nel browser (vista completa, "Solo ristampe", ricerca, apertura/chiusura dei riquadri anno): nessun
  `arrows` su nessun arco, colori e tratteggi identici a prima, nessun errore in console.

## 2026-10-06 — Distinzione RISTAMPA/ESTRATTO nei collegamenti libro↔rivista; rimozione della "ristampa articolo→articolo"; esclusione durevole di JA2213

Su richiesta esplicita, con un elenco nominale dei 10 collegamenti coinvolti. Backup fatto prima di ogni modifica:
`backup_visualizzazione_20261006-1611.html`, `backup_genesi_20261006-1611.html`,
`grafo_eco/backup_genera_rdf_20261006-1611.py`, `grafo_eco/backup_genera_dati_sito_20261006-1611.py`,
`grafo_eco/backup_estrai_tutto_20261006-1611.py`, `grafo_eco/backup_ontologia_eco_20261006-1611.ttl`,
`grafo_eco/dati_estratti/backup_estratti_libri_20261006-1611.csv`,
`grafo_eco/dati_estratti/tutto/backup_articoli_riviste_tutte_20261006-1611.csv`,
`grafo_eco/dati_estratti/tutto/backup_riviste_tutte_20261006-1611.csv`,
`grafo_eco/dati_estratti/tutto/backup_report_estrazione_20261006-1611.txt`,
`grafo_eco/dati_estratti/tutto/backup_ristampe_articolo_articolo_20261006-1611.csv`,
`backup_posizioni_iniziali_20261006-1611.js`, `backup_CHANGELOG_20261006-1611.md`,
`backup_Opera_Persa_Documentazione_Tecnica_20261006-1611.docx`.

### Due relazioni libro↔rivista fino a oggi confuse sotto un'unica etichetta "ristampa"
Fino a questa revisione, qualunque collegamento fra un articolo e un libro (`prism:isVersionOf`) veniva mostrato e
descritto allo stesso modo, ma in realtà il corpus contiene due relazioni opposte, già distinguibili nei dati
(`grafo_eco/dati_estratti/estratti_libri.csv`) ma non ancora nel grafo né nei testi del sito:

- **RISTAMPA** (direzione rivista → libro): l'articolo è la versione originale, poi ripubblicata integralmente nel
  libro - il libro è il contenitore. Resta su `prism:isVersionOf`/`eco:notaRistampa`, linea piena arancione, freccia
  verso il libro (`arrows:"to"`), come prima.
- **ESTRATTO** (direzione libro → rivista): il libro è la fonte, l'articolo ne è solo un'anticipazione
  giornalistica uscita prima o intorno alla pubblicazione del libro. Semanticamente l'opposto della ristampa, ma
  finora descritta con le stesse proprietà.

I 10 collegamenti seguenti (articolo de L'Espresso → libro) sono stati identificati come ESTRATTO, tramite un
elenco esplicito e non tramite `eco:tipoLibro` (vedi sotto, caso "Postille"): JA2150→*Storia delle terre e dei
luoghi leggendari*, JA1169→*Il pendolo di Foucault*, JA0849→*Il nome della rosa* (1980), JA1882→*Storia della
bellezza*, JA1971→*Storia della bruttezza*, JA1763→*Baudolino*, JA2064→*Il cimitero di Praga*,
JA1504→*L'isola del giorno prima*, JA1881→*La misteriosa fiamma della regina Loana*,
JA1448→*La ricerca della lingua perfetta nella cultura europea*. Tutti gli altri collegamenti articolo→libro
restano RISTAMPE.

- **Ontologia (`grafo_eco/ontologia_eco.ttl`, v1.2→v1.3)**: due nuove proprietà, `eco:estrattoDi`
  (`rdfs:subPropertyOf dcterms:relation`, dominio `fabio:JournalArticle`, range `fabio:Book`) ed
  `eco:notaEstratto` (`rdfs:subPropertyOf rdfs:comment`) - equivalenti di `prism:isVersionOf`/`eco:notaRistampa`
  per il caso ESTRATTO, perché usare quelle due proprietà anche per un estratto sarebbe semanticamente improprio
  (il libro non è una "versione" dell'articolo, è il contrario). Voce aggiunta allo STORICO VERSIONI.
- **`grafo_eco/genera_rdf.py`**: nuovo insieme esplicito `ESTRATTI_VERI` (i 10 ID sopra, uno per uno, ciascuno
  commentato con il titolo del libro) che decide quali righe di `estratti_libri.csv` producono `eco:estrattoDi`
  invece di `prism:isVersionOf` - una verifica automatica a fine script confronta questo insieme con il CSV e si
  blocca con un errore se smettono di corrispondere. **Caso particolare non toccato**: il libro *Postille a Il
  nome della rosa* (JA0914, da Alfabeta) ha `eco:tipoLibro="estratto"` nei dati, ma è una ristampa integrale in
  volume, non un'anticipazione - per questo NON è nell'elenco `ESTRATTI_VERI` ed è rimasto su `isVersionOf`/
  `eco:notaRistampa`, come richiesto esplicitamente. **Il campo `eco:tipoLibro="estratto"` di quel libro resta
  quindi incoerente con la relazione reale** (segnalato, non corretto, in attesa di decisione).
- **`grafo_eco/genera_dati_sito.py`**: nuovo campo `estratto` sul nodo-articolo (parallelo a `ripubblicato`, ma
  calcolato da `eco:estrattoDi` invece che da `prism:isVersionOf`) e nuovo tipo di arco `estrattoDi` nel grafo.
  **Decisione presa** (tra le scelte lasciate aperte): un articolo-estratto NON conta come "ripubblicato" da
  nessuna parte - non cambia colore del nodo, non compare nella vista "Solo ristampe", non entra nel conteggio
  dei libri con ristampe - perché il libro non lo contiene, lo precede. Due nuove query SPARQL
  (`queries/articoli_estrattodi.rq`, `queries/articoli_note_estratto.rq`), parallele alle esistenti
  `articoli_isversionof.rq`/`articoli_note_ristampa.rq`.

### Visualizzazione: freccia invertita e tratteggiata per gli estratti, in entrambe le pagine
- **`visualizzazione.html`**, `stileArco(type)`: `estrattoDi` disegnato con lo stesso tratteggio e colore già
  usati per la (ora rimossa) "ristampa dello stesso articolo" - `dashes:[5,4]`, `COLORI.articolo_rist` - ma
  freccia verso la rivista (`arrows:"from"`), l'opposto della ristampa. Vale sia sugli archi aggregati sul
  riquadro-anno sia su quelli del singolo articolo, perché entrambi passano per la stessa funzione.
- **`genesi.html`**: stessa distinzione portata nella funzione equivalente `stileArcoConfluenza`, riscritta per
  essere guidata dal tipo di arco reale invece che dal campo `tipo_libro` del libro (che per *Postille* avrebbe
  dato la freccia sbagliata, essendo quel libro classificato "estratto" pur essendo collegato da una vera
  ristampa) - non richiesto esplicitamente, ma necessario perché questa pagina condivide lo stesso modello di dati
  e si sarebbe rotta silenziosamente non appena gli estratti hanno smesso di usare `isVersionOf`. **Limite noto,
  non corretto**: il titolo/sottotitolo della scheda e la legenda di questa pagina restano guidati dal campo
  `tipo_libro` del libro (non dal tipo di arco), quindi per *Postille* mostrano ancora un testo "da estratto"
  anche se la sua unica freccia reale è, correttamente, una ristampa a linea piena - incoerenza minore, puramente
  testuale, segnalata e non corretta in questo giro.
- **Legenda**: "Ristampa in volume (rivista → libro)" ed "Estratto (libro → rivista)" al posto della vecchia
  voce unica "ristampa".
- **Schede**: scheda articolo con "Estratto da:" (parallela a "Ripubblicato in:") e "Nota (estratto):"; scheda
  libro/Raccolte con conteggi separati di articoli-ristampa e articoli-estratto.
- **Conteggio "libri con ristampe" (home, tab Articoli)**: era un numero scritto a mano nel codice ("19"),
  nonostante il resto dello stesso blocco sia esplicitamente calcolato dal grafo per non disallinearsi mai (vedi
  commento in `visualizzazione.html`) - controllato con grep su richiesta esplicita, risultava già sbagliato
  prima di questa modifica (i libri con almeno una vera relazione `isVersionOf`, ristampe ed ex-estratti insieme,
  sono 30, non 19) e ora, separati gli estratti, sono **20**. Sostituito con un calcolo dal vivo
  (`new Set(DATI.edges.filter(...)).size`), come gli altri conteggi dello stesso blocco.

### Eliminata la "ristampa dello stesso articolo" (arco articolo→articolo)
Non più di interesse. Rimosso ovunque: il CSV `grafo_eco/dati_estratti/tutto/ristampe_articolo_articolo.csv` e il
suo caricamento in `genera_rdf.py`; il tipo di arco `ristampaArticolo` in `stileArco`,
`costruisciVistaTutti`/`Ristampe`; i campi `ristampato_come` e i blocchi "Ristampa di:"/"Ristampato anche come:"
nella scheda articolo; la voce di legenda; la sezione "Un caso particolare: la ristampa articolo → articolo" nella
scheda Documentazione; il tooltip "ristampa dell'articolo omonimo"; e il ramo di codice che teneva visibili
entrambi gli articoli della coppia. Rimossa anche una funzione e tre blocchi di codice morto
(`mostraDettagliPerId`, `data-vai-articolo`) che esistevano solo per quella funzionalità.

### Esclusione dell'articolo del 2016 "Che bell'errore!" (JA2213)
Rimosso da ogni nodo, conteggio, esportazione e ricerca, mantenendo l'omonimo articolo del 1985 (JA0947).
**Gli ID `JA####` non sono stati ricalcolati** (dipendono dalla posizione della riga nell'Excel originale, usata
come riferimento incrociato - vedi la voce del 24/09 "Fase 4"): la riga è stata solo rimossa da
`articoli_riviste_tutte.csv`, con `riviste_tutte.csv` (conteggio L'Espresso: 1625→1624) e `report_estrazione.txt`
aggiornati di conseguenza. Gli Excel originali (`Dataset completo.xlsx`, `Indice.xlsx`) non sono stati toccati.
Per rendere l'esclusione durevole a una futura ri-estrazione, `grafo_eco/estrai_tutto.py` ha ora un insieme
esplicito e commentato `ID_ARTICOLI_ESCLUSI = {"JA2213"}`, applicato *dopo* l'assegnazione degli ID (non prima, per
non spostare la posizione - e quindi l'ID - delle righe successive).

### Conteggi scritti a mano, controllati con grep (non a memoria) e aggiornati
Articoli totali 2580→2579, articoli di rivista 2214→2213 (quest'ultimo compare anche, correttamente invariato,
come "2214 righe grezze" nella sezione Documentazione che descrive il foglio Excel originale - quello non va
aggiornato, perché la riga esiste ancora nell'Excel, è solo esclusa in estrazione); conteggio "libri con ristampe"
19→20 (vedi sopra - un numero già sbagliato prima di questa modifica, non introdotto da essa).

### Rigenerazione e verifica
Rigenerato con `genera_rdf.py` poi `genera_dati_sito.py`, come da procedura. `posizioni_iniziali.js` è stato
ricalcolato (il Mac non ha Chromium per Playwright: calcolo eseguito in una sessione Claude con accesso a un
browser, come già fatto il 24/09, e il file risultante riportato nella cartella principale) - 579 nodi nella
vista "tutti", 184 in "solo ristampe".

Controlli eseguiti: 2739 nodi/3118 archi nel grafo (2579 articoli, 115 riviste, 14 quotidiani, 31 libri: 19
raccolte + 12 estratto, invariati); 28574 triple, stesso numero esatto nei 4 formati RDF
(`dati_rdf/grafo_completo.ttl`/`.nt`/`.rdf`/`.jsonld`, verificato con `rdflib`, non solo dal log dello script); 10
`eco:estrattoDi` (esattamente i 10 ID richiesti, nessuno in più/meno) e 527 `prism:isVersionOf`; tutte le 10 query
della pipeline (`grafo_eco/queries/*.rq`) e tutte le 15 query di esempio del sito (`query_esempio.js`) eseguite
senza errori; `JA2213` assente da ogni file generato (grep su tutto il progetto, zero risultati); nessun errore
reale in console su `visualizzazione.html` e `genesi.html` (solo un fetch di Google Fonts bloccato dalla rete
dell'ambiente di test, non un difetto del sito); frecce verificate nella direzione giusta per ristampa ed estratto,
sia aggregate sul riquadro-anno sia sul singolo articolo, in entrambe le pagine.

### Metadati e testi
Corretti tutti i punti trovati con grep su "ristamp"/"ripubblicat"/"isVersionOf" in `visualizzazione.html`,
`genesi.html`, `genera_dati_sito.py`, `genera_rdf.py`, `ontologia_eco.ttl` e nei CSV, per usare la parola
"estratto" dove si tratta davvero di un estratto (non più una generica "ristampa"): legenda, tooltip, schede
articolo/libro/Raccolte, scheda Documentazione, spiegazioni delle query SPARQL di esempio.

## 2026-09-25 — Riscrittura del trascinamento e dell'apertura dei gruppi per anno, con fisica elastica locale condivisa

Due giri di lavoro consecutivi sullo stesso meccanismo, documentati qui insieme perché il secondo riusa
direttamente il codice introdotto dal primo. Backup di `visualizzazione.html` fatto prima di ciascuna modifica
(`backup_visualizzazione_20260924-2259.html` e `backup_visualizzazione_20260925-0021.html`).

### Giro 1 — Trascinamento: da "vicini diretti" a una vera simulazione elastica locale
Su segnalazione diretta: il trascinamento precedente (vedi "Riscrittura — Disposizione e interazione del grafo" del
24/09) faceva reagire i soli vicini diretti del nodo trascinato, senza tenere conto di ciò che li circondava -
risultato non sempre naturale, in particolare per nodi con pochi collegamenti.

- **Nuova "zona attiva"** (`calcolaZonaAttiva`): il nodo trascinato e i suoi vicini diretti (**zona**, liberi di
  muoversi) più i vicini dei vicini (**ancoraggio**, fermi ma agenti: esercitano comunque la loro attrazione o
  repulsione, così la zona non si assesta "nel vuoto"). Solo fra i nodi attualmente visibili, quindi il
  comportamento è identico sotto qualunque filtro o ricerca.
- **Fisica dedicata al trascinamento** (`OPZIONI_FISICA_TRASCINAMENTO`): stesse costanti di forza della
  disposizione iniziale (`gravitationalConstant`, `springLength`, `springConstant`, `avoidOverlap`), con
  `centralGravity:0` (la zona non deve mai essere tirata verso il centro del canvas) e un damping scelto con prove
  reali nel browser per un assestamento morbido, senza rimbalzi, entro un secondo e mezzo-due secondi dal rilascio
  (`LIMITE_ASSESTAMENTO_MS`, rete di sicurezza indipendente dal criterio di "fermo").
- **Criterio di "fermo"** (`SOGLIA_PX_FERMO`/`CONTROLLI_FERMO_DI_SEGUITO`): la zona si considera assestata quando lo
  spostamento massimo, controllato ogni 90ms, resta sotto una soglia minima per due controlli di seguito; a quel
  punto la fisica si spegne di nuovo e tutto torna esattamente com'era (`physics:false`) salvo le nuove coordinate.
- **Verifica**: battuta con una nuova batteria di test automatici (posizioni lette con `network.getPositions()`,
  non impressione visiva): rapporto fra distanza media finale e iniziale sempre in un intervallo ragionevole (0,93
  nel caso di prova) dopo trascinamenti sia piccoli sia grandi, nessun collasso su un punto né disposizione a
  cerchio geometrico perfetto, nessun nodo estraneo alla zona mosso, posizioni identiche a 2s e a 5s dal rilascio,
  nessun timer residuo dopo l'assestamento. Verificato anche con `REATTIVITA_LOCALE` disattivato: il trascinamento
  torna a muovere solo il nodo trascinato, come prima di questa funzionalità.

### Giro 2 — Apertura di un gruppo per anno: dalla corona geometrica alla stessa fisica del trascinamento
Su segnalazione diretta (con screenshot): il doppio clic su un riquadro anno disponeva gli articoli su una
"corona" (un cerchio) intorno alla rivista/quotidiano - una disposizione geometrica imposta, non la posizione
naturale che la fisica stessa avrebbe scelto, visibile anche solo toccando la rivista subito dopo l'apertura (gli
articoli si "aggiustavano" in una disposizione diversa, più naturale).

- **Rimosso il vecchio sistema a corona** (`calcolaPosizioniCoronaRivista`, `ricalcolaCoronaRivista`,
  `posizioneLibroSeVisibile`) e il vecchio "srotolamento" a tempo fisso (`DURATA_APERTURA_MS` usato solo per questo):
  un solo sistema resta in uso per aprire un gruppo, non due in parallelo.
- **Apertura basata sulla stessa zona attiva del trascinamento** (`ricalcolaMembriApertiRivista`), con la sola
  differenza che la rivista/quotidiano resta fermo invece di seguire il mouse: stesse ancore esterne (compreso un
  eventuale libro collegato a un singolo articolo del gruppo, che così esercita davvero la sua attrazione), stessa
  massa e dimensione reale di ciascun nodo (`styleNodo`) passate al calcolo.
- **Calcolo invisibile, non dal vivo**: a differenza del trascinamento (che deve rispondere in tempo reale sotto il
  mouse), l'apertura calcola la posizione finale su una rete `vis-network` temporanea fuori schermo, usando la
  stessa fisica e lo stesso criterio di "fermo" del trascinamento (non il calcolo a convergenza usato per la
  disposizione iniziale, pensato per un caso diverso) - poi anima tutti gli articoli con un unico movimento morbido
  fino a quella posizione (`animaNodiVerso`), mai attraverso un anello o una corona intermedi. Gli articoli
  compaiono inizialmente vicino al riquadro, con un piccolo sparpagliamento deterministico calcolato dal loro id
  (`sparpagliamentoDeterministico`) così da non comparire mai esattamente sovrapposti.
- **Due bug reali corretti durante lo sviluppo**, entrambi scoperti confrontando il calcolo invisibile con quello
  (già approvato) del trascinamento sullo stesso caso: (1) al calcolo invisibile mancavano massa e dimensione reali
  dei nodi (tutti trattati come uguali), che cambiano l'equilibrio calcolato da barnesHut/avoidOverlap; (2) le
  ancore esterne venivano cercate solo intorno alla rivista, mai intorno ai singoli articoli del gruppo, perdendo
  così un eventuale libro collegato a un solo articolo.
- **Chiusura**: doppio clic sulla rivista/quotidiano richiude tutti i suoi gruppi aperti, con un movimento morbido
  di rientro nel riquadro (non una dissolvenza) - scelta per affidabilità: il movimento di rientro riusa lo stesso
  meccanismo di animazione già usato e verificato per l'apertura, mentre una dissolvenza avrebbe richiesto un
  nuovo calcolo di trasparenza mai provato.
- **Verifica**: nessuna fase ad anello durante l'apertura (deviazione standard delle distanze dalla rivista sempre
  ampia, mai vicina a zero); un semplice clic sulla rivista subito dopo l'apertura non sposta nulla (0px, in ogni
  scenario provato: grafo completo, ricerca, riviste con pochi o molti collegamenti); distanza dalla rivista agli
  articoli aperti paragonabile a quella verso gli altri riquadri anno; nessuna sovrapposizione fra articoli;
  articoli con libro collegato attratti naturalmente verso di esso; posizioni identiche a 2s e a 5s dall'apertura;
  apertura di più gruppi della stessa rivista in sequenza (fino a 110 articoli contemporaneamente in un caso di
  prova) e chiusura completa, senza sovrapposizioni né errori; stessa apertura ripetuta due volte (dopo una
  chiusura) con risultato identico; nessun errore in console; l'intera batteria di regressione generale del sito
  (caricamento, click, zoom, filtri, ricerca, pulsanti, cambio scheda, schermo stretto) rieseguita senza errori;
  trascinamento invariato, riverificato con la stessa batteria del Giro 1 con risultati numericamente identici.
- **Limite noto, non risolto in questo giro**: un vero trascinamento (non un semplice clic) della rivista, subito
  dopo l'apertura di un gruppo molto numeroso e con pochi altri collegamenti reali intorno ad essa, può talvolta
  causare un riassestamento più visibile del previsto. Verificato a fondo che non è un difetto del calcolo di
  apertura in sé (il calcolo invisibile è perfettamente coerente con se stesso: ripetuto sulla stessa posizione,
  senza alcuna perturbazione, dà lo stesso risultato al pixel) ma una sensibilità del meccanismo di trascinamento
  introdotto nel Giro 1, di fronte a una zona con molti nodi simili e poche ancore esterne reali - riscontrata,
  in forma più lieve, anche trascinando (non solo aprendo) una rivista molto connessa senza alcun gruppo aperto.
  Su indicazione esplicita, si è scelto di non intervenire sul trascinamento per risolverlo in questo giro; il
  semplice clic (senza trascinare) resta sempre affidabile per verificare che una zona sia già assestata.

## 2026-09-24 — Fasi 1–3 della revisione per solidità scientifica (FAIR, trasparenza, riproducibilità)

Backup completo pre-modifica: `Opera Persa – backup prima di SPARQL.zip` sulla Scrivania.

### Fase 1 — SPARQL come base della visualizzazione
- La generazione dei dati del sito non legge più il grafo RDF "a mano" (chiamate dirette `g.subjects`/`g.value`/`g.objects`
  di rdflib): usa query SPARQL vere e proprie, salvate come file `.rq` commentati in italiano in `grafo_eco/queries/`.
- Nuovo script unico `grafo_eco/genera_dati_sito.py`, che sostituisce `genera_visualizzazione.py` +
  `genera_esportazioni.py` (rimasti nella cartella solo come riferimento storico, non più da eseguire — verranno rimossi
  in Fase 5 con conferma esplicita): un solo comando rigenera `dati.js`, le esportazioni in `dati_rdf/`, il grafo
  incorporato per la sezione SPARQL e le statistiche live del dataset.
- Verificato che l'output (nodi/archi del grafo di visualizzazione) è identico, come insieme, a quello prodotto dalla
  pipeline precedente: nessuna differenza.

### Fase 2 — Interrogazione SPARQL nel sito
- Nuova scheda "Interroga (SPARQL)" in `visualizzazione.html`: query SPARQL scritte ed eseguite direttamente nel
  browser (motore [Oxigraph](https://github.com/oxigraph/oxigraph) via WebAssembly, da CDN jsDelivr, versione 0.5.11
  fissata), sull'intero grafo incorporato nella pagina — nessun server, nessun dato che lascia il computer del
  visitatore.
- 13 query di esempio cliccabili: le 8 query della pipeline (testo identico ai file `.rq`) più 5 query pensate per chi
  non conosce SPARQL, ciascuna con una spiegazione in linguaggio semplice.
- Risultati in tabella, scaricabili in CSV.
- Verifica: le 13 query sono state eseguite con Oxigraph (Node.js) contro il grafo completo attuale, confermando che
  producono righe e nomi di colonna corretti nell'ordine atteso.

### Fase 3 — Solidità scientifica (parziale: la parte legata alla pubblicazione è stata rimandata su richiesta)
- Nuova sezione "Fonti, criteri di selezione, completezza e limiti del corpus" nella scheda Documentazione: criteri di
  inclusione delle raccolte, normalizzazione dei nomi di testate, punteggio di affidabilità delle ristampe rilevate
  automaticamente, dati ricostruiti da un'anomalia di Excel, note editoriali escluse dalla ricerca automatica — tutto
  ricostruito dai file di lavoro in `grafo_eco/dati_estratti/`.
- Metadati di dataset in VoID/DCAT aggiunti a `ontologia_eco.ttl` (titolo, descrizione, data, versione, vocabolari
  usati). `dcterms:license` e `dcterms:creator` (nome da confermare) restano deliberatamente incompleti: la scelta
  finale è rimandata alla pubblicazione.
- Sezione "Come citare e licenza" aggiunta come segnaposto esplicito, da completare alla pubblicazione.
- Ontologia aggiornata a v1.2 (era v1.1 del 15/09/2026).
- **Rimandato su richiesta esplicita** (non necessario finché il progetto non viene pubblicato): dominio definitivo
  per gli URI al posto di `example.org`, scelta della licenza, testo esatto della citazione.
- **Ancora da fare**: piano di collegamento a Wikidata/VIAF/SBN con prova su un sottoinsieme (proposto separatamente).

### Fase 4 — Controlli e caccia ai bug
- **Bug di completezza scoperto e corretto**: il file Excel di partenza ("Dataset completo.xlsx") era stato
  aggiornato dopo l'ultima estrazione dei dati, con 12 articoli mai estratti (11 di quotidiano, 1 di rivista) e
  1 titolo corretto nel frattempo ("tigra" → "tigre", refuso). Scoperto durante il controllo a campione richiesto
  in questa fase, confrontando righe del sito con l'Excel.
- **Perché non si è rieseguita semplicemente l'estrazione**: gli ID degli articoli (`JA####`/`NA####`, usati come
  riferimento in diversi file di lavoro curati a mano) sono assegnati in base alla posizione della riga nel foglio
  Excel. Le 11 righe di quotidiano mancanti non erano in fondo al foglio ma sparse al suo interno: una
  riesecuzione completa avrebbe spostato l'ID di quasi tutti i 355 articoli di quotidiano già estratti,
  invalidando in silenzio i riferimenti incrociati esistenti. Verificato riga per riga che questo non sarebbe
  successo per le riviste (dove la riga nuova era l'ultima del foglio) ma sarebbe successo per i quotidiani.
  Applicata quindi una correzione mirata (non una nuova esecuzione): i 12 articoli mancanti sono stati aggiunti
  con nuovi ID in coda (`NA0356`-`NA0366`, `JA2214`), senza toccare nessuno dei 2568 ID già assegnati. Script e
  log completi in `grafo_eco/dati_estratti/tutto/correggi_estrazione_2026-09-24.py` e nella nota aggiunta a
  `report_estrazione.txt`.
- **Bug indipendente scoperto durante la correzione**: le tabelle di riepilogo `riviste_tutte.csv` e
  `quotidiani_tutti.csv` (conteggio articoli per testata, usato anche nella generazione RDF) riportavano già,
  prima di oggi, un conteggio errato per la rivista QUERY (2 invece di 1) - causa non nota, indipendente dalle
  righe mancanti. Corretto rigenerando per intero le due tabelle dai CSV di dettaglio (sono aggregati puri, senza
  curazione manuale, quindi sicuro).
- Rieseguita la pipeline completa (`genera_rdf.py` → `genera_dati_sito.py`) con i dati corretti: dataset ora a
  2580 articoli (2214 di rivista + 366 di quotidiano, invariate le 115 riviste e i 14 quotidiani distinti),
  28.567 triple totali. Riverificate tutte le 13 query di esempio della scheda SPARQL con Oxigraph (Node.js):
  tutte corrette. Riverificati tutti i formati di esportazione RDF (.ttl, .nt, .rdf, .jsonld): stesso numero di
  triple in tutti e quattro, nessun errore di parsing.
- **Bug di visualizzazione scoperto e corretto**: alcuni conteggi del sito (numero di articoli in home e nella
  scheda Articoli, numero di articoli su riviste/quotidiani nella scheda Documentazione) erano scritti a mano
  nell'HTML invece di essere calcolati dal grafo - lo stesso rischio di disallineamento già corretto in Fase 2
  per il conteggio delle triple. Ora sono calcolati dinamicamente dal grafo al caricamento della pagina, cosa che
  ha anche risolto il loro disallineamento (mostravano ancora 2568 articoli invece di 2580). Stessa correzione applicata alle dimensioni dei 6 file scaricabili nella scheda Documentazione (erano scritte a mano e già imprecise prima di oggi): ora calcolate da `genera_dati_sito.py` al momento della generazione.
- **Bug di validità HTML scoperto durante la correzione precedente (non causato da essa)**: nel correggere questi
  conteggi, il nuovo elemento ha rischiato una collisione con un `id` HTML già in uso altrove nella pagina (il
  contatore dei risultati filtrati nella scheda Articoli) - evitata rinominando l'elemento nuovo. Notato per
  completezza anche un secondo `id` duplicato preesistente e non correlato (`elenco-sidebar`, condiviso
  deliberatamente fra le schede Articoli e Raccolte per riutilizzare lo stesso stile, come documentato in un
  commento in `stile.css`): non modificato, perché non causa problemi funzionali e non è nato da queste modifiche.
- Controlli ancora in corso: schermate del sito su schermo stretto/mobile, assenza di errori in console,
  funzionamento interattivo di grafo/filtri/schede di dettaglio/download - bloccati in questo ambiente dalla
  mancanza di un browser realmente funzionante (vedi nota a parte).

### Fase 5 — Pulizia della cartella
Eliminati, dopo conferma esplicita ed elenco completo mostrato prima:
- 5 script superati (`genera_visualizzazione.py`, `genera_esportazioni.py`, `costruisci_html.py`,
  `estrai_dati.py`, `estrai_espresso.py`), sostituiti dalla pipeline unica `genera_dati_sito.py` e da
  `estrai_tutto.py`.
- 10 file CSV/log superati in `dati_estratti/` (versioni vecchie già sostituite da quelle in `tutto/`, o
  orfani non più letti da nessuno script) e l'intera cartella `dati_estratti/prova_espresso/` (prova iniziale
  limitata a L'Espresso).
- `ontologia_eco-graph.html`: non risultava collegato né dal sito né da nessuno script - confermato superfluo
  e rimosso (compresa la copia duplicata in `Claude outputs/`).
- Cartelle di scarto/rigenerabili: `grafo_eco/__pycache__/`, `grafo_eco/layout_iniziale/node_modules/`,
  `_to_delete/`, `_backup_2026-09-24/` (superata dal backup verificato sulla Scrivania), `Claude outputs/`.
- Rimossi anche alcuni file di debug lasciati per errore sulla Scrivania (fuori da questa cartella) durante
  il test del backup di Fase 0.
Non toccati (motivo non chiaro/da confermare): `Indice.xlsx` (non usato da nessuno script, probabile file
personale) e `posizioni_iniziali.js` con lo strumento che lo genera (`grafo_eco/layout_iniziale/`, esclusi i
`node_modules` già rimossi) - funzionalità di ottimizzazione del caricamento del grafo che risulta scritta ma
non collegata da nessuna parte in `visualizzazione.html`.
Rieseguita l'intera pipeline dopo la pulizia: stessi risultati di prima (28.567 triple, stessi conteggi),
nessuna rottura.

### Ritocco — Stabilità del grafo interattivo
Su segnalazione diretta: il grafo restava percepibilmente "mobile" anche dopo l'assestamento iniziale (in
particolare riaprendo la vista o cambiando filtro). Alzato il valore di `damping` nella fisica del grafo da 0.65
a 0.85 (unico parametro toccato, nessun altro cambiamento): dissipa l'energia residua più in fretta, quindi il
grafo si ferma prima, senza modificare la disposizione finale, la distanza fra i nodi o la risposta al
trascinamento - solo il tempo per cui resta visibile un residuo di movimento.

### Bug corretto — Il filtro anni non funzionava nella vista "Solo ristampe"
Su segnalazione diretta: cambiando l'intervallo di anni nella vista a grafo, il filtro funzionava solo per
"Tutti gli articoli" e non per "Solo ristampe" - la funzione che costruisce quella vista
(`costruisciVistaRistampe`) non leggeva mai l'intervallo scelto. Corretto applicando lo stesso trattamento già
usato in "Tutti gli articoli", inclusi gli stessi due casi limite già gestiti lì: la coppia di ristampa
articolo→articolo (es. "Che bell'errore!", 1985 e 2016) resta visibile se almeno uno dei due anni è
nell'intervallo scelto, e un libro/rivista senza nessun articolo incluso nell'intervallo non resta più come
nodo isolato. Verificato con una simulazione della funzione contro i dati reali: nessun articolo fuori
dall'intervallo scelto compare più, ed entrambi i casi limite si comportano come previsto.

### Fase 6 — Nuova documentazione tecnica, in linguaggio non tecnico
Riscritta integralmente `Opera_Persa_Documentazione_Tecnica.docx` (19 capitoli), a sostituzione della precedente
`Opera_Persa_Documentazione_Tecnica copia 2.docx`: struttura della cartella, flusso RDF -> SPARQL -> dati del
sito, come rigenerare il sito da zero, ontologia e vocabolari riusati, elenco e spiegazione di tutte le query
(comprese le 5 pensate per chi non conosce SPARQL), la nuova sezione SPARQL nel sito, criteri di solidità
scientifica, stato di licenza/citazione, risultati dei controlli con i casi reali trovati, changelog. Corrette
nella nuova versione due imprecisioni ereditate dal documento precedente: il numero di libri nel grafo (31
`fabio:Book` - 19 raccolte + 12 anticipazioni - non 19) e il vocabolario usato per i link ACNP delle riviste
(`rdfs:seeAlso`, non `owl:sameAs`, verificato con una query SPARQL diretta sul grafo). Aggiornata per coerenza
anche la sezione "Struttura dei dati" della documentazione integrata nel sito, che riportava lo stesso conteggio
di 19 libri senza le 12 anticipazioni. Pipeline (28.567 triple, 2.580 articoli, 115 riviste, 14 quotidiani, 31
libri) riverificata identica dopo questa modifica, che ha toccato solo testo e non dati.

### Ritocco — Limite massimo di 5 secondi all'assestamento del grafo
Su segnalazione diretta: pur con il damping già alzato (vedi sopra), il grafo poteva restare percepibilmente
in movimento più a lungo del previsto in alcuni casi (viste con molti nodi, filtri cambiati di frequente).
Aggiunta una rete di sicurezza indipendente dai parametri della fisica: da quando il grafo torna visibile (dopo
un caricamento o un cambio di vista/filtro) o da quando un nodo trascinato viene rilasciato, un timer di 5
secondi chiama `network.stopSimulation()` se per allora il movimento non si fosse già esaurito da solo. Non
disattiva la fisica (resta sempre accesa, come da principio già in uso - vedi il commento "LA FISICA E' SEMPRE
ACCESA" nel codice): si limita a garantire un tetto massimo, e riparte automaticamente da sola alla perturbazione
successiva. Ogni nuova perturbazione riazzera il conto alla rovescia. Non tocca nessuno dei parametri della
fisica (damping, springLength, gravitationalConstant, ecc.), quindi non cambia né la disposizione finale né il
comportamento durante il trascinamento.

### Pilota — Collegamento a Wikidata per le riviste principali
Primo esperimento (non ancora esteso a tutto il grafo) del collegamento a Wikidata proposto in Fase 3: le 20
riviste con più articoli nel grafo sono state cercate su Wikidata (ricerca per nome, poi verifica manuale di
ciascun candidato - descrizione, tipo/P31, eventuali alias) e collegate con `rdfs:seeAlso` solo quando il
candidato era inequivocabile: 9 collegate (L'Espresso, Rivista di estetica, Il Verri, Marcatré, Alfabeta,
Radiocorriere TV, Noi Donne, Il Menabò, Archivio di filosofia), 11 scartate perché senza risultati pertinenti,
di tipo sbagliato (es. "Pirelli" e "SIPRA" trovano l'azienda, non la rivista; "Quindici" e "Filosofia" trovano
un numero/un comune e la disciplina filosofica, non la rivista) o ambigue (due voci Wikidata quasi identiche per
"Lettere Italiane"). Dettaglio completo, comprese le 11 scartate e il motivo di ciascun scarto, in
`grafo_eco/dati_estratti/wikidata_riviste_pilota.csv`: lo stesso file, filtrato sulla colonna `esito`, e' letto
direttamente da `genera_rdf.py`, che aggiunge i 9 collegamenti confermati a ogni esecuzione della pipeline.
Corretto durante questo lavoro un bug scoperto nel farlo: `riviste.rq` aveva un solo `OPTIONAL` generico per
`?link`, che con due `rdfs:seeAlso` sulla stessa rivista (ACNP + Wikidata) restituiva due righe invece di una,
facendo perdere in silenzio uno dei due link nella pagina (`add_node` scarta la riga duplicata). Corretto con due
`OPTIONAL` distinti, ciascuno filtrato sul dominio atteso (`acnpsearch.unibo.it` / `wikidata.org`); aggiunto un
nuovo campo `linkWikidata`, mostrato accanto al link ACNP sia nel pannello dettagli del grafo sia nell'elenco
"Per periodico". Verificato che tutte le 115 riviste hanno ancora il loro link ACNP originale (110, invariato) e
che le 9 con Wikidata hanno ora entrambi i link, non uno al posto dell'altro. Aggiunta anche la sezione
"Collegamento a Wikidata: un pilota, non ancora esteso a tutto" alla documentazione integrata nel sito (scheda
Documentazione), con lo stesso contenuto già riportato qui e nel capitolo 17.1 della documentazione Word.

### Riscrittura — Disposizione e interazione del grafo, per una stabilità totale
Riscrittura completa del meccanismo che dispone e fa reagire il grafo interattivo, su segnalazione diretta di
un comportamento non voluto: con la fisica sempre accesa (vedi sopra, "Ritocco — Limite massimo di 5 secondi"),
un semplice clic, un filtro, un cambio di scheda o l'apertura di un pannello di dettaglio potevano far muovere
leggermente qualche nodo - corretto ma non prevedibile per chi si aspetta un grafo stabile una volta disposto.
Il vecchio meccanismo a fisica-sempre-accesa (incluso il timer di sicurezza dei 5 secondi, il "trucco della
massa" sui nodi rilasciati e i gestori d'evento che decidevano quando la fisica fosse "pronta") è stato rimosso
per intero e sostituito con uno più semplice:

- **Disposizione calcolata una volta sola, fuori schermo.** All'apertura della pagina, una rete `vis-network`
  temporanea e invisibile (mai mostrata) calcola la disposizione con la fisica accesa; le coordinate risultanti
  vengono lette con `getPositions()` e assegnate ai nodi della rete vera, che nasce già con la fisica spenta
  (`physics:false`) e non la riaccende mai più, per nessun motivo. Usare la stessa identica libreria per calcolo
  e visualizzazione (invece di uno strumento diverso, come il tentativo con d3-force in `layout_iniziale/`, mai
  agganciato e ora concettualmente superato) elimina il rischio di un "salto di correzione" quando le due
  simulazioni non coincidono esattamente.
- **Iterazioni di assestamento ridotte da 500 a 150** (tempo di apertura del grafo: circa 2-2,5 secondi, prima
  7-9), con una disposizione verificata praticamente indistinguibile a vista.
- **Due nuovi pulsanti nella vista a grafo**: "Ripristina disposizione" (torna alla disposizione calcolata,
  annullando i trascinamenti manuali) e "Centra" (inquadra tutti i nodi visibili senza spostare nulla).
- **Filtri e ricerca riscritti** per non ricalcolare mai la disposizione: si limitano a mostrare/nascondere
  (proprietà `hidden`) e a colorare i nodi già posizionati. Quando una ricerca seleziona solo alcuni articoli
  dentro un gruppo di ristampe raggruppato in un unico cerchio, il cerchio resta visibile finché contiene almeno
  un risultato, con lo stile del risultato più pertinente al suo interno - il numero mostrato sul cerchio resta
  quello del gruppo intero, una scelta di semplicità dichiarata esplicitamente.
- **Nuova funzionalità opzionale, attiva** (interruttore unico nel codice, `REATTIVITA_LOCALE`): quando si
  trascina un nodo, solo i suoi vicini diretti (collegati da un arco) reagiscono per un istante e poi si fermano
  da soli in meno di un secondo; il resto del grafo non si muove mai. Disattivata automaticamente per i
  pochissimi nodi con più di 40 vicini diretti visibili (`SOGLIA_GRADO_REATTIVITA`), per non trascinare
  visibilmente metà grafo insieme a un solo nodo. Durante lo sviluppo è stato trovato e corretto un bug reale di
  vis-network: un nodo senza la proprietà `physics` esplicita ha di default `physics:true`, quindi alla prima
  riaccensione della fisica globale (necessaria per questa funzionalità) tutti i ~578 nodi senza quella proprietà
  esplicita si mettevano in movimento invece dei soli vicini diretti - corretto impostando `physics:false` in
  modo esplicito su ogni nodo.
- **Verifica**: battuta con una batteria di test automatici in un vero browser (lettura diretta delle coordinate
  dei nodi con `network.getPositions()`, non solo impressione visiva), ripetuta più volte con ricariche della
  pagina: tempo di apertura e stabilità delle posizioni a 1s/5s/30s; nessun movimento su 10 click; trascinamento
  di 5 nodi, ognuno resta esattamente dove rilasciato; nessun movimento su zoom/pan/doppio-clic-sfondo/apertura e
  chiusura pannello; posizioni identiche prima e dopo ogni combinazione di filtri/ricerca poi azzerata; i due
  nuovi pulsanti funzionano correttamente; nessun movimento cambiando scheda; nessun errore in console su
  schermo stretto (390×844) e su una seconda finestra del browser; posizioni corrette dopo una rigenerazione dei
  dati. Con la reattività locale attiva, in più: solo il nodo trascinato e i suoi vicini diretti cambiano
  posizione; tutto fermo di nuovo un secondo dopo il rilascio; nessuno scatto o ripresa di movimento con
  trascinamenti ravvicinati anche sul nodo più connesso del grafo; con l'interruttore disattivato il
  comportamento torna identico a prima di questa funzionalità.
- **Codice più corto**: il file risultante ha meno righe di prima, non solo un comportamento più stabile.
- **Documentazione aggiornata di conseguenza**: nuova sezione "Come funziona la Vista a grafo (disposizione e
  interazione)" nella scheda Documentazione del sito, capitolo 12.2 della documentazione tecnica Word riscritto
  per intero, e `grafo_eco/layout_iniziale/README.md` aggiornato per spiegare perché il tentativo con d3-force lì
  contenuto è stato definitivamente superato.

### Revisione — Disposizione del grafo precalcolata offline, per un layout leggibile fin dall'apertura
Su segnalazione diretta (con screenshot): pur con il grafo ormai stabile (vedi sopra, "Riscrittura — Disposizione e
interazione del grafo"), la disposizione all'apertura risultava troppo "ammassata" e difficile da leggere - causa
individuata dalla stessa segnalazione: il tetto di 150 iterazioni usato per restare veloci (circa 2-2,5 secondi)
non lasciava mai alla fisica il tempo di arrivare a un vero equilibrio, a differenza della vecchia versione "da
cellulare" del sito (fisica sempre accesa, mai fermata da un tetto), che una volta assestata del tutto risultava
visibilmente più leggibile.

- **Calcolo spostato fuori dal browser di chi visita il sito.** Nuovo script `grafo_eco/layout_iniziale/
  precalcola_layout.js` (Node.js + Playwright): apre la VERA pagina `visualizzazione.html` in Chromium headless con
  `?precalcolo=1`, lasciando la stessa fisica vis-network già in uso girare senza limite di tempo fino a un vero
  equilibrio (a differenza del tentativo precedente con d3-force in questa stessa cartella, mai riuscito per lo
  stesso motivo: un motore di calcolo diverso da quello di visualizzazione produce sempre un risultato leggermente
  diverso). Le coordinate risultanti, per entrambe le viste ("tutti gli articoli" e "solo ristampe"), vengono
  salvate in `posizioni_iniziali.js` nella cartella principale del progetto.
- **Tre livelli, dal preferito al ripiego**, decisi automaticamente all'apertura di ogni vista: (1) posizioni
  precalcolate, se il file esiste e un controllo di corrispondenza (numero di nodi + hash degli identificativi)
  conferma che rispecchia i dati attuali - nessuna fisica, apertura quasi istantanea; (2) se il file manca (per
  esempio computer senza Playwright/Chromium), si ricalcola nel browser come già succedeva, senza nessun avviso
  perché è una condizione normale; (3) se il file c'è ma non corrisponde più ai dati (dimenticato di rigenerarlo),
  un avviso in console lo segnala e si ricalcola comunque nel browser come al punto 2 - mai un dato mancante o
  sbagliato, solo un'apertura più lenta nei casi 2 e 3.
- **Integrato in `genera_dati_sito.py`**: ultimo passaggio della pipeline, rilancia automaticamente il precalcolo
  ogni volta che i dati cambiano. Se Node.js o Playwright/Chromium non sono disponibili sul computer, il passaggio
  viene saltato con una spiegazione a schermo, senza interrompere il resto della generazione - situazione nota e
  verificata sul Mac principale di questo progetto, dove il download del browser Chromium per Playwright è bloccato
  dalla rete: il precalcolo va quindi eseguito altrove (per esempio in una sessione Claude con accesso a un
  browser, come per questa stessa consegna) e il file risultante copiato nella cartella principale.
- **Parametri di fisica: confrontate tre combinazioni a convergenza vera** (screenshot delle tre nel report di
  consegna). I parametri ORIGINALI, semplicemente lasciati girare senza tetto di iterazioni invece che fermati a
  150, hanno prodotto il risultato più leggibile delle tre - le combinazioni con spaziatura più ampia
  (`gravitationalConstant`/`springLength`/`avoidOverlap` maggiori) davano un nucleo centrale leggermente più
  compatto, non più leggibile. Nessun parametro di forza è stato quindi cambiato: il precalcolo riusa direttamente
  gli stessi parametri `barnesHut` già in uso nel ripiego, cambia solo quanto a lungo la fisica gira (senza tetto
  pratico invece che 150 iterazioni).
- **Nodi isolati o poco connessi: verificato quantitativamente** (correlazione fra grado del nodo e distanza dal
  centro dopo la convergenza, non solo impressione visiva) che migrano naturalmente ai margini del grafo con la
  sola convergenza vera, senza bisogno di nessun accorgimento aggiuntivo (per esempio un anello forzato attorno al
  nucleo, valutato e scartato perché non necessario).
- **Etichette dei cluster per anno (i rettangoli viola, es. "1970 (7)") nascoste di default**, per evitare
  l'accavallamento con archi e altre etichette segnalato nello screenshot: ricompaiono automaticamente sopra una
  soglia di zoom (spazio sufficiente intorno a ciascuna) o subito, a qualunque zoom, passando il mouse su un
  cluster specifico. Le etichette di riviste/quotidiani/libri non sono toccate, perché già leggibili senza
  affollarsi allo stesso modo.
- **Corretta l'inquadratura iniziale**: il primo `fit()` (adatta lo zoom per mostrare tutto il grafo) poteva
  risultare troppo zoomato, perché calcolato prima che il contenitore del grafo (nascosto con `display:none` finché
  non si apre quella scheda) avesse davvero preso le sue dimensioni finali - corretto con un doppio
  `requestAnimationFrame` prima del calcolo dell'inquadratura.
- **Tempo di apertura misurato**: circa 680ms in media (5 aperture, con il precalcolo presente e corrispondente),
  contro i circa 2-2,5 secondi di prima (ripiego a 150 iterazioni nel browser, sempre disponibile e invariato per
  chi non ha il precalcolo).
- **Verifica**: rieseguita per intero la stessa batteria di test automatici già in uso (posizioni a 1s/5s/30s;
  nessun movimento su 10 click; trascinamento di 5 nodi, ognuno resta esattamente dove rilasciato (con la
  reattività locale attiva, anche i vicini diretti si muovono per un istante, comportamento atteso e già
  documentato - riverificato separatamente che il nodo trascinato resta comunque sempre esattamente dove
  rilasciato); nessun movimento su zoom/pan/doppio-clic/apertura pannello; posizioni identiche dopo filtri/ricerca
  azzerati; i due pulsanti "Ripristina disposizione"/"Centra" funzionano; nessun movimento cambiando scheda;
  nessun errore in console; su schermo stretto; tutti i test della reattività locale (Tappa 2); espansione di un
  cluster; ricerca con evidenziazione. In più, tre prove nuove richieste per questa revisione: tempo di apertura
  (sopra); ripiego funzionante rinominando temporaneamente `posizioni_iniziali.js` (il sito continua a funzionare,
  nessun avviso, come atteso per un file del tutto assente); coerenza dopo una modifica reale dei dati (rimosso un
  nodo di prova, rigenerato il precalcolo, confermato che conteggio e hash cambiano di conseguenza e che un file
  con hash volutamente non corrispondente fa scattare l'avviso in console e il ricalcolo di ripiego, come previsto).
- **Vecchio tentativo con d3-force** (`genera_layout_iniziale.js` e le sue dipendenze, in questa stessa cartella,
  mai agganciato al sito) spostato in `grafo_eco/layout_iniziale/tentativo_d3force_abbandonato/` per tenerlo fuori
  dai piedi senza cancellarlo (cancellare richiede un permesso esplicito sul computer, non ancora richiesto).
- **Documentazione aggiornata di conseguenza**: sezione "Come funziona la Vista a grafo" nella scheda Documentazione
  del sito aggiornata, capitolo 12.2 della documentazione tecnica Word aggiornato con una nuova sezione dedicata,
  `grafo_eco/layout_iniziale/README.md` riscritto per descrivere il meccanismo attuale (e tenere traccia, come
  riferimento storico, di entrambi i tentativi precedenti: la stabilizzazione nascosta nel browser e, prima ancora,
  d3-force).

## 2026-09-15 — v1.1 dell'ontologia (peer-review OWL/RDF, FRBR, FAIR/LOD)
Vedi il commento "STORICO VERSIONI" in `grafo_eco/ontologia_eco.ttl` per il dettaglio completo.

## Prima del 2026-09-15 — v1.0
Versione iniziale del progetto. Data di creazione non tracciata in modo formale.
