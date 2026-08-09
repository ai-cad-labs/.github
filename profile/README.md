<div align="center">

![AI-CAD logo](assets/AICAD-org_logo.png)
# AI-CAD Labs

</div>

An open-source organization building the autonomous mechanical-engineering department:
the harness that runs it, the gallery of its real design runs,
and the lineage they grew out of.

[The Flagship Repo](https://github.com/ai-cad-labs/ai-cad) |
[The Repos](#the-repos) |
[Runs Gallery](#design-runs-gallery) |
[Case Study](#case-study) |
[Live Dashboard](#live-dashboard) |
[Quickstart](https://github.com/ai-cad-labs/ai-cad#get-exploring--quickstart) |
[Discussions](https://github.com/ai-cad-labs/ai-cad/discussions)

---

## [AI-CAD](https://github.com/ai-cad-labs/ai-cad) : Our Flagship Repo

**An OSS multi-agent harness for Mech. Eng. CAD**

_AI-CAD is an autonomous engineering department you commission,_

_AI-CAD is not a CAD modeling tool you operate._

Give it a plain-English brief or a hand-drawn sketch,
and a team of LLM agents delivers real, manufacturable parts and assemblies:

- **Plans** : the machine and decomposes it into parts
- **Writes** : parametric [CadQuery](https://github.com/CadQuery/cadquery) Python code
- **Renders** : every part to engineering views, and **looks** at them
- **Critiques** : the geometry against design-for-manufacturing and design-for-assembly rules
- **Repairs** : and re-judges until the design **survives review and delivers your intent**

_Agents **looking** at what they built, and **argue about it** until it **survives review** and **delivers your intent**_

All of this interactively inside your coding agent of choice,
and with visibility in a [**live dashboard**](#live-dashboard).

Every run writes a simple directory of files
that you can read, diff, and version like any other engineering record.

There is **no server** and **no database**.
AI-CAD is built on top of your **coding-agent**.

<div align="center">

![The AI-CAD live dashboard after the impeller run: project header with make/buy part counts, revision and conflict counters, part cards with render thumbnails, and the agent activity waterfall](assets/dashboard.png)

_Your engineering department at work:
parts land as agents deliver, verdicts post,
and the [activity waterfall](#live-dashboard) traces every agent in real time._

</div>

---

## The repos

| Repo | What it is |
|---|---|
| [**ai-cad**](https://github.com/ai-cad-labs/ai-cad) | **The flagship. Start here.** A Claude Code multi-agent CAD harness: planning, CAD design, validation, manufacturability review, and assembly negotiation agents collaborate over [CadQuery](https://github.com/CadQuery/cadquery) to design real parts and assemblies. |
| [**ai-cad-example-projects**](https://github.com/ai-cad-labs/ai-cad-example-projects) | The run gallery: complete, unedited design runs with narrative logs, drawings, and exports. See it work before you run it. |
| [**ai-cad-pydanticai**](https://github.com/ai-cad-labs/ai-cad-pydanticai) | The predecessor implementation (PydanticAI), preserved as a point-in-time research artifact. |

**Ready to run one?**
Clone [**ai-cad**](https://github.com/ai-cad-labs/ai-cad)
and follow its [quickstart](https://github.com/ai-cad-labs/ai-cad#get-exploring--quickstart).

---

## Guiding Design Principles

### Defends design intent

    The system refuses generic manufacturing advice
    that contradicts the intent and machine goals.

(See [the run that argued back](#case-study).)

### Manufacturability is a hard gate, not an afterthought

    A DFM/DFA rulebook scores each design;
    repair proposals that worsen the score are automatically rejected
    by a regression gate with full traceability.

### Agents that see

    Every part and assembly is rendered to 8 engineering views
    (front / top / right / iso, in wireframe and clean styles).

    A vision-capable evaluator agent sees those renders:
    geometry is judged from engineering lenses, not just executed.

### Design machine components as stateful Python code (not immutable mesh props)

    Unlike most text-to-3D tools that generate meshes
    (excellent for game assets and concept art),

    AI-CAD writes parametric CAD code:
    every part is a Python program with named dimensions,

    exporting STEP and STL that a machine shop or downstream CAD system accepts.

### Harness-agnostic

    Canonical agent, skill, and tool content lives once in `.shared/`;
    each harness (`.claude/`, `.opencode/`) is a thin symlinked shell over it.

### The filesystem is the API

    Every run writes a self-describing project directory:
    goals, design log, per-part geometry, negotiation records, reflections.
    Exports STEP and STL for every part.
    No opaque database for facts to hide behind:
    the frontend, replay, and analysis all read the same files.

### Deterministic tool layer

    Geometry execution, rendering, DFMA evaluation, spec validation, dimension checks, and export
    are deterministic bash-callable Python tools.

    Validation happens independently of any LLM.

### Mortality-proof orchestrator

    If the orchestrator agent is killed, or runs out of context window,
    a fresh one reconstructs all state from the project directory alone.

    That is also how a crashed run resumes: no checkpoint database needed.

### Runs debrief themselves

    A run reaches terminal state by writing a structured `run_reflection.md`:
    what failed, what the run improvised to protect the result,
    and what would make the next run smarter.
    Agentic telemetry ships judgment, not just logs.

---

<div align="center">

![The impeller part page in the dashboard: engineering views of the backswept impeller with its validation verdict and DFMA findings](assets/impeller-4view.png)

_Eight views per part, judged like a drawing sheet:
this is what the vision evaluator sees before any geometry ships._

</div>

---

<a name="live-dashboard"></a>

## Live Dashboard : Watch the machine think

<div align="center">

![The dashboard's assembly page after the impeller run: the full assembly in four colored engineering views (top, iso, front, right) with a per-part color legend and the agent activity waterfall](assets/assembly-4view.png)

_2 hours of autonomous design, traced live:
the agent waterfall above,
the assembly taking shape in four engineering views._

</div>

A read-only local dashboard renders live runs:
drawing sheets, assembly negotiations, and a live agent activity waterfall.
It ships with the [flagship repo](https://github.com/ai-cad-labs/ai-cad)
and reads the run's files directly: the filesystem is the API.

---

## Design Runs Gallery

Real, unedited design runs live in the public gallery:
[`ai-cad-labs/ai-cad-example-projects`](https://github.com/ai-cad-labs/ai-cad-example-projects).
Every run ships its spec, plan, step-by-step design log, per-part geometry,
multi-view renders, STEP/STL exports, and its own debrief.
No geometry there was human-authored.

| Run | What it built | The numbers | Wall clock |
|---|---|---|---|
| [`impeller_assembly`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/impeller_assembly) | A belt-driven centrifugal compressor core, from a hand-drawn sketch ([the case study](#case-study)) | 6 components (3 designed, 3 catalog) · 0.8000 mm clearance measured five ways · 6 backswept blades at 10.5° · reviewer verdict: ship | ~2h12m |
| [`piston_crank`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/piston_crank) | The 5-part IC-engine core at top-dead-center | 7-instance assembly · a locked dimension chain that held end-to-end · mid-run self-checkpoint and cold resume | 71.3 min |
| [`spur_gear`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/spur_gear) | A meshing involute gear pair | Deterministic mesh proof: 0.00 mm³ interference at the correct half-tooth phase · 0 repair cycles | ~49.8 min |
| [`treasure_chest`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/treasure_chest) | The control baseline: a 4-part chest | 13 agents, 0 failures, 0 repairs · 3 findings deferred with written reasoning | 32.8 min |

<a name="case-study"></a>

<details>
<summary>
<h2>Case Study : Impeller Assembly : the run that argued back</h2>

<div align="center">

![A centrifugal compressor assembly in shaded isometric: six backswept impeller blades in green on an upright bearing housing in red, grooved pulley-shaft behind, lock nut and small inlet bearing on the shaft nose](assets/assembly-iso-filled.png)

**Designed end-to-end from a single hand-drawn sketch:**
_a six-component impeller rig assembly,
rendered from the design run's assembly geometry._

Details: the [`impeller_assembly`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/impeller_assembly) run in the public gallery.

</div>

</summary>

The best argument for the architecture is a run where the system
disagreed with its own tooling and was right.
Every claim below is on file in the public exhibit:

[`impeller_assembly`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/impeller_assembly).

The input was a hand-drawn cross-section sketch and a five-bullet brief:
a belt-driven centrifugal compressor core with backswept blades.

Moments from that run show what a manufacturing gate with judgment looks like:

- **The system defended the user's design intent against its own evaluator.**
  Mid-run, the DFM evaluator (judging the wheel under a mis-selected
  3-axis milling ruleset) recommended cutting the impeller to 4 blades
  and straightening them into flat radial walls.
  That advice would have quietly destroyed exactly what the brief asked for.
  Both orchestrator generations refused it,
  recorded the refusal in `open_issues.md`,
  and passed an explicit do-not-comply guard downstream
  so no later agent could obey it by accident.
- **The headline requirement shipped as a machined dimension.**
  The brief asked for 0.5 to 1.0 mm of running clearance;
  the run delivered 0.8000 mm,
  confirmed by five independent measurements
  and realized structurally in a part,
  not left to an assembly stack-up that can drift.

User intent held as a first-class constraint,
not one voice in a negotiation the tooling usually wins.
The full record, refusals included, is public and unedited:

  6 STEP/STL exports,
  fourteen agent spawns across 2 sessions,
  roughly 2h12m of autonomous work, one repair cycle,
  reviewer verdict: ship.

The complete provenance chain,
from sketch to brief to per-part geometry to the run's own debrief,
is public:
[`impeller_assembly`](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/impeller_assembly)
[`run_reflection.md`](https://github.com/ai-cad-labs/ai-cad-example-projects/blob/main/impeller_assembly/run_reflection.md).

[Read the full exhibit](https://github.com/ai-cad-labs/ai-cad-example-projects/tree/main/impeller_assembly) | [Browse all runs](https://github.com/ai-cad-labs/ai-cad-example-projects)

</details>

---

## Getting help

The canonical help page is
[**SUPPORT.md**](https://github.com/ai-cad-labs/.github/blob/main/SUPPORT.md).
The short version:

- **Questions and problems**: open an issue on
  [github.com/ai-cad-labs/ai-cad](https://github.com/ai-cad-labs/ai-cad/issues).
- **"What should healthy output look like?"**: study a complete run in the
  [run gallery](https://github.com/ai-cad-labs/ai-cad-example-projects).
- **Conventions and internals**:
  [`AGENTS.md`](https://github.com/ai-cad-labs/ai-cad/blob/main/AGENTS.md)
  is the canonical map for anyone (human or agent) working in the flagship repo.

## Contribution Invitation

Contributions are welcome, and we want you to feel welcome making them.

You do not need to be a CAD veteran
or a machine-learning engineer to have a big impact:
documentation, DFM/DFA rule improvements, gallery runs,
and issue reports all move the project forward.

| Channel | Best for |
|---|---|
| [Issues](https://github.com/ai-cad-labs/ai-cad/issues) | Bugs and defects |
| [Discussions](https://github.com/ai-cad-labs/ai-cad/discussions) | Show your runs, ask questions, propose machines |

**Suggesting a feature or a rule**:

open an issue describing the change and why it matters.
DFM/DFA rule proposals are a first-class contribution surface:
the rulebooks have a documented proposal schema
(see the [`dfm-rules` skill](https://github.com/ai-cad-labs/ai-cad/tree/main/.shared/skills/dfm-rules)),
and rules can be proposed, promoted, or retired over time.

Full contribution instructions, including bug-report format and test suites:
[**CONTRIBUTING.md**](https://github.com/ai-cad-labs/.github/blob/main/CONTRIBUTING.md).

---

## License

Every public **ai-cad-labs** repo ships under the
[Apache License 2.0](https://github.com/ai-cad-labs/ai-cad/blob/main/LICENSE),
each with its own LICENSE and
[NOTICE](https://github.com/ai-cad-labs/ai-cad/blob/main/NOTICE);
the NOTICE attribution travels with every redistribution.

<details>
<summary><h2>Citing AI-CAD</h2></summary>

```bibtex
@software{ai_cad,
  title   = {AI-CAD: a multi-agent mechanical CAD harness},
  author  = {{Saif Raja on behalf of the ai-cad-labs project}},
  year    = {2026},
  url     = {https://github.com/ai-cad-labs/ai-cad},
  license = {Apache-2.0}
}
```

</details>

---

If you read this far,
[open an issue](https://github.com/ai-cad-labs/ai-cad/issues) with the machine you want designed, \
and it **will** get run.

**⭐ If AI-CAD is useful to you, please consider giving [the flagship](https://github.com/ai-cad-labs/ai-cad) a star! It helps⭐**

---

<div align="center">

_Maintained by [@saif-raja](https://github.com/saif-raja) on behalf of **AI-CAD Labs**._

_**Copyright** (C) 2026, per each repo's LICENSE._

</div>
