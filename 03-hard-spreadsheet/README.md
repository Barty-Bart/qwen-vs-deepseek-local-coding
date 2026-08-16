# Test 03 — spreadsheet

The prompt is in [`prompt.md`](prompt.md). Both models got it identically.

Neither produced a working spreadsheet first time, so I gave feedback and let
them try again. Twice. I never told either model what was wrong — only what I
saw on screen.

## Round 1 — the original prompt

| | File | Time |
|---|---|---|
| DeepSeek | [`deepseek-01.html`](deepseek-01.html) | 3m 51s, 6 turns |
| Qwen | [`qwen-01.html`](qwen-01.html) | ~14m |

Both render. Neither accepts input.

## Round 2 — after this prompt

Sent to both models, identical:

> I opened your spreadsheet in a browser and it does not work.
>
> I cannot click a cell to select it, and I cannot type a value into a cell and
> press Enter. Clicking does nothing and typing does nothing, so there is no way
> to enter any data at all.
>
> Fix it so that: clicking a cell selects it and shows its contents in the
> formula bar; typing replaces the cell contents; pressing Enter commits the
> value, moves the selection down, and displays the computed result; and Tab
> commits and moves right.
>
> Also check the cells that currently show #CIRCULAR! and #ERROR! — several are
> showing errors that should hold ordinary values.

| | File | Time |
|---|---|---|
| DeepSeek | [`deepseek-02.html`](deepseek-02.html) | 8m 38s |
| Qwen | [`qwen-02.html`](qwen-02.html) | 10m 46s |

Both still broken.

## Round 3 — after this prompt

More detail this time, still no diagnosis. The two reports differ because the
two failures looked different on screen.

**To DeepSeek:**

> I opened deepseek-02.html in a browser and it is still completely broken.
>
> The grid renders and looks correct. But nothing responds at all: clicking any
> cell does not select it, typing does nothing, pressing Enter does nothing,
> arrow keys do nothing. Not one single interaction has any effect. The page
> looks finished but is completely inert.

**To Qwen:**

> I opened qwen-02.html in a browser. It is partly working, and the pattern is
> very specific.
>
> WHAT WORKS — the keyboard: on load, cell A1 is already selected. I can type a
> value, press Enter, and it is stored correctly. The selection then moves down
> to A2. Arrow keys move the selection fine.
>
> WHAT DOES NOT WORK — the mouse: clicking on any cell never selects it. Nothing
> happens at all. This is true for every cell in the grid.

| | File | Time | Result |
|---|---|---|---|
| DeepSeek | [`deepseek-03.html`](deepseek-03.html) | 10m 03s | still broken |
| Qwen | [`qwen-03.html`](qwen-03.html) | 16m 08s | **works** |

Both bugs were one line. DeepSeek declared `const cells = []` and never created
the rows, so every access threw. Qwen had an edit overlay sitting on top of the
grid, swallowing clicks before they reached a cell.

### Total across all three rounds

| | Round 1 | Round 2 | Round 3 | **Total** | Working? |
|---|---|---|---|---|---|
| DeepSeek | 3m 51s | 8m 38s | 10m 03s | **22m 32s** | no |
| Qwen | ~14m | 10m 46s | 16m 08s | **~41m** | yes |

Qwen's round 1 is approximate: it hung for roughly 10 minutes on a `node` test
harness it wrote itself that never exited, and the session was resumed rather
than restarted.

## Test 3.1 — thinking on, reasoning effort low

Fresh sessions, no memory of the rounds above, the same original `prompt.md`.
Both models set to `enable_thinking: true` and `reasoning_effort: low`, and both
given the same sentence through the chat template:

> Reasoning effort is set to low. Keep your thinking brief and focused, moving
> directly to the conclusion without unnecessary elaboration.

| | File | Time | Turns | Ran its own code |
|---|---|---|---|---|
| DeepSeek | [`deepseek-3.1-low.html`](deepseek-3.1-low.html) | **12m 49s** | 44 | syntax check only (3x `node --check`) |
| Qwen | [`qwen-3.1-low.html`](qwen-3.1-low.html) | **34m 56s** | 10 | executed it (7x `node -e`) |

Qwen's works. DeepSeek's evaluates formulas correctly but cell selection is
broken past the first row.

### Thinking off vs thinking on

| | 3 rounds, thinking off | One shot, thinking on |
|---|---|---|
| DeepSeek | 22m 32s — never worked | 12m 49s — mostly works |
| Qwen | ~41m — worked after round 3 | 34m 56s — works |

Thinking on took DeepSeek further in 12m 49s than 22m 32s of debugging did. The
one-line bug that made `-01`, `-02` and `-03` inert never appeared once the model
was allowed to think.

Note the two models use different, non-overlapping effort scales — Qwen takes
`low`/`medium`/`xhigh`, DeepSeek takes `low`/`high`/`max` — and each level only
changes which sentence is prepended to the prompt. DeepSeek's `low` normally
prepends nothing, so the sentence above was supplied to both to keep it even.
