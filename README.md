# PyTorch uv Template

PyTorchの実験・学習用プロジェクトをすぐに開始するためのGitHub Templateです。

Python環境と依存関係の管理には `uv` を使用し、VS CodeおよびJupyter Notebookでの利用を想定しています。

## Features

- uvによるPython環境・依存関係管理
- PyTorch
- NumPy
- Matplotlib
- Jupyter Notebook / ipykernel
- Ruff による Lint / Format
- VS Code 設定済み（自動インタプリタ検出・保存時フォーマット）
- `uv.lock` による再現可能な開発環境

## Quick Start

このリポジトリをGitHub Templateとして使用することで、新しいPyTorchプロジェクトを簡単に開始できます。

### 1. GitHubから新しいリポジトリを作成

このリポジトリのGitHubページから **Use this template** を選択し、新しいリポジトリを作成します。

例:

```text
pytorch-uv-template
        ↓
Use this template
        ↓
my-pytorch-project
```

### 2. 作成したリポジトリをクローン

PowerShellで作業ディレクトリへ移動します。

```powershell
cd C:\Users\<username>\src
```

作成したリポジトリをクローンします。

```powershell
git clone <repository-url>
cd <repository-name>
```

### 3. uvで環境を構築

```powershell
uv sync
```

`pyproject.toml` と `uv.lock` をもとに、プロジェクト用の `.venv` と必要なパッケージが準備されます。

### 4. VS Codeで開く

```powershell
code .
```

`.vscode/settings.json` により、仮想環境 `.venv` のPythonインタプリタが自動認識されます。
手動で切り替える場合は以下を実行します：

```text
Ctrl + Shift + P
→ Python: Select Interpreter
→ .venv\Scripts\python.exe
```

### 5. PyTorchの動作を確認

```powershell
uv run python src/main.py
```

正常に動作すると、PyTorchのバージョンなどが表示されます。

例:

```text
PyTorch: 2.x.x+cpu
CUDA available: False
```

CPU版PyTorchを使用している場合、`CUDA available: False` でも問題ありません。GPU (CUDA) 版を利用したい場合は後述の「GPU (CUDA) 版 PyTorchの利用」を参照してください。

### 6. Jupyter Notebookを使う

VS Codeで次のNotebookを開きます。

```text
notebooks/playground.ipynb
```

Notebook右上のカーネル選択から、プロジェクトの `.venv` を選択します。

例:

```text
Python 3.14.x (.venv)
```

`ipykernel` は開発依存関係としてインストールされているため、そのままセルを実行できます。

---

## Daily Usage

プロジェクト作成後は、基本的に以下のコマンドで作業できます。

### VS Codeを起動

```powershell
code .
```

### Pythonスクリプトを実行

```powershell
uv run python src/main.py
```

### パッケージを追加

通常の依存関係を追加する場合:

```powershell
uv add <package>
```

例えば、pandasを追加する場合:

```powershell
uv add pandas
```

scikit-learnを追加する場合:

```powershell
uv add scikit-learn
```

複数のパッケージをまとめて追加することもできます。

```powershell
uv add pandas scikit-learn
```

### 開発用パッケージを追加

テストやLintなど、開発時のみ必要なパッケージは開発依存関係として追加します。

```powershell
uv add --dev <package>
```

例えばpytestを追加する場合:

```powershell
uv add --dev pytest
```

### コードの静的チェック / フォーマット (Ruff)

```powershell
uv run ruff check .
uv run ruff format .
```

### 依存関係を同期

GitHubから変更を取得した場合などは、必要に応じて次を実行します。

```powershell
uv sync
```

### 依存関係を更新

依存関係を新しいバージョンへ更新する場合:

```powershell
uv lock --upgrade
uv sync
```

---

## GPU (CUDA) 版 PyTorch の利用

デフォルトではクロスプラットフォームで軽量な CPU 版 PyTorch がインストールされます。  
NVIDIA GPU を搭載したマシンで CUDA 版 PyTorch を使用したい場合は、`pyproject.toml` に PyTorch の公式インデックス設定を追加します。

### 設定例 (CUDA 12.6 の場合)

`pyproject.toml` に以下を追記します：

```toml
[[tool.uv.index]]
name = "pytorch-cu126"
url = "https://download.pytorch.org/whl/cu126"
explicit = true

[tool.uv.sources]
torch = { index = "pytorch-cu126" }
torchvision = { index = "pytorch-cu126" }
```

