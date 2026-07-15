# LabVIEW to Python Industrial Skill

[English](../README.md) | [简体中文](README.zh-CN.md) | 日本語

**telux** が作成した、LabVIEW の研究・産業計測アプリを Python に移行する
ための Agent Skill とルールです。測定ロジック、データ lineage、装置安全、
UI、配布 EXE を独立した証拠ゲートで検証します。

このページはコミュニティ翻訳の要約です。相違がある場合は英語の
`SKILL.md` を優先してください。

## 原則

- UI の外観より先に VI/subVI の挙動とデータ処理を移行する。
- Industrial UI、LabVIEW-style UI、simulator、real adapter は同じ workflow を使う。
- quick preview は操作確認専用で、完全分解能の証拠にしない。
- target-derived CSV roundtrip を独立した LabVIEW algorithm parity と呼ばない。
- 実際のクリック、入力、スクロール、hover と新しいスクリーンショットを使う。
- source UI、simulator、packaged EXE、real hardware を別々に判定する。

## インストール

```bash
npx skills add k-telux/labview-to-python-industrial-skill \
  --skill labview-to-python-industrial \
  --agent codex
```

利用例と実プロジェクト由来の匿名化された入出力は
[examples](../examples/README.md) を参照してください。正規仕様は
[SKILL.md](../skills/labview-to-python-industrial/SKILL.md) です。
