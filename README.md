# stereoscopic_prediction

# Predizione dell'Immagine Stereoscopica con Reti Convoluzionali

Questo progetto utilizza un modello di rete convoluzionale encoder-decoder per prevedere l'immagine destra in un setup stereoscopico partendo da una singola immagine RGB (camera sinistra). Il dataset utilizzato è **Flickr1024**, caratterizzato da immagini di scena sinistra (con suffisso `_L`) e destra (con suffisso `_R`). Il modello è stato addestrato con una funzione di perdita combinata di **SSIM** e **RMSE** per migliorare la qualità della previsione.

## Requisiti

Prima di eseguire il progetto, assicurarsi di avere:

- Python 3.12.5 installato.
- Un ambiente con librerie di machine learning e computer vision per gestire il modello e il preprocessing delle immagini.

## Dipendenze

Assicurarsi di installare le seguenti librerie per eseguire il progetto. Utilizzare il comando:

```bash
pip install tensorflow opencv-python numpy matplotlib scikit-image pillow gdown
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
```

### Organizzazione delle immagini
Ogni sottocartella (`Test`, `Validation`, `Training`) contiene immagini stereo con nomi che terminano con `_L` per le immagini sinistre e `_R` per quelle destre. Esempio di nomi di file:

```
- esempio1_L.png (immagine sinistra)
- esempio1_R.png (immagine destra)
```

## Istruzioni per l'esecuzione del progetto

### 1. Configurazione dell'ambiente virtuale

**Opzione 1: Utilizzo di Anaconda**
- Creare un nuovo ambiente con Python 3.12.5:
  ```bash
  conda create -n stereovision python=3.12.5
  ```
- Attivare l’ambiente:
  ```bash
  conda activate stereovision
  ```

**Opzione 2: Ambiente virtuale con `venv`**
- Creare e attivare un ambiente virtuale:
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
  dataset_dir = "path/to/dataset/Flickr1024"
  ```
- Sostituire `"path/to/dataset/Flickr1024"` con il percorso effettivo della cartella `dataset/Flickr1024`.

### 4. Addestramento del modello
- Per addestrare il modello, eseguire il notebook o il file di script configurato.
- Durante l'addestramento, il modello utilizzerà le immagini nel dataset `Training` e validerà le prestazioni con il set `Validation`.

### 5. Valutazione su immagini di test
- Una volta addestrato, il modello può essere testato sulle immagini presenti nella cartella `Test` del dataset.
- I risultati vengono visualizzati confrontando le immagini sinistre (input) e quelle destre (target) con le previsioni del modello.

### Opzioni di Salvataggio e Checkpoint
- Il modello e le metriche vengono salvati automaticamente utilizzando callback come `ModelCheckpoint` e `EarlyStopping` per evitare il sovra-allenamento.

## Esecuzione del codice

Eseguire tutte le celle nel notebook o eseguire il file Python per addestrare il modello e visualizzare i risultati. 

---

Questo README è organizzato per fornire tutte le informazioni necessarie a impostare il progetto in un ambiente di sviluppo e permette di gestire facilmente le dipendenze e il dataset.
