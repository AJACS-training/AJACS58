# AJACS薩摩　パスウェイデータベースの紹介とKEGG PATHWAYの使い方  
情報・システム研究機構  
ライフサイエンス統合データベースセンター  
守屋 勇樹 moriya@dbcls.rois.ac.jp  
2016/01/26 AJACS薩摩  

---
## パスウェイデータベースとは
タンパク質や化合物等の分子間相互作用のネットワークをデータベース化、視覚化したもの

イメージ (KEGG)
![pathway](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-pathway.png)

可視化することで生命現象を理解しやすくする  
データベース化することで網羅的に扱えるようになる
- ゲノムアノテーションや種間比較、遺伝子発現のエンリッチメント解析、モデル化、シミュレーションなどに利用できるようになる  

歴史的には代謝経路の表現から始まった  
現在ではタンパク質間相互作用、シグナル伝達系、遺伝子制御、環境シグナルなど様々なものが含まれる

---
## いろいろなパスウェイデータベース
pathguid: http://www.pathguide.org/
- パスウェイリソースのリスト約 550　(2013)
  - タンパク質間相互作用
  - 代謝パスウェイ
  - シグナリングパスウェイ
  - パスウェイダイアグラム
  - 転写因子・遺伝子制御ネットワーク
  - タンパク質-化合物間相互作用
  - 遺伝的相互作用ネットワーク
  - アミノ酸配列解析
  - その他

Availability: 有料か無料か  
Standards: 標準データ形式(BioPAX, SBML等)に準拠しているかどうか
- BioPAX は静的なマップ表現
- SBML は kinetics も取り扱えるため、シミュレーションなどで利用可能

どのパスウェイデータベースを解析に使えば良いかは、対象生物や対象パスウェイ、目的によって異なる  
ここでは BioCyc, Reactome, KEGG PATHWAY を紹介する

----
## BioCyc
- ウェブサイト：http://biocyc.org/
- 開発：SRIインターナショナル（Stanford Research Institute）
- 対象：大腸菌からヒトまで、7,600 種以上
  - 専門家が手作業で作成した文献ベースのデータ＋自動ツール
  - 代謝パスウェイのみ
- 利用：アカデミックフリー
- データ形式：BioPAX SBML

![biocyc1](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc1.png)


#### 対象生物種を見てみよう  
- http://biocyc.org/biocyc-pgdb-list.shtml
  - 種毎の Database
    - Tier 1：専門家が手作業で作成した文献ベースのデータ
    - Tier 2：自動ツールで作成したデータを手作業で修正
    - Tier 3：自動ツールで作成
  - MetaCyc だけは 2,000 種以上から構築


