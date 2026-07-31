# Halal Terminal MCP - Penapisan saham & ETF patuh Shariah untuk ejen AI

![AAPL halal status](https://api.halalterminal.com/api/badge/AAPL.svg) _lencana langsung daripada API, sematkan satu untuk sebarang simbol_

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

Pelayan **Model Context Protocol** rasmi untuk [Halal Terminal](https://halalterminal.com). Berikan **22 alat** kepada ejen AI anda untuk menjawab soalan kewangan Islam: tapis sebarang saham atau ETF merentasi **5 metodologi** (AAOIFI, DJIM, FTSE, MSCI, S&P), audit portfolio, kira **zakat** dan **penulenan dividen**, serta tarik data pasaran langsung, berita dan fail SEC. Berfungsi dalam **Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose**, dan mana-mana klien MCP lain.

> *"Adakah AAPL halal?"* · *"Audit portfolio saya: AAPL 30%, MSFT 20%, JNJ 50%"* · *"Kira zakat atas pegangan saya."*

## Permulaan pantas

1. **Dapatkan kunci API percuma** - pendaftaran e-mel sahaja di [api.halalterminal.com](https://api.halalterminal.com). Tiada kad kredit. Kunci tiba dalam peti masuk anda dalam beberapa saat.
2. **Sambungkan klien anda** - ayat tunggal di bawah (atau lihat [CONNECT.md](CONNECT.md) untuk Cursor, Windsurf, Cline, dan lain-lain).
3. **Tanya soalan pertama anda** - `"Adakah AAPL halal?"` → ejen memanggil `screen_stock` dan mengembalikan keputusan merentasi kesemua 5 metodologi.

## Pemasangan

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

Panduan persediaan penuh untuk semua klien: [CONNECT.md](CONNECT.md).

## Apa yang anda dapat - 22 alat merentasi 8 kategori

| Kategori | Alat |
|---|---|
| **Penapisan** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **Data pasaran** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **Analisis ETF** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **Portfolio & senarai pantau** | `scan_portfolio`, `manage_watchlist` |
| **Perbandingan** | `compare_stocks` |
| **Pendapatan & zakat** | `get_dividends`, `calculate_zakat` |
| **Berita & fail** | `get_news`, `get_sec_filings` |
| **Laporan & pendidikan** | `generate_report`, `islamic_finance_education` |

Rujukan input/output penuh dalam [TOOLS.md](TOOLS.md). Panduan arahan hujung ke hujung dalam [EXAMPLES.md](EXAMPLES.md).

## Mengapa Halal Terminal

- **5 metodologi, satu alat.** AAOIFI, DJIM, FTSE Shariah, MSCI Islamic, dan S&P Shariah (setiap satunya dengan peraturan aktiviti perniagaan dan ambang nisbah kewangan yang tersendiri), ditunjukkan bersebelahan bagi setiap saham supaya pengguna memilih piawaian yang mereka ikuti.
- **Penapisan ETF peringkat pegangan.** Setiap komponen ditapis, ditimbang, dan diagregatkan menjadi keputusan keseluruhan serta kadar penulenan setiap dolar. Merangkumi SPY, QQQ, VTI, ISDU, SPUS, HLAL, dan 8,000+ ETF.
- **Zakat & penulenan, dikira.** Zakat 2.5% terhadap ambang nisab terkini; pengiraan pendapatan tidak suci setiap dividen berdasarkan nisbah hasil tidak patuh penerbit.
- **Penapisan indeks pukal.** Larian picu-dan-tinjau pada S&P 500, NASDAQ-100, FTSE 100, dan lain-lain; tapis mengikut metodologi, sektor, atau patuh-sahaja.
- **Percuma, tiada kad kredit.** Pendaftaran e-mel → kunci dalam peti masuk anda dalam beberapa saat → ~5–10 penapisan penuh sebulan tanpa kos.

## Titik hujung & pengangkutan

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

Pengangkutan yang disokong: **SSE** (disyorkan), **stdio** (melalui penghubung `@halalterminal/mcp` ini untuk klien yang memerlukannya).

## Pelan & kuota

API Halal Terminal adalah **dihitung berasaskan token**, bukan berasaskan permintaan.

| Pelan | Token bulanan | Harga | Nota |
|---|---|---|---|
| **Percuma** | 50 | $0 | ~5–10 penapisan penuh · pendaftaran e-mel, tiada kad kredit |
| **Permulaan** | 2,500 | $19 | Pelabur individu |
| **Pro** | 15,000 | $49 | Webhooks, keutamaan pukal |
| **Enterprise** | Unlimited | $199+ | Metodologi tersuai, SLA |

Daftar: [api.halalterminal.com](https://api.halalterminal.com) · Harga: [halalterminal.com/pricing](https://halalterminal.com/pricing)

## Apa yang pelayan MCP ini BUKAN

- **Bukan fatwa.** Setiap keputusan adalah penapisan berasaskan metodologi. Rujuk ulama yang berkelayakan untuk hukum peribadi.
- **Bukan platform perdagangan.** Tiada integrasi broker, tiada pelaksanaan pesanan.
- **Bukan sistem amaran masa nyata.** Hanya permintaan-respons dalam v1; amaran berpandu webhook ada dalam hala tuju Pro+.
- **Hanya Bahasa Inggeris dalam v1.** Penyampaian Bahasa Arab + Perancis ada dalam hala tuju.

## Soalan Lazim

### Adakah pelayan MCP ini percuma untuk digunakan?

Ya. Pakej `@halalterminal/mcp` adalah Apache-2.0 dan percuma. API Halal Terminal mempunyai peringkat percuma (500 token / bulan, tiada kad kredit) yang merangkumi ~100 penapisan saham penuh (mencukupi untuk menilainya sebelum menaik taraf).

### Dengan klien AI manakah ia serasi?

Mana-mana klien yang menyokong Model Context Protocol melalui **SSE** atau **stdio**: Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose, dan banyak lagi. SSE disyorkan; pakej `@halalterminal/mcp` membalutkannya sebagai stdio untuk klien yang belum menyokong SSE.

### Bagaimanakah "halal" ditentukan?

Setiap keputusan menggunakan peraturan yang diterbitkan oleh metodologi yang dipilih - **AAOIFI**, **Dow Jones Islamic Market (DJIM)**, **FTSE Shariah**, **MSCI Islamic**, dan **S&P Shariah**. Dua lapisan: (1) penapisan **aktiviti perniagaan** (tiada alkohol, perjudian, kewangan konvensional, kandungan dewasa, senjata, khinzir, …), kemudian (2) ambang **nisbah kewangan** (contohnya hutang berfaedah melebihi nilai pasaran, aset tidak cair, bahagian hasil faedah). Pelayan MCP memperlihatkan kelima-lima keputusan supaya pengguna, atau ulama, boleh memilih piawaian yang mereka ikuti.

### Apakah penulenan dividen?

Apabila anda memegang saham dengan bahagian hasil tidak patuh yang kecil, ulama menghendaki menderma bahagian tidak patuh daripada sebarang dividen yang diterima. `calculate_zakat(calculation_type="purification", …)` dan `get_dividends(include_purification=True)` mengira jumlah itu secara automatik.

### Bolehkah ia menapis ETF?

Ya. `screen_etf` melalui setiap pegangan asas, menggunakan metodologi pada setiap satunya, dan mengembalikan keputusan keseluruhan, peratusan patuh, dan kadar penulenan agregat. ETF Sukuk diuruskan secara berasingan (metodologi berasaskan aset).

### Bolehkah saya menapis keseluruhan indeks sekaligus?

Ya. `bulk_screen` mencetuskan larian tidak segerak pada indek seperti S&P 500, NASDAQ-100, FTSE 100, dan membolehkan anda meninjau status, menapis keputusan mengikut metodologi / sektor / patuh-sahaja, dan membezakan dua larian.

### Adakah ia menyokong webhook untuk perubahan pematuhan?

Webhook adalah ciri pelan Pro dalam hala tuju API; v1 pelayan MCP ini hanya permintaan-respons.

### Di manakah saya melaporkan pepijat atau meminta alat?

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) atau e-mel yassir@halalterminal.com.

## Ketahui lebih lanjut

- [Rujukan API](https://api.halalterminal.com/api-reference)
- [Membina pelayan MCP kewangan Islam](https://www.halalterminal.com/blog/posts/islamic-finance-mcp-server)
- [Apakah kewangan Islam?](https://www.halalterminal.com/research/what-is-islamic-finance)
- [Panduan penapisan Sukuk](https://www.halalterminal.com/research/sukuk-screening)
- [Adakah saham saya halal? Penapis](https://www.halalterminal.com/stocks)

## Sebahagian daripada ekosistem Halal Terminal

[Laman web](https://www.halalterminal.com) · [API](https://api.halalterminal.com/api-reference) · [SDK Python](https://github.com/goww7/halalterminal-sdk-python) · [SDK JS](https://github.com/goww7/halalterminal-sdk-js) · [Claude plugin](https://github.com/goww7/halalterminal-claude-skills) · [Discord bot](https://github.com/goww7/halal-discord-bot) · [TradingView indicator](https://github.com/goww7/halal-pine) · [Penjejak portfolio](https://github.com/goww7/halal-portfolio-tracker)

## Projek berkaitan (OSS saudara)

Alat sumber terbuka yang berkongsi API Halal Terminal yang sama: permukaan berbeza, data sama:

| Projek | Apa itu | Lesen |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Plugin Claude Code - kemahiran terpilih, arahan slash, dan sub-ejen pembina portfolio di atas pelayan MCP ini. | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | Ejen ReAct sumber terbuka untuk penyelidikan kewangan halal - CLI + UI web; menyokong OpenAI / Anthropic / LLM tempatan. | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Bot Discord - arahan slash `/halal AAPL`, `/portfolio`, `/trending`. | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | Aplikasi Next.js 14 - masukkan pegangan, dapatkan pematuhan setiap saham + % halal portfolio + penulenan yang perlu dibayar. Penerapan Vercel satu klik. | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | Penunjuk TradingView Pine Script v5 yang memaparkan status pematuhan di atas carta. Dikemas kini harian daripada API ini. | MIT |

## Lesen & tanda dagang

Apache-2.0 - lihat [LICENSE](LICENSE).

"Halal Terminal", "HalalTerminal", dan logo Halal Terminal adalah tanda dagang terpelihara - lihat [TRADEMARKS.md](TRADEMARKS.md).

## Perundangan

- [Perundangan & Penafian](https://halalterminal.com/legal) - kerangka pendidikan-penyelidikan, penafian pelaburan, notis pematuhan Shariah, had liabiliti, notis bidang kuasa
- [Dasar Privasi](https://halalterminal.com/privacy)
- [Dasar Kuki](https://halalterminal.com/cookies)

## Sokongan

- Hubungi: yassir@halalterminal.com
- Papan pemuka: [api.halalterminal.com/dashboard](https://api.halalterminal.com/dashboard)
- Dokumen API: [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Dikuasakan oleh Halal Terminal - [halalterminal.com](https://halalterminal.com)


---

Sebahagian daripada [ekosistem terbuka Halal Terminal](https://github.com/goww7/awesome-islamic-finance):
[API](https://api.halalterminal.com) · [Pelayan MCP](https://github.com/goww7/halalterminal-mcp) · [SDK Python](https://github.com/goww7/halalterminal-sdk-python) · [SDK JS](https://github.com/goww7/halalterminal-sdk-js) · [Set data](https://github.com/goww7/sp500-shariah-compliance) · [Awesome Islamic Finance](https://github.com/goww7/awesome-islamic-finance)