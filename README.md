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


## 第一段階: Vim プラグイン

`install.ps1` は vim-plug を `$HOME\vimfiles\autoload\plug.vim` に導入し、次のプラグインをインストールします。

- `yegappan/lsp` — Vim 9 向け LSP クライアント（Language Server の設定は第二段階）
- `junegunn/fzf` / `junegunn/fzf.vim` — fuzzy finder
- `tpope/vim-fugitive` — Git 操作
- `airblade/vim-gitgutter` — Git hunk 表示・操作
- `tpope/vim-surround` — quote / bracket / tag の編集
- `tpope/vim-commentary` — コメント操作

### 追加した主なキーマップ

| キー | 動作 |
| --- | --- |
| `<Space>ff` | ファイル検索 |
| `<Space>fb` | バッファ検索 |
| `<Space>fg` | Git 管理ファイル検索 |
| `<Space>gs` | Fugitive の Git status |
| `<Space>hp` | Git hunk preview |
| `<Space>hs` | Git hunk stage |
| `<Space>hu` | Git hunk undo |
| `gcc` | 現在行のコメント切り替え |
| `gc{motion}` | motion 範囲のコメント切り替え |

`vim-surround` は Vim の operator / motion に沿った標準キーマップをそのまま使用します。

### プラグインの更新

Vim 内で次を実行します。

```vim
:PlugUpdate
```

不要になったプラグインを `vim/vimrc` の `Plug` 行から削除した場合は:

```vim
:PlugClean
```

第一段階では LSP クライアント本体だけを導入します。Pyright、Ruff、gopls、yaml-language-server などの Language Server は第二段階で設定します。
