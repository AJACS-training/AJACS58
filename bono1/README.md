# ゲノム配列とそれに付与されたデータの使い方 at AJACS薩摩

情報・システム研究機構 ライフサイエンス統合データベースセンター  
[坊農 秀雅](http://bonohu.jp/) bono@dbcls.rois.ac.jp  
2016年1月26日 鹿児島大学桜ヶ丘キャンパス

----

これは統合データベース講習会AJACS薩摩「ゲノム配列とそれに付与されたデータの使い方」の資料です。   

----

## 概要

本講習は、だれでも自由に使うことができる公共データベース(DB)のうちゲノム配列に関して、それに付与されたデータの使い方を、ウェブツールを活用して、研究のさまざまな場面で使う方策について学びます。    

----

## 講習の流れ
今回の講習では、コンピュータを使って以下の内容について説明します。

- 研究現場で頻繁に使われるデータベースやツールを知る
- ゲノム配列を探す
	- NCBI
- ゲノム配列から探す
	- Web上で
		- BLAST
		- GGGenome
	- Local BLASTで(紹介のみ)
- アノテーションを足して見る
	- UCSCのtrack
		- ENCODE TF Binding
		- TFBS Conserved
		- Resetのやり方
	- Ensemblへジャンプ
		- Synteny
		- Resequencing


----

##### 講習に際しての注意とお願い

- みんなで同時にアクセスするとサイトにつながりにくくなることが予想されます。
    - 資料を見ながら自力で進められそうな方はどんどん先に、そうでない方は講師と一緒にすすめていきましょう。
    - サイトの反応が悪い時はタイミングをずらして実行してみてください。
    - 反応が無いからと言って何度もクリックするとますます繋がらなくなってしまいます。おおらかな気持ちで臨みましょう。
- わからないことがあったら挙手にてスタッフにお知らせください。
    - 遠慮は無用です(そのための講習会です!)。おいてけぼりは楽しくありません。
- 質問や個別の相談がある方は講習時間が終わったあとでも講師を捕まえて話してください。
 
----

## 研究現場で頻繁に使われるデータベースやツールを知る
### [統合TV](http://togotv.dbcls.jp/)
- 生命科学分野の有用なデータベースやツールの使い方を動画で紹介するウェブサイト
    - http://togotv.dbcls.jp/
[![統合TVトップページ](https://i.gyazo.com/9b890666bc8176d672d1e4f560162d05.png)](https://gyazo.com/9b890666bc8176d672d1e4f560162d05)

    - YouTube版もあります http://www.youtube.com/user/togotv/videos
[![統合TVYouTube支店](http://i.gyazo.com/4c4ffa07ba8a0ea1846a2e76be02284e.png)](http://gyazo.com/4c4ffa07ba8a0ea1846a2e76be02284e)
    - ウェブサイトへのアクセスから結果の見方まで、操作の一挙手一投足がわかります。
        - 講義・講習などの参考資料や後輩指導の教材として利用できます。
        - 本講習中、本家サイトが繋がらない時は、統合TVのYouTube版を見ればおおよその内容がわかるようになっています。
        - 今回の講習に関連する内容の多くは、[統合TVのゲノム・核酸 配列解析 カテゴリー](http://togotv.dbcls.jp/ja/genome.html)にあります。
        - 過去の講習会の内容はそのほとんどが[統合TVに収録](http://togotv.dbcls.jp/ja/lecture.html)されており、いつでもどこでも繰り返し復習できるようになっています。
    - お探しの動画が見つからない or 統合TV未掲載の場合は、[統合TV番組リクエストフォーム](http://togotv.dbcls.jp/ja/contact.html)へどうぞ!!
    - **統合TVを作ってみたい方、募集中**です。ご連絡下さい。

----

## ゲノム配列を探す

さまざまな生物種のゲノム配列が解読されています。それを自らの研究に利用しない手はありません。その利用の第一歩としてそれを探してくる方法を学びます。

### NCBI
- NCBI(National Center for Biotechnology Information)
	- http://www.ncbi.nlm.nih.gov/
- アメリカ合衆国の予算(NIH)による分子生物学情報のリソース
- いろんな調べ物、基本ここから

####【実習1】NCBIからゲノム配列を検索、取得する

1. **中東呼吸器症候群**の原因ウイルスのゲノム配列を取得しましょう。日本語しかわからない場合は、NBDCの[データベース横断検索](http://biosciencedbc.jp/dbsearch/)から英語名を調べましょう。その結果、出てくる``Middle East respiratory syndrome``でNCBIから検索します  
[![Gyazo](http://i.gyazo.com/4b14584d8cae14de8717a5b1b31d21af.png)](http://gyazo.com/4b14584d8cae14de8717a5b1b31d21af)


2. 検索結果を見ましょう。それぞれのDBの横にある数字は、検索ヒット数です。ゲノム配列が得たいので、``Genome``の項目(ヒット数1件)をクリックして詳細を取得します  
[![https://gyazo.com/59d401eee38017a64719e9ae631ff113](https://i.gyazo.com/59d401eee38017a64719e9ae631ff113.png)](https://gyazo.com/59d401eee38017a64719e9ae631ff113)


3. Middle East respiratory syndrome coronavirusのゲノム構造と各種リンクが表示されます。``RefSeq``のところにあるIDをクリックするとRefSeq(リファレンス配列(Reference Sequence)のデータベース)のレコードが表示されます  
[![Gyazo](http://i.gyazo.com/fcc3c14b8158238233cd4b6087866db8.png)](http://gyazo.com/fcc3c14b8158238233cd4b6087866db8)

4. 得られるRefSeqのレコードを見ましょう。ゲノムにコードされているタンパク質配列などを確認しましょう  
5. そのレコードの一番下にゲノム配列が記述されています。ゲノム塩基配列を抜き出すには、最上部の``FASTA``をクリックします  
[![Gyazo](http://i.gyazo.com/cd454ae926b1299e37680aaa7dc1906f.png)](http://gyazo.com/cd454ae926b1299e37680aaa7dc1906f)


6. MERSコロナウイルスのゲノム配列が得られました!  
[![Gyazo](http://i.gyazo.com/20fe76da0752e3b5abafcb632c3f69db.png)](http://gyazo.com/20fe76da0752e3b5abafcb632c3f69db)

蛇足: [GOLD(Genomes Online Database)](https://gold.jgi-psf.org/)というゲノム塩基配列解読プロジェクトを集めたデータベースを使うと、すでに終了したプロジェクトだけでなく、現在進行中のゲノムプロジェクトやメタゲノムプロジェクトについても調べることができます
[【参考】GOLD -Genomes Online Database- の使い方(統合TV)](http://togotv.dbcls.jp/ja/20150515.html)

----
##ゲノム配列から探す
ゲノム配列が得られてもその中から欲しい領域を目で見つけてくること(眼grep(「めグレップ」)と呼んでいます)は容易ではありません。そこで、コンピュータの力を借りることになります。

### Web上で
- BLAST(Basic Local Alignment Search Tool)
	- http://blast.ncbi.nlm.nih.gov/
	- 前世紀から使われている配列類似性検索のデ・ファクト・スタンダード
	- かつては遠縁の配列相同性を検出するためのツール
	- 今はほぼ完全一致を探すために用いられることも多い

[![Gyazo](http://i.gyazo.com/0805e3f1ea046192de5a52cac47dce58.png)](http://gyazo.com/0805e3f1ea046192de5a52cac47dce58)
(スライド出典: [「配列解析基礎」 by 坊農秀雅](http://www.slideshare.net/sayamatcher/140905bono))

####【余談】なぜ相同性じゃなく類似性か
- 遺伝学では、相同性という言葉はタンパク質のアミノ酸配列や遺伝子の塩基配列が共通の祖先をもつときに用いる
- バイオインフォマティクスでは、タンパク質やDNAでの相同性は、配列類似性に基づいて判断される
	- http://togetter.com/li/307635
	
[![Gyazo](http://i.gyazo.com/883c9871790d3a201513809d9eb38adc.png)](http://gyazo.com/883c9871790d3a201513809d9eb38adc)

- 現在(2016年1月)のBLASTウェブインターフェース
	- Assembled Genomesに対する生物種ごとのBLAST検索が上位に
	- Basic BLAST(以下に説明)が下の方に

[![Gyazo](http://i.gyazo.com/cf4ffab8417471c36c940d2c31fdbf40.png)](http://gyazo.com/cf4ffab8417471c36c940d2c31fdbf40)
(スライド出典: [「配列解析基礎」 by 坊農秀雅](http://www.slideshare.net/sayamatcher/140905bono))

- GGGenome
	- 「じぇじぇじぇのむ」と読みます(参考: [GGRNA](http:/ggrna.dbcls.jp/)(「ぐぐるな」))
	- http://gggenome.dbcls.jp/
	- 上記のAssembled Genomesに対する高速検索のツール
	
####【実習2】GGGenomeを使ってゲノム配列から探す

1. http://gggenome.dbcls.jp/ にアクセスします  
[![Gyazo](http://i.gyazo.com/f0ffa1901878ade96d9f4274b235eb86.png)](http://gyazo.com/f0ffa1901878ade96d9f4274b235eb86)

2. ``CTGACGGTCA``(10塩基)を入力して「検索」ボタンを押します。この塩基配列がヒトゲノム中で何回出てくるか、簡単にわかります  
[![Gyazo](http://i.gyazo.com/ca47196af2a9e98a291a7a68ff69177d.png)](http://gyazo.com/ca47196af2a9e98a291a7a68ff69177d)

3. 検索ボタンの右にある生物種を``S.cerevisiae``にして検索しなおしましょう。ヒット数はどう変化するでしょうか?  
[![Gyazo](http://i.gyazo.com/0d519de6d1c0fa8982ff55d8e3b9eae3.png)](http://gyazo.com/0d519de6d1c0fa8982ff55d8e3b9eae3)

4. 染色体と位置のところにリンクがあり、これをクリックするとUCSC Genome Browserの該当箇所になります。その使い方は次節で説明します  

- [【復習用】高速配列検索 GGGenome《ゲゲゲノム》の使い方(統合TV)](http://togotv.dbcls.jp/ja/20131025.html) 
- English version available here -> [GGGenome: a fast and simple DNA sequence search engine(TogoTV)](http://togotv.dbcls.jp/ja/20150514.html)

### (参考)LocalBLASTで
検索する質問配列の数が多くなると、いちいちウェブブラウザを開いて貼り付けてクリックして…が大変になります。それを克服する方法として、Local(自分のパソコン)にBLASTのプログラムをインストールしてBLASTを実行する方法(``LocalBLAST``)があります。[詳しくはこちらの資料](
http://motdb.dbcls.jp/?AJACS32%2Fbono#e17b6eed)を御覧ください。実際にセットアップする統合TVもそこから紹介しています。

----
## アノテーションを足して見る
ゲノム解読がなされて終わりではありません。どこに遺伝子がコードされているか、転写因子の結合領域はどこかなど、ゲノム上の座標に対して注釈付けがなされていきます。それが``ゲノムアノテーション``です。

### ゲノム配列にはバージョンがある
当然最新のものが一番ゲノム配列としては正確なものになっているはずなのですが、**ゲノムアノテーションが最新のものに対しても遅滞なくきちんとなされているわけではなく**、利用目的によってうまく選択しないといけないのが現状です。

 - Human
	 - GRCh38/hg38
	 - GRCh37/hg19
 - Mouse
	 - GRCm38/mm10
	 - NCBI37/mm9

### ゲノムブラウザ
それを見る方法としてゲノムブラウザが使われます。ここではウェブブラウザ上で使えるゲノムブラウザとして有名なUCSC Genome Browser(「ゆーしーえすしー げのむ ぶらうざー」)とEnsembl Genome Browser(「あんさんぶる」)の使い方を学びます。

####【実習3】UCSC & Ensembl Genome Browserに隠されたアノテーションを発掘する

- Track HubでFANTOM5, cancer

1. http://genome.ucsc.edu/ にアクセスします  
2. 上部のメニューバーの``Genomes``にマウスをのせると上述のヒトとマウスのアッセンブリが選択できますが、ここでは気にせずそのままクリックします。  
3. groupに``Mammal``、genomeに``Human``、assemblyに``Feb.2009 (GRCh37/hg19)``を選び、search termに``HIF1``と入力すると入力補完されるので、一番上の``HIF1A``を選び、submitボタンを押しましょう  
[![https://gyazo.com/6b98e53d802a833793e674ff37eb21bf](https://i.gyazo.com/6b98e53d802a833793e674ff37eb21bf.png)](https://gyazo.com/6b98e53d802a833793e674ff37eb21bf)

4. HIF1Aがコードされたゲノム上の領域が表示されます
[![https://gyazo.com/bdbbb1a3cb3835e4db052b0c5843528f](https://i.gyazo.com/bdbbb1a3cb3835e4db052b0c5843528f.png)](https://gyazo.com/bdbbb1a3cb3835e4db052b0c5843528f)
これがゲノムブラウザの基本画面です。このページにあるさまざまなボタンなどいろいろと操作して必要な情報を追加したり、見たくない情報を削除したりします。

5. 上部のnavigationボタンでmoveやzoom in/out等できますが、遺伝子名検索でたどり着いた場合、mRNAの領域に拡大されて表示されるので、zoom out ``3x``しておきましょう  
[![https://gyazo.com/1d6b096e08ec68e38ee8fae6e53f0e72](https://i.gyazo.com/1d6b096e08ec68e38ee8fae6e53f0e72.png)](https://gyazo.com/1d6b096e08ec68e38ee8fae6e53f0e72)

6. 画面下の方にあるのがアノテーションです。Phenotype and Literature カテゴリー中の``COSMIC``が'hide'になっているのを``dense``に変えて、``refresh``ボタンを押してみましょう
[![https://gyazo.com/a4130a4abc68b93803584ce5aa2ff8bb](https://i.gyazo.com/a4130a4abc68b93803584ce5aa2ff8bb.png)](https://gyazo.com/a4130a4abc68b93803584ce5aa2ff8bb)

7. そうすると、上部のゲノム領域にこのゲノムアノテーション(COSMIC)が付加されて表示されます(画像中央、赤色)
[![https://gyazo.com/8ae374468cf7f99b684496068319ffd9](https://i.gyazo.com/8ae374468cf7f99b684496068319ffd9.png)](https://gyazo.com/8ae374468cf7f99b684496068319ffd9)

8. dense,squich, pack, fullとなるに連れて、情報量が多くなります。``full``にしてみると…
[![https://gyazo.com/4375db31f539aba1af1af1777546123f](https://i.gyazo.com/4375db31f539aba1af1af1777546123f.png)](https://gyazo.com/4375db31f539aba1af1af1777546123f)

9. この図は見たい情報のところをクリックすると詳細情報が得られます。たとえば、COSMICの気になる部分のIDをクリックすると
[![https://gyazo.com/2b52bd8f59a6b4256f1d069c3b69eff5](https://i.gyazo.com/2b52bd8f59a6b4256f1d069c3b69eff5.png)](https://gyazo.com/2b52bd8f59a6b4256f1d069c3b69eff5)
その個別のアノテーションの詳細情報が見れます。

10. このゲノムアノテーションそのものについて詳しく知りたい場合、さきほどshowに切り替えた選択画面の上にあったリンクをクリックしてみましょう。詳しい説明が得られます  
[![https://gyazo.com/7c21fba54853479d3d648d878f2fd11c](https://i.gyazo.com/7c21fba54853479d3d648d878f2fd11c.png)](https://gyazo.com/7c21fba54853479d3d648d878f2fd11c)
このようにして必要な情報を足していって、自分のほしい情報を得ます。

11. いろいろいじってしまうと元に戻したい時があります。その場合は、``default tracks``ボタンを押すとResetされ、元のゲノムアノテーションに簡単に戻せます  
[![https://gyazo.com/e37518349806c036f070a079b6dfa9cb](https://i.gyazo.com/e37518349806c036f070a079b6dfa9cb.png)](https://gyazo.com/e37518349806c036f070a079b6dfa9cb)

12. このページにあるゲノムアノテーションの検索は、その左の``track search``ボタンから可能です。*cancer*をキーワードに検索してみると…
[![https://gyazo.com/24ef8682285d7879a8025c078f75bede](https://i.gyazo.com/24ef8682285d7879a8025c078f75bede.png)](https://gyazo.com/24ef8682285d7879a8025c078f75bede)

13. さらに、UCSC Genome Browserのサーバー上ではなく、外部で管理されているデータをゲノムブラウザ上に表示することもできます。上部のメニューの My Data の中にあるTrack Hubsをクリックした画面で``cancer``で検索すると以下の様な外部データが利用可能とわかります。
[![https://gyazo.com/0b434ffd362d5f9a846c1de2632a2c4c](https://i.gyazo.com/0b434ffd362d5f9a846c1de2632a2c4c.png)](https://gyazo.com/0b434ffd362d5f9a846c1de2632a2c4c)

14. また、上部のメニューのうち、Viewをクリックして出てくる``Ensembl``をクリックすると、今見ている領域のEnsembl Genome Browserの該当領域へジャンプします  
[![https://gyazo.com/07a9546a5bbf54abc0488348c71cafa9](https://i.gyazo.com/07a9546a5bbf54abc0488348c71cafa9.png)](https://gyazo.com/07a9546a5bbf54abc0488348c71cafa9)
が、HIF1A遺伝子が見当たりません。なぜでしょうか?

15. これはEnsemblに飛んだ先がGRCh38のゲノムアッセンブリで、**UCSC側とバージョンが違っていて座標がずれている**からです。しょうがないので、真ん中のGene:のところで``HIF1A``を検索しましょう。
[![https://gyazo.com/5663fa4c073b5e119ac01a547c0ce1bb](https://i.gyazo.com/5663fa4c073b5e119ac01a547c0ce1bb.png)](https://gyazo.com/5663fa4c073b5e119ac01a547c0ce1bb)
[![https://gyazo.com/f09fea3c99669a41bc3f334ba1022ceb](https://i.gyazo.com/f09fea3c99669a41bc3f334ba1022ceb.png)](https://gyazo.com/f09fea3c99669a41bc3f334ba1022ceb)
【重要】ゲノム配列はバージョンが同じならどこのサイトでも同一ですが、 **アノテーションは提供サイトで異なります**  

16. 左カラムのメニュー中のComparative Genomicsの``Synteny``をクリックすると、ヒトとマウスの間のシンテニーマップが表示されます  
[![https://gyazo.com/7266536d5e87a533918d7e95449e4fee](https://i.gyazo.com/7266536d5e87a533918d7e95449e4fee.png)](https://gyazo.com/7266536d5e87a533918d7e95449e4fee)

- [【復習用】UCSC Genome Browserの使い方〜表示+ENCODE編〜 2012(統合TV)](http://togotv.dbcls.jp/ja/20120528.html)


ここまで出来て時間のある方は、自分の興味のある遺伝子やtrackを試してみましょう。余裕のある方は、[ウイルスの持ち出した宿主の遺伝子配列がコードされている領域をアミノ酸配列レベルでゲノム中から探し当てる 2012(統合TV)](http://togotv.dbcls.jp/ja/20121030.html)で説明されているラウス肉腫ウイルスゲノム配列を取得、その痕跡をニワトリゲノムから探してみるのをやってみましょう。

- [【発展編】UCSC genome browserの使い方～配列取得編～2013](http://togotv.dbcls.jp/ja/20131113.html)
- [【発展編】UCSC Genome Browserの使い方〜wig形式のファイルをトラックとして追加する〜(統合TV)](http://togotv.dbcls.jp/ja/20120116.html)
