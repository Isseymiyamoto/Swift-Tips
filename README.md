# iOS-Tips
iOSに関しての知見を集める

## Swift 文法

### 三項演算子

何らかの値に呼応して、2つの選択肢が考慮される場合に用いられる

```swift

// MARK: - how to use
    
    // 条件式 ? trueの時の処理 : falseの時の処理
    
// MARK: - example 

    var isFollowed: Bool = false
    isFollowed ? print("このユーザーにフォローされています") : print("このユーザーにはフォローされていません")
    // 出力: このユーザーにはフォローされていません 

```

### Nil Coalescing 演算子

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


## レイアウト

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



