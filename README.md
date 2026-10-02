# JaviD Future Bot

A free desktop program that automates USDT-margined perpetual futures trading on
**Bitget**, **Binance** and **OKX**. It runs on your own computer with your own exchange
API keys. There is no relay server between you and the exchange. Windows and macOS.

Built and run by one independent developer in South Korea.

| Exchange | Page and download |
|---|---|
| Bitget | [bg.javidtrading.com](https://bg.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=readme) |
| Binance | [bn.javidtrading.com](https://bn.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=readme) |
| OKX | [okx.javidtrading.com](https://okx.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=readme) |
| Bybit | Port finished and in testing. Not downloadable yet. |

Leveraged futures can lose your entire deposit. Read [Risk](#risk) before connecting a key.

---

## You can try it with no API key

Shadow Mode runs the full strategy on live market prices against a virtual
2,000 USDT balance. It needs no API key, no identity verification and no deposit.
You can watch it trade for days before you decide whether to connect anything.

## What it connects to

```
Your PC  ->  exchange API          (orders, prices, balances)
Your PC  ->  one CloudFront edge  (a CDN; what it served was not identified)
```

Measured on 2026-08-19 on the Bitget build of that date, with a network monitor: exactly
two outbound hosts, the exchange API and one CloudFront edge. No analytics endpoint, no
telemetry, and no connection to any developer-owned server. That was one run on one machine with one build.
It is a check you can repeat yourself with any firewall or network monitor, not a security
audit.

Your API key is stored on your computer. Create it with read and futures trading permissions
only and leave withdrawal permission off; the program never needs it.

## How it trades (short version)

- Three strategies scan USDT perpetual futures and enter, add and exit on fixed rules.
- In the Bitget build (V19.7), positions are added to at fixed 30% spacing as price moves
  against them, and stop-loss is off by default (you can turn it on). That is why open positions can sit deep in the red:
  the design waits for the move back rather than cutting the loss.
- Every order is sent from your machine with your key, so the account and the funds stay
  under your control.

### The rule that removed forced liquidation in the backtest

This section and the backtest below describe the **Bitget build (V19.7)**. The backtest
has not been run on the Binance or OKX builds currently on their pages, which are an older
version line (V18) with different defaults. Its result does not apply to them.

The strategies lean on a simple bet: a coin that spikes tends to come back toward where it
traded before. A freshly listed coin has no "before", so that bet has nothing to stand on.

In the backtest below, the one rule that removed forced liquidation was **no entry into a
coin listed less than 90 days ago**. With the gate switched off, the same data produced a
forced liquidation on 2025-10-09. Tightening the add-on spacing from 30% to 20%
brought liquidation back even with the 90-day gate on, ending at -30.5%. Coins under a delisting notice are blocked
as well.

## Backtest: 805 pump windows from two years of 1-minute data

- **Sample:** every pump window between September 2024 and September 2026 in which a coin
  tripled or more inside a single month: 805 windows across 425 coins.
- **Method:** the full 1-minute candles of those windows were downloaded and the program
  was run over them bar by bar. Entries, add-ons and exits came from the same program code
  that is distributed, not from a model fitted to the chart.
- **Result:** 2,023 trades, zero forced liquidations, deepest point -64% of starting
  equity (mid-2025), final +96%. The -64% and the +96% come from the same run and belong
  together.
- At the most crowded moment the margin ratio read 38.2%, roughly 15x of room before the
  liquidation line, measured against the strictest liquidation threshold.

**Limits.** The sample is 805 pump windows and nothing else, so trades from ordinary
market conditions, gains and losses alike, are absent, and a real account curve does not
look like this. Only coins that can still be queried today were scanned, so anything
delisted in between was never a candidate (survivorship bias). Market behaviour that did
not occur within these two years is not represented. The zero liquidations hold inside
these 805 windows and say nothing about what lies outside them. Trading fees are included;
funding and slippage are not, and with those added the result would have been worse.

These are recalculated figures over past prices, not the trade record of a live account.
Dashboard screenshots from a live account running an earlier build, connected to a
different exchange, are at [bg.javidtrading.com/results](https://bg.javidtrading.com/results?utm_source=github&utm_medium=repo&utm_campaign=readme). They are a record of that
account, not of this backtest.

## Installing

1. Download the build for your exchange from its page above.
2. Unzip and run it. The program is not code-signed, so Windows SmartScreen or macOS
   Gatekeeper warns on first launch. The steps to get past that, and the SHA-256 of each
   build so you can confirm the file you received is the one that was published, are at
   [bg.javidtrading.com/install-help](https://bg.javidtrading.com/install-help?utm_source=github&utm_medium=repo&utm_campaign=readme)
3. Start in Shadow Mode. Connect a key only when you have seen enough.

No coding is needed. It is a graphical desktop application.

## Source code

The program is distributed as a compiled, obfuscated build. Its source is not published;
this repository holds documentation. That makes it different from open-source bots such as
freqtrade or passivbot, and it is why the network check above matters: you can verify what
the program connects to without reading its code.

## How it is paid for

There is no subscription, no paid tier and no upsell. The developer earns the exchange's
broker rebate on trading fees made through the program. That is a conflict of interest,
and you should know about it.

## Risk

These are leveraged futures on a real exchange. A position can be liquidated and your
entire deposit can go to zero. Open positions can sit deep in the red for a long time
before they close: one short on the operator's account reached -1,960.68% unrealized
(CYS, 2026-08-20) before it closed at +50.77%. Past results are a record of what already happened, not a forecast.
Nothing here is investment advice.

## Contact

- Telegram community: https://t.me/+P_CukTNNKRI4ZDVl
- Email: support@javidtrading.com
