# SwiftUI
## 基礎1
var body: some View {：Viewの最初に呼ばれるやつ。汎用的なViewな型
NavigationView {とか
VStack(alignment: .leading) {とか
は構造体をnewしてる。()がなかったらinitには何もわたさない。{}はinitの最後の変数にクロージャを渡しているだけ
Text(input.title)は特殊なViewが返っているが、それに対して.font(.title)などをして設定できるモディファイヤーという

## 基礎2
private(set)というアクセス修飾子は外から編集ができないだけ
プロパティラッパー
@State：View内の可変値をUIに出力したい場合。カウンターの値とか
@Binding:@Stateの値を子ビューに渡してどうこうできる。子ビューもstruct。
@StateObject：ViewModelクラス側で制御したものをViewに出したい場合に使う。ViewModel側は@Publishedで就職された変数があり、そいつをViewで出す。
@ObservedObject:StateObjectを親ビューから受け取る時にこれで宣言する




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
.assign  ：プロパティに値を代入する .map { _ in true } .assign(to: \.isLoading, on: viewController)viewControllerの.isLoadingにtrueを代入する
.store：subscriptionをバインドしても消えてしまうから変数に入れるというだけ
.eraseToAnyPublisher()：戻り値を単純化する
用途：非同期実装は煩雑なコードになるのでこれを使って簡単に書く。swift concurrencyを使うともっとシンプルになる

## Swift Concurrency
### 1
for await time in timer.values {で非同期待ちループができる。
AsyncSequenceプロトコルに準拠するとできる。AsyncStreamで既存のコードを非同期にすることも可能。
### 2
async letでスコープ内で複数の非同期を待てる。タスクグループという機能もある。
Task{},Task.detach{}スコープ外で動く。
エラーの伝搬とかキャンセルの仕方で実装が変わる
### 3
sendable スレッド間で渡しても安全だという保証する。キャプチャーとプロトコルがある。swift6ではsendableじゃないとエラー
### 4
classではなくactorで宣言すると複数からアクセスができなくなる。値を渡すときはsendableが必須になる。
classの宣言に@MainActorをつけるとメインスレッドで動く。await MainActor.run {}でメインスレッドに移すこともできる。
Task{}←Task構造体で、initに渡すものはないけど、クロージャーだけ渡してる

