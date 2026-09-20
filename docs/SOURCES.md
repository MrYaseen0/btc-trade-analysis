# Proof of sources — 5 BTC strategies (researched 2026-09-20)

## X access — honest status
Direct X browsing was attempted and FAILED: x.com/search redirects to the login flow
(sign-in required, no bypass attempted) and the xcancel.com mirror is suspended
("service is suspended due to ongoing legal proceedings"). So no live X feed was read.
2 of 5 strategies are verifiably from X posts (via a thread mirror + a verbatim quote in
news coverage). The other 3 are the closest verifiable trader sources from Sept 2026.
Nothing was invented: every handle, quote, and link below is verbatim from search results.

| # | Strategy | Trader / author | Link | X-verified? |
|---|----------|-----------------|------|-------------|
| 1 | ICT Liquidity Sweep + Displacement | @casper_smc — X thread "My $100,000 ICT crypto trading strategy" | https://xstalk.com/profile/casper_smc/status/1877439213437698489 | YES — via xstalk mirror of full thread (X login-walled) |
| 2 | $78K Consolidation Breakout | Michaël van de Poppe @CryptoMichNL, X post Sep 14 2026: "Nothing has changed on #Bitcoin as it's still consolidating here. I'd much rather want to see that we're breaking through $78,000..." | https://finbold.com/trading-expert-sets-bitcoins-price-for-end-of-october-2026/ | YES — verbatim X post quoted in coverage |
| 3 | Defined-risk call spread (85/95 Sep) | Jean-David Pequignot (Deribit CCO), Markus Thielken (10x Research) via FXStreet, Aug 27 2026 | https://www.fxstreet.com/cryptocurrencies/news/bitcoin-experts-prefer-this-defined-risk-strategy-for-the-next-leg-higher-in-prices-202608271248 | NO — closest verifiable source |
| 4 | Funding-rate contrarian squeeze | Unnamed X analyst via AMBCrypto (Sep 3); positioning data via AsiaTokenFund (Sep 20) | https://ambcrypto.com/decoding-bitcoins-september-trap-is-drop-to-52k-looming-for-btc/ ; https://asiatokenfund.com/btc-price-prediction-82600-or-bust-bitcoins-next-72-hours-are-make-or-break/ | NO — closest verifiable source |
| 5 | SMC $79.2K confluence bounce | TradeNexus2000 + C-ICT Trader on Binance Square (~Sep 19); corroborated by aminrahmani888 on TradingView | https://www.binance.com/en/square/post/368688423979353 ; https://www.binance.com/en/square/post/368182085833618 | NO — Binance Square / TradingView posts |

## Market-data provenance (all real, fetched 2026-09-20 ~23:30 PKT)
- Price: Bitstamp BTC/USD OHLC — the SAME feed as the TradingView BITSTAMP:BTCUSD chart
  captured earlier. Daily: 1000 candles (2023-12-26 → 2026-09-20). 4H: 1000 candles
  (~2026-04-05 → 2026-09-20). 1H: 1000 candles (→ 2026-09-20 18:00 UTC).
  (Binance API was geo-blocked from this server, so Bitstamp + OKX were used.)
- Funding: OKX BTC-USDT-SWAP funding-rate history, public endpoint, 286 records (~95 days).
  Note: OKX 7d-average funding stayed POSITIVE through all of September 2026 — the
  "deeply negative funding" claim in one article did not verify on this feed.

## Backtest method (see backtest.py — fully reproducible)
- 1x spot, no leverage, no fees/slippage modeled. Per-trade returns compounded from $10,000.
- S1 (4H): sweep of 20-candle swing low + bullish displacement (>1.3x ATR14) -> long,
  SL = sweep low - 0.2 ATR, TP = 2R, 40-candle timeout.
- S2 (daily): long on daily close crossing above $78,000; exit on close back below $78,000.
- S3 (event): long spot Aug 27 close (80,279) -> Sep 19 close (81,252); 85/95 call-spread
  payoff shown as exact math vs premium (options pricing needs Deribit IV data).
- S4 (daily + funding): 7d avg funding < 0 AND 4 straight red daily candles -> long next open;
  TP +6%, SL -4%, 12-day timeout, exit if funding turns crowded (>0.15%).
- S5 (1H, live paper trade): limit fill mid-zone 81,175 (zone 81,050-81,300, posted Sep 19);
  SL on 1H close < 80,450; TP1 81,900; TP2 83,500.

## Results (results.json)
- S1: 10 trades, 20.0% win, -9.36% total, max DD -11.88%, PF 0.46
- S2: 12 trades, 0.0% win, -29.34% total, max DD -25.46% (2026 chop whipsawed every cross)
- S3: 1 trade (event), +1.21% spot leg
- S4: 0 trades — setup never triggered in 95-day window (funding never went negative)
- S5: TP1 HIT Sep 19 15:00 UTC, +0.89% in 15h. Holding for TP2 would have STOPPED on Sep 20.
- WINNER: S5 (SMC confluence bounce). Pine Script: smc_confluence_bounce.pine
