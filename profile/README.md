<!-- DRAFT for Saif's pass -->

# AI-CAD Labs

An open-source AI engineering department for mechanical design:
LLM agent teams that take a plain-language brief to a parametric CAD assembly,
with drawings, design rationale, and manufacturability review along the way.

<!-- BANNER SLOT: rides the 1c taste sitting; interim = none -->

## The repos

| Repo | What it is |
|---|---|
| [**ai-cad**](https://github.com/ai-cad-labs/ai-cad) | The flagship: a Claude Code multi-agent CAD harness. Planning, CAD design, validation, manufacturability review, and assembly negotiation agents collaborate over [CadQuery](https://github.com/CadQuery/cadquery) to design real parts and assemblies. |
| [**ai-cad-example-projects**](https://github.com/ai-cad-labs/ai-cad-example-projects) | The run gallery: complete, unedited design runs with narrative logs, drawings, and exports. |
| [**ai-cad-pydanticai**](https://github.com/ai-cad-labs/ai-cad-pydanticai) | The predecessor implementation (PydanticAI), preserved as a point-in-time research artifact. |

## Start here

Clone [ai-cad](https://github.com/ai-cad-labs/ai-cad) and follow its README quickstart.
Windows users: clone with `git clone -c core.symlinks=true`, or work in WSL.

Every public repo ships under Apache-2.0.
