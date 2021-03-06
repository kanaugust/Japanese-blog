テキスト・データを簡単にクリーン・アップしながらExploratoryのベータ版に世界中から登録してくれたユーザーの普段使っているデータ分析ツール上位ランキングを出してみた

おかげさまで現在、世界中からたくさんの人たちにExploratory Desktopのベータ・トライアルの方にサインアップしていただいています。もしまだサイン・アップしてなくて興味のある方はぜひ[こちら](http://docs.exploratory.io/tutorials/flight4.html)からどうぞ。
ところで、サインアップしていただく時に、皆さんの普段使っているデータ分析ツールが何か、聞かせてもらっています。そのデータがこちらにあるので、それを元にどういったツールが今世界中で人気があるか出してみたいと思いますが、実はいくつか面倒くさい問題があります。

- カンマ区切りなので、単純にツールごとに集計できない
- フリーフォームなので、スペースがいろんなとこに入ってたり、英語の大文字、小文字が混じってて、実は同じ名前であるのに同じ名前としてカウントできない。

![](images/favtool1.png)

こういったデータって結構データ分析をやっていると普通だったりするのですが、Exploratoryを使うと簡単にクリーン・アップすることができます。クリーン・アップした最後にはトップ５のデータ分析ツールを出してみたいと思います。

##1. カンマ区切りなので、単純にツールごとに集計できない

今のままだと、1つの文字列になっているため、複数のツールが書かれている場合でも別々のツールとして計算することができません。なので、str_sprit関数を使って、一つの文字列になってるものを複数の文字列に変換したいと思います。
![](images/favtool.png)


これは、textに対するコマンドなので、Working with Text functionを選び、str_spritを選びます。
![](images/favtool2.png)

str_spritによって一つの文字列になってるものを複数の文字列に変換することができ、データタイプもlistになりました。
![](images/favtool3.png)

でも、今のままだと1行にR, Excel, tabeleau, pythonが入っていて、それぞれのツールごとの個数を計算することができます。なので、この入れ子構造になっているのを、一回ブレイクして、R, Excel, tabeleau, python をそれぞれの行に落としこむ必要があります。unnestコマンドを使うとそれをすることができます

![](images/favtool4.png)

カラムのヘッダーからunnestをクリックします。

![](images/favtool5.png)

これで、unnestコマンドによって入れ子構造じゃなくなりましたね。

![](images/favtool6.png)

##2.実は同じ名前であるのに同じ名前としてカウントできない。

この状態で、チャート画面で、一度ビジュアライズしてみます。

![](images/favtool-chart.png)

すると、上位に小文字と大文字のRがあったり、スペースが入り混じっているせいで、実は同じ名前であるのに同じ名前としてカウントできていませんね。

テーブル画面でも、同じPythonでもpythonになっていたり、Pythonになっていたり、PYTHONになっていたりして、同じPythonを表しているのに、英語の大文字、小文字が入り混じっているために同じものとして計算できなくなっています。なので、str_title関数を使って、タイトルを統一したいと思います。

![](images/favtool7.png)

これは、textに対するコマンドなので、Working with Text functionを選び、そこから、str_titleを選びます。

![](images/favtool8.png)

str_titleによって、Pythonに統一されましたね。
![](images/favtool9.png)

次に、このようにスペースがいろんなとこにはいっていますね。このままだと、実は同じ名前であるのに同じ名前としてカウントできません。str_trim関数を使って、スペースを取り除きたいと思います。

![](images/favtool10.png)

これは、textに対するコマンドなので、Working with Text functionを選び、そこから、str_trimを選びます。

![](images/favtool11.png)

str_trimによって、スペースが取り除かれましたね。
![](images/favtool12.png)


##3.上位ランクのデータ分析ツールを出す

これから、ユーザーの上位ランクのデータ分析ツールを出してみたいと思います。

Exploratoryを使って簡単にクリーン・アップすることができました。しかし、それでも、NA値と呼ばれるような、空の値などの計算することができないデータがあります。トップ５のデータ分析ツールだけを出したいので、そういう場合は、NA値を排除しましょう。

![](images/favtool20.png)

これは、NA値に対するコマンドなので、Working with NAを選び、そこから、Remove NAを選びます。

![](images/favtool21.png)

Remove NAによって、NA値が取り除かれましたね。
![](images/favtool22.png)

これで、ビジュアライズしてみます。
![](images/favtool23.png)

数が多いので、上位だけにズームしてみます。上位から順に、R、Python, Excel, Tableau, Sqlであることがわかりました。
![](images/favtool25.png)


RのフロントエンドとしてRの世界だけで話題になっているのかなと思っていましたが、どうやらExcel、Tableau等、既存のBIツールで提供される簡単なデータ分析以上のことをやってみたい、もしくは必要という方々も結構いるようです。

##興味を持っていただいた方、実際に触ってみたい方へ

Exploratoryは[こちら](http://docs.exploratory.io/tutorials/flight4.html
)からβ版の登録ができます。こちらがinviteを完了すると、ダウンロードできるようになります。

チュートリアルは[こちら](http://docs.exploratory.io/tutorials/intro.html
)から見ることができます。

英語が読める方は[Introducing Exploratory Desktop — UI for R](https://blog.exploratory.io/introducing-exploratory-desktop-ui-for-r-895d94ef3b7b#.4dncgv1rt
)もどうぞ




