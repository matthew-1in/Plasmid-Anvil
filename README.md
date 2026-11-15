# Plasmid&Anvil

An interactive **DNA / plasmid design workbench** that runs entirely in the browser. No build step, no server, no dependencies. Open `index.html` and start designing.

Everything is contained in a single self-contained HTML file (`index.html`).

## Features

- **Visual workbench.** Build circular plasmids or linear strands from drag-and-drop BioBrick parts (promoters, RBSs, coding sequences, terminators, origins, tags). Pan, zoom, marquee-select and move pieces freely. Toggle any construct between circular and linear.
- **Double-stranded nucleotide editor** (ApE-style). Edit either strand with the complement kept in sync, see sticky-end overhangs as missing `N`s, translate coding sequences in-line, add draggable comments, and resolve ambiguous `N` bases one strand at a time. Anything that isn't A, T, C, G or N glows red so you can't miss it.
- **Reading frames and annotations.** Click an annotation in the editor for its part info beside the sequence, and translate any selection in any of the six reading frames.
- **Three ways to search.** Plain Search treats `N` as a wild card on both sides, Exact search takes your query literally, and Mismatch search allows a budget of mismatches you set. Find and replace works from all three.
- **Checked against the reference.** The cloning simulation is cross-checked against [C6-Multiplatform](https://github.com/UCB-BioE-Anderson-Lab/C6-Multiplatform), J. Christopher Anderson's implementation of the Construction File format ([Anderson et al. 2023](https://pubmed.ncbi.nlm.nih.gov/37956196/)): PCR, digest, Golden Gate and Gibson produce the same molecules on the same inputs, and a construction file exported here runs there. `REVIEW-v5.0.md` records the review that established this.
- **Cloning simulation.** Drag PCR, Golden Gate, Gibson, SOE, PCA, Ligation and Digest cards onto the bench, drop in oligos, strands and enzymes, and run them through the same logic as a C6-style construction file. Chain experiments so one product feeds the next, and export any experiment or chain as a construction file. Runs take N as a wild card in strands and parts and turn down any other ambiguity code there; a recognition site may use the whole IUPAC alphabet, since a code in a site has one meaning.
- **Construction files, both ways.** Export any card or pipeline as a construction file, and paste one back in to get the pipeline it describes: a card per step, wired together, with the sequences it declares dropped into the slots and any capsule templates saved to the library. A file that cannot be read says which line is wrong and why.
- **Capsules.** Turn a working pipeline into one card. Every slot the pipeline filled itself becomes an input on the front, the wiring between the steps is kept inside, and running it hands back the products you chose. A capsule is used like any other experiment card, can be stacked into a pipeline, and can go inside another capsule; they live under **Saved capsules** on the Cloning tab, with folders of their own. In a construction file a capsule is written as a template — a header naming it and its inputs, the steps it is made of, and a `Product` line — and then called like any other step.
- **Flowcharts you can publish.** Any pipeline or capsule opens a flowchart of its steps, with the run order and the wiring editable from it. **Export view** redraws the same graph as an engineering flowchart — rectangular boxes, straight lines, right angles, black on white, each box listing what it takes in and what it makes — and saves as SVG. A capsule is drawn once as its own labelled chart above, then appears as a single step below.
- **Reverse engineering.** Drop in the strand you want to end up with and get the card that would make it: Reverse PCR, Digest, Gibson, Golden Gate, SOE or PCA, each checked by running the design forwards.
- **Digests, maps and custom enzymes.** Drag a restriction enzyme onto a strand to cut it with correct overhangs, or just map every site it binds. Define your own enzyme with a recognition sequence and cut-position sliders.
- **The enzyme databank, bundled.** Every restriction enzyme REBASE lists with a recognition sequence travels inside the file too, searchable from the Cloning tab by name, organism or site, and filterable to the ones whose cut is known, the ones a supplier sells, or the iGEM assembly standards. Keep one and it joins My enzymes, ready to drag onto a strand.
- **The iGEM Registry, bundled.** All 77,314 parts travel inside the file in compressed form, searchable from the Parts tab by name, description or sequence, with every match reachable by scrolling. Sequences up to 1,000 bp come with it; keep one and it lands in My Parts as ordinary, uncompressed sequence.
- **Auto-annotate.** Drop a strand into the Auto-annotate card and it comes back annotated: open reading frames, promoters, ribosome binding sites, terminators, BioBrick ends, unique cut sites and protein tags, each on or off from a checklist, plus exact copies of registry parts and of your own saved parts.
- **Computational biology.** Pairwise alignment (Needleman–Wunsch), a BLAST-style local similarity search against your own sequences, and a profile / HMM-style consensus, each with a results viewer and downloadable output.
- **Sanger sequencing.** Open an `.ab1` and read the chromatogram: four dye traces, the base called at each peak, and each nucleotide's share of the signal wherever you point. Choose a range or view the whole read, and put the confidence of each call or the dye signal at each peak behind the traces as bars. **Auto-analyze** grades the read against the strand it should be — Perfect, Point mutation, Deletion / insertion / other sequence, Perfect partial or Bad read — and says where every change is and what the read could not reach.
- **Library and files.** Save parts, constructs and experiment setups; import GenBank (`.gb`/`.ape`), FASTA, DNA Strider (`.str`) and SnapGene (`.dna`); export GenBank, FASTA, Strider, a portable JSON library, and strand diagrams as SVG, PNG or JPEG.
- **Sync.** Every Plasmid&Anvil window open on the machine stays in step by itself. Point the app at a sync file in a shared folder (OneDrive, Dropbox, a network drive) and the browser and the desktop app share one library; it's written as you work and on a half-minute heartbeat, and closing with anything it hasn't seen warns you first. Signed in on claude.ai, it rides your account instead.
- **Desktop app.** **Desktop app → Download for Windows** hands you one `.exe` that opens in a window of its own, with nothing installed. Download again and it offers to update the copy you have rather than fetch another. See `desktop/README.md`.

## Usage

Open `index.html` in any modern browser, or host it anywhere static (for example GitHub Pages).

### GitHub Pages

In the repository settings, under **Pages**, set the source to the `main` branch (root). GitHub will serve the app at `https://mission2mars2025.github.io/<repo-name>/`.

## Notes

- The bundled Registry data comes from the 2023 dump of the iGEM parts table (Zenodo 10.5281/zenodo.10071333, CC BY 4.0). Sequences over 1,000 bp are left out to keep the file a sensible size; those parts are still listed and the search says so.
- The bundled enzyme data comes from REBASE, the Restriction Enzyme Database (Roberts et al., rebase.neb.com), which is where the Registry's own enzyme pages take their cut sites from. iGEM publishes no enzyme table of its own, so the assembly-standard enzymes it names are flagged in the databank instead. Enzymes whose cut position REBASE has not determined are listed for reference but cannot be run.
- Your library and workbench are saved in the browser's local storage, and in a sync file or your Claude account if you set one up.
- The cloning and computational tools are teaching aids. They model the common cases well but aren't a substitute for a full validator. Verify any construct before building it in the lab.
- The bundled starter-kit sequences are reference values for prototyping. Check them against the iGEM Registry before ordering DNA.
- Sanger traces are held for the session you open them in, not saved to the library: a trace is megabytes of numbers, and the library goes to browser storage and the sync file. Save the base calls as a part to keep them.
- `changelog.txt` lists what changed in each version.

## License

MIT, see `LICENSE`.

---

Made by **Matthew Lin** · Contact: mission2mars2025@gmail.com
