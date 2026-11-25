# FSL BET Skull Strip

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Skull-strips a T1-weighted image with FSL bet using a configurable fractional intensity threshold and outputs the brain-extracted T1w.**

Runs FSL bet on the T1w with -f frac inside the brainlife/fsl 6.0.4 container (robust centre estimation and bias/neck clean-up are not used). Use it as a simple, fast brain extraction; lower frac values give a larger brain outline.

| | |
|---|---|
| 📥 **Inputs** | `neuro/anat/t1w` |
| 📤 **Outputs** | `neuro/anat/t1w` |
| 🐳 **Container** | `brainlife/fsl:6.0.4-patched2` |
| ⚙️ **Resources** | 4 GB memory · 1 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.953](https://doi.org/10.25663/brainlife.app.953) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `t1` | `neuro/anat/t1w` | yes | T1-weighted image (NIfTI) to skull-strip. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `t1_brain` | `neuro/anat/t1w` | Skull-stripped (brain-extracted) T1w image produced by FSL's bet (fractional intensity threshold only; -R disabled, see main). |

<details>
<summary><b>⚙️ Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `frac` | number | `0.5` | BET fractional intensity threshold (0-1, default 0.5). Smaller values give larger brain outline estimates. |

</details>

<!-- brainlife-app:end -->

Skull-strip a T1w volume with FSL's bet.

## Inputs

- `t1` (neuro/anat/t1w)

## Outputs

- `t1_brain` (neuro/anat/t1w) -- Skull-stripped (brain-extracted) T1w image produced by FSL's bet (fractional intensity threshold only; -R disabled, see main).

## Usage

Brainlife.io: run via `braise-app-run`/`braise-app-pipeline` (once registered
with `braise-app-create`), or the web UI.

Locally (outside brainlife): copy `config.json.example` to `config.json`,
fill in real file paths, then run `./main` from this directory. `main` pulls
its own container (`singularity exec docker://...`) -- no local install of
the underlying tool needed, only Singularity itself.

Note: `brainlife/fsl:6.0.4-patched2` ships only Python 2, so `main` parses
`config.json` on the host and invokes FSL's `bet` directly inside the
container rather than running `brain_extract.py` in-container. The original
`brain_extract.py` script is kept in this repo for reference/standalone use
(run it directly if you have FSL + Python 3 installed locally).

Entrypoint: `brain_extract.py` (see note above on how `main` actually invokes FSL)

## Authors

- Gabriele Amorosino <g.amorosino@gmail.com>

## License

MIT, see `LICENSE`.