#### 好きな生物のパスウェイを見てみよう
- 好きな生物種をクリック（例： [EcoCyc](http://biocyc.org/ecocyc/index.shtml)）
- 右上の検索ボックスで "glycolysis" や "tca" などの好きな単語を入力し、Quick Search ボタンをクリック
- ![biocyc6](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc6.png)
- パスウェイが存在する場合、リストが表示されるので、クリック
- 代謝産物のパスウェイが表示される
- More Detail ボタンをクリックすると、酵素の情報が追加され、もう一度 More Detail ボタンをクリックすると代謝産物の構造情報が追加される
- 右の Options メニューから、表示のカスタマイズやダウンロードが可能
- ![biocyc3](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc3.png)


#### 種間比較をしてみよう
- 右の Option メニューの [Species Comparison](http://ecocyc.org/compare-frame-in-orgs?type=PATHWAY&object=GLYCOLYSIS&initial-orgs=(ECOLI)&detail-level=1) をクリック
- 比較する種の選択画面が表示されるので、比較したい好きな種を入力し、OK をクリック
- ![biocyc7](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc7.png)
- パスウェイや遺伝子、オペロン構造などが比較できる


#### 好きな生物の Overview パスウェイを見てみよう  
- 右の Option メニューの [Show on Cellular Overview](http://ecocyc.org/overviewsWeb/celOv.shtml?orgid=ECOLI&pnids=GLYCOLYSIS) をクリック
- ![biocyc2](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc2.png)


### サンプル・データをマッピングしてみよう  
- 右のメニューの Overlay Experimental Data ＞ Upload Data from File
- 出てきた入力フォームのファイルアップロード部のすぐ下の (or "paste data" directly into form) のリンクをクリック
- ![biocyc4](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc4.png)
- テキストエリアに切り替わるので、テキストエリア右上の Gene example をクリックすると、サンプル・データが入る
- データのカラム（1〜3）を入力して Submit ボタンをクリック
- ![biocyc5](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-biocyc5.png)


----
## Reactome
- ウェブサイト：http://www.reactome.org/
- 開発：EMBLE-EBI 他
- 対象：ヒトを中心に脊椎動物、酵母、植物、19 種
  - 専門家が手作業で作成した文献ベースのデータ
  - 代謝パスウェイ以外も
- 利用：フリー
- データ形式：BioPAX, SBML
- 外部のReactome
  - Plant reactome: http://plantreactome.oicr.on.ca/

![reactome1](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-reactome1.png)

#### 好きな生物のパスウェイを見てみよう  
- Browse Pathways ボタンをクリック
- 左にパスウェイのリスト、右にパスウェイマップが表示。連動して動作

#### パスウェイをハイライトさせてみよう  
- マップ左上の虫眼鏡アイコンをクリックして、 "glycolysis"や"tca"などの単語を入力すると、候補がリストアップされるので選択

#### サンプル・データをマッピングしてみよう  
- 右上の Analysis: アイコンをクリック
- http://www.reactome.org/PathwayBrowser/#TOOL=AT
- ファイルアップロード部のすぐ下の click here to paste your data... をクリック
- 右のサンプルをクリックして GO ボタンをクリック

----
## Unipathway
- ウェブサイト： http://www.unipathway.org/
- 開発：SIB (the Swiss Institute of Bioinformatics) - Swiss-Prot group 他
- 対象：タンパク質の知識データベース UniProt に登録されている種
  - Uniprot の情報を KEGG PATHWAY, MetaCyc にマッピング
  - 代謝パスウェイのみ
- 利用：フリー

![unipathway1](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-unipathway1.png)

----
## KEGG PATHWAY
- ウェブサイト：http://www.kegg.jp/
- 開発：京都大学
- 対象：ゲノムの決まった全生物種（真核生物、真性細菌、古細菌）4,000 種以上
  - 専門家が手作業で作成した文献ベースのデータ＋自動ツール
    - リファレンスパスウェイ：専門家が手作業で文献ベースから作成（BioCyc の Tier 1(MetaCyc)に相当）
    - 種毎のパスウェイ（手動）：自動ツールで作成し、手作業で修正（BioCyc の Tier 2 に相当）
    - 種毎のパスウェイ（自動）：自動ツールで作成（Buicyc の Tier 3 に相当）
  - 代謝パスウェイ以外も
- 利用：アカデミックフリー
- データ形式：KGML
  - [KEGGscape] (http://apps.cytoscape.org/apps/keggscape) で Cytoscape に読み込み可能

![kegg1](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-kegg1.png)

#### グローバルマップを見てみよう  
- http://www.kegg.jp/kegg/pathway.html
- 1.0 Global and overview maps の [Metabolic pathways](http://www.kegg.jp/kegg-bin/show_pathway?map01100) をクリック
  - 右の [[KEGG Atlus](http://www.kegg.jp/kegg/atlas/?01100)] は Java で動くビューワーで、自由度が少し高い分、動作が重たい
- 左にモジュールのリスト（KEGG におけるパスウェイの小さい機能単位）、右にマップが表示
- 機能単位毎にパスウェイを強調表示できる

#### 生物種毎のグローバルマップを見てみよう  
- プルダウンメニューから生物を選択し、Go をクリック

#### 個別のパスウェイマップを見てみよう  
- http://www.kegg.jp/kegg/pathway.html
- 1.1 以下の好きなパスウェイをクリック
  - 右上の Help でそれぞれの図形の意味を見てみよう

好きな生物のパスウェイを見てみよう  
- 緑色の箱で、その生物の持つパスウェイを表現

#### リファレンスパスウェイと種毎のパスウェイの関係  

![kegg2](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-kegg2.png)

![kegg3](https://github.com/moriya-dbcls/AJACS58/blob/master/moriya/images/a58-kegg3.png)

#### 対象生物種を見てみよう  
- http://www.kegg.jp/kegg/catalog/org_list.html
  - KEGG では 3-4 文字の独自の生物種コードを使用している
  - データが手作業で修正されているか自動ツールで作成されているかはテーブルには情報が無い
  - 生物種コードのリンクをクリックすると、種の情報のページに飛ぶ
  - "Annotation" が manual -> 手作業（hsa等）、KOALA -> 自動ツール（pps等）

#### サンプル・データをマッピングしてみよう  
- http://www.genome.jp/kegg/tool/map_pathway2.html
- KEGG Mapper

#### KEGG データベースにはない新規遺伝子をマッピングしてみよう  
- BlastKOALA, ghostKOALA, KAAS

#### KGML ファイルをダウンロードしてみよう  

--
