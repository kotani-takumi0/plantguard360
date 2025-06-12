# PlantGuard 360
作物の病害を早期検知し、葉面積や果実検出から収量を推定する **Edge AI** プロジェクト  
（機械学習エンジニア職インターン応募用ポートフォリオ）

---

## クイックスタート

```bash
# 1. リポジトリを取得
git clone https://github.com/kotani-takumi0/plantguard360.git
cd plantguard360

# 2. Poetry で環境構築（Step 2 でファイルを追加予定）
poetry install

# 3. データセットをダウンロード（準備中）
python scripts/download_data.py plantvillage

# 4. ベースライン学習（CPU でも動作確認）
python notebooks/00_baseline.ipynb

##使用データセット
| 名称                   | ライセンス     | 主な内容                 |
| -------------------- | --------- | -------------------- |
| PlantVillage         | CC BY 4.0 | 38 作物・病害分類（約 54k 画像） |
| PlantDoc v2          | MIT       | 屋外実写の病害分類（約 2.6k 画像） |
| Plant Pathology 2021 | CC BY 4.0 | リンゴ葉 4 クラス（約 23k 画像） |


#プロジェクトロードマップ
1.データ統合 & EDA
2.ViT Tiny でベースライン構築
3.屋外データでファインチューニング
4.YOLOv9-seg による果実検出・収量推定
5.ONNX 量子化 & Raspberry Pi ベンチマーク
6.FastAPI + Docker でデモ公開

##依存ライブラリ
Python 3.11
PyTorch / torchvision
timm, wandb
Poetry で一括管理（pyproject.toml 参照）
