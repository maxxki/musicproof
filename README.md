# MusicProof — Kryptographischer Nachweis für KI-generierte Musik

> **Research Prototype | Not legally validated | Educational use only**

MusicProof demonstriert eine kryptographisch gesicherte Nachweiskette für
KI-generierte Musikwerke. Es dokumentiert Urheberschaft, menschliche
Kreativbeiträge und Integrität — von der ersten KI-Generierung bis zum
fertigen Track.

---

## Motivation

Das BGH-Urteil vom 11.06.2024 (Az. I ZR 192/23) hat klargestellt:
**KI-generierte Werke sind nur urheberrechtlich geschützt, wenn der Mensch
kontrollierende Eingriffe vorgenommen hat.**

MusicProof beweist diese Eingriffe technisch:

- **Wer** hat wann welchen Prompt verwendet
- **Welche** menschlichen Edits wurden vorgenommen
- **Dass** der Track nicht plagiiert ist
- **Wie** Royalties fair verteilt werden

---

## Architektur-Übersicht

┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   KI-Modell │───▶│  Genesis    │───▶│  Human      │───▶│   Final     │
│(StableAudio │    │   Block     │    │   Edits     │    │   Track     │
│   MusicGen) │    │             │    │ (DAW-Plugin)│    │             │
└─────────────┘    └──────┬──────┘    └──────┬──────┘    └──────┬──────┘
│                  │                  │
▼                  ▼                  ▼
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Prompt-Hash│    │  Edit-Hash  │    │ Audio-Hash  │
│  + TSA      │    │  + HSM-Sig  │    │ + Blockchain│
│  + HSM-Sig  │    │  + TSA      │    │ + Smart     │
│             │    │  + Duration │    │   Contract  │
└─────────────┘    └─────────────┘    └─────────────┘
│                  │                  │
└──────────────────┴──────────────────┘
│
▼
┌─────────────┐
│ Hash-Chain  │
│ verifzbar.) │
└─────────────┘
│
▼
┌─────────────┐
│ PDF/A-3b    │
│ Gerichts-   │
│ gutachten   │
└─────────────┘
plain


---

## BGH-Konformität (Az. I ZR 192/23)

| Anforderung | Technischer Nachweis | Status |
|-------------|---------------------|--------|
| **Kontrollierende Eingriffe** | Jeder Edit = eigener Chain-Block mit Timestamp | ✅ Konzept |
| **Schöpfungshöhe** | Gesamtdauer menschlicher Edits (>5 Min = Schutz) | ✅ Konzept |
| **Lückenlose Dokumentation** | Hash-Verkettung Genesis → Final | ✅ Konzept |
| **Integrität** | HSM-Quorum + Dual-TSA + Blockchain | ✅ Konzept |
| **Nachweisbarkeit** | PDF/A-3b Gerichtsgutachten | ✅ Konzept |

---

## Core Features

| Feature | Beschreibung | Technologie |
|---------|-------------|-------------|
| **DAW-Integration** | Erfasst jeden Edit in Echtzeit | VST3/AU Plugin (ZeroMQ + HMAC) |
| **Hash-Chain** | Kryptographisch verkettete Blöcke | SHA-256 + Previous-Hash |
| **HSM-Quorum** | 3-of-5 geografisch verteilte Signaturen | ECDSA-P256 (PKCS#11) |
| **Dual-TSA** | Unabhängige Zeitstempel | Telekom + SwissSign |
| **Blockchain-Anker** | Dezentraler Integritätsbeweis | Bitcoin/Ethereum |
| **Plagiat-Check** | Ähnlichkeitsanalyse + ZKP | Chromaprint/AcoustID |
| **Royalty-Split** | Automatische Verteilung | Solidity Smart Contract |
| **Post-Quantum** | Zukunftssichere Signaturen | SPHINCS+ (NIST FIPS 205) |

---

## Technologie-Stack

| Komponente | Bibliothek | Lizenz |
|------------|-----------|--------|
| DAW-Bridge | ZeroMQ + HMAC | LGPL |
| Krypto-Chain | pycryptodome | BSD |
| HSM-Integration | python-pkcs11 | Apache-2.0 |
| TSA-Zeitstempel | rfc3161 | MIT |
| Blockchain | web3.py | MIT |
| PDF-Report | ReportLab + pikepdf | BSD / MPL-2.0 |
| Post-Quantum | liboqs-python | MIT |
| Smart Contract | Solidity ^0.8.19 | MIT |

---

## Schnellstart

```bash
# 1. Repository klonen
git clone https://github.com/maxxki/musicproof.git
cd musicproof

# 2. Dependencies installieren
pip install -r requirements.txt

# 3. Test-Workflow ausführen
python music_proof_chain.py

Projektstruktur
plain

musicproof/
├── music_proof_chain.py          # Core: Hash-Chain + BGH-Prüfung
├── court_report_generator.py      # PDF/A-3b + PAdES Gerichtsgutachten
├── daw_plugin_bridge.py           # VST3/AU Plugin + HMAC-IPC
├── maxxki_music_proof_bridge.py   # MAXXKI-Registry Integration
├── music_royalty_splitter.py      # Solidity Smart Contract
├── sphincs_plus_wrapper.py        # Post-Quantum Signaturen
├── quantum_fortified_chain.py     # Krypto-Grundlage (HSM, TSA)
└── tests/

Was dieses Repo nicht enthält
❌ Trainierte KI-Modelle (StableAudio, MusicGen) — Nur API-Integration
❌ Produktions-HSM (Thales, Utimaco) — Mock-Implementierung
❌ Echte TSA-Verträge — Entwicklungs-Tokens
❌ Audi-Fingerprint-Datenbank — Nur Interface-Definition
❌ Rechtsgültige Gutachten — Template ohne QP-Review
❌ Deployter Smart Contract — Nur Solidity-Source

    Die rechtliche Wirksamkeit hängt von qualifizierter HSM-Hardware,
    akkreditierten TSA-Diensten, einem beglaubigten Gutachter und der
    konkreten Rechtsprechung des jeweiligen Gerichts ab.

BGH-Urteil 2024 — Zusammenfassung

    "Ein Werk, das mittels KI erzeugt wurde, kann urheberrechtlichen Schutz
    genießen, wenn der menschliche Nutzer die für die Schöpfungshöhe
    maßgeblichen Gestaltungsentscheidungen getroffen hat."

MusicProof beweist diese Entscheidungen:

    Prompt-Design → Genesis-Block mit Prompt-Hash
    Parameter-Tuning → Generation-Params-Hash
    Post-Editing → HumanEditEvent mit Duration + Input-Data
    Mastering → Finalisierungs-Block mit Audio-Hash

Schwelle: ≥ 5 separate Edits ODER ≥ 300 Sekunden Gesamtdauer
Disclaimer
Dies ist ein Forschungsprototyp. Die rechtliche Wirksamkeit der
erzeugten Beweise hängt ab von:

    Qualifizierter HSM-Hardware (FIPS 140-2 Level 3+)
    Akkreditierten Zeitstempeldiensten (eIDAS)
    Beglaubigung durch einen Sachverständigen
    Der konkreten Rechtsprechung des zuständigen Gerichts

Der Code demonstriert technische Machbarkeit, ersetzt aber keine
anwaltliche Beratung oder gerichtliche Anerkennung.
Lizenz
MIT License — Siehe LICENSE
Kontakt 
Für kommerzielle Integration, HSM-Anbindung, TSA-Verträge und
rechtliche Begleitung: Maximilian Kiefer
MusicProof © 2026
