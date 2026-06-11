# 自宅PC セットアップ手順（まっさら → このリポジトリを編集できるまで）

自宅PC（Windows）にはまだ Git も GitHub CLI も入っていない前提。
上から順にやれば、サイトを clone して編集・push できる状態になる。
※ 各コマンドは PowerShell で実行（スタート → "PowerShell" で起動）。

> 📌 **このファイルはリポジトリ内にあるため、clone 前は自宅PCで読めない。** 対策:
> - GitHub のWebで直接読める → https://github.com/atdirakg9020121-afk/skyflip-site/blob/main/HOME_PC_SETUP.md
> - またはこのページをスマホでブックマーク／会社で開いて手元に控えておくとよい。
> - STEP 1〜3（Git/gh導入・認証）さえ済めば clone でき、以降はローカルで読める。

---

## STEP 1. Git をインストール
1. https://git-scm.com/download/win を開く → インストーラがダウンロードされる
2. 実行して、基本はそのまま「Next」で進めてOK（既定設定で問題なし）
3. インストール後、PowerShell を**新しく開き直して**確認:
   ```powershell
   git --version
   ```
   → `git version 2.xx.x` のように出ればOK

## STEP 2. GitHub CLI (gh) をインストール
1. https://cli.github.com/ を開く → "Download for Windows" でインストーラ取得
2. 実行してインストール
3. PowerShell を**開き直して**確認:
   ```powershell
   gh --version
   ```
   → `gh version 2.xx.x` が出ればOK

> 補足: winget が使えるなら、上記2つは以下のコマンドでも入る:
> ```powershell
> winget install --id Git.Git -e
> winget install --id GitHub.cli -e
> ```
> （インストール後は PowerShell を開き直すこと）

## STEP 3. GitHub にログイン（gh で認証）
```powershell
gh auth login
```
対話形式で聞かれるので、こう答える:
- **What account?** → `GitHub.com`
- **Preferred protocol?** → `HTTPS`
- **Authenticate Git with your GitHub credentials?** → `Yes`
- **How to authenticate?** → `Login with a web browser`
- 画面に表示される **8桁のコード**を control + クリックで開くブラウザに入力 → 承認

> 使うアカウントは会社PCと同じ **atdirakg9020121-afk**。
> ブラウザでそのアカウントにログインした状態で承認すること。

確認:
```powershell
gh auth status
```
→ `Logged in to github.com account atdirakg9020121-afk` が出ればOK

## STEP 4. Git の名前・メールを設定（コミットの署名）
会社PCと揃えておく:
```powershell
git config --global user.name "atdirakg9020121-afk"
git config --global user.email "atdirakg_9020121@yahoo.co.jp"
```

## STEP 5. リポジトリを clone
好きな作業フォルダに移動してから:
```powershell
cd ~\Documents          # 置きたい場所へ（例）
git clone https://github.com/atdirakg9020121-afk/skyflip-site.git
cd skyflip-site
```

## STEP 6. サイトを開いて確認
ビルド不要。ブラウザで開くだけ:
```powershell
start index.html
```

## STEP 7. 編集 → 反映の流れ（毎回これ）
```powershell
# ファイルを編集したあと
git add -A
git commit -m "変更内容を書く"
git push
```
→ push すると GitHub Pages が自動で再ビルドし、1〜2分で公開URLに反映:
https://atdirakg9020121-afk.github.io/skyflip-site/

---

## つまずきポイント早見表
| 症状 | 対処 |
|---|---|
| `git` / `gh` が「コマンドが見つからない」 | PowerShell を開き直す（PATH反映のため）。それでもダメなら再インストール |
| push で認証エラー | `gh auth login` をやり直す。アカウントが atdirakg9020121-afk か確認 |
| clone で「Permission denied」 | リポジトリはPublicなので clone 自体は誰でも可。push 時の認証を確認 |
| 改行の警告 (LF→CRLF) | 無害。Windowsでは正常なので無視してよい |
| Pages に反映されない | 1〜2分待つ／ブラウザを Ctrl+F5 でスーパーリロード |

## この後やること
clone できたら `CLAUDE.md` を開く。自宅再開のクイックスタートと残タスク（素材・プレースホルダー差し替え）が全部まとまっている。
アプリ本体のソースも別途あるなら、同じ作業フォルダに置いておくと Claude が仕様確認しやすい。
