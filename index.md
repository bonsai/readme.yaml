# README.yaml

GitHubリポジトリを、AIやツールが少ない読み取り量で理解するためのメタデータ仕様。

## 2枚で読む

- `README.md` — 人間が読む。背景、思想、使い方、ストーリー。
- `README.yaml` — 機械が読む。概要、状態、タグ、統計、関連、読むべき入口。

この2つは置き換えではなく補完関係。

## 読み取り順

```
README.yaml
    ↓
全体像を把握
    ↓
必要なファイルだけ読む
    ↓
README.md / source / demo
```

## README.yaml に入れるもの

- repository: リポジトリの目的
- metadata: topics / tags / status / type / skills
- read: 人間・機械・demo・sourceの入口
- stats: commits / files / languages など
- portfolio: ポートフォリオ上の位置づけ
- relations: 関連・派生・発展先
- history: 系譜・履歴への入口

## 原則

1. 人間向けREADMEを置き換えない
2. 機械が最初に読む情報を小さくまとめる
3. 統計情報は可能な限り自動生成する
4. YAMLに長い説明文を重複させない
5. 必要なときだけ詳細ファイルを深掘りする

## Status

`readme.yaml/v0` として試作中。