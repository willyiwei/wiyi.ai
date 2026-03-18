# CLAUDE.md — Frontend Website Rules

## Always Do First

– **Load the `frontend-design` skill** at `./plugin/plugins/frontend-design` before writing any frontend code. No skipping, no exceptions, every single session.

## Reference Images

– When a reference image is given: replicate the layout, spacing, typography, and color with precision. Use placeholder content throughout (images via `https://placehold.co/`, generic copy). Nothing gets added or improved beyond what the reference shows.

– When there is no reference image: build from scratch with genuine craft (see guardrails below).

– Take a screenshot of the output, compare it against the reference, fix what is off, and screenshot again. Run at least 2 comparison rounds. Only stop when there are no visible differences left, or the user says to.

## Local Server

– **Everything gets served on localhost** — taking a screenshot from a `file:///` URL is not acceptable.

– Spin up the dev server using `node serve.mjs` (this serves the project root at `http://localhost:3000`)

– `serve.mjs` is in the project root. Get it running in the background before any screenshot step.

– Check whether the server is already up before starting it again. One instance at a time.

## Screenshot Workflow

– Puppeteer lives at `[YOUR_PROJECT_PATH]`. The Chrome executable is at `[YOUR_CHROME_CACHE_PATH]`.

– **Screenshots always come from localhost:** `node screenshot.mjs http://localhost:3000`

– Each screenshot is written to `./temporary screenshots/screenshot-N.png`, auto-incremented and never overwritten.

– To attach a label: `node screenshot.mjs http://localhost:3000 label` → saves as `screenshot-N-label.png`

– `screenshot.mjs` is in the project root. Do not modify it.

– Once the screenshot is saved, read the PNG from `temporary screenshots/` using the Read tool — Claude can view and analyze it from there.

– Comparisons need to be precise: “heading is 32px but reference shows ~24px”, “card gap is 16px but should be 24px”

– Go through: spacing/padding, font size/weight/line-height, colors (exact hex), alignment, border-radius, shadows, image sizing

## Output Defaults

– One `index.html` file with all styles inline, unless told otherwise

– Tailwind CSS loaded through CDN: `<script src=”https://cdn.tailwindcss.com”></script>`

– Use `https://placehold.co/WIDTHxHEIGHT` for placeholder images

– All layouts are mobile-first

## Brand Assets

– Before starting any design work, look through the `brand_assets/` folder. It could have logos, color guides, style guides, or images.

– If something is in there, use it. Placeholders have no place when real assets exist.

– A logo in the folder gets used. A defined color palette means those exact values get used — no making up brand colors.

## Anti-Generic Guardrails

– **Colors:** The default Tailwind palette (indigo-500, blue-600, etc.) is off the table. Build the palette from a custom brand color.

– **Shadows:** Flat `shadow-md` is not an option. Build depth with layered, color-tinted shadows at low opacity.

– **Typography:** Headings and body text get different fonts. Pair a display or serif with a clean sans-serif. Large headings get tight tracking (`-0.03em`), body text gets generous line-height (`1.7`).

– **Gradients:** Stack multiple radial gradients on top of each other. Bring in grain and texture through an SVG noise filter.

– **Animations:** Stick to `transform` and `opacity` only. `transition-all` is never used. Easing should feel spring-like.

– **Interactive states:** hover, focus-visible, and active states are required on every clickable element. No skipping.

– **Images:** Layer a gradient overlay (`bg-gradient-to-t from-black/60`) on top, and apply a color treatment using `mix-blend-multiply`.

– **Spacing:** Every spacing decision follows consistent tokens. Random Tailwind steps are not acceptable.

– **Depth:** Build with a surface hierarchy in mind (base → elevated → floating). Everything sitting flat at the same level is not good enough.

## Hard Rules

– Nothing gets added that is not already in the reference

– The goal is to match the reference, not make it better

– One screenshot pass is never enough

– `transition-all` is never used

– Default Tailwind blue or indigo cannot be the primary color
