# 🍅 PlantGuard 360

**トマトを中心とした植物の葉画像から病害を早期検知する Vision Transformer (ViT) プロジェクト**

> この README は *2025‑06‑14 時点* の進捗をまとめたものです。今後の実装・検証に合わせて随時更新します。

---

## 1. プロジェクト概要

* **社会課題** : 異常気象による作物被害・食料不安
* **目的** : 葉画像を用いて病害をリアルタイム検知し、防除タイミングを最適化して ROI を向上
* **現状性能** : 複数植物クラスを含むモデルで **Macro F1 ≒ 0.93**（ViT‑tiny + 転移学習）

---

## 2. ディレクトリ構成（暫定）

```
plantguard360/
├── notebooks/           # 解析・可視化用 Jupyter Notebook
│   └── 01_baseline.ipynb
├── src/                 # 本番コード（学習・推論）
│   ├── dataset.py
│   ├── augment.py
│   ├── model.py
│   ├── train.py
│   └── infer.py
├── docs/                # 事業背景・ROI 試算などの資料
│   ├── Problem_Brief.md
│   └── Gap_Report.md
├── data/                # 生データ（Git 管理外 / .gitignore 済）
├── outputs/             # 学習済みモデル・ログ（同上）
├── .gitignore
├── Makefile             # 再現コマンド集
├── Dockerfile           # 実行環境固定（CPU 版）
└── README.md            # 本ファイル
```

---

## 3. セットアップ & 再現方法

### 3.1 ローカル実行

```bash
# 依存ライブラリのインストール (Poetry 推奨)
poetry install --no-dev

# データダウンロード (Kaggle API 使用)
python scripts/download_data.py --out data/

# 学習（GPU があれば自動検知）
make train                # => outputs/model.pt

# 推論サンプル
make infer IMG=sample.jpg
```

### 3.2 Docker 実行（再現性保証）

```bash
docker build -t pg360 .
docker run -v $(pwd)/data:/data pg360 make train
```

---

## 4. 現状の成果

| モデル構成             | Macro F1 |
| ----------------- | -------- |
| ViT‑tiny baseline | 0.91     |
| ViT‑tiny + データ拡張  | **0.93** |

* **Synthetic‑Stress**（強光・角度ズレ）環境では F1 が *0.81* まで低下 → ギャップ解消が課題
* Grad‑CAM++ により疾患部位の可視化を確認

---

## 5. 今後のロードマップ（抜粋）

| 期日         | 目標                  | KPI                  |
| ---------- | ------------------- | -------------------- |
| 2025‑06‑21 | Gap 実験レポート完了        | Stress F1 低下幅を定量化    |
| 2025‑06‑28 | Active Learning PoC | 追加 50 枚で F1 +2pt     |
| 2025‑07‑05 | Exec Summary PDF v1 | TAM・ROI・PoC 計画を1枚に整理 |

---

## 6. 参考リンク

* **データセット** : PlantVillage / PlantDoc ほか
* **プレプリント** : DINOv2 (Meta, 2023)
* **関連研究** : Fourier Domain Adaptation など

---

### ライセンス

MIT License

> メンテナ： @kotani‑takumi0  — ご意見・PR 大歓迎です 🙌
>>>>>>> d4943e1 (Initial setup from VSCode)
