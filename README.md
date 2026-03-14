# ColpoAI — AI-Assisted Cervical Lesion Detection at Colposcopy

A clinical decision support tool for detecting pre-cancerous cervical lesions at colposcopy, built to support a nurse + GP remote workflow in low-resource settings.

This project is the technical implementation supporting the research study:
**"Development and Validation of an AI Model for Detection of Pre-cancerous Cervical Lesions at Colposcopy"**
— University of Limpopo, Faculty of Health Sciences, School of Medicine
— Funded by SAfAIDS and ASCCP (Australian Society for Colposcopy and Cervical Pathology)

---

## What it does

ColpoAI analyses colposcopy images and outputs a structured clinical decision support report for each case, including:

- **Probability scores** across four classifications: Cervical Cancer, HSIL, LSIL, Normal
- **Confidence score** with transparent factor-by-factor breakdown (explainability layer)
- **Recommended next action**: urgent review, follow-up per protocol, or escalation
- **Observed visual cues** and visibility limitations documented per case
- **Clinician handover output** formatted for nurse capture → GP review workflow

The tool runs locally in the browser — no server, no data upload, no external API calls during clinical use.

---

## Clinical context

Cervical cancer is the leading cause of cancer-related deaths among women in South Africa, with an age-standardised incidence rate of 35.3 per 100,000 — nearly three times the global average.

Key challenges this tool addresses:
- **Inter-observer variability** in colposcopy interpretation (accuracy reported at ~84.5% even among experienced clinicians)
- **Limited specialist access** — only 12.6% of clinicians across 23 African countries had received colposcopy training
- **Centralised services** concentrated in tertiary hospitals, creating long wait times for diagnosis
- **Algorithmic bias** — existing AI models are not validated on South African cervical image data

ColpoAI is designed to support task-sharing: nurses capture images in the field, the AI provides a structured triage output, and the GP reviews remotely.

---

## AI model & logic

- Built using **Generative AI** for model logic development and interface generation
- Classification output: `cervical_cancer`, `hsil`, `lsil`, `normal`
- Confidence scoring uses a **rule-based explainability layer (rule_based_v1)** that maps observed visual cues and visibility limitations to a confidence score with full audit trail
- Visual cues scored include: exophytic/mass-like lesions, friability/active bleeding, heterogeneous surface, ulcerated architecture
- Penalties applied for: specular glare, blood obscuring the cervix, speculum occlusion
- All reasoning is surfaced in the UI — no black-box outputs

---

## Study design (research backing)

- **Study type**: Prospective observational cohort
- **Target N**: ~500 patients, ~2,000 images (pre-acetic acid, post-acetic acid, post-Lugol's iodine)
- **Gold standard**: Histopathology from LLETZ / cone biopsy specimens
- **Study sites**: Mankweng Provincial Hospital (public) + Quality Care Private Hospital (private), Limpopo, South Africa
- **Primary objective**: Classify images into Normal / LSIL / HSIL+ using histopathology as reference
- **Secondary objectives**: Compare public vs. locally fine-tuned model performance; benchmark AI vs. trained colposcopists; evaluate usability

---

## Running locally

Open `colpo_ai.html` directly in any modern browser. No installation required.

Case data is embedded as a structured JSON object in the HTML — update the `CASE` variable to load a new case.

---

## Project structure

```
oncology/
├── colpo_ai.html                        # Main clinical decision support interface
├── a_002.html                           # Alternate interface version
├── ColpoAi Final Research Proposal.pdf  # Full research proposal (University of Limpopo)
├── a_data/                              # Build assets
├── a_data_002/                          # Build assets (v2)
└── js/                                  # JavaScript modules
```

---

## Authors & collaborators

- **Silvia Adinda** — AI model logic, interface development, technical implementation
- **Dr. Lucia Chimanga** — Principal Investigator, University of Limpopo
- **Dr. Claris Tigere** — Co-Investigator, Quality Care Private Hospital

---

## Disclaimer

This tool is for **clinical decision support only**. It does not establish a diagnosis. All outputs must be confirmed using local clinical guidelines and appropriate referral pathways. Not a substitute for standard of care.
