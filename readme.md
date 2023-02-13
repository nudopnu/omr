# Readme

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

- `models`

    Beinhaltet ein vortrainiertes U-Net-Model

## Initiales Setup

1. __Repositories Klonen__

    Wahlweise `code/fetch-repos.sh` ausführen, oder selbst beide Repositories in den Ordner `code` Klonen:
    ```bash
    git clone https://github.com/nudopnu/omr-unet.git
    git clone https://github.com/nudopnu/omr-application.git
    ```

2. __OMR Anwendung__

    _Voraussetzungen_:
    - NodeJS: https://nodejs.org/en/download/

    In den Ordner `code/omr-application/` wechseln und dort die lokalen Abhängigkeiten installieren:
    ```bash
    npm install
    ```
3. __Basis-Datensatz entpacken__

    Inhalt von `datasets/generated.zip` in gleichnamigem Ordner `datasets/generated/` entpacken.