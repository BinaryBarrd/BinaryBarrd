<img src="assets/banner.svg" width="100%" alt="Aditya Bansal, AI safety researcher: How can I trust a model I can't fully see inside?">

<p align="center">
  <a href="https://linkedin.com/in/binarybarrd"><img src="https://img.shields.io/badge/LinkedIn-binarybarrd-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="https://x.com/BinaryBarrd"><img src="https://img.shields.io/badge/X-@BinaryBarrd-000000?style=flat-square&logo=x&logoColor=white" alt="X"></a>
  <a href="https://orcid.org/0009-0008-5408-3434"><img src="https://img.shields.io/badge/ORCID-0009--0008--5408--3434-A6CE39?style=flat-square&logo=orcid&logoColor=white" alt="ORCID"></a>
</p>

I'm an undergrad at BITS Pilani trying to figure out how AI systems fail when someone is actually trying to break them: how they fail, why they fail, and whether they deserve the trust people put in them. Benchmarks only tell part of that story, so I go looking for the rest. I implement backdoor attacks, poke around inside models with mechanistic interpretability, and audit AI systems and web services that are already out in the real world.

Alongside that, I work at a startup building production voice agents and pipelines. Next, I want to point the same lens at them: where voice pipelines break, and what it takes to make them safe.

### Right now

- **Researching:** how AI systems signal trustworthiness, and whether those signals hold up under audit
- **Building:** real-time voice agents and retrieval services at a stealth AI startup
- **Open to:** research internships · predoc roles · AI safety fellowships · applied ML research

---

### The thread: break it, look inside, audit it, build it

#### 🧪 Break it
**How cheaply can a model be compromised?** 250 poisoned samples are enough to plant a backdoor in an LLM.

<details>
<summary>Details</summary>
<br>

- [Replicated constant-number data poisoning](https://github.com/BinaryBarrd/Poisoning-attacks-on-LLMs-using-small-sample-size) (Souly et al., 2025) on Pythia-410M with a denial-of-service backdoor.
- Clean perplexity stays at 32; on the trigger it jumps to 643. Token-wise loss analysis shows the exact moment the trigger breaks the model.
- The whole pipeline trains on an 8 GB MacBook (Adafactor, gradient accumulation, FP32), so anyone can reproduce it.

</details>

#### 🔬 Look inside
**A black-box test can't catch a model that knows it's being tested, so I work white-box.**

<details>
<summary>Details</summary>
<br>

- Framed LLM backdoor auditing as a [Stackelberg security game](https://github.com/adityasharma1307/white-box-using-ssg): a defender with a limited budget picks which layers to inspect, and an adversary plants or amplifies backdoors with LoRA.
- Led the probe side: activation-steering detectors in TransformerLens.
- Found a geometric asymmetry: backdoors planted from scratch form detectable activation clusters, while backdoors that amplify something already latent in the model hide in its existing geometry and evade standard probes.
- Submitted to the ICML 2026 Mechanistic Interpretability Workshop.

</details>

#### 🔍 Audit it: *current focus*
**The models deciding what we pay and what we qualify for are rarely inspected, and their trust cues rarely say what they rest on.**

<details open>
<summary>Details</summary>
<br>

- **AI trustworthiness cue taxonomy** (2026–present), mentored by Prof. Siddharth Mehrotra (BITS Pilani) and Prof. Pascal König (VU Amsterdam). A two-layer taxonomy of trust cues (scores, badges, explanations, disclaimers) across finance, healthcare and content moderation. Each cue traces back to NIST AI RMF properties and is classified on six dimensions and by who receives it.
- **[Loan eligibility audit](https://github.com/BinaryBarrd/loan-eligibility-audit):** black-box audited nine Indian lenders' eligibility calculators and built a method that recovers each rule from its probe log alone. All nine are fixed formulas (1,507 / 1,507 probes matched within ₹1), yet they give the same person very different "You are eligible" answers.
- **User study:** participants compare nine anonymised lenders on their own figures, then rate trust before and after the hidden assumptions are revealed. Measured on a validated scale (McKnight et al., 2011) and mapped back onto the taxonomy.
- **Ride-hailing pricing** (IIT BHU, 2025): 100 routes queried at the same moment from 6 accounts on iOS and Android. 58% of routes showed fare differences between devices, yet OS-level discrimination was ruled out (p > 0.13). Findings presented to the Central Consumer Protection Authority, Ministry of Consumer Affairs, Government of India.

</details>

#### 🎙️ Build it
**I build the kind of system I study, which keeps the research honest.**

<details>
<summary>Details</summary>
<br>

- I own the real-time voice pipeline: streaming TTS over a custom WebSocket protocol, four swappable vendors, and model-native turn detection. Time to first audio fell from **2.1 s to under 300 ms** in production.
- I built the retrieval service, with output guardrails that stop answers leaking without blocking legitimate questions. Caching cut repeat lookups from 1.5 s to 30–50 ms.
- Every LLM output is checked against a deterministic parser before it's accepted. When four runs failed in a row, all four were gaps in my prompts, not the model misbehaving. Most of the time, trust comes down to verification like this.

</details>

---

### Toolkit

`PyTorch` `Transformers` `TransformerLens` `PEFT / LoRA` `CVXPY` `SHAP` `XGBoost` `FastAPI` `Vector DBs` `Streaming STT/TTS` `LLM agents`

<sub>Before safety: as a founding engineer at an earlier startup (2024), I trained RL policies for satellite collision avoidance. That was my first time working on a system where an unexplained decision is not acceptable.</sub>
