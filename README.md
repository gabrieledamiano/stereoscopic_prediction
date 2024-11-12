## Predizione dell'Immagine Stereoscopica con Reti Convoluzionali

Questo progetto utilizza un modello di rete convoluzionale encoder-decoder per prevedere l'immagine destra in un setup stereoscopico partendo da una singola immagine RGB (camera sinistra). Il dataset utilizzato è **Flickr1024**, caratterizzato da immagini di scena sinistra (con suffisso `_L`) e destra (con suffisso `_R`). Il modello è stato addestrato con una funzione di perdita combinata di **SSIM** e **RMSE** per migliorare la qualità della previsione.

## Requisiti

Prima di eseguire il progetto, assicurarsi di avere:

- Python 3.12.5 installato.
- Un ambiente con librerie di machine learning e computer vision per gestire il modello e il preprocessing delle immagini.

## Dipendenze

Assicurarsi di installare le seguenti librerie per eseguire il progetto. Utilizzare il comando:

```bash
pip install tensorflow opencv-python numpy matplotlib scikit-image pillow gdown tqdm
```

### Librerie principali utilizzate:
- `tensorflow`: per costruire e addestrare il modello encoder-decoder.
- `opencv-python` (`cv2`): per la gestione delle immagini.
- `numpy`: per le operazioni numeriche.
- `matplotlib`: per la visualizzazione delle immagini e dei risultati.
- `scikit-image`: per calcolare SSIM e PSNR.
- `gdown`: per scaricare dataset direttamente da Google Drive, se necessario.
- `tqdm`: per le barre di avanzamento durante l’elaborazione.
- `json`: per salvare e caricare configurazioni e risultati.

**Note**: La lista completa dei pacchetti importati è `os, cv2, numpy, tensorflow, matplotlib.pyplot, ImageDataGenerator, EarlyStopping, ModelCheckpoint, ReduceLROnPlateau, train_test_split, tqdm, json, load_model, random`.

## Struttura del Progetto

Organizzare la cartella del progetto come segue per garantire il corretto funzionamento del codice:

### Struttura Iniziale
All'inizio, il progetto richiede solo la cartella **dataset/Flickr1024**, organizzata come segue:

```
├── dataset/Flickr1024/                     # Cartella principale del dataset
│   ├── Test/                               # Dataset di test
│   ├── Validation/                         # Dataset di validazione
│   └── Training/                           # Dataset di addestramento
├── ProgettoVP_Autoencoder.ipynb            # Notebook Jupyter contenente il codice
```

### Organizzazione delle immagini
Ogni sottocartella (`Test`, `Validation`, `Training`) contiene immagini stereo con nomi che terminano con `_L` per le immagini sinistre e `_R` per quelle destre. Esempio di nomi di file:

```
- esempio1_L.png (immagine sinistra)
- esempio1_R.png (immagine destra)
```

## Istruzioni per l'esecuzione del progetto

### 1. Configurazione dell'ambiente virtuale

È possibile configurare l’ambiente virtuale in due modi: tramite interfaccia grafica di Anaconda oppure tramite prompt di comando. 

#### Opzione 1: Utilizzo dell’interfaccia grafica di Anaconda

1. **Aprire Anaconda Navigator**.
2. **Selezionare la scheda "Environments"** nella barra laterale.
3. **Cliccare su "Create"** per creare un nuovo ambiente.
4. **Assegnare un nome all'ambiente** (ad esempio `stereovision`).
5. Selezionare **Python 3.12.5** come versione del linguaggio.
6. Cliccare su **"Create"** per avviare la creazione dell'ambiente. Anaconda impiegherà alcuni minuti per configurare l'ambiente con le librerie di base.
7. Una volta completato, l'ambiente sarà pronto all’uso. È possibile installare ulteriori librerie nella sezione "Environments" utilizzando il comando pip o con il pulsante **"Open Terminal"** all'interno di Anaconda Navigator.

#### Opzione 2: Creazione tramite Prompt di Comando di Anaconda

1. Aprire il **Prompt di Anaconda**.
2. Eseguire il seguente comando per creare un nuovo ambiente:
   ```bash
   conda create -n stereovision python=3.12.5
   ```
3. Attivare l’ambiente con:
   ```bash
   conda activate stereovision
   ```

#### Opzione 3: Ambiente virtuale con `venv` (Prompt di Comando)

1. Creare e attivare un ambiente virtuale:
   ```bash
   python3 -m venv stereovision_env
   source stereovision_env/bin/activate  # Su Windows: stereovision_env\Scripts\activate
   ```

### 2. Installazione delle dipendenze
Installare le librerie necessarie tramite pip:
```bash
pip install tensorflow opencv-python numpy matplotlib scikit-image pillow gdown tqdm
```

### 3. Configurazione del percorso del dataset
- Assicurarsi che il percorso del dataset sia specificato correttamente nel codice:
  ```python
  base_dir = r'C:/TuoPercorso'  # Modificare questa variabile per cambiare la base del percorso
  dataset_dir = os.path.join(base_dir, "dataset/Flickr1024")
  ```
- Sostituire `TuoPercorso` con il percorso effettivo della cartella che contiene il dataset. Il percorso completo sarà concatenato a `"dataset/Flickr1024"` per indicare la posizione effettiva del dataset.

### Download del Dataset
Il dataset **Flickr1024** può essere scaricato automaticamente direttamente dal notebook `ProgettoVP_Autoencoder.ipynb`. Il notebook contiene una funzione che utilizza l’ID del file di Google Drive per scaricare e decomprimere il dataset nella cartella `dataset/Flickr1024`, organizzando il contenuto nelle cartelle `Test`, `Validation` e `Training`. 

> **Nota**: Il dataset viene scaricato solo se non è già presente in locale nella struttura di cartelle specificata.


### 4. Addestramento del modello
- Per addestrare il modello, eseguire il notebook `ProgettoVP_Autoencoder.ipynb` o il file di script configurato.
- Durante l'addestramento, il modello utilizzerà le immagini nel dataset `Training` e validerà le prestazioni con il set `Validation`.

### 5. Valutazione su immagini di test
- Una volta addestrato, il modello può essere testato sulle immagini presenti nella cartella `Test` del dataset.
- I risultati vengono visualizzati confrontando le immagini sinistre (input) e quelle destre (target) con le previsioni del modello.

### Opzioni di Salvataggio e Checkpoint
- Il modello e le metriche vengono salvati automaticamente utilizzando callback come `ModelCheckpoint` e `EarlyStopping` per evitare il sovra-allenamento.

## Modello Preaddestrato

È disponibile un modello preaddestrato nel file `complete_autoencoder_combined_ssim_rmse.keras`, che può essere utilizzato per verificare il codice e valutare la qualità delle predizioni senza eseguire un nuovo addestramento. Questo file `.keras` fa riferimento a un modello già addestrato che consente un rapido test e verifica del codice.

## Esecuzione del codice

Eseguire tutte le celle nel notebook `ProgettoVP_Autoencoder.ipynb` per addestrare il modello e visualizzare i risultati. 

---

Questo README è strutturato per fornire tutte le informazioni necessarie a impostare il progetto in un ambiente di sviluppo, gestire facilmente le dipendenze e il dataset, utilizzare un modello preaddestrato per il test e lavorare con il notebook Jupyter `ProgettoVP_Autoencoder.ipynb`.
