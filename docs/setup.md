# Setup

## Android Setup

```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var webView: WebView
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        webView = WebView(this).apply {
            settings.apply {
                javaScriptEnabled = true
                domStorageEnabled = true
                allowFileAccess = true
            }
            
            addJavascriptInterface(JSApplication(this@MainActivity), "JSApplication")
        }
        
        setContentView(webView)
    }
}
```

## iOS Setup

```swift
class ViewController: UIViewController {
    private var webView: WKWebView!
    private var jsApplication: JSApplication!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Create JS Application handler
        jsApplication = JSApplication()
        
        // Setup WebView
        let config = WKWebViewConfiguration()
        let userContentController = WKUserContentController()
        userContentController.add(jsApplication, name: "JSApplication")
        config.userContentController = userContentController
        
        webView = WKWebView(frame: view.bounds, configuration: config)
        jsApplication.webView = webView
        view.addSubview(webView)
    }
}
```