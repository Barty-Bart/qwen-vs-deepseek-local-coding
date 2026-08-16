Create a single self-contained HTML file: a tower defence game.

Board:
- 960x600 canvas, 40px grid. A winding path from the left edge to the right edge that enemies follow.
- Towers may only be placed on non-path cells, one tower per cell.

Towers (four types):
- Archer: cheap, fast, single target.
- Cannon: slow, splash damage.
- Frost: slows enemies.
- Sniper: long range, high damage.
Select a tower from a side panel, then click a cell to place it. Show a range circle while placing and when a tower is selected. Each tower can be upgraded three times and sold for 70% of what was spent on it.

Enemies:
- Waves of increasing difficulty, at least three enemy types, plus a boss every 5 waves.
- Health bars above each enemy. An enemy reaching the end costs lives.

Game loop:
- Start with 150 gold and 20 lives. 20 waves total.
- Gold awarded for kills, plus a wave-completion bonus.
- A "Send Wave" button, a 1x/2x speed toggle, and pause.
- Game over at 0 lives; victory after clearing wave 20.

Must visibly work:
- Projectiles travel from tower to enemy.
- Splash damage hits multiple enemies at once.
- Frost visibly slows enemies.
- The HUD always shows gold, lives, and wave number.

No libraries, no CDN, no external assets. The file must run correctly when opened directly in a browser.
Output the complete HTML file and nothing else.
