# iOS-Tips
iOSに関しての知見を集める

## Swift 文法

### 変数の定義

```swift

private lazy var
最初のアクセス時にインスタンスが作られる
selfが存在してから呼ばれることが保証されるので、インスタンス生成時にselfが使えるメリットあり

lazy loading means that it will not actually load that property on till it's time for it to happen

https://www.slideshare.net/tomohirokumagai54/lazy-var-cocoakansai-cswift

weak var
protocolに対して使用？delegateを強参照で持つと親子共にメモリから解放されなくなる

fileprivate func
ファイル内でのみ参照される

などなど調べる


```

### for-in文

繰り返し処理

```

for 定数名 in 式 where式(省略可能){
    処理
}

範囲演算子: Swiftでは、２つの数の間を表す構造体とそのインスタンスを生成する演算子「..<」　と「...」が用意されている

A..<B  →  A <= x < B
A...B  →  A <= x <= B

for i in 1..<5 {
    print(i)
}

// expected output
1
2
3
4

```


### 列挙型(enum)

```swift

enum 列挙型の名前: 各要素に割り当てたいData型{
    case xxx
    case xxx
}

enum NotificationType: Int{
    case follow
    case like
    case reply
    case retweet
    case mention
}

let oneNotification = NotificationType.follow

```

### 三項演算子

何らかの値に呼応して、2つの選択肢が考慮される場合に用いられる

```swift

// MARK: - how to use
    
    // 条件式 ? trueの時の処理 : falseの時の処理
    
// MARK: - example 

    var isFollowed: Bool = false
    isFollowed ? print("このユーザーにフォローされています") : print("このユーザーにはフォローされていません")
    // 出力: このユーザーにはフォローされていません 
    
    
    // another example 
    
    var config: NotificationType?
    
    config = .message
    var icon_title = config === .message ? "message" : "reply"

```

### Nil合体演算子

2つの値に関して、前者がnilであった場合、後者を返す

```swift

// MARK: - how to use
    
    // a ?? b
    
// MARK: - example 

    var a:String? = nil
    var b = "b"
    
    b = a as? String ?? ""
    // bには""が代入される
```

### オプショナル束縛(optional binding)構文

#### if-let文

オプショナル方の式の値がnilではなかった場合、その値をif文のthen節で使いたい場合に利用する
使用したい変数がnilでない値を持っていた場合、その値が開示されて左辺の変数に代入される
条件部で定義された変数や定数はthen節でのみ参照されるが、この変数や定数に、元のオプショナル方の変数などと同じ名前を使うこともできる
二つの変数をコンマで区切って連続して定義することも可能

ex
```swift

let birthYear: Int? = Int(1998)

if let year = birthYear{
  print(year)
}

```

#### guard文

オプショナル束縛に限定した構文ではないが、想定外の状況が発生した場合にその処理から抜け出すための構文

構文
```swift
guard 条件 else { break や return }
```

条件に記述した条件が成立しなかった場合にelse節が実行され、そのコードブロックから抜け出す



## UIKitに関する情報


### UIButton

UIButtonに関する基本的な設定(よく使うプロパティ、関数など)

```swift

// MARK: Properties

    let actionButton: UIButton = {
        // buttonタイプの決定
        let button = UIButton(type: .system)
        // 文字色やボーダー色など
        button.tintColor = .white
        // 背景色
        button.backgroundColor = .twitterBlue
        // タイトル・imageの設置
        button.setTitle("タイトル", for: .normal)
        button.setImage(UIImage(named: "new_tweet"), for: .normal)
        // タイトルのフォント設定
        button.titleLabel?.font = UIFont.boldSystemFont(ofSize: 14)
        // ボーダーに関する設定
        button.layer.borderColor = UIColor.twitterBlue.cgColor
        button.layer.borderWidth = 1.25
        // actionハンドラの設定
        button.addTarget(self, action: #selector(actionButtonTapped), for: .touchUpInside)
        
        return button
    }()
    
// MARK: Lifecycle
    
    override func viewDidLoad(){
        super.viewDidLoad()
        
        任意の親View.addSubView(actionButton)
    
    }
    
// MARK: Selectors
    
    @objc func actionButtonTapped(){
        // buttonが押された際の挙動をここに書く
        print("buttonが押されました")
    }


```

###  UILabel

UILabelに関する基本的な設定(よく使うプロパティ、関数など)

```swift

// MARK: Properties



```


### UIImageView

UIImageViewに関する基本的な設定(よく使うプロパティ、関数など)

