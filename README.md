# Hamilton's Bridge

An interactive explainer that walks from complex numbers to quaternions, following the path William Rowan Hamilton took in 1843. Each idea comes with a live figure you can drag, slide or step through.

The whole site is one self-contained `index.html`: no build step, no dependencies, no server.

## What's on the page

| # | Section | What you can do |
|---|---------|-----------------|
| 1 | **Turning the plane** | Drag `z`, set the angle and length of `w`, and watch `zw` scale and rotate. Repeated products trace a circle or a spiral. |
| 2 | **Euler's formula** | Add the terms of the series for `e^{iθ}` one at a time and watch the head-to-tail spiral settle on the unit circle. |
| 3 | **Why not three?** | Guess what `ij` equals in a system of triples and see why the `j` part always comes out as `c²`, which can never be −1. |
| 4 | **The rules** | Tap any cell of the multiplication table to compare `ab` with `ba`. Also covers the conjugate, inverse and `(pq)* = q*p*`. |
| 5 | **ℂ inside ℍ** | Four ways the complex numbers live inside the quaternions: a copy of ℂ along every axis, Euler's formula for any axis, the scalar–vector product, and the Cayley–Dickson pair `z₁ + z₂j`. |
| 6 | **A sphere of √−1** | Move a unit axis `u` around a 3D sphere and check that `u² = −1` and that `(2+u)(1−3u) = 5 − 5u`. |
| 7 | **Order matters** | Two darts side by side, one doing rotation A then B, the other B then A, with `q_B q_A − q_A q_B` shown live. |
| 8 | **q v q\*** | The rotation lab: set an axis and an angle from 0° to 720°. An inset shows `q` moving at half speed on its complex circle, and the readout splits the vector into parallel and perpendicular parts. Includes a worked example. |
| 9 | **Gimbal lock** | Yaw, pitch and roll rings around the dart, with a warning when the roll axis lines up with the yaw axis. |
| 10 | **Slerp** | Slerp compared with blending Euler angles: traced nose paths and a chart of how fast the dart turns, with hover readouts. |
| 11 | **Calculator** | Enter two quaternions to get `pq`, `qp`, their difference, the lengths, the inverse, the 2×2 complex matrix and the axis–angle form. |
| 12 | **The family** | ℝ → ℂ → ℍ → 𝕆 → sedenions, and the property lost at each doubling. |

The dart at the top of the page turns non-stop, blending smoothly between random orientations with slerp.

## Running it

Open `index.html` in any modern browser. That's all.

When you're online, the fonts ([Spectral](https://fonts.google.com/specimen/Spectral), [Source Sans 3](https://fonts.google.com/specimen/Source+Sans+3) and [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)) load from Google Fonts. Offline, the page falls back to system fonts and everything still works.

To serve it locally (optional):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

### Publishing on GitHub Pages

1. Push the folder to a repository, with `index.html` at the root.
2. In the repository, open **Settings → Pages**.
3. Under **Source**, pick the branch (for example `main`) and the `/ (root)` folder, then save.

## Conventions used in the code

A quick reference, since quaternion code can follow several conventions:

- **Component order:** `[w, x, y, z]` for `q = w + xi + yj + zk`, with the scalar part first.
- **Product:** the Hamilton product, with `ij = k`, `jk = i`, `ki = j`.
- **Vectors** are pure quaternions `[0, x, y, z]`, and the space is right-handed with `k` pointing up in the figures.
- **Rotation:** `v' = q v q*` with `q = cos(θ/2) + u sin(θ/2)`, where a positive angle turns counter-clockwise when you look down the axis `u`.
- **Composition** is in the world frame: "A, then B" is `q_B q_A`.
- **Euler angles** (gimbal and slerp demos): intrinsic Z-Y′-X″ (yaw, pitch, roll), built as `q = q_yaw · q_pitch · q_roll`. Positive pitch lifts the nose.
- **Slerp** takes the shorter arc: if `q_A · q_B < 0`, it flips `q_B` to `−q_B` first.

All the math lives in the small `Q` (quaternion) and `V` (3-vector) helper objects at the top of the script. Rendering uses plain Canvas 2D, with a simple perspective projection and painter's-algorithm shading for the dart.

## Accessibility and display

- Light and dark themes follow the system setting.
- Honors `prefers-reduced-motion`: the hero dart stays still and smooth scrolling is turned off.
- The layout works on phones down to about 400px wide. In 3D views, a horizontal drag orbits the camera and a vertical swipe still scrolls the page.
- Controls are native sliders, selects and buttons with visible keyboard focus. The multiplication table can be used with Tab and Enter.

## Background

On 16 October 1843, walking along the Royal Canal in Dublin, Hamilton realised that a consistent algebra for rotations in space needed a third imaginary unit `k` and had to give up commutativity. He scratched `i² = j² = k² = ijk = −1` into the stone of Broom Bridge. A plaque marks the spot today.

Further reading:

- W. R. Hamilton, *On Quaternions* (1844–1850), *Philosophical Magazine*
- K. Shoemake, "Animating Rotation with Quaternion Curves", SIGGRAPH 1985 (the paper that introduced slerp)
- J. C. Baez, "The Octonions", *Bulletin of the AMS* 39 (2002), for the full Cayley–Dickson ladder and Hurwitz's theorem

## Files

```
hamiltons-bridge/
├── index.html   the whole site: markup, styles and script
└── README.md    this file
```
