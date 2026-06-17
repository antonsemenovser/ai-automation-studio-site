# AI Automation Studio — Claude Design design system

Source of truth for the studio's brand, extracted from `../index.html` (`:root` tokens +
live components). Each `*.html` here is a **self-contained preview card**: its first line is
a `<!-- @dsCard group="…" -->` marker, which Claude Design compiles into `_ds_manifest.json`
and renders in the Design System pane.

Pushed to claude.ai/design via the `/design-sync` skill (DesignSync tool) so every mockup,
deck or landing Claude Design generates for the studio is already on-brand.

## Cards
- `01-colors`, `02-typography`, `12-section-heading` — **Foundations** (palette, gradients, Inter scale, section headers)
- `03-buttons`, `04-badge-chips`, `05-service-card`, `06-catalog-card`, `07-feature-step`, `10-header-nav`, `14-feed-card`, `15-form-fields` — **Components**
- `08-chat-mockup`, `09-cta-panel`, `11-hero`, `13-pricing` — **Patterns** (full hero, pricing grid)

## Re-sync after editing
```
python3 ~/.claude/bin/ds-bundle.py --check ~/pro/ai-automation-studio-site/design-system   # validate markers + sizes
```
Then in Claude Code: `/design-sync` → pick the "AI Automation Studio" project → push.
Tokens live in each card's `:root`; if the site's brand changes in `index.html`, update the
cards here and re-run the check + sync. Keep card HTML faithful to the real site CSS.
