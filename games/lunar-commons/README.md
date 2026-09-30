# Lunar Commons

A 3D board game about governing resources at the lunar south pole. It runs in any
modern browser with WebGL. The game is a single `index.html` file that loads
three.js r128 from cdnjs. Everything else is inline.

Four operators take turns. Each round, every operator chooses how to fund its
work: **alone**, through the **commons**, or in a **consortium**. That choice
decides who sees the survey data, who can use the power towers, and whether the
region ends in **stagnation**, **monopolization**, or **sustained growth**.

## Play

Open `index.html` in a browser. To serve it locally instead:

```bash
python3 -m http.server -d games/lunar-commons 8000
# then open http://localhost:8000
```

- Seats can be human (hot-seat on one screen) or AI.
- Drag to orbit, scroll or pinch to zoom, right-drag or two-finger drag to pan, `R` to reset the view.
- Choose an action, then click a tile. On touch screens, tap a tile and confirm.

## Rules summary

| Model | Costs | Survey data | Power towers | Revenue |
|---|---|---|---|---|
| Alone | Full price | Private | Serve only you | Keep 100%. New outposts declare a safety zone on the 4 bordering tiles |
| Consortium (2+ members) | 25% off | Shared with members | Serve members | 20% pooled and split among members |
| Commons | Pool pays up to half | Public | Serve everyone | 30% to the commons pool, which builds public relay towers |

Actions: survey (2), land outpost (5), power tower (6). Each outpost yields
ice + sun + tower bonus each round, minus 1 upkeep.

## Code layout

The pure game rules and AI sit between `// ===LOGIC-START===` and
`// ===LOGIC-END===` in `index.html`. That block has no DOM or three.js
dependency, so it can run headless for balance checks:

```bash
sed -n '/===LOGIC-START===/,/===LOGIC-END===/p' games/lunar-commons/index.html > /tmp/logic.js
```

Crater and massif names are real south-polar features, but their positions are
stylized. Credits are fictional. This is an educational simulation, not
financial advice.
