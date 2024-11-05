# Controllo input (input validation) in HTML & CSS

```
form input:not([type="submit"]):optional {
    border-color: gray;
}

form input:not([type="submit"]):required:valid {
    border-color: greenyellow;
}

form input:not([type="submit"]):invalid {
    border-bottom-color: red;
}

input:not([type="submit"]):focus:valid {
    background-color: lightgreen;
}

input:not([type="submit"]):focus:invalid {
    background: lightsalmon;
}

form:invalid input[type="submit"] {
    display: none;
}

form:invalid::after {
    color: red;
    border: 1px solid red;
    background-color: lightsalmon;
    border-radius: 20px;
    width: 50%;
    padding: 10px 0;
    margin: 10px auto;
    display: block;
    text-align: center;
    content: "I dati non sono corretti...";
}

```
Iniziamo con questo pezzo di CSS. Quello che starai pensando sarà sicuramente: "Ma che è 'sta roba??"

Non preoccuparti, con questo documento capirai esattamente a cosa serve questo codice e imparerai anche a migliorarlo!

## Il tag `<form>`

Come si può intuire dal titolo, questo pezzo serve per gestire in maniera grafica (il CSS d'altronde serve per creare l'interfaccia grafica della pagina) il controllo dell'input di un utente. Ma facciamo un passo indietro.

Fin'ora abbiamo visto in HTML tag come `<title>`, `<h1>`, `<img>`, `<a>`, `<p>` e il famoso `<div>`.
Questi tag hanno tutti una cosa in comune: creano degli elementi che vengono renderizzati dal browser (mostrati a schermo).

Invece adesso vedrai un tag per ricevere in input dei dati, il tag `<form>`.

Come detto prima, il tag `<form>` serve per ricevere in input dei dati dall'utente. I dati inseriti tramite questo tag vengono inviati al server che ospita la pagina web, oppure vengono usati dal browser locale per modificare la pagina in base a quello che è stato inserito (come fa il CSS riportato all'inizio).

Il tag `<form>` non è usato nell stesso formato di un `<p>` o di un `<h1>`, ma come un `<a>`, ovvero è **necessario** specificare dei _parametri_, che vedremo di seguito.

Si può dire che `<form>` ricordi anche il `<div>`, ovvero è un tag che ne contiene altri. A differenza del `<div>`, che può contenere qualsiasi tipo e combinazione di tag, il `<form>` contiene una serie di tag specifici, più avanti vedremo i più importanti.

## `<form>`: sintassi

Il tag `<form>` segue questa sintassi: `<form action="programma" method="post"></form>`. Vediamo ora i suoi parametri.

### `action` e i metodi del `<form>`
Partiamo dal parametro `action="programma"`. Serve per indicare al sito dove mandare i dati quando vengono inviati. Quel programma viene eseguito dal server web, e può essere scritto in qualsiasi linguaggio, dal PHP a C# o persino in linguaggio macchina, non ha alcuna importanza.

Per rendere meglio l'idea, prendiamo in considerazione il `<form>` sul mio sito: `<form action="upload.php" method="post">`. Qui l'attributo `action` è uguale a `upload.php`. Quindi quando il `<form>` viene inviato, il server eseguirà `upload.php`, passandogli come argomento in ingresso i dati ricevuti dal `<form>` e poi eseguendo delle operazioni sui dati inseriti, come ad esempio la somma di tutti i numeri o il salvataggio dei dati inseriti in un documento.

Invece l'argomento `method` indica quale metodo HTTP da usare per inviare i dati al server (di solito è `get` o `post`).

#### Una parentesi sui metodi HTTP

Teniamo a mente l'esempio di `<form>` fatto prima, ovvero `<form action="upload.php" method="post">`.

##### `get`

Il metodo `get` viene usato per richiedere dei dati al server.

Una richiesta di tipo `get` viene inviata ogni volta che si cerca di visualizzare una pagina di un sito web. 
Ad esempio, ogni volta che io digito `youtube.com` nel mio browser questo invierà una richiesta di tipo `get` al server `youtube.com` per ricevere il file `index` (ecco perché è importante che il file principale del sito si chiami `index`!). 

Quando `get` viene usato per un `<form>`, i dati inseriti nel `<form>` saranno usati per richiedere un documento sul server. I dati inseriti verranno inviati nell'URL (l'URL è il percorso dove si trova il documento remoto, eg. youtube.com/index.html) come parametri per ricevere dal server una parte specifica del documento richiesto. I parametri vengono inviati in forma `?campoinput1=qualcosa&campoinput2=qualcosaltro&...`. Cosa significhino `campoinput1` e `campoinput2` lo vedremo dopo. 

Il metodo `get` però ha delle limitazioni: può inviare solo 2048 caratteri totali e questi caratteri possono solo essere caratteri ASCII. 

##### `post`

