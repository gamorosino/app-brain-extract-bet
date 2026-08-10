# FSL BET Skull Strip

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
