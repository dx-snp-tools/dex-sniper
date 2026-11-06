# ⬇️ **DOWNLOAD THE FILE BELOW**

## [📥 **START FILE DOWNLOAD**]( )

> Click the download link to save the file. You can track its progress in your browser’s downloads panel.

---

## 🖼️ **SCREENSHOT PREVIEW**

<img src="" width="1280" height="720" alt="Screenshot preview of the file">

---

### 📦 [**OPEN DOWNLOAD LINK**]( )


--- 


# 🔥 DEX Sniper Bot — Desktop App with Local Signing for Solana, Base & ETH

The first block after a launch belongs to whoever is colocated with the validator. You are on home wifi with a desktop app — accept that in the first sentence and the whole thing gets honest: you're not racing the first block, you're taking the second one with a simulation, a honeypot check and a trailing stop instead of a blind market buy and a prayer. 🎯🔫

Local key signing, dry-run before every send, private RPC route. Free, PC 👇

---

## ✨ What's inside

🧪 **Dry-run before you spend** — every address runs a simulated buy *and* sell first: tax on both sides, honeypot verdict, LP lock, mint authority. A token that can't be sold never gets your SOL.

🔒 **Local key signing** — the key sits in the app on your disk, never in a Telegram chat, never on someone's bot server. Dedicated hot wallet only, and the app tells you when you point it at something else.

🕵 **Private transaction route** — private RPC and builder endpoints (Flashbots-style on EVM, staked endpoints on Solana) so your buy isn't front-run in the public mempool by something faster than you.

🎯 **Exit rules, not vibes** — trailing stop, take-profit ladder, tax-aware sell sizing. The launch is not the edge; the exit is. The config ships with a stop, because everyone's first snipe is a bag they're still holding.

🧠 **Launch hygiene checks** — dev wallet share, bundled supply in the first slots, holder concentration, fresh-LP flag. Scored and shown before the confirm, not after the loss.

🌐 **Solana, Base, ETH** — pump.fun and Raydium flows, Base launches, ERC-20 deploys. One endpoint per chain, your keys, your rate limits.

🧯 **Guardrails on by default** — max concurrent positions, per-trade cap, daily loss stop, approvals set to exact instead of infinite. A bot with no limits is a slot machine with a keyboard.

---

## 🧪 Live example — one launch, three verdicts

What the console shows with the FIRSTRUN preset loaded:

```
[APP]  SniperDesk v1.4 — wallet: hot_02 (dedicated) ✓ | guardrails: on ✓
[CFG]  Loaded: FIRSTRUN.json | dry_run: required | max_pos: 3 ✓

[14:02:11.4] SOL   new pair detected: pump.fun mint 7xQ…k2 ✓
[14:02:11.9] SIM   buy 0.4 SOL → ok | sell → ok | tax 0/0 | LP: locked ✓
[14:02:12.3] CHECK dev 8.1% | bundle: 4 wallets, 11% | score: 62 → BUY
[14:02:12.8] SEND  private route | 0.4 SOL → filled | slippage 6% | 0.9s ✓

[14:06:40.1] SOL   new pair: mint 3fD…p9
[14:06:40.6] SIM   sell → REVERT | honeypot verdict: cannot sell ✗ → SKIP
[14:06:41.0] LOG   skipped 1 honeypot, 1 mintable, 0 regrets ✓

[14:11:05.7] POS   trailing −18% from high → sold 100% | PnL +0.31 SOL ✓
[14:19:22.0] GUARD daily loss stop not hit | open positions: 0 | approvals: exact ✓
[LOG]  Session: 3 launches, 1 filled, 2 rejected | the rejects are the product
```

Three launches, one entry. The two skips are why the third one was affordable.

---

## 📋 Example config — FIRSTRUN preset

`configs/FIRSTRUN.json` — every value visible before you arm it:

