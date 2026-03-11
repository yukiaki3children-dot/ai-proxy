# AI思考チーム — Vercelプロキシ デプロイ手順

## フォルダ構成
```
vercel-proxy/
├── api/
│   ├── openai.js   ← OpenAI プロキシ関数
│   └── gemini.js   ← Gemini プロキシ関数
├── public/
│   └── index.html  ← フロントエンド（ここを使うか、claude.aiのHTMLにVercel URLを入力）
├── package.json
├── vercel.json
└── README.md
```

---

## デプロイ手順（5ステップ）

### Step 1: GitHubにリポジトリを作成
1. https://github.com にアクセスしてログイン
2. 「New repository」→ 名前（例: `ai-proxy`）→「Create repository」
3. このフォルダの中身をすべてアップロード（またはgit pushで）

### Step 2: Vercelにデプロイ
1. https://vercel.com にアクセスしてGitHubでログイン
2. 「New Project」→ 作成したリポジトリを選択
3. 設定はデフォルトのまま「Deploy」をクリック
4. デプロイ完了後、URLが発行される（例: `https://ai-proxy-xxx.vercel.app`）

### Step 3: 環境変数を設定（重要）
Vercelのプロジェクトページで：
1. 「Settings」→「Environment Variables」を開く
2. 以下の2つを追加する：

| Key | Value |
|-----|-------|
| `OPENAI_API_KEY` | `sk-proj-gOtHUD5...`（OpenAIのAPIキー） |
| `GEMINI_API_KEY` | `AIzaSyDDRBq...`（GeminiのAPIキー） |

3. 「Save」後、「Deployments」から「Redeploy」を実行

### Step 4: HTMLにVercel URLを入力
ダウンロードした `index.html` をブラウザで開き、
上部の設定欄に Vercel URL（例: `https://ai-proxy-xxx.vercel.app`）を入力して「保存して分析開始」をクリック。

### Step 5: 動作確認
- Phase 1: ChatGPT（gpt-4o）が調査
- Phase 2: Gemini（gemini-1.5-flash）が分析
- Phase 3: Claude + ChatGPT + Gemini が総合討議

---

## 注意事項
- Vercel URLを入力しない場合は Claude のみで動作（フォールバック）
- APIキーはVercelの環境変数に保存されるため、HTMLには記載不要で安全
- Vercelの無料プランで十分動作します
