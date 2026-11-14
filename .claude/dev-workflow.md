# dev-workflow の設定

dev-workflow プラグインのスキル（work-issues / bump-version / note-release）が読む、このリポジトリ固有の設定。
リポジトリの `.claude/dev-workflow.md` に置く。使わないスキルの節は消してよい。
値が決まっていない項目は `なし` と書く（スキルはその手順を飛ばす）。空のままにしない。

## 共通

| 項目 | 値 |
|---|---|
| 開発ブランチ | `main` |
| 本番ブランチ | `main` |
| 仕様の根拠（docs） | `README.md` と `index.html` |
| GitHub Projects | `KazumasaIwazaki` の Project `1` |

## work-issues

| 項目 | 値 |
|---|---|
| 対象にする Status | `In progress` |
| 確認待ちにする Status | `confirmation` |
| 実装が済んだときの Status | `Review` |
| 動かさない Status | `Todo` / `Done` / `cancel` |
| ブランチ名 | `feature/<番号>-<内容>` |
| PR の本文で Issue を閉じるか | `Closes #<番号>` を書く |

### 検査

実装のあと、上から順に通す。

```bash
# index.html が参照するローカルのファイルがすべて在ること
grep -oE '(src|href)="[^"#:]+"' index.html | sed -E 's/^[a-z]+="//; s/"$//' | sort -u | while read -r f; do [ -e "$f" ] || echo "missing: $f"; done
```

### 動作確認

ローカルの `index.html` をブラウザ（Claude in Chrome など）で開き、PC 幅とスマホ幅で表示を確かめる。
`main` へのマージは GitHub Pages にそのまま公開されるので、マージ前に必ず確かめる。
