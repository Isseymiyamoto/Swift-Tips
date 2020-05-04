# Swit-Tips
Swiftに関しての知見を集める


## UIKit



## レイアウト

#### frame

Viewのサイズや位置を決めるもの, 親Viewに対しての位置を指定する  
例えば下記では、view.addSubView(button)で親Viewはviewであるので、それに対してx方向0,y方向0に長さ100,200のbuttonを設置することになる

```frame.swift

class frameController: UIViewController{

//MARK: - Properties

    let button: UIButton = {
        let button = UIButton()
        button.setTitle("frameについて", for: .normal)
        button.frame = CGRect(x: 0, y: 0, width: 100, height: 200)
        return button
    }()

//MARK: - Lifecycle

    override viewDidLoad(){
        super.viewDidLoad()
        
        view.addSubView(button)
    }
}


```

