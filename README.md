# Earnings and Budgeting Tool

A command-line utility for turning an hourly rate or an annual/monthly salary
into a full pay breakdown, and for splitting monthly rent with roommates.
Every calculator can be run non-interactively via CLI arguments, interactively
via prompts, or a mix of both — any value you don't supply is simply asked
for.

## Features

- **Hourly Rate Breakdown**: Converts an hourly rate and a workweek into
  weekly, monthly, and yearly totals.
- **Annual Income Breakdown**: Converts an annual (or monthly) salary into
  its hourly, weekly, monthly, and yearly equivalents, assuming a standard
  40-hour (5-day, 8-hour) workweek.
- **Rent Split**: Splits monthly rent evenly across roommates and shows the
  income remaining after rent.
- **Smart Value Parsing**: Accepts plain numbers or shorthand like `4.5k` /
  `250k` for thousands, and `/mo` / `/yr` (or "month" / "year") to indicate
  a time frame. The `k` shorthand only applies when it's attached directly
  to a number, so it won't misfire on unrelated text in the same input.
- **CLI or Interactive**: Pass values straight on the command line, or leave
  a flag bare to be walked through prompts. Invalid or out-of-range CLI
  values are rejected with a warning and the tool falls back to prompting
  instead of silently accepting bad data.
- **Clean Table Output**: Results print as auto-sized, boxed tables; columns
  that aren't used by a given calculator (like `% of Total`) are omitted
  rather than left blank.

---

## Usage & Flags

### Run Everything Interactively
```bash
earnings --all
```
Walks through each calculator one at a time, asking `[y/N]` whether to run
it (and accepting inline values after the `y`, e.g. `y 24.50 40`).

### Targeted Command Flags
```bash
# Hourly rate -> weekly / monthly / yearly breakdown
earnings --hourly-rate

# Annual (or monthly) income -> hourly / weekly / monthly / yearly breakdown
earnings --annual-rate

# Split monthly rent across roommates
earnings --monthly-rent
```

Each flag also accepts its values inline, in order, skipping the matching
prompt(s):
```bash
earnings --hourly-rate 24.50 40          # rate, hours/week
earnings --annual-rate 80k/yr             # annual amount
earnings --monthly-rent 1500 4500 2       # rent, income, roommates
```

### Help
```bash
earnings            # prints usage only
earnings -h         # prints full option list
earnings --help     # same as -h
```

---

## Input Syntax Examples

When prompted for a value, you can type a plain number or use shorthand:

- **Thousands shorthand**: `5k` parses as `5000`; `4.5k` parses as `4500`.
- **Time frame**: for income amounts, add `/wk`, `/mo`, or `/yr` to skip the
  follow-up question — e.g. `1k/wk`, `5k/mo`, `120k/yr`. If you enter a bare
  number with no time frame, you'll be asked to type `/wk`, `/mo`, or `/yr`
  to clarify.

---

## Requirements

- Python 3.10 or newer (uses `float | None` type hint syntax).
- Zero external dependencies — only the standard library (`argparse`, `sys`,
  `re`).