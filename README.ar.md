# Halal Terminal MCP - فحص الأسهم وصناديق الاستثمار المتداولة المتوافقة مع الشريعة لوكلاء الذكاء الاصطناعي

![AAPL halal status](https://api.halalterminal.com/api/badge/AAPL.svg) _live badge from the API, embed one for any symbol_

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

الخادم الرسمي لبروتوكول **Model Context Protocol** الخاص بـ [Halal Terminal](https://halalterminal.com). منح وكيل الذكاء الاصطناعي **22 أداة** للإجابة على الأسئلة المالية الإسلامية: فحص أي سهم أو صندوق استثمار متداول عبر **5 منهجيات** (AAOIFI, DJIM, FTSE, MSCI, S&P)، ومراجعة المحافظ الاستثمارية، وحساب **الزكاة** و**تطهير الأرباح**، وجلب بيانات السوق المباشرة والأخبار وإيداعات SEC. يعمل داخل **Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose**، وأي عميل MCP آخر.

> *"هل AAPL حلال؟"* · *"راجع محفظتي: AAPL 30%، MSFT 20%، JNJ 50%"* · *"احسب زكاة ما أملك."*

## البدء السريع

1. **احصل على مفتاح API مجاني** - التسجيل بالبريد الإلكتروني فقط على [api.halalterminal.com](https://api.halalterminal.com). لا حاجة لبطاقة ائتمان. يصلك المفتاح إلى صندوق الوارد في ثوانٍ.
2. **اربط عميلك** - الأوامر المختصرة أدناه (أو راجع [CONNECT.md](CONNECT.md) للحصول على إرشادات Cursor وWindsurf وCline وغيرها).
3. **اطرح سؤالك الأول** - `` `"Is AAPL halal?"` `` → يستدعي الوكيل `screen_stock` ويعيد الأحكام عبر المنهجيات الخمسة جميعها.

## التثبيت

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

### Cursor / Windsurf / SSE المباشر

```
https://mcp.halalterminal.com/sse?api_key=ht_yourkey
```

دليل الإعداد الكامل لجميع العملاء: [CONNECT.md](CONNECT.md).

## ما تحصل عليه - 22 أداة عبر 8 فئات

| الفئة | الأدوات |
|---|---|
| **الفحص** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **بيانات السوق** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **تحليل صناديق الاستثمار المتداولة** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **المحفظة وقائمة المراقبة** | `scan_portfolio`, `manage_watchlist` |
| **المقارنة** | `compare_stocks` |
| **الدخل والزكاة** | `get_dividends`, `calculate_zakat` |
| **الأخبار والإيداعات** | `get_news`, `get_sec_filings` |
| **التقارير والتعليم** | `generate_report`, `islamic_finance_education` |

مرجع الإدخال/الإخراج الكامل في [TOOLS.md](TOOLS.md). جولات توضيحية شاملة للأوامر في [EXAMPLES.md](EXAMPLES.md).

## لماذا Halal Terminal

- **5 منهجيات، أداة واحدة.** AAOIFI وDJIM وFTSE Shariah وMSCI Islamic وS&P Shariah - كل منها بقواعد نشاط تجاري مميزة وعتبات نسب مالية - يتم عرضها جنبًا إلى جنب لكل سهم ليتمكن المستخدمون من اختيار المعيار الذي يتبعونه.
- **فحص صناديق الاستثمار المتداولة على مستوى المكونات.** يتم فحص كل مكون وتقدير أوزانه وتجميعها في حكم إجمالي بالإضافة إلى معدل تطهير لكل دولار. يغطي SPY وQQQ وVTI وISDU وSPUS وHLAL وأكثر من 8000+ صندوق استثمار متداول.
- **الزكاة والتطهير، محسوبان.** زكاة 2.5% مقابل عتبة نصاب مباشرة؛ وحساب الدخل غير المطهر لكل توزيعة أرباح بناءً على نسبة الإيرادات غير المتوافقة للمصدر.
- **فحوصات المؤشرات المجمّعة.** عمليات التشغيل والاستطلاع على S&P 500 وNASDAQ-100 وFTSE 100 وغيرها؛ مع التصفية حسب المنهجية أو القطاع أو المتوافق فقط.
- **الخطة المجانية، بدون بطاقة ائتمان.** التسجيل بالبريد الإلكتروني → يصلك المفتاح في ثوانٍ → نحو 5-10 فحوصات كاملة شهريًا بدون تكلفة.

## نقطة النهاية والنقل

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

البروتوكولات المدعومة: **SSE** (موصى به)، **stdio** (عبر حزمة `@halalterminal/mcp` هذه للعملاء التي تحتاج إليها).

## الخطط والحصص

واجهة برمجة تطبيقات Halal Terminal **token-metered**، وليست request-metered.

| الخطة | الرموز الشهرية | السعر | الملاحظات |
|---|---|---|---|
| **Free** | 50 | $0 | نحو 5-10 فحوصات كاملة · تسجيل بالبريد الإلكتروني، بدون بطاقة ائتمان |
| **Starter** | 2,500 | $19 | المستثمرون الأفراد |
| **Pro** | 15,000 | $49 | Webhooks، أولوية الفحص المجمّع |
| **Enterprise** | Unlimited | $199+ | منهجيات مخصصة، اتفاقية مستوى الخدمة |

التسجيل: [api.halalterminal.com](https://api.halalterminal.com) · التسعير: [halalterminal.com/pricing](https://halalterminal.com/pricing)

## ما ليس عليه خادم MCP هذا

- **ليس فتوى.** كل حكم هو نتيجة فحص مبني على المنهجية. استشر عالمًا مؤهلًا للحصول على أحكام شخصية.
- **ليس منصة تداول.** لا تكاملات مع وسطاء، ولا تنفيذ للطلبات.
- **ليس نظام تنبيهات في الوقت الفعلي.** طلب-استجابة فقط في v1؛ وتنبيهات مدفوعة بـ Webhooks في خارطة طريق Pro+.
- **الإنجليزية فقط في v1.** دعم العرض بالعربية والفرنسية في خارطة الطريق.

## الأسئلة الشائعة

### هل خادم MCP هذا مجاني للاستخدام؟

نعم. حزمة `@halalterminal/mcp` مرخصة بموجب Apache-2.0 ومجانية. تقدم واجهة برمجة تطبيقات Halal Terminal خطة مجانية (500 رمز شهريًا، بدون بطاقة ائتمان) تغطي نحو 100 فحص كامل للأسهم - كافية لتقييمها قبل الترقية.

### مع أي عملاء ذكاء اصطناعي يعمل؟

أي عميل يدعم بروتوكول Model Context Protocol عبر **SSE** أو **stdio** - Claude Desktop وClaude Code وCursor وWindsurf وCline وContinue وZed وGoose وغيرها. يُنصح بـ SSE؛ تحزم `@halalterminal/mcp` هذه البروتوكول كـ stdio للعملاء التي لا تدعم SSE بعد.

### كيف يُحدّد "الحلال"؟

يطبق كل حكم القواعد المنشورة للمنهجية المختارة - **AAOIFI** و**Dow Jones Islamic Market (DJIM)** و**FTSE Shariah** و**MSCI Islamic** و**S&P Shariah**. طبقتان: (1) فحص **النشاط التجاري** (لا كحول، ولا قمار، ولا تمويل تقليدي، ولا محتوى للبالغين، ولا أسلحة، ولا لحم خنزير، …)، ثم (2) عتبات **النسب المالية** (مثل الديون التي تحمل فوائد مقابل القيمة السوقية، والأصول غير السائلة، وحصة الدخل من الفوائد). يُتيح بروتوكول MCP جميع الأحكام الخمسة ليتمكن المستخدم - أو العالم - من اختيار المعيار الذي يتبعونه.

### ما هو تطهير الأرباح؟

عندما تملك سهمًا بحصة صغيرة من الإيرادات غير المتوافقة، يتطلب العلماء التصدق بالحصة غير المتوافقة من أي توزيعة أرباح تتلقاها. يقوم `calculate_zakat(calculation_type="purification", …)` و`get_dividends(include_purification=True)` بحساب هذا المبلغ تلقائيًا.

### هل يمكنه فحص ETFs؟

نعم - يقوم `screen_etf` بفحص كل أصل أساسي، وتطبيق المنهجية على كل منها، وإرجاع حكم إجمالي ونسبة توافق ومعدل تطهير مجمع. يتم التعامل مع ETFs السكوك بشكل منفصل (منهجيات قائمة على الأصول).

### هل يمكنني فحص مؤشر كامل دفعة واحدة؟

نعم - يُطلق `bulk_screen` عملية تشغيل غير متزامن على مؤشرات مثل S&P 500 وNASDAQ-100 وFTSE 100، ويتيح لك الاستعلام عن الحالة، وتصفية النتائج حسب المنهجية / القطاع / المتوافق فقط، ومقارنة الفرق بين عمليتين.

### هل تدعم Webhooks لتغييرات الامتثال؟

Webhooks ميزة في خطة Pro على خارطة طريق واجهة برمجة التطبيقات؛ الإصدار v1 من بروتوكول MCP هذا يدعم طلب-استجابة فقط.

### أين أبلغ عن الأخطاء أو أطلب أدوات؟

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) أو البريد الإلكتروني yassir@halalterminal.com.

## تعرّف أكثر

- [مرجع واجهة برمجة التطبيقات](https://api.halalterminal.com/api-reference)
- [بناء خادم MCP للتمويل الإسلامي](https://www.halalterminal.com/blog/posts/islamic-finance-mcp-server)
- [ما هو التمويل الإسلامي؟](https://www.halalterminal.com/research/what-is-islamic-finance)
- [دليل فحص السكوك](https://www.halalterminal.com/research/sukuk-screening)
- [هل سهمي حلال؟ أداة الفحص](https://www.halalterminal.com/stocks)

## جزء من نظام Halal Terminal البيئي

[الموقع الإلكتروني](https://www.halalterminal.com) · [API](https://api.halalterminal.com/api-reference) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [Claude plugin](https://github.com/goww7/halalterminal-claude-skills) · [Discord bot](https://github.com/goww7/halal-discord-bot) · [TradingView indicator](https://github.com/goww7/halal-pine) · [Portfolio tracker](https://github.com/goww7/halal-portfolio-tracker)

## مشاريع ذات صلة (مفتوحة المصدر شقيقة)

أدوات مفتوحة المصدر تشترك في نفس واجهة برمجة تطبيقات Halal Terminal - واجهات مختلفة، نفس البيانات:

| المشروع | ما هو | الترخيص |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Claude Code plugin - مهارات منتقاة، وأوامر slash، ووكيل فرعي لبناء المحافظ فوق خادم MCP هذا. | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | وكيل ReAct مفتوح المصدر لأبحاث التمويل الحلال - CLI + واجهة ويب؛ يدعم OpenAI / Anthropic / نماذج لغوية كبيرة محلية. | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Discord bot - أوامر slash `/halal AAPL` و`/portfolio` و`/trending`. | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | تطبيق Next.js 14 - أدخل الأصول، واحصل على الامتثال لكل سهم + نسبة الحلال للمحفظة + التطهير المستحق. نشر على Vercel بنقرة واحدة. | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | مؤشر TradingView Pine Script v5 يظهر حالة الامتثال على الرسوم البيانية. يتم تحديثه يوميًا من واجهة برمجة التطبيقات هذه. | MIT |

## الترخيص والعلامات التجارية

Apache-2.0 - انظر [LICENSE](LICENSE).

"Halal Terminal" و"HalalTerminal" وشعار Halal Terminal علامات تجارية محفوظة - انظر [TRADEMARKS.md](TRADEMARKS.md).

## القانوني

- [القانوني وإخلاء المسؤولية](https://halalterminal.com/legal) - إطار التعليم والبحث، وإخلاء مسؤولية الاستثمار، وإشعار الامتثال للشريعة، وحدود المسؤولية، وإشعارات الاختصاص القضائي
- [سياسة الخصوصية](https://halalterminal.com/privacy)
- [سياسة ملفات تعريف الارتباط](https://halalterminal.com/cookies)

## الدعم

- التواصل: yassir@halalterminal.com
- لوحة التحكم: [api.halalterminal.com/dashboard](https://api.halalterminal.com/dashboard)
- وثائق API: [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Powered by Halal Terminal - [halalterminal.com](https://halalterminal.com)

---

جزء من [النظام البيئي المفتوح Halal Terminal](https://github.com/goww7/awesome-islamic-finance):
[API](https://api.halalterminal.com) · [خادم MCP](https://github.com/goww7/halalterminal-mcp) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [مجموعات البيانات](https://github.com/goww7/sp500-shariah-compliance) · [Awesome Islamic Finance](https://github.com/goww7/awesome-islamic-finance)