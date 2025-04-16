# SwiftUI

## Combine
publisherとsubscriberでデータのやり取りができる仕組み。
subscriberにクロージャ設定して、sendってやるとそれが呼ばれる
クラス外でクロージャを設定できる仕組みも
非同期処理でよく使われて、APIのレスポンス待ちの実装に使ったりする。
swift concurrencyで代替可能
キーワード
PassthroughSubject
AnyPublisher
.send：データを送る
.sink：「publisherからの全ての出力を受け取る終点」publisher.sink(とかかいて実装を書く。
.flatMap：サブスクライバーで実行中に再度publisherからのreturnを待つ時に使う。これをつかうと、.sinkでリテラル値で受け取れる。mapでやるとpublisherのpublisherになる
.map：sinkの前にデータ変換する。returnするとsinkに渡る
.assign


