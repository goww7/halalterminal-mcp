# Halal Terminal MCP - Penyaringan saham & ETF sesuai syariah untuk agen AI

![AAPL halal status](https://api.halalterminal.com/api/badge/AAPL.svg) _lencana langsung dari API, sematkan satu untuk simbol apa pun_

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

Server resmi **Model Context Protocol** untuk [Halal Terminal](https://halalterminal.com). Berikan agen AI Anda **22 alat** untuk menjawab pertanyaan keuangan Islam: saring saham atau ETF apa pun di **5 metodologi** (AAOIFI, DJIM, FTSE, MSCI, S&P), audit portofolio, hitung **zakat** dan **pemurnian dividen**, serta tarik data pasar langsung, berita, dan pengajuan SEC. Berfungsi di dalam **Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose**, dan klien MCP lainnya.

> *"Apakah AAPL halal?"* · *"Audit portofolio saya: AAPL 30%, MSFT 20%, JNJ 50%"* · *"Hitung zakat atas kepemilikan saya."*

## Mulai cepat

1. **Dapatkan kunci API gratis** - pendaftaran hanya email di [api.halalterminal.com](https://api.halalterminal.com). Tanpa kartu kredit. Kunci tiba di kotak masuk Anda dalam hitungan detik.
2. **Hubungkan klien Anda** - satu baris perintah di bawah (atau lihat [CONNECT.md](CONNECT.md) untuk Cursor, Windsurf, Cline, dan lainnya).
3. **Ajukan pertanyaan pertama Anda** - `"Apakah AAPL halal?"` → agen memanggil `screen_stock` dan mengembalikan putusan di semua 5 metodologi.

## Instal

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

### Cursor / Windsurf / SSE langsung

```
https://mcp.halalterminal.com/sse?api_key=ht_yourkey
```

Panduan pengaturan lengkap untuk semua klien: [CONNECT.md](CONNECT.md).

## Yang Anda dapatkan - 22 alat di 8 kategori

| Kategori | Alat |
|---|---|
| **Penyaringan** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **Data pasar** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **Analisis ETF** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **Portofolio & daftar pantau** | `scan_portfolio`, `manage_watchlist` |
| **Perbandingan** | `compare_stocks` |
| **Pendapatan & zakat** | `get_dividends`, `calculate_zakat` |
| **Berita & pengajuan** | `get_news`, `get_sec_filings` |
| **Laporan & edukasi** | `generate_report`, `islamic_finance_education` |

Referensi input/output lengkap ada di [TOOLS.md](TOOLS.md). Panduan prompt end-to-end ada di [EXAMPLES.md](EXAMPLES.md).

## Mengapa Halal Terminal

- **5 metodologi, satu alat.** AAOIFI, DJIM, FTSE Shariah, MSCI Islamic, dan S&P Shariah - masing-masing dengan aturan aktivitas bisnis dan ambang rasio keuangan yang berbeda - ditampilkan berdampingan per saham sehingga pengguna dapat memilih standar yang mereka ikuti.
- **Penyaringan ETF tingkat holding.** Setiap konstituen disaring, dibobot, dan diagregasikan menjadi putusan keseluruhan ditambah tingkat pemurnian per dolar. Mencakup SPY, QQQ, VTI, ISDU, SPUS, HLAL, dan 8,000+ ETF.
- **Zakat & pemurnian, dihitung.** Zakat 2.5% terhadap ambang nisab yang aktif; perhitungan pendapatan tidak murni per-dividen berdasarkan rasio pendapatan tidak patuh penerbit.
- **Penyaringan indeks massal.** Proses pemicu-dan-polling pada S&P 500, NASDAQ-100, FTSE 100, dan lainnya; saring berdasarkan metodologi, sektor, atau hanya yang patuh.
- **Tingkat gratis, tanpa kartu kredit.** Pendaftaran email → kunci di kotak masuk Anda dalam hitungan detik → ~5-10 penyaringan penuh per bulan tanpa biaya.

## Endpoint & transportasi

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

Transport yang didukung: **SSE** (disarankan), **stdio** (melalui bridge `@halalterminal/mcp` ini untuk klien yang membutuhkannya).

## Paket & kuota

API Halal Terminal menggunakan **pengukuran token**, bukan pengukuran permintaan.

| Paket | Token per bulan | Harga | Catatan |
|---|---|---|---|
| **Free** | 50 | $0 | ~5-10 penyaringan penuh · pendaftaran email, tanpa kartu kredit |
| **Starter** | 2,500 | $19 | Investor individu |
| **Pro** | 15,000 | $49 | Webhook, prioritas massal |
| **Enterprise** | Unlimited | $199+ | Metodologi kustom, SLA |

Daftar: [api.halalterminal.com](https://api.halalterminal.com) · Harga: [halalterminal.com/pricing](https://halalterminal.com/pricing)

## Apa yang BUKAN server MCP ini

- **Bukan fatwa.** Setiap putusan adalah penyaringan berbasis metodologi. Konsultasikan dengan ulama yang berkualifikasi untuk putusan pribadi.
- **Bukan platform perdagangan.** Tidak ada integrasi broker, tidak ada eksekusi order.
- **Bukan sistem peringkat waktu nyata.** Hanya permintaan-respons pada v1; peringatan berbasis webhook ada di peta jalan Pro+.
- **Hanya bahasa Inggris di v1.** Render Arab + Perancis ada di peta jalan.

## Pertanyaan yang sering diajukan

### Apakah server MCP ini gratis digunakan?

Ya. Paket `@halalterminal/mcp` bersifat Apache-2.0 dan gratis. API Halal Terminal memiliki tingkat gratis (500 token / bulan, tanpa kartu kredit) yang mencakup ~100 penyaringan saham penuh - cukup untuk mengevaluasinya sebelum meningkatkan paket.

### Dengan klien AI mana saja ini berfungsi?

Klien apa pun yang mendukung Model Context Protocol melalui **SSE** atau **stdio** - Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose, dan lainnya. SSE disarankan; paket `@halalterminal/mcp` membungkusnya sebagai stdio untuk klien yang belum mendukung SSE.

### Bagaimana "halal" ditentukan?

Setiap putusan menerapkan aturan yang dipublikasikan dari metodologi yang dipilih - **AAOIFI**, **Dow Jones Islamic Market (DJIM)**, **FTSE Shariah**, **MSCI Islamic**, dan **S&P Shariah**. Dua lapisan: (1) penyaringan **aktivitas-bisnis** (tanpa alkohol, perjudian, keuangan konvensional, konten dewasa, senjata, babi, …), lalu (2) ambang batas **rasio-keuangan** (misalnya utang berbunga terhadap kapitalisasi pasar, aset tidak likuid, bagian pendapatan bunga). MCP mengekspos kelima putusan sehingga pengguna - atau ulama - dapat memilih standar yang mereka ikuti.

### Apa itu pemurnian dividen?

Ketika Anda memegang saham dengan bagian kecil pendapatan tidak patuh, para ulama mengharuskan mendonasikan fraksi tidak patuh dari dividen apa pun yang diterima. `calculate_zakat(calculation_type="purification", …)` dan `get_dividends(include_purification=True)` menghitung jumlah itu secara otomatis.

### Bisakah ini menyaring ETF?

Ya - `screen_etf` menelusuri setiap holding dasar, menerapkan metodologi pada masing-masing, dan mengembalikan putusan keseluruhan, persentase patuh, dan tingkat pemurnian agregat. Sukuk ETFs ditangani secara terpisah (metodologi berbasis aset).

### Bisakah saya menyaring seluruh indeks sekaligus?

Ya - `bulk_screen` memicu proses asinkron pada indeks seperti S&P 500, NASDAQ-100, FTSE 100, dan memungkinkan Anda memeriksa status, menyaring hasil berdasarkan metodologi / sektor / hanya yang patuh, serta membandingkan dua proses.

### Apakah ini mendukung webhook untuk perubahan kepatuhan?

Webhook adalah fitur paket Pro di peta jalan API; v1 dari MCP ini hanya permintaan-respons.

### Di mana saya melaporkan bug atau meminta alat?

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) atau email yassir@halalterminal.com.

## Pelajari lebih lanjut

- [Referensi API](https://api.halalterminal.com/api-reference)
- [Membangun server MCP keuangan Islam](https://www.halalterminal.com/blog/posts/islamic-finance-mcp-server)
- [Apa itu keuangan Islam?](https://www.halalterminal.com/research/what-is-islamic-finance)
- [Panduan penyaringan Sukuk](https://www.halalterminal.com/research/sukuk-screening)
- [Apakah saham saya halal? Screener](https://www.halalterminal.com/stocks)

## Bagian dari ekosistem Halal Terminal

[Situs web](https://www.halalterminal.com) · [API](https://api.halalterminal.com/api-reference) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [Plugin Claude](https://github.com/goww7/halalterminal-claude-skills) · [Bot Discord](https://github.com/goww7/halal-discord-bot) · [Indikator TradingView](https://github.com/goww7/halal-pine) · [Pelacak portofolio](https://github.com/goww7/halal-portfolio-tracker)

## Proyek terkait (OSS serupa)

Alat sumber terbuka yang membagikan API Halal Terminal yang sama - antarmuka berbeda, data sama:

| Proyek | Apa ini | Lisensi |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Plugin Claude Code - keterampilan pilihan, perintah slash, dan subagen pembuat portofolio di atas server MCP ini. | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | Agen ReAct sumber terbuka untuk riset keuangan halal - CLI + antarmuka web; mendukung OpenAI / Anthropic / LLM lokal. | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Bot Discord - perintah slash `/halal AAPL`, `/portfolio`, `/trending`. | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | Aplikasi Next.js 14 - masukkan holding, dapatkan kepatuhan per saham + % halal portofolio + pemurnian yang terutang. Deploy Vercel satu klik. | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | Indikator TradingView Pine Script v5 yang menumpangkan status kepatuhan pada grafik. Diperbarui harian dari API ini. | MIT |

## Lisensi & merek dagang

Apache-2.0 - lihat [LICENSE](LICENSE).

"Halal Terminal", "HalalTerminal", dan logo Halal Terminal adalah merek dagang yang dilindungi - lihat [TRADEMARKS.md](TRADEMARKS.md).

## Hukum

- [Hukum & Penyangkalan](https://halalterminal.com/legal) - bingkai edukasi-riset, penyangkalan investasi, pemberitahuan kepatuhan syariah, batas tanggung jawab, pemberitahuan yurisdiksi
- [Kebijakan Privasi](https://halalterminal.com/privacy)
- [Kebijakan Cookie](https://halalterminal.com/cookies)

## Dukungan

- Kontak: yassir@halalterminal.com
- Dasbor: [api.halalterminal.com/dashboard](https://api.halalterminal.com/dashboard)
- Dokumen API: [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Ditenagai oleh Halal Terminal - [halalterminal.com](https://halalterminal.com)

---

Bagian dari [ekosistem terbuka Halal Terminal](https://github.com/goww7/awesome-islamic-finance):
[API](https://api.halalterminal.com) · [MCP server](https://github.com/goww7/halalterminal-mcp) · [Python SDK](https://github.com/goww7/halalterminal-sdk-python) · [JS SDK](https://github.com/goww7/halalterminal-sdk-js) · [Dataset](https://github.com/goww7/sp500-shariah-compliance) · [Awesome Islamic Finance](https://github.com/goww7/awesome-islamic-finance)