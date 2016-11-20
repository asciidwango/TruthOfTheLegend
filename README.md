# Truth of the Legend アフターサービス

2016/05/04 A.Fujita

１２年ぶりの「Unix考古学」いかがだったでしょうか？

5/10 の「Unix考古学」の夕べの講演資料を
[ここ](TruthOfTheLegend-20160510.pdf)
に置いておきます。

5/31 の「Unix考古学」の夕べ２の講演資料を
[ここ](TruthOfTheLegend-20160531.pdf)
に置いておきます。

6/28 の「Unix考古学」の夕べ in 福岡の講演資料を
[ここ](TruthOfTheLegend-20160628.pdf)
に置いておきます。

7/23 の「Unix考古学」の夕べ in JUSの講演資料を
[ここ](TruthOfTheLegend-20160723.pdf)
に置いておきます。

7/30 の OSCKyoto "Implementation of 4.4BSD luna68k" の講演資料を
[ここ](TruthOfTheLegend-20160730.pdf)
に置いておきます。

11/12 の KOF "Implementation of 4.4BSD luna68k" の講演資料を
[ここ](TruthOfTheLegend-20161112.pdf)
に置いておきます。

「Unix考古学」で紹介している文献のリストを
[ここ](papers.md)
に置いておきます。

## 連載記事の「実習編」の記事
単行本の「あとがき」に書いたように、
単行本には収録しなかった連載記事の「実習編」の記事を
連載時の校正前原稿をそのまま掲載しています。

付録の CDROM が残っていない、
当時の実行環境がない・・・等の問題により
記事どおりの挙動をしない場合があるので
注意してください。


### 7th Edition Unix の実習
現在、CentOS6 を使って再現を試みています。
第７回については若干の修正で動作することを確認していますが、
第８回の「カーネルの構築」ところでトラブってます。（笑）

今後、随時確認を行って報告する予定です。

* [第7回　Seventh Edition Unixを体験する 2003年11月](practice/200311-07.md)
    - 取り敢えず Seventh Edition を起動してみる
    - Seventh Editionのフルインストール
    - 簡易 shutdown コマンドの作成

* [第8回　Seventh Edition での環境構築   2003年12月](practice/200312-08.md)
    - Seventh Edition Unix のセットアップについて
    - カーネルの構築
    - dz ドライバの追加

* [第9回　Seventh Edition Unixで学ぶ    2004年１月](practice/200401-09.md)
    - タイムゾーンの変更
    - date コマンドの Y2K 問題対応
    - shutdown コマンドふたたび

### 2BSD の実習

* [第12回　Second Berkeley Software Distribution 2004年４月](practice/200404-12.md)
* [第13回　2BSDのex/vi                           2004年５月](practice/200405-13.md)
* [第14回　Berkeley Pascal System                2004年６月](practice/200406-14.md)

---

## VAX-11/780のエミュレーション

### SIMHふたたび
連載終了後、長らくご無沙汰していたSIMHですが、
連載終了時の 3.0-1 から大きくアップデートされていて、
最新リリースは 3.9-0 になっています。

