# Setup

No coding is needed. The order below is deliberate: you can see the program run before you
create any API key.

## 1. Download and start

Pick the page for your exchange and download the Windows or macOS build:

- Bitget: [bg.javidtrading.com](https://bg.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=setup)
- Binance: [bn.javidtrading.com](https://bn.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=setup)
- OKX: [okx.javidtrading.com](https://okx.javidtrading.com/?utm_source=github&utm_medium=repo&utm_campaign=setup)

Unzip and start it. The build is not code-signed, so Windows SmartScreen or macOS
Gatekeeper shows a warning on first launch. How to get past it, and the SHA-256 of each
build so you can confirm your file matches the published one:
[bg.javidtrading.com/install-help](https://bg.javidtrading.com/install-help?utm_source=github&utm_medium=repo&utm_campaign=setup)

## 2. Turn on Shadow Mode (no key needed)

Shadow Mode trades live market prices against a virtual 2,000 USDT balance. No API key, no
identity verification, no deposit. Pick some symbols, start it, and watch how it opens,
adds to and closes positions, including how it handles positions that move against it.

## 3. Create an API key, only when you want to go live

On your exchange's API management page, create a key with **read** and **futures trading**
permissions. Leave **withdrawal off**; the program never needs it. Turn on IP restriction
if your exchange offers it. Bitget and OKX keys also need a passphrase.

Paste the key into the settings tab and run the connection test. The key is stored on your
computer only.

Each exchange page has a step-by-step signup and API key guide with screenshots.

## 4. Size

The first entry is about 1/300 of your balance in the default mode; add-ons make the
position larger from there. Below about
1,000 USDT, exchange minimum order sizes and fees start to get in the way, so 1,000 USDT or
more is recommended.

## 5. Keep it running

The program trades only while it is running. If you close it, open positions stay on the exchange with nothing managing them until you
restart it; on restart the program detects them and resumes managing them. An always-on mini PC or a low-cost cloud VM keeps it running.

---

Leveraged futures can lose your entire deposit. Not investment advice.
Questions: https://t.me/+P_CukTNNKRI4ZDVl · support@javidtrading.com
