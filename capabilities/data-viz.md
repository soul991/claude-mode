# Capability: charts and data visualisation

Use for any chart, plot, dashboard, or KPI display.

## Pick the form from the question

| Question | Form |
|----------|------|
| How does it change over time? | line (or area for totals) |
| How do categories compare? | bar (horizontal when labels are long) |
| What is the relationship between two numbers? | scatter |
| What is the distribution? | histogram or box plot |
| What are the parts of a whole? | stacked bar; pie only for 2-4 slices |
| Where are the patterns in a matrix? | heatmap |

Avoid 3D, dual axes unless unavoidable, and truncated bar axes (bars start at zero).

## Rules

- Title states the takeaway ("Sales doubled in Q3"), not just the variable.
- Label axes with units; label lines directly instead of using a legend when you can.
- Colour carries meaning: one highlight colour against muted greys; a sequential
  palette for magnitude; a diverging palette only around a meaningful midpoint.
- Never rely on colour alone (add labels, markers, or patterns); check
  colour-blind safety.
- Remove chart junk: heavy gridlines, borders, shadows, redundant labels.
- Sort categories by value unless they have a natural order.
- Same series, same colour across every chart in a deliverable.

## Code defaults

```python
import matplotlib.pyplot as plt
fig, ax = plt.subplots(figsize=(8, 4.5), dpi=200)
ax.plot(x, y, color="#1F6FEB", lw=2)
ax.set_title("Sales doubled in Q3", loc="left", fontsize=14, weight="bold")
ax.spines[["top", "right"]].set_visible(False)
ax.set_ylabel("Revenue (USD m)")
fig.tight_layout(); fig.savefig("chart.png")
```

## KPI tiles and dashboards

Big number, small label, a comparison (vs last period), and an unambiguous
direction cue. Group related metrics; limit to what a decision needs.

## Verify

Recompute the plotted numbers from source data in code. Open the image and
check labels are not clipped and text is legible at its final size.
