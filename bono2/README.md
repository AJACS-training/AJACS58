# 次世代シーケンサーから得られたデータの使い方 at AJACS薩摩

情報・システム研究機構 ライフサイエンス統合データベースセンター  
[坊農 秀雅](http://bonohu.jp/) bono@dbcls.rois.ac.jp  
2016年1月27日 鹿児島大学桜ヶ丘キャンパス


----

これは統合データベース講習会AJACS薩摩「次世代シーケンサーから得られたデータの使い方」の資料です。 

----

## 概要

本講習は、次世代シーケンサー(NGS)から得られたデータに関して、その使い方に主眼を置き、
1. NGSデータの扱い方とその解釈法、探し方
2. 統計解析環境[R](http://www.r-project.org/)とハイスループットなゲノムデータの解析とそれらを理解するためのツール[Bioconductor](http://bioconductor.org/)を利用したデータ解析する基礎知識
について学びます。 

NGS配列データを直接解析するさまざまな方法論については、本講習のレベルを超えるので[「次世代シークエンサーDRY解析教本」](http://bonohu.jp/blog/2015/10/08/ngs_dat/)などを参考にしてください。

----

## 講習の流れ

講習ではまずNGSデータ解析に関して説明したあと、【実習】を皆さんとやっていきます。早くできてしまった人は、【発展】をやってみたりしてください。今回すでにR本体はすでにインストールされています。

- 昨日の復習
- NGSデータ解析の概要
- よく用いられるNGSの応用
- Sequence Read Archive (SRA)
- R/BioconductorでNGSデータ解析

## 参考
### NGSそのもの

- 清水厚志 **次世代シーケンサーデータの取扱と疾患ゲノム解析の基礎** 統合データベース講習会AJACS津軽 [DOI: 10.7875/togotv.2015.110](http://doi.org/10.7875/togotv.2015.110)
- 鈴木絢子 **次世代シーケンサーを用いたがん細胞のオミクス解析** 統合データベース講習会AJACS米子 [DOI: 10.7875/togotv.2015.090](http://doi.org/10.7875/togotv.2015.090)

 
### NGSデータ解析
-  坊農秀雅 **次世代シークエンサーにより得られたデータの解析** *領域融合レビュー*, **4**, e008 (2015) [DOI: 10.7875/leading.author.4.e008](http://doi.org/10.7875/leading.author.4.e008) 
- 清水厚志・坊農秀雅 監修「次世代シークエンサーDRY解析教本」秀潤社 2015 [ISBN978-4-7809-0920-3](http://bonohu.jp/blog/2015/10/08/ngs_dat/) 

### R/Bioconductor
自分でインストールする際には以下の[統合TV](http://togotv.dbcls.jp/) を参考に行ってください。

![togotv](http://togotv.dbcls.jp/ja/images/logo_togotv15.png)

* [統計解析ソフト「R」の使い方 導入編](http://togotv.dbcls.jp/20090313.html)
* [統計解析ソフト「R」の使い方 導入編(MacOSX)](http://togotv.dbcls.jp/20090618.html)
* [統計解析ソフト「R」の使い方 正規化編](http://togotv.dbcls.jp/20090319.html)
* [統計解析ソフト「R」の使い方 ヒートマップ編](http://togotv.dbcls.jp/20091219.html)
* [統計解析ソフト「R」での立廻り](http://togotv.dbcls.jp/20111107.html)

--
## 昨日の復習

[UCSC Genome Browser](http://genome.ucsc.edu/)開いてTrack Data Hubsで``FANTOM``を検索してみましょう。Track Data Hubsへは、上部メニューの``My Data``のなかの``Track Hubs``からアクセスできるのでしたね。大事なことなので2回言いました。
- 画像をドラッグ&ドロップすると…
- shiftキーを押しながら、 領域を選択すると…

これらも実は次世代シーケンサー(NGS: Next Generation Sequencer)から得られた配列由来のデータです。立派なNGSデータ解析です。では、どうやって作られているか？概略をお話しましょう…。

## NGSデータ解析の概要

NGSそのものの話は過去のAJACSの講義、例えば[AJACS津軽の清水さんの講習](http://togotv.dbcls.jp/ja/20151121.html)を参照してください。

[![leading_authors](http://leading.lifesciencedb.jp/wordpress/wp-content/uploads/2015/05/Bono-4.e008-Fig.2.jpg)](http://dx.doi.org/10.7875/leading.author.4.e008)

出展: 領域融合レビュー, **4**, e008 (2015) [DOI: 10.7875/leading.author.4.e008](http://dx.doi.org/10.7875/leading.author.4.e008) の **図2 データ解析のハブとなるFASTQ形式**

###FASTQ形式
FASTQフォーマット、とも言う。
- 4行/readが基本単位
 - 1行目: @ID (コメント)
 - 2行目: 塩基配列
 - 3行目: +ID
 - 4行目: クオリティ値
- したがって、5000万リード(MiSeq v3) x 4行 = 2億行
 - ファイルサイズも8Gbyteを超えることも
 - FAT32フォーマットでは扱えず、NTFSやexFAT
 - いわゆる「開く」ことが不可能

```FASTQファイルの実例(抜粋)
SRR001356.1 2023DAAXX:5:1:123:563 length=33
TGTCGGTCCAGCTCGGCCTTGGGCTCCGTTTTC
+SRR001356.1 2023DAAXX:5:1:123:563 length=33
-IIIIIIII8IIIIIIIIIII6IIIIIIIII9I
@SRR001356.2 2023DAAXX:5:1:123:476 length=33
TCTGAACCCGACTCCCTTTCGATCGGCCGCGGG
+SRR001356.2 2023DAAXX:5:1:123:476 length=33
IIIIIIIIIIIIIIIIIIIIIGIIIIIII-III
@SRR001356.3 2023DAAXX:5:1:121:746 length=33
GTGGCAGCGTTTTTGGGCCCGCCGCTTGCCGTT
+SRR001356.3 2023DAAXX:5:1:121:746 length=33
IIIII&IIIIIIIIIIIIIIIIHI1IIIIIIII
```

シーケンサーの種類に関係なく、データ解析はFASTQ形式のファイルから、マッピングかアセンブルするのが基本。RNA-seqやChIP-seqというのは配列解読の応用の話で、後述します。

### マッピング (mapping)
- すでに決定されたゲノム配列に対して、手持ちの配列がそのどの部分に相当するか写像(マッピング)すること。
- ゲノム配列決定された生物種では、普通はこちらのアプローチで配列解析する。

### アセンブル (assemble)
- 手持ちの短い配列から元の長い配列(ゲノムなど)を組み立てる(assemble)こと。
- ゲノム配列を決定するプロセスで必要。

### NGSデータ解析に関わるデータフォーマット

|フォーマット名|読み方|拡張子|用途|
|:-----------|:----|:----|---|
|FASTA|ふぁすた or ふぁすとえー|	.faや.fasta	|1行目に“>”で始まるヘッダ行，2行目以降に実際の塩基配列文字列という配列データ形式|
|FASTQ|ふぁすときゅー|	.fqや.fastq	|NGS配列データ形式のデファクトスタンダード．配列クオリティ値付き，４行1エントリ|
|SRA|えすあーるえー|	.sra|	NGS配列データ配布フォーマット．NCBI SRA-toolkitを使ってFASTQを生成できる|
|SAM|さむ|	.sam|	ゲノムマッピングした時に生成されるアラインメントのフォーマット．プレーンテキスト形式|
|BAM|ばむ|	.bam|	ゲノムマッピングした時に生成されるアラインメントのフォーマット．バイナリ形式|
|GTF(GFF)|じーてぃーえふ (じーえふえふ)|	.gtf(.gff)|	ゲノム上のどこに遺伝子があるかなどが記述されたゲノムアノテーションのフォーマット|
|BED|べっど|	.bed	|ゲノム上のどこに遺伝子があるかなどが記述されたゲノムアノテーションのフォーマット|
|VCF|ぶいしーえふ|	.vcf	|Variant Call Format．配列の多型を記述するフォーマット．bcfはvcfのバイナリ版|

UCSC Genome Browser上に出ているTrackは、このBED形式のデータが基本となっています。

## よく用いられるNGSの応用
塩基配列情報が関係する研究分野、すべてに応用されています。以下の様な分野によく使われています。


1. ゲノムの解析(Exome, WGBS(Whole Genome Bisulfite Sequence))
2. トランスクリプトームの解析(RNA-seq)
3. DNA結合タンパク質の結合配列の解析(ChIP-seq)
4. メタゲノムの解析


[![leading_authors](http://leading.lifesciencedb.jp/wordpress/wp-content/uploads/2015/05/Bono-4.e008-Fig.1.jpg)](http://dx.doi.org/10.7875/leading.author.4.e008)

出展: 領域融合レビュー, **4**, e008 (2015) [DOI: 10.7875/leading.author.4.e008](http://dx.doi.org/10.7875/leading.author.4.e008) の **図1 公共データベースSRAへのエントリー数を研究分野ごとに分類したもの**

### RNA-seq

- RNA-seqという言葉が広く流布
 - Transcriptome sequencing(transcriptを配列解読して出現回数を発現強度とする解析)の意味であることが大半

#### ごく簡単な解析の流れ

1. Reference genome へ transcript を mapping
2. Splice alignment (Bowtie & Tophat)
3. (既知の)転写単位ごとの発現情報化(cufflinks)
4. 可視化(cummeRbund) 

RNAseqデータ解析の流れ
[![https://gyazo.com/853b91e878481a618b508d649b6b62b2](http://i.gyazo.com/853b91e878481a618b508d649b6b62b2.png)](https://gyazo.com/853b91e878481a618b508d649b6b62b2)

参考: マイクロアレイデータ解析の流れ
[![https://gyazo.com/b994c7bfe73d69daf17d05a01ebab593](http://i.gyazo.com/b994c7bfe73d69daf17d05a01ebab593.png)](https://gyazo.com/b994c7bfe73d69daf17d05a01ebab593)

### Exome

- DNA-seqとはあまりいわず、主にExome(エキソンの部分だけResequence)

#### ごく簡単な解析の流れ(ヒトやマウス)
1. データのクレンジング
2. Reference genomeへのmapping (BWA)
3. 変異(SNV:Simple Nucleotide Variation)をcall
4. 変異のアノテーション

詳しくは、データ解析教本p163の図を参照

### ChIP-seq

- ChIP: Chromatin ImmunoPrecipitation(免疫沈降)
- ターゲットのタンパク質
 - ヒストン
 - 転写因子

#### ごく簡単な解析の流れ
1. Reference genome へmapping
2. peak call (MACS2)

### メタゲノム

- 細菌叢の全ゲノムを解析
- 16S rRNAのみを解読。細菌の割合を解析

#### ごく簡単な解析の流れ
1. シーケンスリードをアッセンブル
2. タンパク質配列をコードするORF(Open Reading Frame)を見いだす
3. 既知の遺伝子配列に配列類似検索
4. KEGGやCOGなど分類のためのDBを用いて機能分類

## Sequence Read Archive (SRA)

NGS解析したら、それは最終的にはデータベースに登録することになる。これまでの塩基配列登録と同じく、NCBI/EBI/DDBJが登録業務を行っている。日本からならDDBJに登録しましょう。

### DDBJ Sequence Read Archive

DDBJのSequence Read ArchiveはDRAとも呼ばれ、[以下のウェブサイト](http://trace.ddbj.nig.ac.jp/dra/)から登録や簡単な検索ができます。

[![https://gyazo.com/cbb761ff307c1072b973f07d58282a63](http://i.gyazo.com/cbb761ff307c1072b973f07d58282a63.png)](https://gyazo.com/cbb761ff307c1072b973f07d58282a63)

### DBCLS SRA

SRAからデータを探すときに便利なツールを我々DBCLSで作成しています。それがこの[DBCLS SRA](http://sra.dbcls.jp/)です。

[![https://gyazo.com/83abfff821baa5a2bbdca99d8abe8f3d](http://i.gyazo.com/83abfff821baa5a2bbdca99d8abe8f3d.png)](https://gyazo.com/83abfff821baa5a2bbdca99d8abe8f3d)

新しいバージョン(New version)のところをクリックして、新しい方で検索してみましょう。

[![https://gyazo.com/e6f63c8b1380231d47063ed74bed5605](http://i.gyazo.com/e6f63c8b1380231d47063ed74bed5605.png)](https://gyazo.com/e6f63c8b1380231d47063ed74bed5605)

【実習1】DBCLS SRA で興味あるNGSデータを探す

1. Trends&Search SRA dataで for more detailsをクリック → 最新の統計情報を見てみましょう
2. Free Keywordで検索してみましょう。例えば``hypoxia``
3. Full Publication Listをクリックして見ましょう

以上のように、DBCLS SRAでは各データに付与された実験手法や実験条件といったメタデータ(「データ」のデータ)に対して検索する手段を提供しています。逆に、メタデータがきっちりとついていないとそのデータは **無いのと同じ** ということになります。この種のデータは誰かが親切に付けてくれるものではなく、上述のDDBJ SRAに登録するときにそのデータを出した研究者が付けるべきものです。

【実習2】マイクロアレイデータも含めた遺伝子発現データの検索に[AOE(All of gene Expression)](http://aoe.dbcls.jp/)が便利です。

1. ヒトをクリック、年数をドラッグ
2. Illumina+others => NGSのみのデータ
3.  ``hypoxia``で検索

[【参考】AOEを使って遺伝子発現データベースの統計を見ながら検索する(統合TV)](http://doi.org/10.7875/togotv.2014.096)

実は、自分で生データを取得して配列から解析しなくてもNGSデータは使えます。すでに解析済みのデータを使うやり方です。それらの手段を以下に紹介します。

- Genome BrowserのTrack
 - 昨日詳しく実習し、本日冒頭でも復習。ゲノム配列に付与されたデータを閲覧する際の基本中の基本だからです
- RNA-seqだとRefExのRNA-seqやFANTOM5 CAGE
 - 昨日の遺伝子発現の講習でも出てきましたが、実はNGSデータの利用例でした
 - [【参考】RefExの使い方(統合TV)](http://doi.org/10.7875/togotv.2014.009)
- ChIP-seqだと[ChIP-Atlas](http://chip-atlas.org/)

【実習3】ChIP-Atlasを使って公共ChIP-seqデータを利用する
4つあるサービスのうち、2つを実習します。

- Target Genes
 - Antigen(遺伝子名)を選んで(例: HIF1A)、View Potential Target Gene'をクリックしてみると…
 - 戻って、"Choose Distance from TSS"を現在の±1kから±5kにしてみましょう
- Colocalization
 - 同様にAntigenを選んで(例: HIF1A)、colocalizeするタンパク質の予測結果を見てみましょう
 - Cell type classを変えて予測結果を見てみましょう

Peak Browserに関してはIGVがインストールする必要があるので、やって見せたいと思います。

## R/BioconductorでNGSデータ解析

Rに関しては過去のAJACSの講義、例えば[AJACS津軽の坊農の講習](http://doi.org/10.7875/togotv.2015.112)を参照してください。
無事、生配列データの処理ができた場合にその後はマイクロアレイデータ解析と同じく、データの解釈が必要になります。それに関してRを用いた解析を実習します。

### 主成分分析(PCA)
PCA(Primary Component Analysis)。 このパートは[ぼうのブログ「RでPCA」](http://bonohu.jp/blog/2013/07/13/pcaonr/)を参考に。

【実習4】Rを起動し以下のファイルに記述されたRのコマンド(`03pca.r`)を実行しなさい。データファイルとして必要な`RMA.txt`は【発展2】で作成したものを利用すればよいのですが、現在作業しているディレクトリにおいておく必要があります。  
この発展課題をやらなくても実行できるように用意してあり、`RMA.txt.zip`というファイルをダブルクリックすることで解凍(圧縮を解く)すると`RMA.txt`というファイルが生成されるようになっています。  
PCAを実行するには、以下のRスクリプトを実行します。

    #タブ区切りのデータを読み込み
    data <- read.table("RMA.txt", header=TRUE, row.names=1, sep="\t", quote="") 
    #主成分分析を実行
    data.pca <- prcomp(t(data))
    #名前を得る
    names(data.pca)
    #標準偏差をプロット
    plot(data.pca$sdev, type="h", main="PCA s.d.")
    #行列を転置
    data.pca.sample <- t(data) %*% data.pca$rotation[,1:2]
    #PCAの結果をプロット
    plot(data.pca.sample, main="PCA")  
    #ラベルに色付け
    text(data.pca.sample, colnames(data), col = c(rep("red", 3), rep("blue",3),rep("green",3),rep("black",3)))
    
一行目でエラーの出る人は、コンピュータに`RMA.txt`ファイルの位置を指示できていないことが多いです。`setwd()`コマンドで`RMA.txt`をコピーしたディレクトリ(フォルダ)を指示します。

図に.CEL.gzの文字がいっぱい入っていて見づらい?そう思った方は[こちらを参照](http://bonohu.jp/blog/2014/09/10/afterjustrma/)

### RNAseqデータ解析(cuffdiffの結果可視化)
cufflinksパッケージに`cuffdiff`という発現データの差分を計算するプログラムがあります。それを実行したあとのデータを可視化する手段として使うBioconductorのパッケージに`cummeRbund`があります([cuffdiffの使用例](http://dx.doi.org/10.1371%2Fjournal.pone.0104283))。

* 参考: [bonohuの発表資料「NGS解析(RNAseq)」](http://dx.doi.org/10.6084/m9.figshare.1216717)

【実習5】Rを起動し以下のファイルに記述されたRのコマンドを実行しなさい。データファイルとして必要なcuffdiffディレクトリ以下のファイルは手持ちのものか、なければサンプルをUSBメモリでお渡しします。現在作業しているディレクトリにおいておく必要があります。

    #Bioconductorを使うときの呪文
    source("http://bioconductor.org/biocLite.R")
    #cummeRbundをインストール
    biocLite("cummeRbund")
    #cummeRbundを召喚
    library("cummeRbund")
    #cuffdiffの結果のディレクトリを指定
    cuff.dir <- "cuffdiff"
    #cuffdiffの結果の読み込む
    cuff <- readCufflinks(dir=cuff.dir)

準備はここまでで、

    cuff

で、読み込んだデータのサマリが見れます。以下、解析事例です。

    #発現密度分布のプロット
    dens <- csDensity(genes(cuff))
    dens
    
    # サンプル方向のデンドログラム
    dend <- csDendro(genes(cuff))
    
    #CSV形式でFPKM値を出力
    gene.matrix <- fpkmMatrix(genes(cuff))
    write.csv(gene.matrix, file="fpkm.csv")
    
詳しくは、マニュアルを読みましょう。

    ?cummeRbund
    
### R Graphical Manualのすゝめ
どんなライブラリがあって、どういった可視化ができるかは[R Graphical Manual](http://rgm3.lab.nig.ac.jp/RGM)が大変便利です。このウェブサイトは国立遺伝学研究所の小笠原理さんによって維持されているRのライブラリに記載されているデモデータをあらかじめ計算して得られるイメージファイルをウェブから閲覧できるというもので、そのライブラリが激しくバージョンアップがなされるRにおいて、現在使用可能かどうかを知る上でも大変有用なものです。

【実習6】ウェブブラウザを起動し、インターネット検索でR Graphical Manualを検索してサイトに辿り着き、サイト内の検索フォームからキーワードcummeRbundで検索しなさい。どのような結果が返ってきたか?前節で紹介したcsDensityのエントリを見つけてみなさい。

【参考】[統計ソフトEZR](http://www.jichi.ac.jp/saitama-sct/SaitamaHP.files/statmed.html)。生存解析、ROC曲線解析、メタアナリシス、サンプルサイズの計算など、医療統計で役立つ解析に特化
