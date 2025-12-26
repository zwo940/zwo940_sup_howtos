<!-- SPDX-License-Identifier: Apache-2.0 -->
<!-- Copyright 2025 Marcus-Erich Seidler (zwo940.de) -->


````md
# zwo940_sup_howtos – Mini-Howto: Repo initialisieren & auf GitHub pushen

Dieses Howto beschreibt, wie ich einen lokalen Ordner als eigenes Git-Repo initialisiere und auf GitHub veröffentliche.

## Voraussetzungen

- Git ist installiert (`git --version`)
- SSH zu GitHub funktioniert (optional, aber empfohlen):
  ```bash
  ssh -T git@github.com
````

Erwartung: „You've successfully authenticated …“

## Ziel

Ich möchte den Ordner `~/dev/projects/zwo940_sup_howtos` als eigenes Git-Repo pflegen und nach GitHub pushen.

---

## 1) In den Ordner wechseln

```bash
cd ~/dev/projects/zwo940_sup_howtos
```

## 2) Git-Repo initialisieren

```bash
git init
```

Optional: Standard-Branch auf `main` setzen (nur falls du noch keinen Commit hast):

```bash
git branch -M main
```

## 3) Sinnvolle .gitignore anlegen (minimal)

Erstelle eine Datei `.gitignore` im Ordner und füge z. B. hinzu:

```gitignore
.DS_Store
Thumbs.db
.idea/
.vscode/
*.tmp
```

> Hinweis: Für reine Markdown-Howtos reicht das oft.

## 4) Erste Dateien committen

```bash
git add .
git commit -m "Initial commit: zwo940_sup_howtos"
```

Falls Git nach Name/E-Mail fragt:

```bash
git config --global user.name "Marcus-Erich Seidler"
git config --global user.email "e-mail@marcus-seidler.de"
```

Dann erneut committen.

## 5) GitHub-Repo erstellen

Auf GitHub:

* New repository
* Name: `zwo940_sup_howtos`
* **Keine** README/License/Gitignore automatisch hinzufügen (damit es keinen Merge-Konflikt gibt)
* Repository erstellen

## 6) Remote setzen (SSH empfohlen)

```bash
git remote add origin git@github.com:<DEIN_GITHUB_USER>/<REPO_NAME>.git
```

Beispiel:

```bash
git remote add origin git@github.com:zwo940/zwo940_sup_howtos.git
```

Prüfen:

```bash
git remote -v
```

## 7) Push nach GitHub

```bash
git branch -M main
git push -u origin main
```

Prüfen (optional):

```bash
git ls-remote origin
```

---

## 8) Typische Fehler & Fixes

### A) `src refspec main does not match any`

Ursache: Noch kein Commit gemacht.

Fix:

```bash
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

### B) `remote origin already exists`

Fix:

```bash
git remote set-url origin git@github.com:<USER>/<REPO>.git
```

### C) `Permission denied (publickey)`

Fix:

1. SSH testen:

   ```bash
   ssh -T git@github.com
   ```
2. Falls nötig: SSH-Key erstellen und bei GitHub hinzufügen.

---

## 9) Alltag: Änderungen pushen

```bash
git status
git add .
git commit -m "Docs: <kurze Beschreibung>"
git push
```

---

## Empfehlung für meinen Workspace (Multi-Repos)

Workspace-Root: `~/dev/projects` ist **kein** Git-Repo.

Eigene Repos:

* `zwo940_app_vorrat`
* `zwo940_pkg_core`
* `zwo940_pkg_ui`
* `zwo940_sup_howtos` (dieses Repo)
* `zwo940_sup_instructions`
* `zwo940_sup_scripts`
