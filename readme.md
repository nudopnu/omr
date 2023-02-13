# Readme
_- Getestet unter Windows 10 x64 -_

## Inhalt/Ordner

- `code`

    Beinhaltet ein Skript zum Klonen folgender Repositories:
    - https://github.com/nudopnu/omr-unet
    - https://github.com/nudopnu/omr-application

- `datasets/generated/abc`

    Beinhaltet vorgenerierte ABC-Dateien, die zum Trainieren des U-Nets verwendet wurden.

- `datasets/generated/classlist.json`

    Datei mit Informationen über die verwendeten Symbolklassen.

- `datasets/generated/base_dataset.zip`

    Enthält, ausgehend von den vorgenerierten ABC-Dateien, `pdf`- und `png`-Versionen der Notenblätter sowie Bounding-Box-Informationen im Ordner `bbox`.

- `datasets/samples`

    Beinhaltet Beispieldateien, die von der Anwendung gelesen werden können einschließlich der Ausgaberesultate als ABC-Dateien.

- `models`

    Beinhaltet ein vortrainiertes U-Net-Model

## Setup

1. __Repositories klonen__

    Wahlweise `code/fetch-repos.sh` ausführen, oder selbst beide Repositories in den Ordner `code` Klonen:
    ```bash
    git clone https://github.com/nudopnu/omr-unet.git
    git clone https://github.com/nudopnu/omr-application.git
    ```

2. __OMR Anwendung starten__

    _Voraussetzungen_:
    - NodeJS: https://nodejs.org/en/download/
    - ImageMagick: https://imagemagick.org/script/download.php#windows 
  
        Die Datei `ImageMagick-7.1.0-62-Q16-HDRI-x64-dll.exe` herunterladen und installieren. Anschließend das Installationsverzeichnis, bspw. `C:\Program Files\ImageMagick-7.1.0-Q16-HDRI`, der `PATH`-Variable hinzufügen.

    In den Ordner `code/omr-application/` wechseln und dort die lokalen Abhängigkeiten installieren und anschließend die Anwendung starten:

    ```bash
    npm install
    npm start
    ```

3. __Basis-Datensatz generieren__

    Nach Starten der Anwendung den ABC-Editor über den Button `Open Editor` öffnen. Anschließend sämtliche `*.abc`-Dateien aus dem Ordner `datasets/generated/abc/` per Drag-And-Drop in den Bereich `- Drop abc files here -` ziehen und den darunterliegenden Button `Run all jobs` anklicken. Dieser Prozess dauert eine Weile aufgrund der hochauflösenden Rasterierung. Alternativ kann auch der Inhalt von `datasets/generated/base_dataset.zip` den Ordner `datasets/generated/` entpackt werden.
    
4. __Training des U-Nets__

    In den Ordner `code/omr-unet` wechseln und die erforderlichen Python Packages installieren:

    ```bash
    pip install -r requirements.txt
    ```

    Anschließend die Jupyter notebooks der Reihe nach ausführen:

    1. `01_augmentation.ipynb`: Erzeugt Augmentierungen anhand der erzeugten PNG-Masken
    2. `02_dataset_generation.ipynb`: Erzeugt Eingabebilder der Größe 256x256 zum Trainieren des das U-Nets
    3. `03_train.ipynb`: Trainiert und evaluiert das U-Net

## Testen der Pipeline

In den Ordner `code/omr-application/` wechseln und dort die Anwendung starten:

```bash
npm start
```

Per Drag-And-Drop Klaviernoten in Form von `png`-Dateien in die Anwendung (bspw. `datasets/samples/sheet_01.png`) laden. Rechts oben unter `Pick a model` ein trainiertes Model (bspw. `unet_256x256_pretrained.h5`) auswählen und kurz warten. Anschließend auf den Button `Read Sheet Music` klicken und die Pipeline wird angestoßen.