Il metodo `post` è fatto apposta per inviare dei dati al server. A differenza del metodo `get`, il metodo `post` non invia i dati al server nell'URL sotto forma di richiesta. Quindi se nel primo caso chiederemo al server `upload.php?campoinput1=qualcosa&campoinput2=qualcosaltro` nel secondo chiederemo solo `upload.php` e invieremo `campoinput1=qualcosa&campoinput2=qualcosaltro` direttamente a `upload.php`. 

Il metodo `post` non è soggetto alle limitazioni del metodo `get`, infatti possiamo usarlo per inviare al server qualsiasi tipo di dato, che sia testo in alfabeto latino, cirillico o lingue asiatiche, o anche altri dati che non siano testo come file e immagini. Se si vuole inviare qualcos'altro che non sia testo ASCII, bisogna specificare come argomento aggiuntivo del `<form>` la codifica da usare: `enctype="multipart/form-data"` specifica la codifica binaria, quindi di non ricodificare i dati del `<form>` e di trattarli come un flusso di dati binari. In questo modo le codifiche dei dati che stiamo inviando vengono preservate.

## I tag di `<form>`: `<label>`, `<input>` e `<textarea>`

Adesso vediamo i principali tag specifici da usare nel `<form>`.

### `<label>`

Iniziamo con `<label>`: questo tag serve per aggiungere un'etichetta agli altri due tag. Questa etichetta verrà mostrata a schermo, ma non solo. 

Questa etichetta viene associata al tag `<textarea>` o `<input>` analogamente ad una classe. Ci tornerà assai utile più avanti quando applicheremo del CSS al nostro `<form>`.

Oltre a mostrare l'etichetta per l'elemento a schermo e ad assegnargli un punto di riferimento analogamente ad una classe, il tag `<label>` è utile per migliorare la compatibilità del nostro sito con strumenti terzi, quali estensioni del browser, strumenti di auto completamento o strumenti per l'accessibilità.

Il tag `<label>` può essere usato in due modi diversi e in base al modo usato si dice che l'etichetta è applicata in modo esplicito o implicito.

```
<label>
    Il codice mostrato è codice HTML?
    <input type="checkbox" />
</label>
```
Nel caso qui sopra abbiamo un'assegnazione dell'etichetta implicita al tag `<input>`, perché `<input>` è contenuto dentro al tag `<label>`.

```
<label for="terms">Dichiaro di aver accettato i Termini di utilizzo.</label>
<input type="checkbox" id="terms">
```
In questo caso l'assegnazione dell'etichetta è esplicita. Da notare come in questo caso il tag `<label>` ha un attributo, `for="terms"`, e il tag `<input>` sottostante ha un argomento in più, `id="terms"`. È in questo modo che si fa l'assegnazione esplicita. Mi spiego meglio.

Per capire come funziona basta leggere letteralmente l'attributo, quindi leggi il primo tag come "applica un etichetta **per** tutti gli elementi identificati come terms". Il secondo invece lo leggiamo come "questo è un input con **id**entificatore terms". Basta un minimo di logica per capire che il nostro tag `<input>` combacia con la descrizione del tag `<label>` e quindi l'etichetta sarà associata a quel tag `input` e non ad altri. L'`id` può essere applicato anche a `<textarea>`.

### `<textarea>`

Il tag `<textarea>` viene usato per creare un riquadro in cui inserire testo su più righe,  che poi verrà inviato al server da rielaborare. È utile per creare delle sezioni commenti all'interno di una pagina, come un blog.

Questo tag accetta degli attributi, alcuni che sono comuni al tag `<input>`, che vedremo dopo.

