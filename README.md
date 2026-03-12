# Pleasanter Schema Builder

CSV・ExcelファイルからローコードプラットフォームPleasanterのサイトパッケージJSON（テーブル定義）を自動生成するブラウザツールです。

## これは何？

Pleasanterで新しいテーブルを作る際、カラムをGUIで1つずつ手動設定する必要があります。  
このツールを使えば、**CSVやExcelをアップロードするだけ**でサイトパッケージJSONが生成でき、Pleasanterにインポートするだけでテーブルが完成します。

KintoneにはCSVからアプリを自動生成する機能がありますが、Pleasanterには同等機能がありません。そのギャップを埋めるために作りました。

## 機能

- **CSV・Excel（.xlsx/.xls）対応** — ドラッグ＆ドロップで読み込み
- **文字コード自動判定** — UTF-8 / Shift-JIS / UTF-16 / BOM対応
- **Excelシート切り替え** — 複数シートのExcelにも対応
- **カラム型の自動推定** — ヘッダー名から日付・数値・テキストなどを自動判定
- **テーブル種別の選択** — Issues（期限付き）/ Results（記録）を切り替え
- **既定列のON/OFF選択** — Title・Body・Status・Manager・Ownerなどを個別に表示設定
- **レコードデータの取り込み** — CSVデータをそのままレコードとして含められる
- **カラム設定の編集** — 表示名・型・必須フラグをGUI上で調整
- **重複ID自動解決** — 同じ型が複数列あっても自動でA→B→C…と採番
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
3. 既定列（Title・Bodyなど）の表示ON/OFFを選択
4. カラムの表示名・型・必須フラグを調整
5. 「JSONを生成」→「ダウンロード」
6. Pleasanterの **管理 → サイトパッケージのインポート** でJSONを選択してインポート

## 注意事項

- CSVの備考列などに **Excelのセル内改行（Alt+Enter）** が含まれている場合、行のパースがずれることがあります。事前に改行を削除してください
- 日付型カラムのセルに日付以外の文字が入っている場合、該当セルは空欄として取り込まれます
- 同じ型のカラムが26列を超える場合はエラーになります（Pleasanterの上限）

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
