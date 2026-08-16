Create a single self-contained HTML file: a working spreadsheet.

Grid:
- 20 rows by 10 columns, labelled A-J across and 1-20 down.
- Click a cell to select it, type to edit. Enter commits and moves down; Tab commits and moves right. Arrow keys move the selection.
- A formula bar showing the raw contents of the selected cell while the grid shows the computed value.

Cell contents:
- Numbers, plain text, or formulas beginning with "=".

Formula support:
- Arithmetic with + - * / and parentheses, respecting operator precedence.
- Cell references such as =A1+B2.
- Ranges in functions: =SUM(A1:A10), =AVERAGE(A1:A10), =MIN, =MAX, =COUNT.
- Nested and combined expressions such as =SUM(A1:A5)*2+B1.

Recalculation:
- When a cell changes, every cell that depends on it recalculates automatically, including chains (C1 depends on B1 depends on A1).

Error handling:
- Circular references show #CIRCULAR! in the affected cell. The page must not hang or crash.
- Invalid formulas show #ERROR!.
- Division by zero shows #DIV/0!.

No libraries, no CDN, no external assets.
Output the complete HTML file and nothing else.
