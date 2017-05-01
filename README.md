# swift-programmatically

swift programmatically without storyboard.

This repo is under GPL LICENSE.

This repo was inspired by [lanqy/swift-programmatically](https://github.com/lanqy/swift-programmatically), but add some changes to suit swift 3 and other swift and refering library changes.

I am focusing on making effective `ViewController`.

## Basis

I provide executable Controller named `ViewController`, to use this, just follow the under steps:

1. Delete Main.storyboard
2. Choose NONE in General - Deployment info - Main Interface
3. Just modify your AppDelegate like this:

```swift
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        window = UIWindow(frame: UIScreen.main.bounds)
        window?.rootViewController = ViewController()
        window?.makeKeyAndVisible()
        return true
    }
```


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


## Effective NavigationController (implements a multi-level nav controller)


```swift
import UIKit

class ViewController: UINavigationController {

    override func viewDidLoad() {
        super.viewDidLoad()
        let item1 = Item1ViewController()
        let item2 = Item2ViewController()
        let item3 = Item3ViewController()
        let controllers = [item1,item2,item3]
        self.viewControllers=controllers
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

class Item3ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = UIColor.black
        self.title = "item3"
        print("item 3 loaded")
    }
}
```


## SearchBar in NavigationBar (combined with a Navigation page)

```swift
import UIKit

class ViewController: UINavigationController {
    override func viewDidLoad() {
        super.viewDidLoad()
        let item1 = Item1ViewController()
        let item2 = Item2ViewController()
        let controllers = [item1,item2]
        self.viewControllers=controllers
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

class Item2ViewController: UIViewController, UISearchControllerDelegate, UISearchBarDelegate,UISearchResultsUpdating {
    
    var searchController : UISearchController!

    func updateSearchResults( for searchController: UISearchController) {
        print(searchController.searchBar.text ?? "ERROR")
    }

    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        self.searchController = UISearchController(searchResultsController:  nil)
        
        self.searchController.searchResultsUpdater = self
        self.searchController.delegate = self
        self.searchController.searchBar.delegate = self
        
        self.searchController.hidesNavigationBarDuringPresentation = false
        self.searchController.dimsBackgroundDuringPresentation = true
        
        self.navigationItem.titleView = searchController.searchBar
        
        self.definesPresentationContext = true
    }
}
```