Gli attributi che `<textarea>` accetta sono:
- `autofocus`, che posiziona il cursore nel riquadro quando la pagina viene caricata. Solo un tag per pagina può averlo impostato. Es.: `<textarea autofocus />`
- `cols` e `rows` specificano la dimensione in righe e colonne di testo del riquadro. Se specificati devono essere numeri interi e positivi. Se non specificati, i valori di default sono `cols="20" rows="2"`. Es.: `<textarea rows="200" cols="100">`
- `disabled`, che può essere `true` o `false`. Questo attributo specifica che l'utente non può interagire con il contenuto del riquadro, quindi non può né scriverci dentro né può copiare il testo all'interno con il mouse o con la combinazione `ctrl+c`. Se il riquadro ha l'attributo `disabled` non sarà inviato al server. Es.: `<textarea disabled />`
- `minlenght` e `maxlenght` servono per specificare il numero minimo e massimo di caratteri (spazi inclusi) che possono essere inseriti nel riquadro. Es.: `<textarea minlenght="10" maxlenght="200">`
- `name` serve per specificare il nome da dare al testo inserito. Questo nome viene usato per far riferimento al riquadro da JavaScript o per far riferimento al testo inserito una volta inviato al server.
Ad esempio, quando su Google facciamo una ricerca e invece di "html" scriviamo "ht**n**l", la pagina ci dice 'Intendevi dire "html"?' e sotto ci dice 'Cerca invece "**htnl**"'. Per far comparire sulla nostra pagina la parola "htnl" che l'utente ha inserito e inviato prima, dobbiamo affidarci al `name` che ha il riquadro dov'era stata inserita la parola "htnl". 
È come quando in C# scriviamo `string variabile = Console.ReadLine()` e sotto  `ConsoleWriteLine("Messaggio inserito: " + variabile)`. Scrivendo `+ variabile` noi stiamo dicendo che vogliamo scrivere il contenuto di `variabile` e non la parola "variabile". L'attributo `name` si comporta analogamente alla dichiarazione di una variabile, ovvero ci permette di specificargli un nome.
Infatti serve per specificare il nome della variabile che contiene il testo inserito nel riquadro. Se riprendiamo l'esempio fatto nella sezione dei metodi HTTP, dove al server inviamo `campoinput1=qualcosa`, l'attributo `name` serve a specificare il nome della variabile che contiene `qualcosa`. Quindi, se imposto `<textarea name="comment">` e inserisco come input `sometext` il server riceverà `comment=sometext`. Es.: `<textarea name="areatesto">`
- `placeholder`, ovvero del testo che viene mostrato all'interno del riquadro quando non è inserito nulla. Questo testo server per dare un suggerimento breve e coinciso all'utente su cosa inserire all'interno del riquadro. `placeholder` non deve essere usato al posto di `<label>`, perché visto che scompare appena viene inserito qualcosa nel riquadro impatta l'accessibilità e l'usabilità della pagina. Invece è molto meglio usare `<label>` e `placeholder` insieme per creare una pagina che sia accessibile e intuitiva da usare, preferendo il tag `<label>` per dare una spiegazione più dettagliata su cosa inserire nel riquadro. L'attributo `placeholder` non può andare a capo. Se viene inserito del testo che va a capo, es: 
    ```
    <textarea placeholder="testo
    che
    va
    a
    capo">
    ```
    il testo verrà mostrato come se fosse stato scritto `<textarea placeholder="testochevaacapo">`.
- `readonly`, a differenza dell'attributo `disabled`, non impedisce di copiare il contenuto del riquadro. Es.: `<textarea readonly />`
- `required` serve a specificare che il riquadro deve contenere qualcosa, altrimenti il `<form>` non sarà inviato. Es.: `<textarea required />`
- `value`, che funziona analogamente all'assegnazione di una variabile in C#. Se prima abbiamo detto che `name` serve per dichiarare una variabile che contiene il testo inserito, allora se io voglio che `variabile` sia `20` scriverò `<textarea name="variabile" value="20">`. `value` serve per specificare il valore iniziale della variabile, ma se l'utente inserisce qualcosa nel riquadro `value` sarà sostituita da quello che l'utente ha inserito.

### `<input>`

`<input>`, da come dice il nome, è il tag principale per poter ricevere dei dati in input dall'utente. 

Visto che supporta una grande varietà di dati in ingresso, diverse tipologie grafiche e una miriade di combinazioni, è uno dei tag più potenti e complessi di tutto il linguaggio HTML. 

Tieni a mente che il tag `<input>` non deve essere chiuso (`</input>` non esiste ed è scorretto). Per chiuderlo invece bisogna fare così: `<input attributo1="qualcosa" attributo2="qualcosaltro" attributo3 />`. Lo `/` finale prima dell'angolare di chiusura specifica che il tag è chiuso. 

Ci sono alcuni attributi universali supportati da `<input>`, indipendentemente dal tipo (vedi di seguito). Sono `id`, `disabled`, `autofocus` (eccetto per il tipo `hidden`) e `title`.

#### Tipi di `<input>`

Il modo in cui un `<input>` funziona varia sensibilmente in base all'attributo `type` che gli viene specificato. Se non è specificato di default è `type="text"`
I tipi di `<input>` disponibili sono:
- `checkbox`, una casella dove mettere una spunta che può essere selezionata o deselezionata.
- `date` serve per inserire una data formata da anno, mese e giorno, senza ora.
- `datetime-local` funziona analogamente a `date`, ma permette anche di inserire un'orario, però senza fuso orario.
- `email` serve per inserire un indirizzo email. Graficamente è uguale a `text` ma ha dei parametri specifici per verificare che sia stato inserito un indirizzo email e non del semplice testo.
- `file` permette di inserire uno o più file.
- `hidden`, un tipo di input che viene inviato al server ma che l'utente non può vedere.
- `image` è un pulsante `submit` grafico.
- `number` serve per inserire un numero. Ha di default dei controlli sul tipo di dato inserito e fa comparire nel riquadro delle freccette per poter scegliere il numero senza scriverlo da tastiera.
- `password` è un riquadro di una sola riga il cui contenuto viene oscurato. Se presente e se il sito non utilizza il protocollo HTTPS, il browser avviserà che il sito non è sicuro.
- `radio` è simile a `checkbox`, ma permette di inserire una sola opzione tra quelle presenti che hanno lo stesso valore di `name`.
- `range` serve per inserire un numero in modo approssimativo. A schermo viene visualizzato come uno slider che di default è sulla posizione centrale.
- `search` è un riquadro per inserire delle stringhe di ricerca. In questo riquadro gli invii vengono automaticamente rimossi.
- `submit` è un pulsante che serve ad inviare il `<form>` nella sua interezza.
- `tel` è un riquadro per inserire un numero di telefono.
- `text` è un riquadro di una sola riga dove inserire del testo. Anche qui gli invii sono automaticamente rimossi.
- `time` serve per inserire un'orario senza fuso.
- `url` server per inserire un URL. Graficamente è uguale a `text` ma ha dei parametri specifici per verificare che sia stato inserito un indirizzo URL e non del semplice testo.

