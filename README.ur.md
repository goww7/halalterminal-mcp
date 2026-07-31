# Halal Terminal MCP - AI ایجنٹس کے لیے شریعت کے مطابق اسٹاک اور ETF اسکریننگ

![AAPL halal status](https://api.halalterminal.com/api/badge/AAPL.svg) _API سے براہ راست بیج، کسی بھی علامت کے لیے ایک ایمبیڈ کریں_

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

[Halal Terminal](https://halalterminal.com) کا سرکاری **Model Context Protocol** سرور۔ اپنے AI ایجنٹ کو **22 ٹولز** دیں تاکہ وہ اسلامی مالیات کے سوالات کا جواب دے: کسی بھی اسٹاک یا ETF کو **5 طریقہ کار** (AAOIFI، DJIM، FTSE، MSCI، S&P) کے مطابق اسکرین کریں، پورٹ فولیوز کی آڈٹ کریں، **زکوٰۓ** اور **ڈیویڈنڈ پیوریفیکشن** کا حساب کتاب کریں، اور براہ راست مارکیٹ ڈیٹا، خبریں اور SEC فائلنگز حاصل کریں۔ **Claude Desktop، Claude Code، Cursor، Windsurf، Cline، Continue، Zed، Goose** اور کسی بھی دوسرے MCP کلائنٹ کے اندر کام کرتا ہے۔

> *"کیا AAPL حلال ہے؟"* · *"میرے پورٹ فولیو کی آڈٹ کریں: AAPL 30%، MSFT 20%، JNJ 50%"* · *"میری ہولڈنگز پر زکوٰۓ کا حساب لگائیں۔"*

## فوری آغاز

1. **مفت API کلید حاصل کریں** - [api.halalterminal.com](https://api.halalterminal.com) پر صرف ای میل سے سائن اپ۔ کریڈٹ کارڈ نہیں۔ چند سیکنڈز میں آپ کے ان باکس میں کلید پہنچ جاتی ہے۔
2. **اپنا کلائنٹ مربوط کریں** - ذیل میں ایک لائنر (یا [CONNECT.md](CONNECT.md) دیکھیں Cursor، Windsurf، Cline اور دیگر کے لیے)۔
3. **اپنا پہلا سوال پوچھیں** - `` `"Is AAPL halal?"` `` → ایجنٹ `screen_stock` کو کال کرتا ہے اور تمام 5 طریقہ کار کے فیصلے واپس کرتا ہے۔

## انسٹال کریں

```bash
# Recommended — no install needed
npx -y @halalterminal/mcp

# Or pin globally
npm install -g @halalterminal/mcp
```

### Claude Desktop

```json
{
  "mcpServers": {
    "halalterminal": {
      "command": "npx",
      "args": ["-y", "@halalterminal/mcp"],
      "env": { "HALALTERMINAL_API_KEY": "ht_yourkey" }
    }
  }
}
```

### Claude Code

```bash
claude mcp add --transport sse halalterminal \
  https://mcp.halalterminal.com/sse \
  --header "X-API-Key: ht_yourkey"
```

### Cursor / Windsurf / direct SSE

```
https://mcp.halalterminal.com/sse?api_key=ht_yourkey
```

تمام کلائنٹس کے لیے مکمل سیٹ اپ گائیڈ: [CONNECT.md](CONNECT.md)۔

## آپ کو کیا ملتا ہے - 8 زمرہ جات میں 22 ٹولز

| زمرہ | ٹولز |
|---|---|
| **اسکریننگ** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **مارکیٹ ڈیٹا** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **ETF تجزیہ** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **پورٹ فولیو اور واچ لسٹ** | `scan_portfolio`, `manage_watchlist` |
| **موازنہ** | `compare_stocks` |
| **آمدنی اور زکوٰۓ** | `get_dividends`, `calculate_zakat` |
| **خبریں اور فائلنگز** | `get_news`, `get_sec_filings` |
| **رپورٹس اور تعلیم** | `generate_report`, `islamic_finance_education` |

مکمل ان پٹ/آؤٹ پٹ حوالہ [TOOLS.md](TOOLS.md) میں ہے۔ اینڈ ٹو اینڈ پرامپٹ واک تھرو [EXAMPLES.md](EXAMPLES.md) میں ہیں۔

## Halal Terminal کیوں

- **5 طریقہ کار، ایک ٹول۔** AAOIFI، DJIM، FTSE Shariah، MSCI Islamic، اور S&P Shariah - ہر ایک میں الگ الگ بزنس ایکٹیویٹی کے اصول اور مالی تناسب کے حدود ہوتے ہیں - ہر اسٹاک کے لیے ایک ساتھ پیش کیے جاتے ہیں تاکہ صارفین وہ معیار منتخب کر سکیں جس کی پیروی کرتے ہیں۔
- **ہولڈنگز سطح ETF اسکریننگ۔** ہر جزو کی اسکریننگ کی جاتی ہے، وزن دیا جاتا ہے، اور مجموعی فیصلے میں جمع کیا جاتا ہے ساتھ ہی فی ڈالر پیوریفیکشن ریٹ۔ SPY، QQQ، VTI، ISDU، SPUS، HLAL، اور 8,000+ ETFs کو کور کرتا ہے۔
- **زکوٰۓ اور پیوریفیکشن، حساب شدہ۔** زندہ نصاب کی حد کے مقابلے میں 2.5% زکوٰۓ؛ جاری کنندہ کی غیر مطابق آمدنی کے تناسب کی بنیاد پر فی ڈیویڈنڈ ناپاک آمدنی کا حساب۔
- **بلک انڈیکس اسکرینز۔** S&P 500، NASDAQ-100، FTSE 100 اور دیگر پر ٹریگر اور پول رنز؛ طریقہ کار، شعبہ، یا صرف مطابق کی فلٹرنگ۔
- **مفت ٹائر، کریڈٹ کارڈ نہیں۔** ای میل سائن اپ → چند سیکنڈز میں آپ کے ان باکس میں کلید → ~5-10 مکمل اسکرینز فی ماہ بغیر کسی قیمت کے۔

## اینڈ پوائنٹ اور ٹرانسپورٹ

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

تعاون یافتہ ٹرانسپورٹ: **SSE** (تجویز کردہ)، **stdio** (اس `@halalterminal/mcp` برج کے ذریعے ان کلائنٹس کے لیے جنہیں اس کی ضرورت ہے)۔

## پلانز اور کوٹا

Halal Terminal API **ٹوکن میٹرڈ** ہے، ریکویسٹ میٹرڈ نہیں۔

| پلان | ماہانہ ٹوکنز | قیمت | نوٹس |
|---|---|---|---|
| **مفت** | 50 | $0 | ~5-10 مکمل اسکرینز · ای میل سائن اپ، کریڈٹ کارڈ نہیں |
| **اسٹارٹر** | 2,500 | $19 | انفرادی سرمایہ کار |
| **پرو** | 15,000 | $49 | ویب ہکس، بلک ترجیح |
| **انٹرپرائز** | Unlimited | $199+ | کسٹم طریقہ کار، SLA |

سائن اپ: [api.halalterminal.com](https://api.halalterminal.com) · قیمتیں: [halalterminal.com/pricing](https://halalterminal.com/pricing)

## یہ MCP سرور کیا نہیں ہے

- **فتویٰ نہیں۔** ہر فیصلہ طریقہ کار پر مبنی اسکریننگ ہے۔ ذاتی فیصلوں کے لیے ایک اہل عالم سے مشورہ کریں۔
- **ٹریڈنگ پلیٹ فارم نہیں۔** کوئی بروکر انٹیگریشن نہیں، کوئی آرڈر ایگزیکوشن نہیں۔
- **ریل ٹائم الرٹ سسٹم نہیں۔** v1 میں صرف ریکویسٹ ریسپانس؛ ویب ہک ڈرائیون الرٹس Pro+ روڈ میپ پر ہیں۔
- **v1 میں صرف انگریزی۔** عربی + فرانسیسی رینڈرنگ روڈ میپ پر ہے۔

## عمومی سوالات

### کیا یہ MCP سرور مفت استعمال کے لیے ہے؟

جی ہاں۔ `@halalterminal/mcp` پیکیج Apache-2.0 ہے اور مفت ہے۔ Halal Terminal API میں ایک مفت ٹائر (500 ٹوکنز / مہینہ، کریڈٹ کارڈ نہیں) ہے جو ~100 مکمل اسٹاک اسکرینز کو کور کرتا ہے - اپ گریڈ کرنے سے پہلے اس کی جانچ کے لیے کافی ہے۔

### یہ کس AI کلائنٹس کے ساتھ کام کرتا ہے؟

کوئی بھی کلائنٹ جو **SSE** یا **stdio** پر Model Context Protocol کو سپورٹ کرتا ہو - Claude Desktop، Claude Code، Cursor، Windsurf، Cline، Continue، Zed، Goose، اور مزید۔ SSE تجویز کردہ ہے؛ `@halalterminal/mcp` پیکیج اسے stdio کے طور پر ریپ کرتا ہے ان کلائنٹس کے لیے جو ابھی SSE کو سپورٹ نہیں کرتے۔

### "حلال" کیسے تعین ہوتا ہے؟

ہر فیصلہ منتخب شدہ طریقہ کار کے شائع شدہ اصولوں پر لاگو ہوتا ہے - **AAOIFI**، **Dow Jones Islamic Market (DJIM)**، **FTSE Shariah**، **MSCI Islamic**، اور **S&P Shariah**۔ دو پرتیں: (1) ایک **بزنس ایکٹیویٹی** اسکرین (نہ شراب، جوا، روایتی مالیات، بالغ مواد، ہتھیار، سور، …)، پھر (2) **مالی تناسب** کی حدود (مثلاً سودی قرضہ مارکیٹ کیپ پر، غیر مائع اثاثے، سودی آمدنی کا حصہ)۔ MCP تمام پانچ فیصلے ظاہر کرتا ہے تاکہ صارف - یا عالم - وہ معیار منتخب کر سکے جس کی پیروی کرتے ہیں۔

### ڈیویڈنڈ پیوریفیکشن کیا ہے؟

جب آپ ایک ایسا اسٹاک رکھتے ہیں جس میں غیر مطابق آمدنی کا ایک چھوٹا حصہ ہو، علماء کسی بھی موصول شدہ ڈیویڈنڈ کے غیر مطابق حصے کا صدقہ کرنے کا تقاضا کرتے ہیں۔ `calculate_zakat(calculation_type="purification", …)` اور `get_dividends(include_purification=True)` وہ رقم خود بخود حساب کرتے ہیں۔

### کیا یہ ETFs کی اسکریننگ کر سکتا ہے؟

جی ہاں - `screen_etf` ہر بنیادی ہولڈنگ کو چلتا ہے، ہر ایک پر طریقہ کار لاگو کرتا ہے، اور مجموعی فیصلہ، مطابق فیصد، اور مجموعی پیوریفیکشن ریٹ واپس کرتا ہے۔ صکوک ETFs الگ سے ہینڈل کیے جاتے ہیں (اثاثہ پر مبنی طریقہ کار)۔

### کیا میں ایک پورے انڈیکس کی ایک ساتھ اسکریننگ کر سکتا ہوں؟

جی ہاں - `bulk_screen` S&P 500، NASDAQ-100، FTSE 100 جیسے انڈیکسز پر غیر ہم وقت رن ٹریگر کرتا ہے، اور آپ کو حیثیت پول کرنے، نتائج کو طریقہ کار / شعبہ / صرف مطابق کے لحاظ سے فلٹر کرنے، اور دو رنز کے درمیان فرق دیکھنے دیتا ہے۔

### کیا یہ مطابقت کی تبدیلیوں کے لیے ویب ہکس کو سپورٹ کرتا ہے؟

ویب ہکس API روڈ میپ پر ایک Pro-plan فیچر ہیں؛ اس MCP کا v1 صرف ریکویسٹ ریسپانس ہے۔

### میں بگز کی رپورٹ یا ٹولز کی درخواست کہاں کروں؟

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) یا ای میل yassir@halalterminal.com۔

## مزید جانیں

- [API حوالہ](https://api.halalterminal.com/api-reference)
- [اسلامی مالیات MCP سرور کی تعمیر](https://www.halalterminal.com/blog/posts/islamic-finance-mcp-server)
- [اسلامی مالیات کیا ہے؟](https://www.halalterminal.com/research/what-is-islamic-finance)
- [صکوک اسکریننگ گائیڈ](https://www.halalterminal.com/research/sukuk-screening)
- [کیا میرا اسٹاک حلال ہے؟ اسکرینر](https://www.halalterminal.com/stocks)

## Halal Terminal ایکوسسٹم کا حصہ

[ویب سائٹ](https://www.halalterminal.com) · [API](https://api.halalterminal.com/api-reference) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [Claude پلگ ان](https://github.com/goww7/halalterminal-claude-skills) · [Discord بوٹ](https://github.com/goww7/halal-discord-bot) · [TradingView انڈیکیٹر](https://github.com/goww7/halal-pine) · [پورٹ فولیو ٹریکر](https://github.com/goww7/halal-portfolio-tracker)

## متعلقہ منصوبے (بہن OSS)

وہ اوپن سورس ٹولز جو Halal Terminal API کو مشترکہ استعمال کرتے ہیں - مختلف سطحیں، ایک ہی ڈیٹا:

| منصوبہ | یہ کیا ہے | لائسنس |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Claude Code پلگ ان - منتخب مہارتیں، سلیش کمانڈز، اور اس MCP سرور پر ایک پورٹ فولیو بلڈر سب ایجنٹ۔ | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | حلال مالیات تحقیق کے لیے اوپن سورس ReAct ایجنٹ - CLI + ویب UI؛ OpenAI / Anthropic / مقامی LLMs کو سپورٹ کرتا ہے۔ | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Discord بوٹ - `/halal AAPL`، `/portfolio`، `/trending` سلیش کمانڈز۔ | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | Next.js 14 ایپ - ہولڈنگز درج کریں، فی اسٹاک مطابقت + پورٹ فولیو حلال % + واجب پیوریفیکشن حاصل کریں۔ ایک کلک Vercel ڈپلائے۔ | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | TradingView Pine Script v5 انڈیکیٹر جو چارٹس پر مطابقت کی حیثیت اوورلے کرتا ہے۔ روزانہ اس API سے ریفریش ہوتا ہے۔ | MIT |

## لائسنس اور ٹریڈ مارکس

Apache-2.0 - [LICENSE](LICENSE) دیکھیں۔

"Halal Terminal"، "HalalTerminal"، اور Halal Terminal کا لوگو محفوظ شدہ ٹریڈ مارکس ہیں - [TRADEMARKS.md](TRADEMARKS.md) دیکھیں۔

## قانونی

- [قانونی اور دستبرداری](https://halalterminal.com/legal) - تعلیمی تحقیقی فریم ورک، سرمایہ کاری دستبرداری، شریعت مطابقت نوٹس، ذمہ داری کی حدود، دائرہ اختیار نوٹس
- [پرائیویسی پالیسی](https://halalterminal.com/privacy)
- [کوکی پالیسی](https://halalterminal.com/cookies)

## سپورٹ

- رابطہ: yassir@halalterminal.com
- ڈیش بورڈ: [api.halalterminal.com/dashboard](https://api.halalterminal.com/dashboard)
- API دستاویزات: [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Halal Terminal کی طرف سے طاقت یافتہ - [halalterminal.com](https://halalterminal.com)

---

[Halal Terminal open ecosystem](https://github.com/goww7/awesome-islamic-finance) کا حصہ:
[API](https://api.halalterminal.com) · [MCP سرور](https://github.com/goww7/halalterminal-mcp) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [ڈیٹاسیٹس](https://github.com/goww7/sp500-shariah-compliance) · [Awesome Islamic Finance](https://github.com/goww7/awesome-islamic-finance)