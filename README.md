# 成功に大事なのは運か努力か？

## 背景

先日、NHKのオイコノミアの再放送で[「経済学で考える　人生は運か努力か？」](https://hh.pid.nhk.or.jp/pidh07/ProgramIntro/Show.do?pkey=001-20170906-31-21587)という特集を見た。

放送の大まかな内容は[こちらのブログ](https://rinrinshappy.com/jinsei-un-oikonomia)がまとめてくださっている。

気になったのがこちら。
>実際に研究をしたアメリカ経済学者、1945年・フロリダ生まれの、ロバート・H・フランク教授は、参加者10万人の大規模なトーナメント戦で優勝する確率はどのくらいかを調べました。
>
>仮定として、努力や才能としての実力が98％、運が2％とするなら、もっとも実力がある人が優勝する確率は何％くらいになるか？
>⇒21.9％に過ぎませんでした。
>
>つまり78.1％の確率で、優勝した人は実力が最大の人ではなかったと言う事です。

本当だろうか？🤔 実力がある人がもっと勝つのでは...？

## 実験

### プログラミング

- [main.js](https://github.com/yuichiro-yoshida/luck-versus-skill/blob/master/main.js)を作成
    - 131,072人(2^17)のトーナメントを100回実行し、「才能と努力の合計値」が最強ではない人が優勝する確率を調査
    - トーナメント参加者個々人には、才能・努力・運の値をそれぞれ0〜100で付与
    - 個々人のスコアの計算式は、`FS = (49 × CStalent + 49 × CSeffort + 2 × CSluck) / 100` を使用
        - 各CS値には0〜100が入る
        - 出典: [Luck Versus Skill: The Role of Chance in Economic Success](https://sinews.siam.org/Details-Page/luck-versus-skill-the-role-of-chance-in-economic-success) （原著についての記事)
    - main.js の `main()` の引数で、以下を設定可能
        - トーナメント実験の施行回数 (デフォルトは100)
        - トーナメントの回戦数(これにより参加者数も決まる) (デフォルトは17)
        - 各勝負が各参加者の「スコアの大小により重みづけられた確率」で決まるのか、単純なスコアの大小で決まるのか (デフォルトは後者)

### 実行
- 実行環境は　Node.js v8.11.2
- リポジトリをクローンし、 `node main.js`
    - または、[JSFiddle環境](https://jsfiddle.net/0crrv0ar/36/)にてexecボタンを実行すると、F12開発者ツールのコンソールに結果を出力する

### 結果
- 単純なスコアの大小で勝敗が決まる場合、「才能と努力の合計値」が最強の人が優勝する確率が94-99％程度だった
- 「スコアの大小により重みづけられた確率」で勝負が決まる場合、「才能と努力の合計値」が最強の人が優勝する確率はほぼ0％だった
- その他(単純なスコアの大小で勝敗が決まる場合)
    - 最も「才能と努力の合計値」の高い人はおおむね10-20人の層である。それが10人未満の時に、次点の「才能と努力の合計値」が高い人が勝つことがある
    - 優勝に必要な運の値は、トーナメント参加者の数に比例して高くなる
    - 「才能と努力の合計値」が最高ではないのに優勝する人は大抵運のスコアを100持っている

### 考察
大きなところでは番組で放送されたような結果にはならず、どちらかというと直感通り、実力のある人がほとんどのケースで優勝した🤔

トーナメントの参加者数は原著の10万人に対して本実験では131,072人と多く、人数が多いほど勝ち抜くことが難しくなると思われるが、この差が70％以上の勝率の差を生むとは考えにくい。試しに16回戦65,536人のトーナメントで実験を行なった場合、「才能と努力の合計値」が最強の人が優勝する確率はそれでも86%程度だった。

原著邦訳[「成功する人は偶然を味方にする--運と成功の経済学」](https://www.amazon.co.jp/gp/product/B06Y5NKNC9)にも当たってみたが、個々の勝負の勝敗の付け方についてこれ以上の詳細は載っていなかった (=単純なスコアによる勝負だろうか？)。

原著で分からない以上この差がどこから来るかは不明であり、もやもやが残るが、教訓めいたことを得るならば「運に頼らず努力せよ」ということになるだろう:innocent:
