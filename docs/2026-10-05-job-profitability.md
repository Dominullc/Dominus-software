# Dominus Workspace: job profitability report (2026-10-05)

The app code lives in the Base44 app "Dominus Workspace" (id 6a7b8d0e98ae407060c65461).
Base44 checkpoint: "Job profitability report (revenue vs recorded cost by project)", git 88a1cee.

## Changes in the Base44 app

- `base44/shared/profitability.js`: new. Pure report math: revenue, cost, profit, margin, collected and open AR per project, plus monthly and category breakdowns, and the CSV export.
- `base44/shared/projectControls.ts`: adds the read-only `portfolio` action. It is scoped to projects the caller can open and returns only trimmed fields.
- `src/pages/ProfitReports.jsx`: new page at `/reports/profitability`, gated by the `contracts` permission.
- `src/App.jsx` and `src/lib/workspaceNav.js`: add the route and the menu entry "Job profitability" under Reports & review.
- `scripts/profitability.test.mjs`: 10 tests. All pass. The existing project-controls and invoice-report suites (30 tests) still pass. Lint, typecheck and build are clean for the touched files.

## Rules

- Revenue is billed invoices only. Drafts count as pipeline. Voided invoices and merged plate invoices are excluded.
- Credit memos reduce revenue.
- Collected amounts are capped at each invoice's total.
- Cost is only ProjectCost rows with status "recorded". Payroll and equipment hours are not costed automatically. A project with revenue but no recorded cost is flagged.

## Benchmark gaps still open

| Benchmark | Biggest remaining gap |
|---|---|
| QuickBooks | Automatic labor/equipment costing from timesheets and equipment hours; cash-basis P&L; recurring invoices; payment links |
| Vitruvi | Cross-project GIS map of work; program-level dashboards |
| Bluebeam | Scale-calibrated length/area measurement; plan revision compare/overlay |
| FiberField | Splice and OTDR/power-meter test records per segment |
| Plate rental | Per-plate utilization and revenue; delivery/pickup dispatch board |
