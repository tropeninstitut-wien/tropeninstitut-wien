# WORKFLOW.md — Arbeitsweise & Architektur (Tropeninstitut Wien)

> Diese Datei beschreibt, wie an diesem Projekt gearbeitet wird.
> Sie dient als verbindliche Referenz für **Claude Cowork** und alle, die lokal am Code arbeiten.
> **Bitte vor dem Arbeiten lesen und einhalten.**

---

## 1. Überblick / Architektur

GitHub ist die **einzige Quelle der Wahrheit**. Lovable, der lokale Rechner und Claude Cowork synchronisieren sich ausschließlich über GitHub.

- **Repository:** `github.com/tropeninstitut-wien/tropeninstitut-wien`
- **Repo-Eigentümer-Account:** `tropeninstitut-wien` (eigener GitHub-Account für dieses Kundenprojekt)
- **Arbeits-/Commit-Account:** `martin00-design` (als Collaborator mit Schreibrecht verbunden)
- **Lokaler Ordner:** ein einziger Git-Clone des Repos auf dem Mac. VS Code **und** Claude Cowork arbeiten auf **demselben** Ordner.
- **Editor / Vorschau:** VS Code mit der Erweiterung **Live Preview** (Microsoft).

### Was in diesem Repo liegt
Aktuell **statische HTML-Mockups** für den Kunden, im Ordner `docs/`:
- `docs/index.html` — Übersichtsseite
- `docs/a/`, `docs/b/`, `docs/c/` — die drei Design-Varianten
- `docs/assets/` — Bilder etc.

> **Wichtig:** Dieses Repo ist **reines statisches HTML** — **kein** Build-Schritt.
> Also **kein** `npm install` und **kein** `npm run dev` nötig. Das gäbe einen Fehler
> („no package.json"), weil es kein React-/Vite-Projekt ist.
> Vorschau stattdessen über **Live Preview** in VS Code oder `open docs/a/index.html`.

---

## 2. Wichtige Regel: `main` ist geschützt

Der `main`-Branch ist durch ein GitHub-**Ruleset** geschützt:
**„Changes must be made through a pull request."**

Das bedeutet: **Direktes Pushen auf `main` ist gesperrt.** Jede Änderung muss über
einen eigenen Branch + Pull Request (PR) laufen. Das ist gewollt und gut — es verhindert
später Konflikte, wenn Lovable automatisch in `main` schreibt.

- ❌ Nicht: lokal auf `main` committen und direkt pushen → wird von GitHub abgelehnt
  (`GH013: Repository rule violations`, `Changes must be made through a pull request`).
- ✅ Stattdessen: Branch anlegen → pushen → PR erstellen → mergen (siehe unten).
- ⚠️ Der **„Sync Changes"-Knopf** in VS Code wird auf `main` deshalb immer scheitern.
  Für `main` daher den Branch-+-PR-Weg im Terminal nehmen.

---

## 3. Standard-Workflow (Schritt für Schritt)

Alle Befehle im **VS-Code-Terminal** (`Terminal → New Terminal`).

### Vor dem Arbeiten: neuesten Stand holen
```bash
git checkout main
git pull --no-edit
```

### Arbeiten
- In VS Code ändern und mit `Cmd` + `S` speichern, **oder** von Claude Cowork ändern lassen.
- Ergebnis über **Live Preview** ansehen.

### Änderung auf `main` bringen (Branch + PR)
```bash
git checkout -b feature/kurzer-name
git add .
git commit -m "kurze, klare Beschreibung"
git push -u origin feature/kurzer-name
```
Danach im Browser:
1. Den im Terminal angezeigten Link öffnen (oder das Repo auf GitHub).
2. **Create pull request** klicken.
3. **Merge pull request** → **Confirm merge**.

### Nach dem Merge: lokal wieder aktualisieren
```bash
git checkout main
git pull --no-edit
```

---

## 4. Hinweise speziell für Claude Cowork

- **Immer zuerst `git pull --no-edit` auf `main`**, bevor Änderungen gemacht werden.
- **Niemals direkt auf `main` pushen** — `main` ist geschützt. Immer Branch + PR verwenden.
- Für jede inhaltliche Änderung einen Branch mit sprechendem Namen anlegen
  (`feature/...`, `fix/...`, `chore/...`).
- Commit-Messages kurz und beschreibend halten.
- Dieses Repo ist **statisches HTML** — keine `npm`-Befehle ausführen.
- Vorschau-/Testanweisungen: `open docs/<variante>/index.html` oder Live Preview.

---

## 5. Zukunft: Verbindung mit Lovable

Geplant ist, die eigentliche App später in **Lovable** zu bauen. Dabei gilt:

- **Lovable importiert KEIN bestehendes Repo.** Beim Verbinden mit GitHub legt Lovable
  **immer ein eigenes, neues Repository** an und behandelt seinen Editor als Quelle der Wahrheit.
- Daraus folgt die Struktur:
  - **Dieses Repo (`tropeninstitut-wien`)** bleibt das **Mockup-/Design-Repo**.
  - Für die App entsteht ein **separates Repo**, automatisch von Lovable erstellt.
- Das neue Lovable-Repo wird **genauso lokal geklont** und nach **exakt diesem Workflow** bearbeitet.
- ⚠️ Ein mit Lovable verbundenes Repo **niemals umbenennen, verschieben oder die Lovable-GitHub-App
  deinstallieren** — das bricht den Sync (teils dauerhaft).
- Goldene Regel beim Lovable-Sync: **Nicht gleichzeitig in Lovable und lokal an denselben Dateien
  arbeiten.** Pro Session entweder–oder, dann bleibt der Sync konfliktfrei.

---

## 6. Begriffe in einem Satz

- **Speichern (`Cmd`+`S`)** = nur lokal auf dem Mac.
- **Commit** = Schnappschuss im lokalen Git.
- **Push** = hoch zu GitHub (für `main` nur über Branch + PR möglich).
- **Pull** = neuesten Stand von GitHub holen.
- **PR (Pull Request)** = der vorgeschriebene Weg, einen Branch in `main` zu mergen.
