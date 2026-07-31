# Halal Terminal MCP - Filtrage conforme a la charia des actions et ETF pour agents IA

![AAPL halal status](https://api.halalterminal.com/api/badge/AAPL.svg) _badge en direct de l'API, integrez-en un pour n'importe quel symbole_

[![npm version](https://img.shields.io/npm/v/@halalterminal/mcp.svg)](https://www.npmjs.com/package/@halalterminal/mcp)
[![Apache 2.0](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)
[![MCP](https://img.shields.io/badge/protocol-MCP-purple)](https://modelcontextprotocol.io)
[![Powered by Halal Terminal](https://img.shields.io/badge/powered%20by-Halal%20Terminal-1f6feb)](https://halalterminal.com)

Le serveur **Model Context Protocol** officiel pour [Halal Terminal](https://halalterminal.com). Offrez a votre agent IA **22 outils** pour repondre aux questions de finance islamique : filtrez n'importe quelle action ou ETF selon **5 methodologies** (AAOIFI, DJIM, FTSE, MSCI, S&P), auditez des portefeuilles, calculez la **zakat** et la **purification des dividendes**, et recuperez les donnees de marche en direct, les actualites et les depots SEC. Fonctionne dans **Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose**, et tout autre client MCP.

> *"AAPL est-elle halal ?"* · *"Auditez mon portefeuille : AAPL 30 %, MSFT 20 %, JNJ 50 %"* · *"Calculez la zakat sur mes avoirs."*

## Demarrage rapide

1. **Obtenez une cle API gratuite** - inscription par e-mail uniquement sur [api.halalterminal.com](https://api.halalterminal.com). Pas de carte de credit. La cle arrive dans votre boite de reception en quelques secondes.
2. **Connectez votre client** - commandes en une ligne ci-dessous (ou consultez [CONNECT.md](CONNECT.md) pour Cursor, Windsurf, Cline, et autres).
3. **Posez votre premiere question** - `"Is AAPL halal?"` → l'agent appelle `screen_stock` et retourne les verdicts pour les 5 methodologies.

## Installation

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

### Cursor / Windsurf / SSE direct

```
https://mcp.halalterminal.com/sse?api_key=ht_yourkey
```

Guide d'installation complet pour tous les clients : [CONNECT.md](CONNECT.md).

## Ce que vous obtenez - 22 outils repartis en 8 categories

| Categorie | Outils |
|---|---|
| **Filtrage** | `screen_stock`, `screen_etf`, `bulk_screen`, `get_screening_result`, `get_all_screening_results` |
| **Donnees de marche** | `get_quote`, `get_stock_info`, `get_price_history`, `get_trending_stocks`, `search_stocks` |
| **Analyse d'ETF** | `get_etf_info`, `etf_purification`, `compare_etfs` |
| **Portefeuille et liste de surveillance** | `scan_portfolio`, `manage_watchlist` |
| **Comparaison** | `compare_stocks` |
| **Revenus et zakat** | `get_dividends`, `calculate_zakat` |
| **Actualites et depots** | `get_news`, `get_sec_filings` |
| **Rapports et education** | `generate_report`, `islamic_finance_education` |

Reference complete des entrees/sorties dans [TOOLS.md](TOOLS.md). Guides de prompts de bout en bout dans [EXAMPLES.md](EXAMPLES.md).

## Pourquoi Halal Terminal

- **5 methodologies, un seul outil.** AAOIFI, DJIM, FTSE Shariah, MSCI Islamic, et S&P Shariah - chacune avec des regles d'activite commerciale distinctes et des seuils de ratios financiers - presentees cote a cote pour chaque action afin que les utilisateurs choisissent la norme qu'ils suivent.
- **Filtrage d'ETF au niveau des constituants.** Chaque constituant est filtre, ponderé et agrege en un verdict global plus un taux de purification par dollar. Couvre SPY, QQQ, VTI, ISDU, SPUS, HLAL, et plus de 8 000 ETF.
- **Zakat et purification, calculees.** Zakat a 2,5 % selon un seuil de nisab en temps reel ; calcul du revenu impur par dividende base sur le ratio de revenu non conforme de l'emetteur.
- **Filtrage en masse d'indices.** Executions par declenchement et interrogation sur le S&P 500, le NASDAQ-100, le FTSE 100, et autres ; filtrez par methodologie, secteur, ou conformite uniquement.
- **Niveau gratuit, pas de carte de credit.** Inscription par e-mail → cle dans votre boite de reception en quelques secondes → environ 5 a 10 filtrages complets par mois sans frais.

## Point de terminaison et transport

```
SSE: https://mcp.halalterminal.com/sse
Auth: X-API-Key: <your_key>   (or ?api_key=<your_key>)
```

Transports pris en charge : **SSE** (recommande), **stdio** (via ce pont `@halalterminal/mcp` pour les clients qui en ont besoin).

## Forfaits et quotas

L'API Halal Terminal est mesuree en **jetons**, pas en requetes.

| Forfait | Jetons mensuels | Prix | Notes |
|---|---|---|---|
| **Gratuit** | 50 | $0 | environ 5 a 10 filtrages complets · inscription par e-mail, pas de carte de credit |
| **Starter** | 2,500 | $19 | Investisseurs individuels |
| **Pro** | 15,000 | $49 | Webhooks, priorite en masse |
| **Enterprise** | Unlimited | $199+ | Methodologies personnalisees, SLA |

Inscription : [api.halalterminal.com](https://api.halalterminal.com) · Tarification : [halalterminal.com/pricing](https://halalterminal.com/pricing)

## Ce que ce serveur MCP N'EST PAS

- **Pas une fatwa.** Chaque verdict est un filtrage base sur une methodologie. Consultez un savant qualifie pour des avis personnels.
- **Pas une plateforme de trading.** Aucune integration de courtier, aucune execution d'ordres.
- **Pas un systeme d'alertes en temps reel.** Requete-reponse uniquement en v1 ; les alertes pilotees par webhooks sont sur la feuille de route Pro+.
- **Anglais uniquement en v1.** Le rendu en arabe et en francais est sur la feuille de route.

## FAQ

### Ce serveur MCP est-il gratuit ?

Oui. Le package `@halalterminal/mcp` est sous licence Apache-2.0 et gratuit. L'API Halal Terminal propose un niveau gratuit (500 jetons / mois, pas de carte de credit) qui couvre environ 100 filtrages complets d'actions - suffisant pour l'evaluer avant de passer a un forfait superieur.

### Avec quels clients IA fonctionne-t-il ?

Tout client prenant en charge le Model Context Protocol via **SSE** ou **stdio** - Claude Desktop, Claude Code, Cursor, Windsurf, Cline, Continue, Zed, Goose, et bien d'autres. SSE est recommande ; le package `@halalterminal/mcp` l'encapsule en stdio pour les clients qui ne prennent pas encore en charge SSE.

### Comment la conformite "halal" est-elle determinee ?

Chaque verdict applique les regles publiees de la methodologie choisie - **AAOIFI**, **Dow Jones Islamic Market (DJIM)**, **FTSE Shariah**, **MSCI Islamic**, et **S&P Shariah**. Deux couches : (1) un filtre d'**activite commerciale** (pas d'alcool, de jeux d'argent, de finance conventionnelle, de contenu adulte, d'armes, de porc, …), puis (2) des seuils de **ratios financiers** (par exemple, dette portant interet par rapport a la capitalisation boursiere, actifs illiquides, part de revenus d'interets). Le MCP expose les cinq verdicts afin que l'utilisateur - ou le savant - puisse choisir la norme qu'il suit.

### Qu'est-ce que la purification des dividendes ?

Lorsque vous detenez une action avec une petite part de revenu non conforme, les savants exigent de donner la fraction non conforme de tout dividende percu. `calculate_zakat(calculation_type="purification", …)` et `get_dividends(include_purification=True)` calculent ce montant automatiquement.

### Peut-il filtrer les ETF ?

Oui - `screen_etf` parcourt chaque titre sous-jacent, applique la methodologie a chacun, et retourne un verdict global, un pourcentage de conformite, et un taux de purification agregue. Les ETF de sukuk sont traites separement (methodologies basees sur les actifs).

### Puis-je filtrer un indice entier en une seule fois ?

Oui - `bulk_screen` declenche une execution asynchrone sur des indices comme le S&P 500, le NASDAQ-100, le FTSE 100, et vous permet d'interroger le statut, de filtrer les resultats par methodologie / secteur / conformite uniquement, et de comparer deux executions.

### Prend-il en charge les webhooks pour les changements de conformite ?

Les webhooks sont une fonctionnalite du forfait Pro sur la feuille de route de l'API ; la v1 de ce MCP est en requete-reponse uniquement.

### Ou signaler des bugs ou demander des outils ?

[github.com/goww7/halalterminal-mcp/issues](https://github.com/goww7/halalterminal-mcp/issues) ou par e-mail yassir@halalterminal.com.

## En savoir plus

- [Reference API](https://api.halalterminal.com/api-reference)
- [Construire un serveur MCP de finance islamique](https://www.halalterminal.com/blog/posts/islamic-finance-mcp-server)
- [Qu'est-ce que la finance islamique ?](https://www.halalterminal.com/research/what-is-islamic-finance)
- [Guide de filtrage des sukuk](https://www.halalterminal.com/research/sukuk-screening)
- [Mon action est-elle halal ? Screener](https://www.halalterminal.com/stocks)

## Fait partie de l'ecosysteme Halal Terminal

[Site web](https://www.halalterminal.com) · [API](https://api.halalterminal.com/api-reference) · [SDK Python](https://github.com/goww7/halalterminal-sdk-python) · [SDK JS](https://github.com/goww7/halalterminal-sdk-js) · [Plugin Claude](https://github.com/goww7/halalterminal-claude-skills) · [Bot Discord](https://github.com/goww7/halal-discord-bot) · [Indicateur TradingView](https://github.com/goww7/halal-pine) · [Suivi de portefeuille](https://github.com/goww7/halal-portfolio-tracker)

## Projets connexes (OSS apparentes)

Des outils open source qui partagent la meme API Halal Terminal - interfaces differentes, memes donnees :

| Projet | Description | Licence |
|---|---|---|
| [**halalterminal-claude-skills**](https://github.com/goww7/halalterminal-claude-skills) | Plugin Claude Code - competences organisees, commandes slash, et un sous-agent de construction de portefeuille base sur ce serveur MCP. | Apache-2.0 |
| [**yassir-oss**](https://github.com/goww7/yassir-oss) | Agent ReAct open source pour la recherche en finance halal - CLI + interface web ; prend en charge OpenAI / Anthropic / LLM locaux. | Apache-2.0 |
| [**halal-discord-bot**](https://github.com/goww7/halal-discord-bot) | Bot Discord - `/halal AAPL`, `/portfolio`, `/trending` commandes slash. | MIT |
| [**halal-portfolio-tracker**](https://github.com/goww7/halal-portfolio-tracker) | Application Next.js 14 - saisissez vos avoirs, obtenez la conformite par action + pourcentage halal du portefeuille + purification due. Deploiement Vercel en un clic. | MIT |
| [**halal-pine**](https://github.com/goww7/halal-pine) | Indicateur TradingView Pine Script v5 qui superpose le statut de conformite sur les graphiques. Actualise quotidiennement depuis cette API. | MIT |

## Licence et marques deposees

Apache-2.0 - voir [LICENSE](LICENSE).

« Halal Terminal », « HalalTerminal », et le logo Halal Terminal sont des marques deposees reservees - voir [TRADEMARKS.md](TRADEMARKS.md).

## Mentions legales

- [Mentions legales et clause de non-responsabilite](https://halalterminal.com/legal) - cadre educatif et de recherche, clause de non-responsabilite en matiere d'investissement, avis de conformite a la charia, limites de responsabilite, mentions de juridiction
- [Politique de confidentialite](https://halalterminal.com/privacy)
- [Politique de cookies](https://halalterminal.com/cookies)

## Assistance

- Contact : yassir@halalterminal.com
- Tableau de bord : [api.halalterminal.com/dashboard](https://api.halalterminal.com/dashboard)
- Documentation API : [api.halalterminal.com/docs](https://api.halalterminal.com/docs) (Swagger) · [api.halalterminal.com/redoc](https://api.halalterminal.com/redoc) (ReDoc)

---

Propulse par Halal Terminal - [halalterminal.com](https://halalterminal.com)

---

Fait partie de l'[ecosysteme ouvert Halal Terminal](https://github.com/goww7/awesome-islamic-finance) :
[API](https://api.halalterminal.com) · [Serveur MCP](https://github.com/goww7/halalterminal-mcp) · [SDK Python](https://github.com/goww7/halalterminal-sdk-python) · [SDK JS](https://github.com/goww7/halalterminal-sdk-js) · [Jeux de donnees](https://github.com/goww7/sp500-shariah-compliance) · [Awesome Islamic Finance](https://github.com/goww7/awesome-islamic-finance)