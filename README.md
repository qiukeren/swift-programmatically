# swift-programmatically

swift programmatically without storyboard.

This repo is under GPL LICENSE.

This repo was inspired by [lanqy/swift-programmatically](https://github.com/lanqy/swift-programmatically), but add some changes to suit swift 3 and other swift and refering library changes.

I am focusing on making effective `ViewController`.


## UITabBarController demo (like the buttom of App Store)

```swift
import UIKit
class ViewController: UITabBarController {
    override func viewDidLoad() {
        super.viewDidLoad()
        let item1 = Item1ViewController()
        //actually we do not have the image, so the demo image is not visible
        let icon1 = UITabBarItem(title: "item1", image: UIImage(named: "someImage.png"), selectedImage: UIImage(named: "otherImage.png"))
        item1.tabBarItem = icon1
        
        let item2 = Item2ViewController()
        let icon2 = UITabBarItem(title: "item2", image: UIImage(named: "someImage.png"), selectedImage: UIImage(named: "otherImage.png"))
        item2.tabBarItem = icon2
        
        let controllers = [item1,item2]
        self.viewControllers = controllers
    }
    
    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
}

class Item1ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        
        view.backgroundColor = UIColor.green
        self.title = "item1"
        print("item 1 loaded")
    }
}

class Item2ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        
        view.backgroundColor = UIColor.red
        self.title = "item2"
        print("item 2 loaded")
    }
}
```
