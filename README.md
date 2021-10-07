# ProbSpace 米国株式市場 将来株価予測
[ProbSpace 米国株式市場 将来株価予測](https://comp.probspace.com/competitions/us_stock_price) コンペのリポジトリ

- directory tree
```
US_StockPricePrediction
├── data    <-- gitで管理するデータ
├── data_ignore <-- gitで管理しないデータ
├── notebooks
└── src <-- .ipynb 以外のコード
```

## Info
- [Kaggle日記という戦い方](https://zenn.dev/fkubota/articles/3d8afb0e919b555ef068)
  - READMEの記述参考

## Memo
- term
  - nb:ノートブック
- 予測対象週の直前のデータを提出した場合のscoreは`0.03985`らしい

## Basics
### **概要**
本コンペティションでは、米国証券取引所の株価推移データを用いて、1週間後の株価を予測するアルゴリズム開発に挑戦いただきます。

### **目的・背景**
この10年で証券会社にとって、株価動向を予測するテクニカル分析へ機械学習モデルを用いることは、当たり前とも言える時代となりました。
今ではWealthNavi・大和証券など、多くの証券会社で機械学習モデルを搭載したロボアドバイザーがサービス提供されており、機関投資家だけではなく多くの個人投資家にとっても身近なものとなりつつあります。

さてこうしたテクニカル分析ですが、"モデル精度の向上"や"話題作り" といった目的で、国内外問わず様々なイベントでコンペティションが開催されております。
しかしながら通常スポンサー付きのコンペティションにおいては、知的財産権の都合上アルゴリズムを公開したり、自己投資への流用が許されないケースがほとんどでした。

そこで今回は、Open Review CompetitionであるProbSpaceの強みを活かし、誰でも自由に優勝者アルゴリズムを使えるよう、あえて定番である株価予測コンペを開催することといたしました。
MITライセンス化を優勝条件と定めておりますため、コンペ終了後、モデルを自由にご活用いただいて問題ございません。（優勝された方は、当ルールについてご了承願います）

株式投資に興味を持っていただく機会となり、また既に投資を行われている皆様にとっても有益なコンペティションとなれば幸いです。

### **課題内容**
2011/11/13～2019/11/17週の計419週間にわたる米国株データをもとに、2019/11/24週の終値を予測いただきます。
今回のコンペにおいては、純粋な時系列データ解析スキルの競技を目的とし、株価・ファンダメンタル情報に関する外部データの使用は不可といたします。
（外部データの使用も含めたコンペティションについては、また別の機会での企画を考えております）
ぜひとも、ご参画ください。

### **参考資料等**
- 門脇大輔 他『Kaggleで勝つデータ分析の技術』2.2.3節, 5.3章
- キヨシの命題ー時系列データに対する特徴量エンジニアリング手法のまとめ

### **Data**
当コンペティションでは、下記3種類のデータが提供されます。

訓練データ(train_data.csv)
企業リスト(company_list.csv)
提出テンプレート(submission_template.csv)
訓練データには、3,278銘柄の米国株それぞれについて、2011/11/13～2019/11/17週の終値が計419期分含まれています。

提出ファイル例を参考に、に2019/11/24週の終値、つまり2019/11/29の終値を予測し、ご提出ください。

#### **データ形式**
3-4文字のアルファベットは、ニューヨーク証券取引所、NASDAQ、アメリカン証券取引所の証券コードです。
- 訓練データ(train_data.csv)
- 企業リスト(company_list.csv)
  - 米国における、2020年4月時点での各証券取引所取り扱い企業一覧です。
  - 訓練データに含まれていない企業も掲載されています。
- 提出テンプレート(submission_template.csv)
  - 提出用のテンプレートファイルです。
  - 予測された2019/11/24週の終値を入力し、ご提出ください。
  - （RMSLEでの評価となるため、値がマイナスとなる場合は提出エラーとなります。ご注意ください）

## Log
### 20211004
- join!
- いくつかの銘柄について、時系列でプロットして見てみる(nb001)
  - 上昇トレンド、下降トレンドなど類似した動きの銘柄がありそう？
    - クラスタリングしてモデル分けるのもあり
- ひとまず予測して提出してみた(nb002)
  - train_data.csvの全てを学習データとしてラグ特徴量を作成して予測した
  - 課題：train_data.csvをtrain, validation, testに分割して学習をする