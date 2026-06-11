# CLAUDE.md — SkyFlip ショーケースサイト

## 🏠 自宅PCで再開するときの最初の一歩（クイックスタート）
このリポジトリは会社PCで作成し、GitHubに公開済み。自宅PCで続きをやるには:

```bash
# 1. クローン（まだ無ければ）
git clone https://github.com/atdirakg9020121-afk/skyflip-site.git
cd skyflip-site

# 2. サイトを確認（ビルド不要。静的HTMLなのでブラウザで開くだけ）
start index.html        # Windows。そのまま開ける

# 3. 編集して反映する流れ
#    ファイルを編集 → git add -A → git commit -m "..." → git push
#    push すると GitHub Pages が自動で再ビルド（1〜2分で公開URLに反映）
```

- 公開URL: https://atdirakg9020121-afk.github.io/skyflip-site/
- GitHubリポジトリ: https://github.com/atdirakg9020121-afk/skyflip-site
- **ビルドツール・依存パッケージは無し**（npm install 不要）。素のHTML/CSS/SVGのみ。
- **アプリ本体のソースは別リポジトリ。** 仕様確認のため、Claudeに作業させる際はアプリ側のリポジトリも開いておくと、実装と仕様のズレ（例: 過去に「星空テーマ」が標準機能と被っていた件）を防げる。

## おすすめ作業順（自宅・詰まり最小ルート）
1. **Partner Center 登録**を真っ先に着手（本人確認の審査待ちが発生するため。`STORE_SUBMISSION_CHECKLIST.md` フェーズ0）
2. 審査を待つ間に **素材を書き出す**（hero動画・テーマ4枚スクショ・アイコン各サイズ）
3. 素材が出たら **サイトのプレースホルダーを差し替え**（下の「差し替え一覧」参照）→ commit & push
4. **electron-builder で appx を一度通す**（技術的に一番の関門。詰まったらClaudeに相談）
5. Store 提出（`STORE_SUBMISSION_CHECKLIST.md` を上から潰す）

## このプロジェクトは何か
デスクトップアプリ **SkyFlip** の紹介用ランディングページ（ショーケースサイト）。
アプリ本体のコードは別リポジトリ（自宅PCにある）。ここは**宣伝・集客専用のサイト**。

## SkyFlip（アプリ本体）について
フリップ型の時計アニメーションを軸に、現実の空をデスクトップに映すアプリ。実装済み機能:
- フリップ時計アニメーション
- 朝・昼・夜で背景色がリニアに変化
- 時刻に応じて太陽・月が空を移動
- 実際の月齢を取得し、本物と同じ満ち欠けを背景に投影
- 現在地の天気とリアルタイム連動（位置情報で自動取得）。雨・雪のとき背景が暗くなる
- OS起動時に自動起動、デスクトップ常駐
- ボタンで月単位カレンダー表示

- 技術スタック: **Electron** / 対応OS: **Windows のみ** / 目的: **収益化**

## 収益化の方針
- 配布の本命: **Microsoft Store**（無料アプリとして公開、署名はStoreが代行）
- 収益モデル: **無料 ＋ テーマ課金**（Store の Add-on / アプリ内課金）
  - 無料: スタンダード
  - 有料テーマ: 桜の舞う春 / ネオン夜景 / 深宇宙と銀河（各 ¥320）
    ※注意: 流れ星は無料の標準演出。有料テーマは標準機能と被らない世界観にする（被ると返金原因）
  - 全部入りパック ¥980
- 課金実装は `StoreContext` API 経由（Electron からは未着手。自宅PCで実装予定）

## このサイトの構成
1ページ完結のランディングページ（詳細は下の「サイトのセクション構成」を参照）。