その後、ロックファイルを更新して同期します。

```powershell
uv lock --upgrade
uv sync
```

`src/main.py` を再実行して `CUDA available: True` と表示されれば完了です。

---

## Project Structure

```text
.
├── .github/
│   └── dependabot.yml       # Dependabot (uv自動更新) 設定
├── .vscode/
│   ├── extensions.json      # VS Code 推奨拡張機能
│   └── settings.json        # VS Code ワークスペース設定
├── notebooks/
│   └── playground.ipynb     # 実験用Jupyter Notebook
├── src/
│   └── main.py              # 動作確認スクリプト
├── .gitignore
├── .python-version          # 使用するPythonバージョン (3.14)
├── pyproject.toml           # プロジェクト定義・依存関係・ツールの設定
├── uv.lock                  # パッケージバージョン固定ファイル
└── README.md
```

### `notebooks/`

Jupyter Notebookを使用した実験やデータ分析を配置します。

```text
notebooks/playground.ipynb
```

は、PyTorch・NumPy・Matplotlibなどの動作確認や簡単な実験に使用できます。

### `src/`

Pythonのソースコードを配置します。

```text
src/main.py
```

テンプレートではPyTorchが正常に利用できるか確認するための簡単なコードを配置しています。

### `pyproject.toml`

プロジェクト情報とPythonパッケージの依存関係を管理します。

パッケージを追加・削除する場合は、直接編集する代わりに基本的に `uv add` や `uv remove` を使用します。

### `uv.lock`

インストールするパッケージの正確なバージョン情報を保持します。

Gitで管理することで、異なる環境でも同じ依存関係を再現しやすくなります。

### `.python-version`

このプロジェクトで使用するPythonバージョンを指定します。

### `.venv`

`uv sync` などを実行すると作成される、このプロジェクト専用のPython仮想環境です。

`.venv` 自体はGitでは管理しません。

---

## Requirements

このテンプレートは以下の環境での利用を想定しています。

- Python 3.14
- uv
- Git
- VS Code
- VS Code Python Extension
- VS Code Jupyter Extension

---

## VS Code

`.vscode/settings.json` により、VS Code 起動時に `.venv` 内の Python インタプリタが自動選択され、保存時に Ruff による自動フォーマットが行われます。

手動で確認・変更したい場合は以下を実行します：

```text
Ctrl + Shift + P
```

続いて、

```text
Python: Select Interpreter
```

を選択します。

Windowsでは、プロジェクト内の次のInterpreterを選択します。

```text
.venv\Scripts\python.exe
```

Notebookを使用する場合も、同じ `.venv` のPython環境をカーネルとして選択してください。

---

## Jupyter Notebook

このテンプレートでは `ipykernel` を開発依存関係として管理しています。

Notebookでカーネルを選択するときは、プロジェクトの `.venv` を使用してください。

VS Codeから次のようなメッセージが表示された場合:

```text
セルを実行するには、ipykernel パッケージが必要です。
```

まず依存関係が同期されているか確認してください。

```powershell
uv sync
```

---

## PyTorch Check

テンプレートに含まれる `src/main.py` を使用してPyTorchの動作を確認できます。

```powershell
uv run python src/main.py
```

実行例:

```text
PyTorch: 2.x.x+cpu
CUDA available: False
```

PyTorchをPythonから直接確認することもできます。

```powershell
uv run python -c "import torch; print(torch.__version__)"
```

---

## Environment Management

仮想環境 `.venv` はGitには含めません。

GitHubで管理するのは主に以下のファイルです。

```text
pyproject.toml
uv.lock
.python-version
```

そのため、新しいPCや別の環境でリポジトリをクローンした場合でも、

```powershell
uv sync
```

を実行することで環境を再構築できます。

---

## Typical Workflow

新しいPyTorchプロジェクトを始める場合:

```text
1. GitHubで「Use this template」
        ↓
2. 新しいRepositoryを作成
        ↓
3. git clone
        ↓
4. uv sync
        ↓
5. code .
        ↓
6. 開発開始（VS Codeが自動で .venv を認識）
```

以降、パッケージが必要になったら:

```powershell
uv add <package>
```

ソースコードを実行するときは:

```powershell
uv run python src/main.py
```

という運用を基本とします。

---