```swift

// MARK: Properties
    
    let profileImageView: UIImageView = {
        let iv = UIImageView()
        // imageの元サイズからUIImageViewのサイズに拡大・縮小する際の方法についての設定
        iv.contentMode = .scaleAspectFit
        // border内にimageを収めるか否か　trueで収める
        iv.clipsToBounds = true
        // 背景色
        iv.backgroundColor = .lightGray
        // ボーダー色・幅
        iv.layer.borderColor = UIColor.white.cgColor
        iv.layer.borderWidth = 4
        return iv
    }()


```

### UIStackView

UIStackViewに関する基本的な設定(よく使うプロパティ、関数など)

```swift
    override func viewDidLoad(){
        super.viewDidLoad()
        
        
        // 並べたい要素を配列に格納する
        let stack = UIStackView(arrangedSubviews: [要素1, 要素2, 要素3])
        // 要素を縦向きor横向きに並べるのかを選択
        stack.axis = .vertical
        // 要素への制約の与え方
        stack.distribution = .fillProportionally
        // 要素毎に開けるスペースの設定
        stack.spacing = 4
        // 要素をどこに揃えて配置するかの設定
        stack.alignment = .leading
        

        view.addSubView(stack)
    }

```

以下参考になるQiita
> https://qiita.com/yucovin/items/ff58fcbd60ca81de77cb

## searchController

// UITableViewに検索バーをつける場合

```swift

// MARK: - Properties

private var isSearchMode: Bool {
    return searchController.isActive && !searchController.searchBar.text!.isEmpty
}
    
// UITableViewに検索バーを設ける
private let searchController = UISearchController(searchResultsController: nil)


// MARK: - Helpers

func configureSearchController(){
    searchController.searchResultsUpdater = self
    searchController.obscuresBackgroundDuringPresentation = false
    searchController.hidesNavigationBarDuringPresentation = false
    searchController.searchBar.tintColor = .shishaColor
    searchController.searchBar.placeholder = "友達を探してみましょう"
    navigationItem.searchController = searchController
    definesPresentationContext = false
}

// MARK: - UISearchResultsUpdating

extension class名: UISearchResultsUpdating{
    func updateSearchResults(for searchController: UISearchController) {
        guard let searchText = searchController.searchBar.text?.lowercased() else { return }
        フィルターした配列 = 全部入った配列.filter({ $0.プロパティ.contains(searchText) || $0.プロパティ.contains(searchText) })
    }
}

```

### UITextView

```

let textView: UITextView = {
    let tv = UITextView()
    tv.isScrollEnabled = true
    tv.isEditable = false
    tv.isSelectable = false
    
    // textに対して、marginをつける方法
    tv.textContainerInset = UIEdgeInsets(top: 16, left: 16, bottom: 16, right: 16)
    
    return tv
}()

```




## UINavigationController関連

### UINavigationController に関するプロパティ、メソッド

```swift

初期化

public init(rootViewController: UIViewController) 
引数に表示したいControllerを明記する

メソッド

画面遷移

open func pushViewController(_ viewController: UIViewController, animated: Bool)
指定したcontrollerに遷移する

open func popViewController(animated: Bool) -> UIViewController?
1つ前のcontrollerに戻す

プロパティ

open var isNavigationBarHidden: Bool
trueでnavigationBarを隠す

```

### UINavigationBar に関するプロパティ、メソッド

```swift

@available(iOS 11.0, *)
open var prefersLargeTitles: Bool
trueにすると、titleViewの幅がviewの幅いっぱいになって、左端からtitleが始まる？


```



## レイアウト

・　boundsとframeの違いはoriginの位置

### frame

Viewのサイズや位置を決めるもの, 親Viewに対しての位置を指定する  
例えば下記では、view.addSubView(button)で親Viewはviewであるので、それに対してx方向0,y方向0に長さ100,200のbuttonを設置することになる

```swift

class frameController: UIViewController{

//MARK: - Properties

    let button: UIButton = {
        let button = UIButton(type: .system)
        button.setTitle("frameについて", for: .normal)
        button.frame = CGRect(x: 0, y: 0, width: 100, height: 200)
        return button
    }()

//MARK: - Lifecycle

    override func viewDidLoad(){
        super.viewDidLoad()
        
        view.addSubView(button)
    }
}


```

### bounds


### Auto Layout

```swift
プログラムでauto Layoutを実装するのに必要なプロパティ
UIView.translatesAutoresizingMaskIntoConstraints = false
```

## アニメーション

UIViewクラスを継承しているUILabelやUIButtonなどはUIViewのクラス関数であるanimate関数を使用することで様々なアニメーションを簡単に行うことができる

```swift

// MARK: - how to use
    
    UIView.animate(withDuration: 何秒かけてアニメーションするか){
        // どのような処理を行うか
    }
    
// MARK: - example 

    
```


## クラスの初期化に関して

```swift

init(coder: NSCoder)
storyboards や nib を利用する場合に必要

init()

```