もっとも、2012年に公開されたこのリリースは、
どうやら Pre-4.0 の位置付けでもあるかのように
[バグが多く](http://simh.trailing-edge.com/interim/)
、さらにGitHubでは
[SIMH v4.0 - Beta](https://github.com/simh/simh)
の開発も進行しているところから、
「SIMH、どのバージョンを使うべきか？」は
相変わらず悩ましい問題です :-)

で、インターネットでSIMHを使ったエミュレーションを
ググって見ると様々な紹介記事が見つけられますが、どうやら
[SIMH v3.8-1](http://simh.trailing-edge.com/sources/simhv38-1.zip)
を使っている事例が多い気がするので、
これが stable version と考えて良さそうです。

### 個人的な思い入れ（笑）
個人的に最近の SIMH で最も魅力を感じるのは  
VAX-11/780 のエミュレーションがサポートされたことです。

連載時にサポートされていた VAX エミュレーションは
このアーキテクチュアの後期のハードウェア実装にあたる
Micro VAX のエミュレーションでした。
このエミュレーションはプロセッサの互換性はあるものの、
周辺デバイスを接続する IO バスは Q-Bus でしたので、
初期の VAX-11 と銘打たれたハードウェアシリーズのために
開発された Unix 32/V から一連の BSD Unix のカーネル実装は
動作しません。なぜなら、このシリーズの IO バスは PDP-11
のために開発された UNIBUS が搭載されていたからです。
つまり、ディスクやテープといった周辺ＩＯ機器のための
デバイスドライバは全てなんらかの修正をする必要があったからです。

SIMHでVAX-11/780のエミュレーションがサポートされたのは
v3.5からのようです。（初出はv3.3だったようですが、v3.4
では一旦サポートから外されていたようです）このサポートでは
もちろんVAX-11のシリーズに搭載されていたSBI/MASSBUS/UNIBUSも
エミュレートされます。つまりデバイスドライバもそのまま使える。

というわけで・・・

連載時には泣く泣く見送った Unix 32/V から 4.3BSD の
エミュレーションの紹介記事を書く環境が整いました。

### VAX-11/780のエミュレーションの紹介記事
手始めに、
一連の「VAX-11/780のエミュレーションの紹介記事」を追跡してみました。

SIMHを使ったVAX-11/780のエミュレーションの紹介のなかで
もっとも古いものは浜田直樹さんの手による紹介記事
(http://zazie.tom-yam.or.jp/starunix/)
のようです。この記事では次の３つのUnixリリースの
エミュレーション方法が紹介されています。

* [32V](http://zazie.tom-yam.or.jp/starunix/32v/32v.html)
* [3BSD](http://zazie.tom-yam.or.jp/starunix/3bsd/3bsd.html)
* [4.0BSD](http://zazie.tom-yam.or.jp/starunix/4.0bsd/4.0bsd.html)

作業に必要な一連のコードは
(http://zazie.tom-yam.or.jp/starunix/starunix.tar.bz2)
に収められています。

ちなみに浜田直樹さんは、単行本の第10章でも紹介している
["A UNIX™ Operating System for the DEC VAX-11/780 Computer"](https://www.bell-labs.com/usr/dmr/www/otherports/32v.html)
のHTMLレンダリングにもコントリビュートされてます。

この浜田さんの作業は
gunkies.orgの[Computer History Wiki!](http://gunkies.org/wiki/)
でも以下のとおり紹介されています。

* [Installing 32v on SIMH](http://gunkies.org/wiki/Installing_32v_on_SIMH)
* [Installing 3 BSD on SIMH](http://gunkies.org/wiki/Installing_3_BSD_on_SIMH)
* [Installing 4.0 BSD on SIMH](http://gunkies.org/wiki/Installing_4.0_BSD_on_SIMH)

さらに彼（おそらくドイツの方だと思います）は
以下の作業手順も紹介してます。

* [Installing 4.1 BSD on SIMH](http://gunkies.org/wiki/Installing_4.1_BSD_on_SIMH)
* [Installing 4.1c BSD on SIMH](http://gunkies.org/wiki/Installing_4.1c_BSD_on_SIMH)
* [Installing 4.2 BSD on SIMH](http://gunkies.org/wiki/Installing_4.2_BSD_on_SIMH)
* [Installing 4.3 BSD on SIMH](http://gunkies.org/wiki/Installing_4.3_BSD_on_SIMH)
* [Installing 4.3 BSD+NFS Wisconsin Unix](http://gunkies.org/wiki/Installing_4.3_BSD%2BNFS_Wisconsin_Unix)
* [Installing 4.3 BSD Quasijarus on SIMH](http://gunkies.org/wiki/Installing_4.3_BSD_Quasijarus_on_SIMH)
* [Installing 4.3 BSD RENO on SIMH](http://gunkies.org/wiki/Installing_4.3_BSD_RENO_on_SIMH)

以上 4.3BSD-tahoe と 4.4BSD-Encumbered を除く
VAX-11/780 で動作する BSD Unix のエミュレーション手順が揃ってます。

この gunkies の紹介からの派生記事は諸々ありますが、
私が見る限り、日本語で、もっとも丁寧で、解りやすい記事は
corbieさんのブログでした。corbieさんが書いておられる
SIMHに関連する記事は全部で以下の９本です。

* [SIMHで古代UNIXを再現](http://blog.livedoor.jp/corbie/archives/3444528.html)
* [SIMHで古代UNIXを再現(2)](http://blog.livedoor.jp/corbie/archives/3481471.html)
* [SIMH - 懐かしの4.2BSD](http://blog.livedoor.jp/corbie/archives/3954141.html)
* [SIMH - 4.0BSDを動かす](http://blog.livedoor.jp/corbie/archives/3978442.html)
* [SIMH - テープ作成コマンドの改良](http://blog.livedoor.jp/corbie/archives/4002149.html)
* [SIMH - テープ読込みコマンドの改良](http://blog.livedoor.jp/corbie/archives/4026481.html)
* [SIMH - 時計のずれ](http://blog.livedoor.jp/corbie/archives/4035791.html)
* [SIMH - 4.1BSDを動かす (1)](http://blog.livedoor.jp/corbie/archives/4068872.html)
* [SIMH - 4.1BSDを動かす (2)](http://blog.livedoor.jp/corbie/archives/4076553.html)

このうち、最初の２本は PDP-11 エミュレーションによる
Unix 7th Edition の実行を扱ったものです。

おそらく「Unix考古学」で紹介したレトロな Unix を体験したい
（前提知識の少ない）若い方々は、この記事から始めるのが
一番楽なのではないかと思います。

### さて・・・
以上のように紹介記事はすでに一通り揃っているので、
私があらたに紹介記事を書き起こす必要はなさそうなのですが・・・

単行本の出版を記念して何かを書き起こしたいと考えてます。
取り敢えず京都の講演までにはなんとかしたい。
ということでネタ探しをしますので、
しばしお待ち下さい。（笑）

EOF
