# raport-ro — structura completa a modelului

Model custom **Ollama** folosit pentru rapoarte AI in limba romana.
Salvat din `/usr/share/ollama/.ollama/models` (server AI) — read-only, nimic modificat pe server.

## Componente incluse in acest repo

```
raport-ro_Vechi_Ai/
├── README.md
├── Modelfile                  # reteta reconstruita (FROM + SYSTEM + TEMPLATE + PARAMS + LICENSE)
├── structura.txt              # fisier descriptiv (manifest/config/params/system/template)
├── manifests/
│   └── registry.ollama.ai/library/raport-ro/latest   # manifestul JSON original
└── blobs/
    ├── sha256-d883bdb8...     # config  (561 B)
    ├── sha256-eb440283...     # template (1.482 B) — ChatML qwen2
    ├── sha256-832dd9e0...     # license (11.343 B)
    ├── sha256-2fcb527e...     # system prompt (357 B) — "analist expert RO"
    └── sha256-bb39d572...     # params (47 B) — {"num_ctx":8192,"temperature":0.5,"top_p":0.9}
```

## ⚠️ LIPSA: weights-ul modelului (NU poate fi pe GitHub)

- Layer-ul de weights `sha256-2bada8a74506...` are **4.683.073.952 B (~4,68 GB)**.
- GitHub NU accepta fisiere mai mari de **100 MB** → **nu a fost inclus**.
- Fara acest fisier modelul NU poate fi rulat/reconstruit identic. Trebuie pastrat in alta parte (alt server / HF / disc extern) inainte de stergerea de pe server.

## Cum se reconstruieste (cu toate fisierele, inclusiv weights-ul)

1. Copiezi `manifests/registry.ollama.ai/library/raport-ro/latest` si toate blobs-urile (inclusiv cel de 4,68 GB) in `/usr/share/ollama/.ollama/models/` pe un host cu Ollama;
2. `ollama list` → va aparea `raport-ro:latest`;
3. Alternativ: `ollama create raport-ro -f Modelfile`.

## Reteta (Modelfile) — esenta modelului

- **FROM:** `qwen2.5:7b-instruct`
- **Familie:** qwen2 | format GGUF | tip 7.6B | cuantizare Q4_K_M | context 32768 (in structura modelului)
- **Params:** `num_ctx 8192`, `temperature 0.5`, `top_p 0.9`
- **System:** "Esti analist expert care scrie EXCLUSIV in limba romana... nu inventezi cifre; marchezi estimarile cu [estimare]; nu lasi rapoartele neterminate."
- **Template:** ChatML (`<|im_start|>`), acelasi ca la qwen2.5:7b-instruct
- **Digest model inregistrat (tags):** `a79c62f1515ec302a5db3f78399e4c4328d9a3790bd5200209ae3af785f9e1e6`
- **modificat:** 2026-07-08 | capabilitati: completion, tools

## Modificat / salvat

- Sursa: server AI `ubuntu-4gb-fsn1-1` (100.89.166.40)
- Salvat: 2026-09-04
