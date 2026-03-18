# Pleasanter Schema Builder

CSV・ExcelファイルからローコードプラットフォームPleasanterのサイトパッケージJSON（テーブル定義）を自動生成するブラウザツールです。

## これは何？

Pleasanterで新しいテーブルを作る際、カラムをGUIで1つずつ手動設定する必要があります。  
このツールを使えば、**CSVやExcelをアップロードするだけ**でサイトパッケージJSONが生成でき、Pleasanterにインポートするだけでテーブルが完成します。

## 機能

- **CSV・Excel（.xlsx/.xls）対応** — ドラッグ＆ドロップで読み込み
- **文字コード自動判定** — UTF-8 / Shift-JIS / UTF-16 / BOM対応
- **Excelシート切り替え** — 複数シートのExcelにも対応
- **カラム型の自動推定** — ヘッダー名から日付・数値・テキストなどを自動判定
- **テーブル種別の選択** — Issues（期限付き）/ Results（記録）を切り替え
- **既定列のON/OFF選択** — Title・Body・Status・Manager・Ownerなどを個別に表示設定
- **既定列へのマッピング** — CSV列をTitle・Bodyなどの既定フィールドに割り当て可能
- **レコードデータの取り込み** — CSVデータをそのままレコードとして含められる
- **カラム設定の編集** — 表示名・型・必須フラグをGUI上で調整
- **重複ID自動解決** — 同じ型が複数列あっても自動でA→B→C…と採番
- **拡張カラム対応** — Classは最大50列（A〜Z＋001〜024）まで対応
- **JSON生成・ダウンロード** — Pleasanter v1.4.23.3準拠のサイトパッケージJSONを出力

## 使い方

### オンラインで使う（インストール不要）

👉 **https://cycats613.github.io/pleasanter-schema-builder/pleasanter-schema-builder.html**

ブラウザで開くだけで動作します。

### ローカルで使う

```bash
git clone https://github.com/cycats613/pleasanter-schema-builder.git
```

`pleasanter-schema-builder.html` をブラウザで直接開くだけで動きます。  
※ ExcelファイルはCDN経由でSheetJSを読み込むためインターネット接続が必要です。CSVのみならオフラインでも動作します。

### Pleasanterへのインポート手順

1. CSVまたはExcelをドラッグ＆ドロップ（またはクリックして選択）
2. テーブル名・種別（Issues/Results）を設定
3. **既定列の表示設定** — Title・Bodyなど表示したい列をON/OFFで選択
4. **カラム設定** — 各列の表示名・型・必須フラグを調整
   - 型ドロップダウンの「既定列 (Builtin)」から Title・Body などを選ぶと、そのCSV列のデータが対応フィールドに入る
5. 「JSONを生成」→「ダウンロード」
6. Pleasanterの **管理 → サイトパッケージのインポート** でJSONを選択してインポート

## カラム型の種類と上限

| 型 | 説明 | 上限 |
|---|---|---|
| 既定列 (Builtin) | Title / Body / Status / Manager / Owner など | — |
| テキスト (Class) | 文字列 | **50列**（A〜Z + 001〜024）※オプション契約時 |
| 数値 (Num) | 数値・金額など | **50列**（A〜Z + 001〜024）※オプション契約時 |
| 日付 (Date) | 日付・日時 | **50列**（A〜Z + 001〜024）※オプション契約時 |
| チェック (Check) | チェックボックス | **50列**（A〜Z + 001〜024）※オプション契約時 |
| 説明文 (Description) | 長文テキスト | **50列**（A〜Z + 001〜024）※オプション契約時 |
| 添付ファイル | ファイル添付 | **25列**（A + 001〜024）※オプション契約時 |

## 既定列へのマッピングについて

型ドロップダウンで「既定列 (Builtin)」グループから列を選択すると、そのCSV列を既定フィールドに割り当てられます。

| 選択した型 | 動作 |
|---|---|
| Title | CSV列の値がタイトルフィールドに入る |
| Body | CSV列の値が内容フィールドに入る |
| Status | CSV列の値が状況フィールドに入る（数値） |
| Manager / Owner | CSV列の値が管理者/担当者フィールドに入る |
| StartTime / CompletionTime | CSV列の値が開始/完了日時に入る（Issues型のみ） |

> マッピングした列はSiteSettingsのColumnsには追加されません（既定フィールドのため）。

## 注意事項

- CSVの備考列などに **Excelのセル内改行（Alt+Enter）** が含まれている場合、行のパースがずれることがあります。事前に改行を削除してください
- 日付型カラムのセルに日付以外の文字が入っている場合、該当セルは空欄として取り込まれます
- Classの拡張列（001〜024）はPleasanterのオプション契約が必要です

## 対応バージョン

Pleasanter **v1.4.23.3** のエクスポートJSONをリバースエンジニアリングして形式を合わせています。

## 技術スタック

- 純粋なHTML / CSS / JavaScript（フレームワーク不使用、単一ファイル）
- [SheetJS (xlsx)](https://sheetjs.com/) — Excelファイルの読み込み（CDN）

サーバー不要。すべてブラウザ上で完結します。

## ライセンス

MIT License

## 関連リンク

- [Pleasanter 公式サイト](https://pleasanter.org/)
- [サイトパッケージ インポート - Pleasanterマニュアル](https://pleasanter.org/manual/site-package-import)
- [紹介記事（Note）](#)（公開後に追記）
