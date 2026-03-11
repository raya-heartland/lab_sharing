# 研究室共有文献サーバー

このリポジトリは、研究室の文献（PDF・書誌情報）を共有するための仕組みです。  
はじめて使う方は、以下の手順を順番に進めてください。

---

## 🗺️ 全体の流れ

```
① Tailscale（VPN）に参加
        ↓
② 文献検索 Web UI を使う（おすすめ）
        ↓
③ Paperless（文献サーバー）にアクセス
        ↓
④ Obsidian で文献リストを閲覧（オプション）
```

---

## ① Tailscale への参加（VPN）

Paperless サーバーはインターネットに直接公開されていません。  
**Tailscale** という VPN アプリを使って、研究室のプライベートネットワークに入る必要があります。

### 手順

1. **荒谷から招待メールが届いたことを確認する**

2. **Tailscale アプリをインストールする**
   - Mac: [https://tailscale.com/download/macos](https://tailscale.com/download/macos)
   - Windows: [https://tailscale.com/download/windows](https://tailscale.com/download/windows)
   - iPhone/iPad: App Store で「Tailscale」を検索
   - Android: Google Play で「Tailscale」を検索

3. **アプリを開いて「Sign in with Google」などでサインイン → 荒谷先生から届いた招待メールのリンクをクリックして承認する**

4. **接続できたら完了。** アプリのアイコンが緑になれば OK です。

> ⚠️ Tailscale を起動していないとサーバーにアクセスできません。  
> 使うときは必ずアプリを起動してください。

---

## ② 文献検索 Web UI の使い方

研究室の文献データベースをブラウザから**キーワードで意味検索**できる Web サービスです。  
Paperless への登録が必要なく、Tailscale に接続するだけですぐ使えます。

### アクセス方法

Tailscale に接続した状態で、ブラウザで以下の URL を開いてください：

```
http://100.65.111.66:8100
```

### 使い方

1. **検索ボックスにキーワードを入力して「検索」ボタンを押す**  
   日本語・英語どちらでも検索できます。  
   例：`カントの定言命法`　`Levinas hospitality`　`オッカム 神の意志`

2. **オプションで絞り込む**  
   - **件数**：5 / 10 / 20 件から選択  
   - **言語**：すべて・日本語のみ（ja）・英語のみ（en）  
   - **重要度重み付け**：一次文献を優先して表示（デフォルト ON）

3. **結果を確認する**  
   各カードには以下の情報が表示されます：
   - スコア（類似度）、重要度（p=）、言語  
   - 文献 ID（例：`#695`）→ Paperless の該当ページへのリンク  
   - テキスト本文（「▼ 全文を表示」で展開可）

4. **結果をファイルとして保存する**  
   検索後に以下の 2 種類のリンクが表示されます：
   - **📥 MD ダウンロード** — 即座にマークダウンファイルをダウンロード  
   - **📥 ページ番号付き** — PDF から実際のページ番号を検索してから生成（数十秒かかることがあります）

### この検索の特徴

この検索は**意味検索（セマンティック検索）**です。キーワードが完全に一致しなくても、意味的に近い文献を見つけられます。

| 通常の全文検索（Paperless） | 意味検索（この Web UI） |
|---|---|
| キーワードが含まれている文献を探す | 意味・概念が近い文献を探す |
| 「定言命法」で検索 → その単語を含む箇所 | 「道徳の根拠」で検索 → 関連する概念も含む箇所 |
| 速い | やや遅い（数秒） |

> ⚠️ 検索は 1 日 200 回まで（IP アドレスごと）の制限があります。

---

## ③ Paperless（文献サーバー）の使い方

Paperless は、研究室で使っている文献管理サーバーです。  
PDF を一元管理して、OCR（文字認識）や検索ができるようになっています。

### アクセス方法

Tailscale に接続した状態で、ブラウザで以下の URL を開いてください：

```
http://100.121.108.24:8000
```

ユーザー名とパスワードは、荒谷から個別にお伝えします。

### できること・できないこと

| 操作 | 可否 |
|---|---|
| 文献（PDF）のアップロード | ✅ できます |
| 文献の閲覧・ダウンロード | ✅ できます |
| 全文検索 | ✅ できます |
| タグの編集・削除 | ❌ できません |
| 他の人がアップした文献の削除 | ❌ できません |

### 文献をアップロードするときのルール

1. **著作権に注意してください。** 自分で購入・入手した PDF のみアップしてください。
2. **重複チェック。** アップ前に検索して、すでに同じ文献が入っていないか確認してください。
3. **OCRは高品質のものを。** OCRはできるだけ高品質に保ってください。欧文・原典が存在するものは原典を優先します
4. **個人情報は入れないでください。** 氏名・住所・成績等が含まれるファイルはアップしないこと。

### 📖 日本語文献の高品質 OCR について

スキャンした日本語 PDF をアップロードする場合、**Paperless 内蔵の OCR よりも精度が高い**方法として、国立国会図書館が開発した **NDLOCR-Lite** を推奨します。

**特徴：**
- GPU 不要、一般的なノートパソコン（Windows / Mac / Linux）で動作
- 図書・雑誌などの縦組み日本語に対応
- 国立国会図書館が無償公開（CC BY 4.0）

**使い方（かんたんな場合：デスクトップアプリ）：**

1. [リリースページ](https://github.com/ndl-lab/ndlocr-lite/releases) から自分の OS に合ったファイルをダウンロード
2. アプリを起動して、PDF またはスキャン画像を読み込む
3. OCR 処理後にテキストが付与された PDF を書き出す
4. その PDF を Paperless にアップロードする

> ⚠️ アプリは日本語（全角文字）を含まないフォルダに置いてください。起動しないことがあります。

**コマンドラインから使う場合（Python 3.10 以上が必要）：**
```bash
git clone https://github.com/ndl-lab/ndlocr-lite
cd ndlocr-lite
pip install -r requirements.txt
cd src
python3 ocr.py --sourceimg 画像ファイル.jpg --output 出力フォルダ
```

詳細は[公式の使い方ガイド](https://lab.ndl.go.jp/data_set/ndlocrlite-usage/)を参照してください。

---

## ④ Obsidian で文献リストを閲覧する（オプション）

このリポジトリの `bib/` フォルダには、Paperless 上の各文献に対応する書誌ノートが入っています。  
**Obsidian**（ノートアプリ）を使うと、これらをリンクつきで快適に閲覧できます。

### Obsidian のインストール

[https://obsidian.md](https://obsidian.md) からダウンロードして、インストールしてください（無料）。

### このリポジトリを Obsidian で開く

このリポジトリは**非公開（プライベート）**です。アクセスするには以下の準備が必要です。

**事前準備：**
1. [GitHub アカウントを作成する](https://github.com/signup)（無料）
2. アカウントのユーザー名を荒谷に伝える → 閲覧権限を付与してもらう

**手順：**

1. **このリポジトリをクローン（ダウンロード）する**

   ターミナル（Mac）またはコマンドプロンプト（Windows）で：
   ```bash
   git clone https://github.com/raya-heartland/lab_sharing.git
   ```
   ※ 実行中に GitHub のユーザー名とパスワード（またはトークン）を求められます。

   **Git を使わない場合：**  
   GitHub のページ（`https://github.com/raya-heartland/lab_sharing`）を開いて、  
   「Code → Download ZIP」でダウンロードして展開してください。

2. **Obsidian を開いて「Open folder as vault」→ダウンロードしたフォルダを選択する**

3. `bib/` フォルダの中に書誌ノートが並んでいます。各ノートには文献の要約・書誌情報・Paperless サーバーへのリンクが含まれています。

> 📖 `bib/` フォルダは読み取り専用のつもりで使ってください。  
> 自分のメモは Obsidian 内の別ノートに書くことをお勧めします。
>
> 🔄 文献リストを最新の状態に更新したいときは、フォルダ内でターミナルを開いて `git pull` を実行してください。

---

## ⑤ AI エージェント・開発者向け API リファレンス（オプション）

Tailscale VPN 内からプログラムで文献を検索・取得したい場合の情報です。

---

### RAG 検索 API（`http://100.65.111.66:8100`）

#### `GET /search` — 意味検索

```
GET http://100.65.111.66:8100/search?q={クエリ}&limit={件数}&lang={言語}&weight={true/false}
```

| パラメータ | 型 | 必須 | 説明 |
|---|---|---|---|
| `q` | string | ✅ | 検索クエリ（自然言語、日英両対応） |
| `limit` | int | — | 返却件数（1〜20、デフォルト: 5） |
| `lang` | string | — | `ja` / `en` / 省略=全言語 |
| `weight` | bool | — | priority 重み付け（デフォルト: `true`） |

**レスポンス例（JSON）：**

```json
{
  "query": "カントの定言命法",
  "count": 5,
  "results": [
    {
      "score": 0.7823,
      "weighted_score": 0.7823,
      "priority": 12,
      "doc_id": 791,
      "path": "araya/Paperless_content_791.md",
      "chunk_index": 163,
      "lang": "de",
      "text": "Handle nur nach derjenigen Maxime..."
    }
  ]
}
```

#### `GET /download` — 結果をマークダウンファイルとして取得

```
GET http://100.65.111.66:8100/download?q={クエリ}&limit=5&pages=false
```

`pages=true` にすると PDF からページ番号を検索します（遅い）。  
`Content-Disposition: attachment` でマークダウンファイルが返ります。

#### `GET /health` — ヘルスチェック

```
GET http://100.65.111.66:8100/health
→ {"status": "ok", "time": "2026-03-11T20:00:00"}
```

---

### Paperless API（`http://100.121.108.24:8000`）

認証は **Token 認証**です。トークンは荒谷からお伝えします。

```
Authorization: Token <YOUR_TOKEN>
```

#### 主なエンドポイント

| 操作 | エンドポイント |
|---|---|
| 文献一覧 | `GET /api/documents/` |
| 文献の詳細・本文テキスト | `GET /api/documents/{id}/` |
| 文献 PDF のダウンロード | `GET /api/documents/{id}/download/` |
| 文献のアップロード | `POST /api/documents/post_document/` |
| タグ一覧 | `GET /api/tags/` |
| 全文検索 | `GET /api/documents/?query={キーワード}` |

**使用例（curl）：**

```bash
# 文献テキストの取得
curl -H "Authorization: Token <TOKEN>" \
     http://100.121.108.24:8000/api/documents/791/

# PDF ダウンロード
curl -H "Authorization: Token <TOKEN>" \
     http://100.121.108.24:8000/api/documents/791/download/ \
     -o output.pdf

# キーワード全文検索
curl -H "Authorization: Token <TOKEN>" \
     "http://100.121.108.24:8000/api/documents/?query=定言命法"
```

**使用例（Python）：**

```python
import requests

TOKEN = "<YOUR_TOKEN>"
BASE  = "http://100.121.108.24:8000"
headers = {"Authorization": f"Token {TOKEN}"}

# 意味検索（RAG API）
resp = requests.get("http://100.65.111.66:8100/search",
                    params={"q": "カントの自律", "limit": 5, "lang": "ja"})
results = resp.json()["results"]

# 該当 PDF を Paperless から取得
for r in results:
    if r["doc_id"]:
        pdf = requests.get(f"{BASE}/api/documents/{r['doc_id']}/download/",
                           headers=headers)
        with open(f"doc_{r['doc_id']}.pdf", "wb") as f:
            f.write(pdf.content)
```

> ⚠️ RAG 検索 API は 1 日 200 回/IP の制限があります。  
> ⚠️ Paperless API トークンは個人に紐づいています。第三者と共有しないでください。

---

## ❓ うまくいかないとき

| 症状 | 確認すること |
|---|---|
| サーバーにつながらない | Tailscale が起動しているか確認 |
| ログインできない | ユーザー名・パスワードを再確認 / 荒谷先生に連絡 |
| PDF が開かない | ブラウザを変えてみる（Chrome 推奨） |
| Obsidian でリンクが壊れている | `bib/` と `media/` が同じフォルダ内にあるか確認 |

問題が解決しない場合は、荒谷にご連絡ください。
