# 風控計算小幫手

為您精確把關每一筆交易的風險。輸入本金、風控百分比、手數與合約規格，即時算出：

- 最大容忍波動（點數與 % 數）
- 每 1 點價值
- 多單／空單止損參考位
- 預計總虧損

支援指數／能源、貴金屬、外匯、加密貨幣四大類，輸入商品符號（如 HK50、XAUUSD、ETH）會自動帶入合約規格。

## 計算公式

- 預計總虧損 = 本金 × 風控%
- 每 1 點價值（USD）= 手數 × 合約規格 ÷ 匯率（1 USD = ? 計價貨幣）
  - USD 計價商品匯率為 1
  - USDJPY、USDCAD 等以美元為基準的貨幣對，匯率直接用當前市價
  - 其他非美元計價（GBPJPY、HK50、JP225…）自動抓取參考匯率（ExchangeRate-API，備援 Frankfurter），抓不到時可手動輸入
- 最大容忍波動 = 預計總虧損 ÷ 每 1 點價值
- 多單止損 = 現價 − 容忍波動；空單止損 = 現價 + 容忍波動

## 部署到 GitHub Pages

1. 在 GitHub 建立新的 repository（例如 `risk-calculator`），設為 Public
2. 上傳 `index.html` 與 `README.md`
3. 到 Settings → Pages，Source 選 `Deploy from a branch`，Branch 選 `main`、資料夾選 `/ (root)`，按 Save
4. 約 1 分鐘後網址會出現：`https://<你的帳號>.github.io/risk-calculator/`

## 合約規格來源

新增商品的規格參考主流 MT5 券商（IC Markets、Exness、Eightcap 等）的多數設定；HK50=50、GER40=25、JP225=100、ETH=10 沿用原版設定。實際下單請以所用券商的合約規格為準。

## 修改合約規格

打開 `index.html`，找到 `productDatabase`，依格式新增或修改商品即可，例如：

```js
'US30': { size: 10, mode: 'indices' },
```

單一 HTML 檔，不需安裝或編譯。