### ファイル
- `index.html` — トップ。日本語コピー全部入り。OGP/JSON-LD/canonical/favicon 設定済み
- `privacy.html` — プライバシーポリシー（位置情報・天気APIの扱い。Store審査用）
- `contact.html` — お問い合わせ（連絡先はプレースホルダー、要差し替え）
- `style.css` — 空・癒やし系デザイン。legal/contactページ用スタイルも含む。レスポンシブ対応済み
- `favicon.svg` — 空＋フリップ時計のアイコン（自作SVG）
- `faq.html` — よくある質問（アコーディオン式）
- `terms.html` — 利用規約（提供者名はプレースホルダー、要差し替え）
- `robots.txt` / `sitemap.xml` — SEO用
- `STORE_LISTING.md` — Microsoft Store 掲載文＋**価格・課金設計の確定版**（サイトと整合させること）
- `LAUNCH_POSTS.md` — ローンチ告知文ストック（X/Reddit/ProductHunt、日英）
- `OGP_DESIGN.md` — OGP画像(assets/ogp.png)のデザイン設計書（案A〜C）
- `ROADMAP.md` — 開発ロードマップ（v1.0実装済み〜v3.0構想）
- `STORE_SUBMISSION_CHECKLIST.md` — Store提出までの全手順（会社可🏢/自宅🏠で分類）
- `LAUNCH_CHECKLIST.md` — 公開ボタンを押す前の最終確認（プレースホルダー残存チェック等）
- `DEMO_STORYBOARD.md` — hero動画/SNS GIF/スクショの絵コンテ＆撮影ガイド
- `404.html` — 404ページ（夜空＋月の世界観。GitHub Pagesが自動使用）
- `CLAUDE.md` — このファイル
- `STORE_LISTING.md` には英語掲載文も追記済み（任意・後追い用）

### サイトのセクション構成（index.html）
①ヒーロー ②コンセプト ③特徴6つ ③.5「一日の移ろい」(朝昼夕夜+月齢の魅せ場) ④テーマ(課金) ⑤DL ⑥フッター

## デザイン/トーンの方針
- コンセプト: 「情報のためでなく、眺めて心地よくなる時計」= 癒やし・リラックス系で差別化
- メインキャッチ: 「窓の外の天気を、机の上に。」
- カラー: 空の青(#4a90d9)を基調に、余白多め

## 残タスク（自宅PCでやること）

### A. 用意する素材ファイル（`assets/` フォルダを作って置く）
- [ ] `assets/hero.mp4` … アプリ動作のループ動画（**最重要**。サイトの第一印象）
- [ ] `assets/hero-poster.jpg` … 動画読み込み前に出るポスター画像
- [ ] `assets/ogp.png` … SNSシェア用 1200×630（作り方は `OGP_DESIGN.md`）
- [ ] テーマ4枚のスクショ（スタンダード/桜/ネオン夜景/深宇宙と銀河）

### B. プレースホルダー差し替え（各ファイルを開いて該当文字列を検索）
画面上で黄色ハイライト or HTMLコメントで目印を付けてある。検索ワードで一発で飛べる:

| ファイル | 検索する目印 | 何に差し替えるか |
|---|---|---|
| `contact.html` | `example@example.com` / `差し替えここまで` | 連絡用メール / XアカウントURL |
| `privacy.html` | `legal__placeholder` | 天気情報サービス名＋そのプライバシーポリシーURL、提供者名 |
| `terms.html` | `legal__placeholder` | 提供者名 |
| `style.css` | `.theme-card__thumb--default` 等 | 仮グラデ → 実スクショの `background-image` |
| `index.html` | `href="#download"` 付近のボタン | 「Microsoft Store で入手」のhref（①ヒーロー/⑤DL）→ 実Store URL |
| `LAUNCH_POSTS.md` | `［公開後にStore URLを記入］` | 各告知文のURL |

### C. 整合性の維持（変えたら両方直す）
- テーマ名・価格を変えたら `STORE_LISTING.md` とサイト(index.html ④)を**両方**更新
- アプリの仕様（機能）を変えたら、このCLAUDE.md の「実装済み機能」とサイト③/③.5、STORE_LISTINGを更新

## 公開方法
GitHub Pages（無料）で公開予定。独自ドメインは後から設定可能。

## 注意
- Partner Center 登録は**個人のMicrosoftアカウント**で行う（会社アカウントではない）。収益は個人のもの。
- このサイトの文面と STORE_LISTING.md はトーンを揃えてある。片方を変えたらもう片方も合わせる。
