<div align="center">

# The Double-Slit Experiment

**An interactive, electron-by-electron simulation of Young's double-slit experiment.**

[Français](README.md) · **English** · [العربية](README.ar.md)

[**▶ Try the demo**](https://lahnabil.github.io/double-slit-experiment/?lang=en) · [How it works](#how-it-works)

<img src="assets/preview.gif" alt="Electrons build interference stripes, then two plain bands once the detector is switched on" width="480">

</div>

---

## The experiment

Electrons are fired, **one at a time**, at a plate with two slits. A screen behind it records where each one lands.

1. **Each electron hits the screen at a single point**, like a marble.
2. **After thousands of hits, stripes appear**: an interference pattern, the signature of a wave. The electron behaved as if it had gone through both slits.
3. **We add a detector** to find out which slit each electron goes through.
4. **The stripes disappear.** Only two bands remain, as you would expect from plain particles.

Nothing changed in the setup except one thing: we looked.

## What the simulation does

- **Free mode**: set the rate (1 to 1,000 electrons per second), switch the detector on or off, clear the screen.
- **36-second sequence**: a narrated run with the controls hidden, made to be screen-recorded and shared (square 1:1 and portrait 4:5).
- **Three languages**: French, English and Arabic (with a right-to-left layout), including the text drawn inside the simulation. It follows the browser's language, or pick one with `?lang=fr`, `?lang=en` or `?lang=ar`.
- **No dependencies**: one HTML file, Canvas 2D, plain JavaScript. No build step.

## How it works

The simulation does not solve the Schrödinger equation. It does what a real detection screen shows: **each electron lands at a random position drawn from the probability distribution the theory predicts.** The pattern emerges from thousands of these draws.

**Without a detector**, the probability follows the two-slit Fraunhofer diffraction pattern:

```
I(u) ∝ cos²(π·k·u) · sinc²(π·b·u)
```

- `cos²(π·k·u)`: the interference fringes between the two possible paths
- `sinc²(π·b·u)`: the diffraction envelope set by the width of each slit
- `u`: the position on the screen, normalised between -1 and 1

**With a detector**, the which-path information destroys the coherence between the two paths. Probabilities add as intensities rather than amplitudes: the interference term vanishes and two humps remain, one per slit.

Each position is drawn by **inverse transform sampling** (a CDF precomputed over 2,400 points, binary search). The random generator is seeded (`mulberry32`), so the sequence plays identically every time.

### Limitations

- The parameters (slit spacing, wavelength) are chosen for readability, not measured on a real apparatus.
- In a real far-field setup, the two "observed" humps overlap more. They are kept apart here so the contrast is visible.
- "The electron goes through both slits at once" is a picture. What the experiment establishes is that it behaves like a wave as long as no information about its path exists. What "really" happens depends on the interpretation of quantum mechanics, and that debate is still open.

## Run it locally

Nothing to install. Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then http://localhost:8000
```

## Structure

```
.
├── index.html               # the whole simulation (HTML + CSS + JS, 3 languages)
├── README.md                # French documentation
├── README.en.md             # English documentation
├── README.ar.md             # Arabic documentation
├── assets/
│   ├── preview.gif          # README preview
│   └── og-image.png         # social sharing image (LinkedIn, X…)
└── LICENSE
```

## Further reading

- Richard Feynman, *The Feynman Lectures on Physics*, Volume III, Chapter 1: the experiment described as "the only mystery" of quantum mechanics.
- Tonomura et al. (1989), *Demonstration of single-electron buildup of an interference pattern*, American Journal of Physics: the experiment carried out one electron at a time, which this simulation reproduces in principle.

## Credits

Designed by **[Nabil Lahlalia](https://github.com/LahNabil)**, founder of [WivoAgency](https://wivoagency.com), and built with the help of Claude (Anthropic).

I'm not a physicist: this project came out of curiosity. If you spot a mistake or a misleading simplification, [open an issue](https://github.com/LahNabil/double-slit-experiment/issues) and I'll learn something.

[MIT](LICENSE) licensed.
