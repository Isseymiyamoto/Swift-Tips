# Swit-Tips
Swiftに関しての知見を集める


## UIKit



## レイアウト

#### frame

定義されたcomponent.


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