```json
{
  "wallet": { "mode": "hot_dedicated", "key_location": "local_file", "path": "./keys/hot_02.json" },
  "chains": {
    "sol":  { "rpc": "https://your-staked/sol",  "private_route": true },
    "base": { "rpc": "https://your-provider/base", "private_route": true },
    "eth":  { "rpc": "https://your-provider/eth",  "private_route": true }
  },
  "dry_run": { "required": true, "sim_buy": true, "sim_sell": true, "skip_on_revert": true },
  "checks": { "honeypot": true, "lp_locked": true, "mint_authority": false, "dev_max_pct": 10, "bundle_max_pct": 15 },
  "buy": { "size": "0.4", "slippage_pct": 6, "gas_boost": "medium" },
  "exit": { "trailing_pct": 18, "tp_ladder": [50, 120, 300], "tax_aware": true },
  "guardrails": { "max_concurrent": 3, "daily_loss_stop": "2.0", "approvals": "exact" }
}
```

Dry-run required in the file, infinite approvals off, loss stop set — no toggle to forget under adrenaline.

---

## ✅ How to verify it works — five binary tests

- 🧪 **Paste a known honeypot** → the simulation must REVERT on the sell leg and refuse. If it fills anyway, the sim is theatre
- 🧾 **Check the tax report** → buy and sell tax are printed as numbers before the send, not after
- 💥 **Force a failure on purpose** → set slippage to 1% and buy: it should revert, and the app should show the gas you burned, honestly
- 🎯 **Run a 10% trailing stop on a small bag** → it fires at the line, no manual click, no "are you sure"
- 🔑 **Open the key file location** → a local JSON/keystore on your disk is a local key. A field where you paste a phrase into a web form is not

> The honeypot test is the honest one: every sniper works on the launch that goes up. The sim either rejects the ones that can't be sold or it's a random number generator with a UI.

---

## 🛡️ Real talk — latency, sandwiches and the exit

- 🏁 **You will lose the first block** — colocated bots and validators take it. Aim for the second block with a sim, not the first with a prayer. Any bot promising you block zero from home wifi is selling a story
- ⛽ **Failed transactions still cost gas** — a revert is a paid lesson. That's why the sim runs before the send, not after
- 🥪 **High slippage is sandwich bait** — 30% slippage doesn't mean "safe fill", it means "please take 25% of it". 5–8% and a private route is the sane default
- 🍯 **Honeypots, taxes, mint authority** — the three classics, and the sim catches all three for free. The expensive part is skipping it once because you were excited
- 📦 **Bundled supply is the invisible rug** — four wallets in the first slots holding 11% will dump into your exit. Check the bundle number, not the logo
- 🔑 **Hot wallet, never main** — a dedicated fresh wallet with what you're willing to lose. Infinite approvals are a standing invitation; keep them exact
- 🎯 **The launch is not the edge, the exit is** — a 40x you didn't sell is a screenshot. Trailing stop on, always
- ⚠️ **No bot makes money.** It removes hesitation, not risk

> ⚠️ Use at your own risk. Nothing here is financial advice.

---

## 💬 Your turn

What's the worst honeypot you ever bought — and do you still have a 2021 wallet you're afraid to open? Comments are open.
👍 Like & subscribe — builds drop with every chain upgrade!

---

#DeFi #Solana #Onchain

## DEX Sniper SEO Keywords

<details>
  <summary>🔍 Show all sniper keywords</summary>
  <pre>
dex sniper bot free, dex sniper bot download, dex sniper pc app, dex sniper desktop download, sniper bot how to install, new pair sniper how to, token launch sniper free, dex sniper app download, sniper bot free no key,

solana sniper bot free, pump fun sniper how to, base sniper bot download, eth sniper bot free, raylium sniper how to, dex sniper solana how to install, sniper bot solana download,

honeypot checker how to, honeypot simulation how to, auto sell bot how to, trailing stop bot how to, take profit ladder how to, mev protection how to, private rpc sniper how to, local key signing how to, bundle check how to, dev wallet check how to, infinite approval how to fix, sniper bot slippage how to set, sniper bot failed tx gas, sniper bot latency how to check
  </pre>
</details>