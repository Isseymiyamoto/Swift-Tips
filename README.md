# Swit-Tips
Swiftに関しての知見を集める

## Swift 文法

#### 三項演算子

何らかの値に呼応して、2つの選択肢が考慮される場合に用いられる

```swift

// MARK: - how to use
    
    // 条件式 ? trueの時の処理 : falseの時の処理
    
// MARK: - example 

    var isFollowed: Bool = false
    isSelect ? print("このユーザーにフォローされています") : print("このユーザーにはフォローされていません")
    // このユーザーにはフォトーされていませんが出力される

```

## UIKit



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

