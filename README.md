# dotfiles

Windows / PowerShell で使う Vim 設定を Git 管理するためのリポジトリです。

## 構成

```text
dotfiles/
├─ vim/
│  └─ vimrc        # 実際に編集・Git管理する Vim 設定
├─ install.ps1     # $HOME\_vimrc にローダーを作成
├─ .gitignore
├─ README.md
└─ LICENSE
```

## 初回セットアップ

PowerShell でこのリポジトリを clone して、ディレクトリへ移動します。

```powershell
git clone https://github.com/kevin6655/dotfiles.git
cd dotfiles
```

その後、インストーラーを実行します。

```powershell
Set-ExecutionPolicy -Scope Process Bypass
.\install.ps1
```

`install.ps1` は `$HOME\_vimrc` を作り、リポジトリ内の `vim\vimrc` を読み込むよう設定します。

既存の `$HOME\_vimrc` がある場合は、上書き前に次の形式でバックアップします。

```text
_vimrc.backup-YYYYMMDD-HHMMSS
```

## Vim 設定を変更する

今後は `$HOME\_vimrc` を直接編集せず、このリポジトリの次のファイルを編集します。

```text
vim\vimrc
```

Vim から現在読み込まれているスクリプトを確認するには:

```vim
:scriptnames
```

一覧に `dotfiles\vim\vimrc` が出ていれば正常です。

## Vim 設定の内容

現在の設定は主に次を対象にしています。

- YAML
- Python
- Go
- SQL
- 相対行番号
- 永続 Undo
- swap による復旧
- write backup
- Vim 標準のファイルタイプ別インデント
- PowerShell / Windows Terminal 上での利用

## 別PCへ展開する

リポジトリを clone したあと:

```powershell
cd dotfiles
Set-ExecutionPolicy -Scope Process Bypass
.\install.ps1
```

これで、そのPCの `$HOME\_vimrc` から clone した `vim\vimrc` が読み込まれます。
