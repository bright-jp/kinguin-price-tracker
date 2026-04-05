# Kinguin Price Tracker

[![Bright Data](https://img.shields.io/badge/Powered%20by-Bright%20Data-blue?style=flat-square)](https://brightdata.jp)
[![Kinguin Price Tracker](https://img.shields.io/badge/Kinguin%20Price%20Tracker-Managed%20Solution-orange?style=flat-square)](https://brightdata.jp/products/insights/price-tracker/kinguin)
[![Python](https://img.shields.io/badge/Python-3.9%2B-yellow?style=flat-square)](https://python.org)

[![Bright Insights Price Tracker](https://raw.githubusercontent.com/danielshashko/bright-insights-assets/main/price-tracker-hero-v2.png)](https://brightdata.jp/products/insights/price-tracker/kinguin)

Kinguin のリアルタイム価格追跡 — デジタルゲームおよびソフトウェアキーのオンラインマーケットプレイス。開始方法は 2 つあります。**フルマネージド**のインテリジェンスプラットフォーム、または Bright Data の AI Scraper Builder で構築する**カスタム scraper**です。

---

## Option 1: Bright Insights - AI 搭載価格追跡（推奨）

**[Bright Insights](https://brightdata.jp/products/insights/price-tracker/kinguin)** は、Bright Data のフルマネージドなリテールインテリジェンスプラットフォームです。scraper の構築も、インフラの保守も不要で、分析可能な構造化価格データをダッシュボード、data feed、または BI ツールにそのまま配信できます。

**Bright Insights がチームに選ばれる理由:**
- 🚀 **セットアップ不要** - すぐに使えるダッシュボードと data feed で数分以内に利用開始
- 🤖 **AI 搭載の推奨機能** - 対話型 AI アシスタントが数百万件のデータポイントを即座に実用的なインサイトへ変換
- ⚡ **リアルタイム監視** - 1 時間ごとから日次までの更新頻度と即時アラート（email、Slack、webhook）
- 🌍 **無制限のスケール** - あらゆる Web サイト、あらゆる地域、あらゆる更新頻度に対応
- 🔗 **プラグアンドプレイ統合** - AWS、GCP、Databricks、Snowflake などに対応
- 🛡️ **フルマネージド** - Bright Data が schema 変更、サイト更新、データ品質を自動で処理

**主なユースケース:**
- ✅ Kinguin の**デジタルゲーム価格の変動**やセールを追跡
- ✅ **期間限定ディール**やフラッシュセールを監視
- ✅ **地域ごとの価格差を自動検出**
- ✅ MAP ポリシー準拠を監視し、価格違反を検出
- ✅ 競合のプロモーションと販促動向を追跡
- ✅ クリーンで正規化されたデータを動的価格設定アルゴリズムや AI モデルに直接投入

> **月額 $250 から - [お客様向け見積もりを取得 →](https://brightdata.jp/products/insights/price-tracker/kinguin)**

---

## Option 2: 独自の Kinguin scraper を構築

事前構築済みの Kinguin scraper API がない？問題ありません。Bright Data の **AI Scraper Builder** なら、数クリックでカスタム Kinguin scraper を生成できます。コーディングは不要です。

### 数分で Kinguin scraper を構築

**[Kinguin AI Scraper Builder を開く →](https://brightdata.jp/products/web-scraper/kinguin)**

ドメインを選択し、必要なデータ要件を指定するだけで、AI scraper builder が自動的に API を作成します。

1. **必要なデータを平易な英語で記述**
2. **AI が scraper API を即座に生成**
3. **API リクエストを実行してすぐに結果を取得**
4. **必要に応じて組み込み IDE でコードを編集**

構築が完了すると、scraper には **Web Scraper ID**（`gd_xxxxxxxxxxxx`）が付与されます。以下の Setup 手順で使用するため、コピーしておいてください。

### 前提条件

- Python 3.9 以上
- [Bright Data account](https://brightdata.jp)（無料トライアルあり）
- Bright Data の **API token**（[取得方法](https://docs.brightdata.jp/general/account/account-settings#api-token)）
- Kinguin 用の **Web Scraper ID**（上記の構築手順で取得）

### Setup

1. **この repository を clone**

   ```bash
   git clone https://github.com/bright-jp/kinguin-price-tracker.git
   cd kinguin-price-tracker
   ```

2. **依存関係をインストール**

   ```bash
   pip install -r requirements.txt
   ```

3. **認証情報を設定**

   `.env.example` を `.env` にコピーし、値を入力します:

   ```bash
   cp .env.example .env
   ```

   ```env
   BRIGHTDATA_API_TOKEN=your_api_token_here
   BRIGHTDATA_DATASET_ID=your_dataset_id_here
   ```

   > **Your Web Scraper ID**
   > [AI Scraper Builder dashboard](https://brightdata.jp/products/web-scraper/kinguin) から取得した Web Scraper ID を
   > `BRIGHTDATA_DATASET_ID` に貼り付けてください（形式: `gd_xxxxxxxxxxxx`）。

---

## Usage

Kinguin scraper の構築が完了し、Web Scraper ID を `.env` に設定すると、Python interface は同じ方法で利用できます。

### 1. URL で特定の商品を追跡

Kinguin の商品 URL のリストを渡して、構造化された価格データを取得します:

```python
from price_tracker import track_prices

urls = [
    "https://www.kinguin.net/product/sample-item-123456",
    # Add more product URLs here
]

results = track_prices(urls)
for item in results:
    print(f"{item.get('title')} - {item.get('final_price', item.get('price'))} {item.get('currency', '')}")
```

または直接実行:

```bash
python price_tracker.py
```

### 2. キーワードで商品を検索

キーワード検索に一致する商品を見つけます:

```python
from price_tracker import discover_by_keyword

results = discover_by_keyword("laptop", limit=50)
```

### 3. カテゴリ URL で商品を閲覧

Kinguin のカテゴリページからすべての商品を収集します:

```python
from price_tracker import discover_by_category

results = discover_by_category(
    "https://kinguin.net/category/example",
    limit=100,
)
```

---

## 出力フィールド

各結果レコードには次のフィールドが含まれます:

| Field | Description |
|-------|-------------|
| `url` | 商品 / リスティング URL |
| `title` | ゲーム / 商品タイトル |
| `initial_price` | 元の価格 |
| `final_price` | 現在の価格 |
| `currency` | 通貨コード |
| `discount` | 割引 |
| `platform` | ゲームプラットフォーム |
| `release_date` | 発売日 |
| `rating` | ユーザー評価 |
| `in_stock` | 在庫状況 |
| `images` | カバー画像 |
| `description` | 商品説明 |
| `timestamp` | 収集タイムスタンプ |

### 出力例

```json
[
  {
    "url": "https://www.kinguin.net/product/sample-item-123456",
    "title": "Example Product Name",
    "brand": "Example Brand",
    "initial_price": 59.99,
    "final_price": 44.99,
    "currency": "USD",
    "discount": "25%",
    "in_stock": true,
    "rating": 4.5,
    "reviews_count": 1234,
    "images": ["https://kinguin.net/images/product1.jpg"],
    "description": "Product description text...",
    "timestamp": "2025-01-15T10:30:00Z"
  }
]
```

---

## 高度なオプション

`trigger_collection()` 関数は、データ収集を制御するためのオプションパラメータを受け付けます:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | integer | - | 返されるレコードの最大数 |
| `include_errors` | boolean | `true` | 結果に error report を含める |
| `notify` | string (URL) | - | snapshot の準備完了時に呼び出す webhook URL |
| `format` | string | `json` | 出力形式: `json`、`csv`、または `ndjson` |

オプション付きの例:

```python
from price_tracker import trigger_collection, get_results

inputs = [{"url": "https://www.kinguin.net/product/sample-item-123456"}]
snapshot_id = trigger_collection(inputs, limit=200, notify="https://your-webhook.com/hook")
results = get_results(snapshot_id)
```

---

## リソース

- 🌟 [Kinguin Price Tracker - Bright Insights (Managed)](https://brightdata.jp/products/insights/price-tracker/kinguin)
- 🏗️ [Build a Kinguin Scraper](https://brightdata.jp/products/web-scraper/kinguin)
- 📖 [Bright Data Web Scraper API Documentation](https://docs.brightdata.jp/scraping-automation/web-scraper-api/overview)
- 🗄️ [Web Scrapers Control Panel](https://brightdata.jp/cp/scrapers)
- 🔑 [How to get an API token](https://docs.brightdata.jp/general/account/account-settings#api-token)
- 🌐 [Bright Data Homepage](https://brightdata.jp)

---

*[Bright Data](https://brightdata.jp) により構築 — 業界をリードする Web データプラットフォーム。*