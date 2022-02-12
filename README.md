# blog-tip-button

This is a throwback button. You can place it on your website to receive Amazon gift cards, cryptocurrency, etc.

これを設置したブログやウェブサイトに対して、支援したい読者がドロップダウンリストで選択すると、それぞれの寄付先やボタンが表示され投げ銭への導線がスムーズになる。


基本的にカスタマイズ必須だが、サイズ感としてはそのままでも、はてなブログのBrooklynサイドバー部分だったらだいたい合う感じの作り。

登録が必要なものはそれぞれアカウントを作らないと寄附が受け取れない。不要なチップボタンはプルダウンから除いてもらえれば。


## リスト選択

ドロップダウンリストを切り替えるのと同時に、画像やボタンなどの要素がスッと入れ替わるスクリプト。

何もない領域にいきなりボタンとかが現れるよりは、デフォルトの画像など設定しておいて、その表示が変わるという遷移のほうが分かりやすいかなと。


## アマギフの部分

アマギフを送るなら、メアド等をユーザ側が知っていないとダメなわけだが、さすがにスパムとかあるのでサイト上にそのまま掲載したくない。

かといっても画像化して載せるとユーザビリティに欠けるし、画像をnoindexし忘れて、googleさんにインデックスされたときには悲惨。


アットマークだけ星印とかにしても、結局ユーザが手入力しなきゃだし、さらにはそもそもユーザがどこかからコピペする手間も出来るだけ省きたい。

ということで、アドレス表示ボタンとコピーボタンを実装。ユーザのデバイスがPCじゃなくても、これならスマホ上でポチポチとタップするだけで済む。


いまどきAmazonギフト券くらいSNS上でやり取りするのかもしれないけれど、twitterアカウントとか明かしてない人もいると思うので。

メールアドレスのコピーボタンはお馴染みのclipboard.js。なのでjQueryを使う。


仕組みとしては、表示ボタンが押されると、まずドメイン直下に準備しておいたtxtファイルを読みに行く。

※このファイルには予めメアドの文字列をcharCodeAtしたものを記載。それっぽいネット上のツールを使って変換しても、より難読化できるのでいい感じに。


→指定されたtxtからメアドが無事取得できればfromCharCodeしつつそのまま表示。

→もし何らかの理由でtxtが読めず、メアド欄が空のままなら、コード内に記載のcharCodeAtで変換済みのメアド数値をfromCharCodeして表示。


そもそもドメイン直下のテキストに記載しておくのはどうなんだ問題と、結局コード内にもcharCodeAtしたもの書いておくんかい問題がある。

とはいえcharCodeAtしたところで暗号化と呼ぶには不十分で、記事ページ内だとボットに読まれる可能性はあるものの、さすがに記事中に生メアドよりはずっといいという結論。


## メタマスクの部分

クリプト周りのボタンはだいたい公式ボタン作成ツールによるものだが、Metamaskのところのスクリプトは自前。

ネット上のサンプルコードを上手いことつぎはぎして、2020年辺りではごく普通にWeb3に接続できていた。


少なくとも当時はPCとスマホ両方のmetamaskで動作確認できていたが、dappsでもいけるっぽい。

でもさすがに今は仕様が色々変わっていそうなので、設置前にきちんと要確認。


## その他応用

規約さえ問題無ければ、QR決済系の○○payとか載せてもいいかもしれない。


→さすがに大手のPayPayやLINE PAYは、大抵いわゆる投げ銭など個人への寄付用途はダメだが、Kyashあたりだと大丈夫っぽい？

→いくつかkyashのチップを扱ったサイトもある。中には事務局に問い合わせておｋという回答だったという話も。現時点でどうかは不明。


→例えばKyashのQRコードを載せるなら、自分のQRコードを読み取ってみると「kyash://qr/u/数字」という感じでアプリ起動のためのURLスキームがあるので、それを画像にリンク。


## 登録すれば使えるもの

・ofuseとかユグドアは説明不要な気がするので省略。

・paypal.me

ペイパルのソーシャルメディア決済ツール。

通常のpaypalアカウントとはまた別。個人的にはもっと広まってほしいが、そもそもQR系のキャッシュレス全盛のいまでは、ペイパル自体マイナー感が否めない。

`https://www.paypal.me/`


・tippin.me

ツイッター連携で暗号資産BTC用の投げ銭。

ツール登場時よりBTCが無駄に高騰してしまった。というかわざわざtwitterつなげて投げ銭くれる人の母数が少ない感覚。逆にみんな欲しがりさんなので。

`https://tippin.me/`


・money button

BTCやBSV、BATなど暗号資産の投げ銭。現状26種。

一部でカルト的な人気のビットコインSVを扱えるのは強い。braveブラウザのBATにも対応。でもボタンの動き(読み込み)がやや遅めなのがちょっと残念。

`https://www.moneybutton.com/`


・coinbaseコマース

コインベースの暗号資産オンライン決済ツール。

登録自体はわりと簡単。海外でcoinbaseユーザは多いので、もし外国向けにコンテンツを提供できているサイトなら良い選択肢になる。

`https://commerce.coinbase.com/`


### 参考：

下記サービスも暗号資産チップボタンは作成できるが、kycがやや面倒。

coingateはkycが最初から厳しかったので導入自体をあきらめた思ひ出。


一方のbitpayは普通に使えていたのだが、2020年辺りからちょい厳しくなり、身分証の申請が必須になってしまった。

海外の仮想通貨決済系の使用感としては、コインベースにわりと近い感じ？


・ビットペイ

`https://bitpay.com/`

・コインゲート

`https://coingate.com/`


## ライセンス表記

Author: maon-git

このリポジトリにはMITライセンスが適用されます。

`https://opensource.org/licenses/mit`
