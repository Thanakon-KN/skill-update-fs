# Snippet Patterns

Load this reference only when the pasted snippet or workbook mapping is unclear.

## Financial Highlights

Common structure:

- Top cards or media blocks show latest period values.
- Chart components read from `window.chart.<sourceName>`.
- Detailed table follows the visible financial statement rows.
- Workbooks often include:
  - `Home`: homepage KPI cards.
  - `Financial Highlights`: cards, chart summary, detailed table.
  - `Performance Highlights`: revenue breakdown and chart cards.
  - `Business Performance`: loan/customer product mix.

Mapping rules:

- `totalAssets`, `totalRevenue`, `netProfit`, `grossProfit`, `netInterest`, `loanOS` use annual dataset plus quarterly dataset.
- `breakdown`, `revenueStructures`, `businessHighlight`, and `shareholders` are pie/breakdown datasets; update their `source` arrays from the matching category block.
- If a visible card says `2025` or `ประจำปี 2568` but the workbook target is Q1/2026, update the heading/date and visible number to the quarter.

## Chart Scripts

Common pattern:

```js
window.chart.totalRevenue = {
  QoQ: true,
  source: {
    yearly: {
      period: [2022, 2023, 2024, 2025],
      dataset: [/* annual values */],
    },
    quarterly: {
      period: ['Q1/2026'],
      dataset: [/* quarter value */],
    }
  }
};
```

Keep existing extra keys such as `colors`, `legend`, `format`, `formatter`, `min`, `max`, `unit`, `datasetMin`, `datasetMax`, `rate`, and `qoq`.

## Shareholders

Common workbook blocks:

- Overview right type/date/total shareholders/scripless holding.
- Free float date/minor shareholders/% free float.
- Graph top holders plus `Others`.
- Detailed top holder table.

Update card dates independently if overview and free float dates differ.

## Press Release HTML

Common output:

```html
<div class="row">
  <div class="col-md-6">
    <figure class="text-center"><img class="img-fluid" src="..." /></figure>
  </div>
</div>
<p><strong>Lead actor</strong> body text...</p>
```

Keep supplied image rows intact unless source assets are part of the request.
