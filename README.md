# PyTorch uv Template

PyTorchの実験・学習用プロジェクトをすぐに開始するためのテンプレートです。

Python環境と依存関係の管理には `uv` を使用し、VS CodeおよびJupyter Notebookでの利用を想定しています。

## Features

- uvによる高速なPython環境・依存関係管理
- PyTorch
- NumPy
- Matplotlib
- Jupyter Notebook / ipykernel
- Ruff
- VS Code対応

## Project Structure

```text
.
├── notebooks/
│   └── playground.ipynb
├── src/
│   └── main.py
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

## Requirements

- Python 3.13
- uv
- VS Code
- VS Code Python Extension
- VS Code Jupyter Extension

## Setup

リポジトリをクローンします。

```powershell
git clone <repository-url>
cd <repository-name>
```

uvでPython環境と依存関係を復元します。

```powershell
uv sync
```

VS Codeでプロジェクトを開きます。

```powershell
code .
```

VS Codeでは、Python Interpreterとしてプロジェクト内の仮想環境を選択します。

Windows:

```text
.venv\Scripts\python.exe
```

## Run

Pythonスクリプトは次のように実行できます。

```powershell
uv run python src/main.py
```

## Jupyter Notebook

`notebooks/` 内のNotebookをVS Codeで開き、カーネルとしてプロジェクトの `.venv` を選択します。

例:

```text
Python 3.13.x (.venv)
```

`ipykernel` は開発依存関係としてインストールされているため、そのままセルを実行できます。

## Adding Packages

通常の依存関係を追加する場合:

```powershell
uv add <package>
```

例:

```powershell
uv add pandas scikit-learn
```

開発用パッケージを追加する場合:

```powershell
uv add --dev <package>
```

例:

```powershell
uv add --dev pytest
```

## Updating Dependencies

依存関係を更新する場合:

```powershell
uv lock --upgrade
uv sync
```

## PyTorch Check

PyTorchが正常に利用できるか確認できます。

```powershell
uv run python src/main.py
```

実行例:

```text
PyTorch: 2.x.x+cpu
CUDA available: False
```

CPU版PyTorchを使用している環境では、`CUDA available: False` でも問題ありません。

## Environment Management

仮想環境 `.venv` はGitには含めません。

環境は `pyproject.toml` と `uv.lock` から再現できるため、新しくクローンした環境では次を実行します。

```powershell
uv sync
```

これにより、プロジェクトに必要なPython環境と依存関係を再構築できます。

## License

必要に応じてライセンスを追加してください。