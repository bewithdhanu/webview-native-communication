# iOS Implementation

```swift
class JSApplication: NSObject, WKScriptMessageHandler {
    weak var webView: WKWebView?
    
    func userContentController(_ userContentController: WKUserContentController, 
                             didReceive message: WKScriptMessage) {
        guard let dict = message.body as? [String: Any],
              let event = dict["event"] as? String,
              let data = dict["data"] as? [Any] else {
            return
        }
        
        switch event {
        case "userClick":
            guard let buttonId = data[0] as? String else { return }
            handleUserClick(buttonId: buttonId)
            
        case "formSubmit":
            guard let username = data[0] as? String,
                  let email = data[1] as? String,
                  let isValid = data[2] as? Bool else { return }
            handleFormSubmit(username: username, email: email, isValid: isValid)
            
        case "userUpdate":
            guard let userId = data[0] as? String,
                  let userEmail = data[1] as? String else { return }
            handleUserUpdate(userId: userId, email: userEmail)
            
        case "profileUpdate":
            guard let profileData = data[0] as? [String: Any],
                  let name = profileData["name"] as? String,
                  let age = profileData["age"] as? Int else { return }
            handleProfileUpdate(name: name, age: age)
        }
    }
    
    private func handleUserClick(buttonId: String) {
        print("Button clicked: \(buttonId)")
    }
    
    private func handleFormSubmit(username: String, email: String, isValid: Bool) {
        print("Form submitted: username=\(username), email=\(email), valid=\(isValid)")
    }
    
    private func handleUserUpdate(userId: String, email: String) {
        print("User updated: userId=\(userId), email=\(email)")
    }
    
    private func handleProfileUpdate(name: String, age: Int) {
        print("Profile updated: name=\(name), age=\(age)")
    }
}
```