Vediamoli adesso nello specifico.

##### `checkbox`
Il tag  `<input type="checkbox">` può avere l'attributo `value`. Quando viene settato in combinazione con l'attributo `name`, quando il `<form>` viene inviato e la spunta è stata messa verrà inviato al server la combinazione `name=value`, altrimenti non verrà inviata. Se `value` viene omesso, avrà come valore di default `on`.
Inoltre può avere l'attributo `checked`, che imposta la spunta come segnata appena la pagina viene caricata. Può essere deselezionata dall'utente. Se `<input type="checkbox">` ha un tag `<label>` associato, per mettere la spunta è possibile cliccare sull'etichetta.
##### `date`
Il tag `<input type="date">` crea un campo dove inserire una data. Quando la data viene inviata al server, viene inviata nel formato AAAA-MM-GG dove A è una cifra dell'anno, M è una cifra del mese e G è una cifra del giorno.
Sul browser però il formato visualizzato dipende dalle impostazioni dell'utente. Noi nella pagina HTML vedremo la data nel formato GG-MM-AAAA.
##### `datetime-local`
Il tag `<input type="datetime-local">` accetta l'attributo `value`, `max` e `min`.
`value` stabilisce la data di default, `min` e `max` sono rispettivamente la data minima e massima accettate nel riquadro.
Per definire il valore di `value`, `max` e `min` come una stringa valida fare riferimento a [questo](https://developer.mozilla.org/en-US/docs/Web/HTML/Date_and_time_formats#local_date_and_time_strings) documento.
Se `min` e `max` sono impostate e viene inserita una data non valida, possono succedere due cose:
1. Il numero non valido inserito viene arrotondato per difetto al valore valido più vicino, impedendoti di inserire il valore errato;
2. Il numero valido viene accettato dal riquadro ma viene riconosciuto come non valido. Questo ci servirà dopo per decorare il riquadro con il CSS.
Se si volesse impostare il fuso orario per il tag `<input type"datetime-local">`, questo può essere fatto in due modi diversi:
1. Si può creare un tag `<input type="hidden" name="fuso" value="+01:00">` per definire il fuso orario che aggiunge un'ora all'ora di base. In questo modo però il fuso orario non può essere modificato e stiamo dando per scontato che il nostro utente inserisca un'ora tenendo a mente del fuso che abbiamo specificato.
2. Si può definire un altro campo per inserire il fuso orario.
In entrambi i casi il fuso orario dovrà essere interpretato dal server per poi elaborarlo ed eseguire delle operazioni basate su quell'orario. Il fuso orario viene inviato al server in un campo separato rispetto a `datetime-local`, quindi bisogna tenerlo a mente per far funzionare correttamente il server.
##### `email`
Il tag `<input type="email">` può accettare l'attributo `multiple`. Se nella pagina ho `<input type="email" multiple />` allora potrò inserire una lista di indirizzi email. Se inserisco del testo che non è un'email nel riquadro, questo verrà riconosciuto come non valido. `email` accetta l'attributo `value`. `value` può avere 3 tipi di valori che sono considerati validi:
1. Una stringa vuota (""), che indica che non è stato inserito nulla o che il valore di `value` è stato cancellato dall'utente.
2. Un indirizzo email valido. Valido non significa che l'indirizzo deve esistere, ma che deve essere scritto come `nome@dominio` oppure come `nome@dominio.tld`. Il dominio è come il proprio nome, è una proprietà che appartiene solo a te e permette di distinguerti dagli altri. Per quanto riguarda il **T**op **L**evel **D**omain (**TLD**), è una proprietà che viene definita dalla IANA e serve per raggruppare in modo molto generico i vari nomi, come se fosse una caratteristica comune. Ad esempio, possiamo considerare il tld come il mestiere di una persona (eg. meccanico) e il dominio come il suo nome (eg. Mario). Ce ne sono tanti di meccanici, ma ce ne sono di meno che si chiamano anche Mario.
3. Se e solo se l'attributo `multiple` è specificato, `value` può essere una lista di indirizzi email divisi con delle virgole.
Se `multiple` è specificato da solo, il riquadro se rimane vuoto è considerato valido.
Inoltre supporta come attributi `maxlenght` e `minlenght`, `pattern`, `placeholder` e `readonly`. `pattern` è un atrributo che specifica un'espressione regolare (chiamata "regex", vedi [qui](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions) per capire come scriverle) che deve essere rispettata per rendere il riquadro valido. 
##### `file`
Il tag `<input type="file">` accetta come attributi `accept` e `multiple`.
`accept` serve per specificare le tipologie di file che vengono accettate. Visto che alcuni tipi di file possono essere identificati in vari modi, è necessario specificare ogni tipologia con cui possiamo identificare quei file. Ad esempio, per identificare un documento di Word scriveremo `accept=".doc,.docx,.xml,application/msword,application/vnd.openxmlformats-officedocument.wordprocessingml.document"`. Per sapere come identificare i file fare riferimento [qui](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#unique_file_type_specifiers) e [qui](https://developer.mozilla.org/en-US/docs/Web/HTTP/MIME_types). Il tag `<input type="file">` per essere usato ha bisogno o di un programma, contenuto nell'attributo `action` del `<form>`, che sia in grado di gestire i file, oppure di codice JavaSceipt che sia in grado di svolgere le stesse funzioni, come spostare i file da qualche parte, modificarne il contenuto o comprimerli.
l'attributo
##### `hidden`
Il tag `<input type="hidden">` può avere solo `name` e `value` come attributi.
Abbiamo visto prima, con l'attributo `datetime-local`, come può essere usato il tag `<input type="hidden">`. Come già specificato, con `hidden` il riquadro non può essere modificato, infatti all'utente non compare, ma viene comunque inviato al server quando viene inviato il `<form>`.
##### `image` e `submit`
`<input type="submit">` accetta come attributo solo `value`, che va a specificare il testo che comparirà all'interno del pulsante. Una volta cliccato invia il `<form>` al server. `<input type="image">` svolge la stessa funzione, ma invece di apparire come pulsante appare come l'immagine specificata dall'attributo `src`. `<input type="image">` supporta anche gli attributi `alt`, `width` e `height`. Se per qualche motivo l'immagine non può essere mostrata a schermo, al suo posto si vedrà un pulsante normale con all'interno la stringa specificata nell'attributo `alt`.
##### `number`
Il tag `<input type="number">` supporta come attributi `max`, `min`, `placeholder` e `readonly`. Il riquadro sarà non valido se verrà inserito un dato che non sia un numero. Inoltre, il riquadro presenta a destra delle freccette per inserire il numero usando solo il mouse. Il tag `<input type=number">` non deve essere usato per dei dati che sono numerici, ma che non sono consecutivi, come codici postali o numeri di telefono.
##### `password`
Il tag `<input type="password">` quando è vuoto ha il valore di una stringa vuota (""). Al suo interno **non** possono essere inseriti degli invii. Se vengono inseriti, saranno automaticamente cancellati. Accetta come attributi `maxlenght`, `minlenght`, `pattern`, `placeholder`, `readonly` e `required`.
##### `radio`
Il tag `<input type="radio">` viene chiamato così perché si comporta come i pulsanti per far avanzare/riavvolgere il nastro di un registratore: non posso avere schiacciati avanti e indietro nello stesso momento, ma posso averne schiacciato uno solo per volta. Per definire un gruppo di pulsanti `radio` è necessario che tutti i membri del gruppo abbiano lo stesso attributo `name`. Si possono creare quanti gruppi di pulsanti `radio` si vogliono. `<input type="radio">` accetta come argomenti `name` e `value`, `required` e `checked`.
##### `range`
Il tag `<input type="range">` definisce un intervallo di valori numerici che possono essere inseriti. Supporta gli argomenti `value`, `name`, `min`, `max`. Se il valore inserito non può essere convertito in un numero float valido, allora lo slider risulterà non valido. Inoltre il suo valore sarà sempre compreso tra `min` e `max`, che di default sono `min="0"` e `max="100"`
##### `search`
Il tag `<input type="search">` accetta come attributi `maxlenght`, `minlenght`, `pattern`, `placeholder`, `readonly` e `required`.
##### `submit`
Il tag `<input type="submit">` accetta come attributi `value`. Se `value` non è specificato allora il testo del pulsante sarà `Submit` o `Submit Query`.
##### `tel`
Il tag `<input type="tel">` si comporta come il tag `<input type="text">` visto che nel mondo ci sono una miriade di modi per scrivere numeri telefonici. La particolarità è per i dispositivi mobili, che quando devono inserire dei dati nel riquadro faranno apparire un tastierino numerico invece della tastiera normale. `tel` accetta come attributi `minlenght`, `maxlenght`, `pattern`, `placeholder`, `readonly`, `required`, `name` e `value`.
##### `text`
Il tag `<input type="text">` accetta i parametri `name`, `required`, `minlenght`, `maxlenght`, `pattern`, `placeholder`, `readonly`, `value`.
##### `time`
Il tag `<input type="time">` è sempre in formato `HH:mm` o `HH:mm:ss`, con 24 ore e zeri che precedono le ore, i minuti e i secondi a una sola cifra. Accetta come attributi `value`, `name`, `max`, `min`, `required` e `readonly`.
##### `url`
Il contenuto del tag `<input type="url">`, per essere ritenuto valido, può essere:
1. Una stringa vuota ("")
2. Un indirizzo scritto in formato `protocollo://server`. Non è necessario che `protocollo` o `server` esistano. Accetta come attributi `required`, `maxlenght`, `minlenght`, `pattern`, `placeholder` e `readonly`.

## CSS Time!
Riprendiamo il codice con cui siamo partiti:
```
form input:not([type="submit"]):optional {
    border-color: gray;
}

form input:not([type="submit"]):required:valid {
    border-color: greenyellow;
}

form input:not([type="submit"]):invalid {
    border-bottom-color: red;
}

input:not([type="submit"]):focus:valid {
    background-color: lightgreen;
}

input:not([type="submit"]):focus:invalid {
    background: lightsalmon;
}

form:invalid input[type="submit"] {
    display: none;
}

form:invalid::after {
    color: red;
    border: 1px solid red;
    background-color: lightsalmon;
    border-radius: 20px;
    width: 50%;
    padding: 10px 0;
    margin: 10px auto;
    display: block;
    text-align: center;
    content: "I dati non sono corretti...";
}

```
A colpo d'occhio possiamo vedere che gli elementi fanno riferimento al tag `<form>` e al tag `input`. Però c'è qualcosa di più. Ci sono altre parole dopo i tag che vengono precedute da due punti. Quelle si chiamano **pseudo-classi**. Vediamo come funzionano e a cosa servono.

### Pseudo-classi

In CSS, una pseudo-classe è una parola chiave che viene aggiunta ad un elemento (che sia un tag o una classe) che specifica il suo stato. Ad esempio, la pseudo-classe `:hover` specifica il momento in cui il mouse passa sopra l'elemento. 

In questo modo noi possiamo cambiare l'aspetto della pagina in base a degli eventi che avvengono sui nostri elementi. 

Alcune pseudo-classi, dette pseudo-classi **funzionali** hanno delle parentesi dopo il nome: lì è dove vanno inseriti gli argomenti della pseudo-classe. 

L'elemento a cui si attacca una pseudo-classe viene definito elemento d'ancoraggio.

Noi adesso vedremo le pseudo-classi specifiche per i `<form>` e in particolare per il tag `<input>`.

### Pseudo-classi di `<input>`
Le pseudo-classi di `<input>` sono:
- `:enabled`
- `:disabled`
- `:read-only`
- `:read-write`
- `:placeholder-shown`
- `:default`
- `:checked`
- `:intermediate`
- `:valid`
- `:invalid`
- `:in-range`
- `:out-of-range`
- `:required`
- `:optional`
- `:user-valid`
- `:user-invalid`

Poi ce ne sono alcune che sono molto comode, come `:hover`, `:focus`, `:active` e `:not()`, che non sono esclusive per il tag `<input>`.

Diamogli un'occhiata da più vicino.

#### `:enabled` e `:disabled`
La pseudo-classe `:enabled` rappresenta gli elementi attivi. Un elemento è attivo se può essere attivato (selezionato, cliccato sopra, scritto dentro, ...). `:disabled` rappresenta tutti gli elementi non attivi, ovvero tutti gli elementi che hanno attributo `disabled`.
#### `:read-write` e `:read-only`
La pseudo-classe `:read-write` rappresenta un elemento modificabile dall'utente, la pseudo-classe `:read-only` invece rappresenta tutti gli elementi non modificabili, sia i riquadri con attributo `readonly` che tutti gli altri elementi della pagina, come `<a>` o `<p>`.
#### `:placeholder-shown`
È autoesplicativa, la pseudo-classe `:placeholder-shown` rappresenta tutti gli elementi con attributo `placeholder`.
#### `:default`, `:checked` e `:indeterminate`
La pseudo-classe `:default` rappresenta tutti gli elementi che non sono ancora stati modificati dall'utente e sono nel loro stato di default. `:checked` rappresenta tutti i tag `<input type="radio">` e `<input type="checkbox">` che sono selezionati. `:indeterminate` invece rappresenta tutti i tag `<input type="radio">` dello stesso gruppo quando non nessuno dei membri è selezionato.
#### `:valid` e `:invalid`, 
Qui ritorna quello che ho detto prima riguardo ai riquadri con contenuto valido. La pseudo-classe `:valid` infatti rappresenta tutti gli elementi con contenuto valido. Questa pseudo-classe è utilissima per far capire all'utente che quello che ha inserito è valido. Al contrario, `:invalid` rappresenta tutti i contenuti che non sono validi.
#### `:in-range` e `:out-of-range`
La pseudo-classe `:in-range` rappresenta tutti gli elementi che hanno ricevuto un input e l'input è compreso tra i valori definiti dagli attributi `min` e `max`. `:out-of-range` invece rappresenta tutti gli elementi che hanno ricevuto un input e l'input non è compreso tra i valori definiti dagli attributi `min` e `max`.
#### `:required` e `:optional`
`:required` rappresenta tutti gli elementi che hanno l'attributo `required`. `:optional` invece rappresenta tutti gli elementi che non hanno l'attributo `required`.
#### `:user-valid` e `:user-invalid`
`:user-valid` rappresenta tutti i riquadri in cui è stato inserito dall'utente un input valido. Questa pseudo-classe è applicata anche quando l'utente invia il `<form>` vuoto. `:user-invalid` invece rappresenta tutti i riquadri in cui è stato inserito dall'utente un input non valido. Deve obbligatoriamente corrispondere a un elemento con pseudo-classe `:invalid`, `:out-of-range` o un elemento vuoto ma con attributo `required`
#### `:hover`
La pseudo-classe `:hover` rappresenta tutti gli elementi su cui l'utente posiziona il mouse sopra, anche senza attivarli.
#### `:focus`
La pseudo-classe `:focus` rappresenta un elemento che è stato selezionato.
#### `:active`
La pseudo-classe `:active` rappresenta un elemento (come un link o un bottone) che è stato attivato dall'utente. La pseudo-classe `:active` viene spesso usata con i tag `<a>`. Quello che è contenuto nella pseudo-classe `:active` sarà sovrascritto da una qualsiasi pseudo-classe che ha a che fare con i link (come `:hover`).
#### `:not()`
La pseudo-classe `:not()` rappresenta degli elementi che **non** corrispondono a delle condizioni (come l'appartenere ad una classe, avere un certo attributo con un valore o appartenere ad una pseudo-classe). La pseudo-classe `:not()` ha delle particolarità:
- È possibile scrivere delle condizioni senza senso. Per esempio è possibile scrivere `:not(*)`, che corrisponde a tutti gli elementi che non sono elementi. Ovviamente è una condizione che non si verrà mai verificata e che non ha senso, quindi non verrà mai applicata.
- `:not(.classe)` corrisponde a **qualsiasi** tag che non abbia la classe `.classe`, inclusi i tag `<head>`, `<body>` e pure `<html>`.
- `:not()` corrisponde letteralmente. Ovvero, se io scrivessi `body:not(ul) a` le proprietà CSS verrebbero applicate a tutti i link (`a`) che sono nel `<body>` e non sono in una lista non ordinata (`not(ul)`). Però se il mio HTML è così:
    ```
    <body
    <ul>
    <li><a href="https://youtbe.com">Youtube</a></li>
    <li>Cose a caso</li>
    </ul>
    </body>
    ```
    Le proprietà al link `https://youtube.com` verrebbero applicate lo stesso, perché nonostante sia un discendente di `<ul>` il link non è applicato direttamente a `<ul>`, quindi il link risulta come appartenere a `<body>` e non essere applicato a `<ul>`.
- È possibile negare diverse caratteristiche nello stesso momento. Ad esempio, `:not(.classe1, .classe2)` è equivalente a scrivere `:not(.classe1):not(.classe2)`.
- Se a `:not()` viene passato un argomento non valido, tutta la regola risulterà non valida e non sarà applicata.

Nel nostro codice di partenza è presente anche lo pseudo-elemento `::after`. 

Uno pseudo-elemento è identificato da `::` che vengono prima del nome e serve per selezionare una parte specifica dell'elemento selezionato.

`::after` serve per selezionare l'ultimo elemento discendente del tag selezionato. Se viene usato, deve essere presente la proprietà `content`. Se la proprietà `content` non è specificata, non è valida o ha come valore `normal` o `none` allora l'elemento non sarà mostrato e si comporterà come se fosse stato impostato `display: none`.

## Ritorno al principio
Ricapitolando, il CSS iniziale, come primo blocco:
1. Seleziona i tag `<form>`
2. Seleziona i tag `<input>` all'interno del `<form>`
3. Seleziona tutti i tag `<input>` che non abbiano attributo `type="submit"`
4. Seleziona tutti i tag `<input>` che non abbiano attributo `required`

Secondo:
1. Seleziona i tag `<form>`
2. Seleziona i tag `<input>` all'interno del `<form>`
3. Seleziona tutti i tag `<input>` che non abbiano attributo `type="submit"`
3. Seleziona tutti i tag `<input>` che abbiano attributo `required`
4. Seleziona tutti i tag `<input>` che siano validi

Terzo:
1. Seleziona i tag `<form>`
2. Seleziona i tag `<input>` all'interno del `<form>`
3. Seleziona tutti i tag `<input>` che non abbiano attributo `type="submit"`
4. Seleziona tutti i tag `<input>` che siano non validi

Quarto:
1. Seleziona i tag `<input>`
2. Seleziona tutti i tag `<input>` che non abbiano attributo `type="submit"`
3. Seleziona tutti i tag `<input>` che siano selezionati
4. Seleziona tutti i tag `<input>` che siano validi

Quinto:
1. Seleziona i tag `<input>`
2. Seleziona tutti i tag `<input>` che non abbiano attributo `type="submit"`
3. Seleziona tutti i tag `<input>` che siano selezionati
4. Seleziona tutti i tag `<input>` che siano non validi

Sesto:
1. Seleziona i tag `<form>`
2. Seleziona i tag `<form>` che siano non validi
3. Seleziona i tag `<input>` all'interno dei `<form>`
4. Seleziona tutti i tag `<input>` che abbiano attributo `type="submit"`

Settimo:
1. Seleziona i tag `<form>`
2. Seleziona i tag `<form>` che siano non validi
3. Seleziona l'ultimo tag discendente da `<form>`

## Fonti
Se hai ancora dubbi o se ci sono parti o specifiche che non sono chiare (o che ho omesso per semplicità), questa è la lista delle pagine che ho usato per creare questo documento:
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form
- https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes
- https://developer.mozilla.org/en-US/docs/Learn/Forms
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Other_form_controls
- https://developer.mozilla.org/en-US/docs/Learn/Forms/UI_pseudo-classes
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation
- https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data
- https://www.w3schools.com/tags/ref_httpmethods.asp
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET
- https://stackoverflow.com/questions/15352739/how-to-submit-form-with-get-method-and-using-uri-template
- https://www.programiz.com/html/form-action
- https://stackoverflow.com/questions/70897265/what-is-the-purpose-of-th-http-get-method-in-forms
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input
- https://www.w3schools.com/tags/att_param_name.asp
- https://www.w3schools.com/jsref/prop_param_name.asp
- https://www.w3schools.com/tags/att_form_name.asp
- https://en.wikipedia.org/wiki/UTF-16
- https://www.quora.com/What-is-the-use-of-name-and-value-parameters-in-input-tag-in-HTML
- https://docs.machform.com/help/using-url-parameters-to-populate-form-fields
- https://dev.to/sidthesloth92/understanding-html-form-encoding-url-encoded-and-multipart-forms-3lpa
- https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/placeholder
- https://en.wikipedia.org/wiki/Newline
- https://stackoverflow.com/questions/12747722/what-is-the-difference-between-a-line-feed-and-a-carriage-return
- https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/readonly
- https://stackoverflow.com/questions/883285/how-does-an-html-form-post-to-an-exe-application
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/enctype
- https://medium.com/@aviator2012/html-form-tags-enctype-attribute-e48f23a08b79
- https://www.w3schools.com/tags/att_form_enctype.asp
- https://stackoverflow.com/questions/64066467/can-http-method-get-be-used-with-multipart-form-data-encoding
- https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/autofocus
- https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled
- https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/maxlength
- https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/minlength
- https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/datetime-local
- https://developer.mozilla.org/en-US/docs/Web/HTML/Date_and_time_formats#local_date_and_time_strings
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email
- https://developer.mozilla.org/en-US/docs/Glossary/Regular_expression
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file
- https://developer.mozilla.org/en-US/docs/Web/HTTP/MIME_types
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/hidden
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/image
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/password
- https://developer.mozilla.org/en-US/docs/Web/Security/Insecure_passwords
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio
- https://stackoverflow.com/questions/5985839/bug-with-firefox-disabled-attribute-of-input-not-resetting-when-refreshing
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/search
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/time
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/url
- https://developer.mozilla.org/en-US/docs/Web/CSS/::after
- https://developer.mozilla.org/en-US/docs/Web/CSS/:enabled
- https://developer.mozilla.org/en-US/docs/Web/CSS/:disabled
- https://developer.mozilla.org/en-US/docs/Web/CSS/:read-write
- https://developer.mozilla.org/en-US/docs/Web/CSS/:read-only
- https://developer.mozilla.org/en-US/docs/Web/CSS/:placeholder-shown
- https://developer.mozilla.org/en-US/docs/Web/CSS/:default
- https://developer.mozilla.org/en-US/docs/Web/CSS/:checked
- https://developer.mozilla.org/en-US/docs/Web/CSS/:indeterminate
- https://developer.mozilla.org/en-US/docs/Web/CSS/:valid
- https://developer.mozilla.org/en-US/docs/Web/CSS/:invalid
- https://developer.mozilla.org/en-US/docs/Web/CSS/:in-range
- https://developer.mozilla.org/en-US/docs/Web/CSS/:out-of-range
- https://developer.mozilla.org/en-US/docs/Web/CSS/:required
- https://developer.mozilla.org/en-US/docs/Web/CSS/:optional
- https://developer.mozilla.org/en-US/docs/Web/CSS/:user-valid
- https://developer.mozilla.org/en-US/docs/Web/CSS/:user-invalid
- https://developer.mozilla.org/en-US/docs/Web/CSS/:hover
- https://developer.mozilla.org/en-US/docs/Web/CSS/:focus
- https://developer.mozilla.org/en-US/docs/Web/CSS/:not
- https://developer.mozilla.org/en-US/docs/Web/CSS/:active

# Creato da La Programmatrice Verde
Chiunque è libero di redistribuire, rielaborare, condividere varianti di questo documento, finché venga citato l'originale come fonte.
