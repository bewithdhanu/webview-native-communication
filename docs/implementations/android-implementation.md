# Android Implementation

```kotlin
class JSApplication(private val context: Context) {
    
    @JavascriptInterface
    fun sendEvent(event: String, dataJson: String) {
        try {
            val data = JSONArray(dataJson)
            
            when (event) {
                "userClick" -> {
                    val buttonId = data.getString(0)
                    handleUserClick(buttonId)
                }
                
                "formSubmit" -> {
                    val username = data.getString(0)
                    val email = data.getString(1)
                    val isValid = data.getBoolean(2)
                    handleFormSubmit(username, email, isValid)
                }
                
                "userUpdate" -> {
                    val userId = data.getString(0)
                    val userEmail = data.getString(1)
                    handleUserUpdate(userId, userEmail)
                }
                
                "profileUpdate" -> {
                    val profileData = JSONObject(data.getString(0))
                    val name = profileData.getString("name")
                    val age = profileData.getInt("age")
                    handleProfileUpdate(name, age)
                }
            }
        } catch (e: Exception) {
            Log.e("JSApplication", "Error processing event: ${e.message}")
        }
    }
    
    private fun handleUserClick(buttonId: String) {
        Log.d("JSApplication", "Button clicked: $buttonId")
    }
    
    private fun handleFormSubmit(username: String, email: String, isValid: Boolean) {
        Log.d("JSApplication", "Form submitted: username=$username, email=$email, valid=$isValid")
    }
    
    private fun handleUserUpdate(userId: String, email: String) {
        Log.d("JSApplication", "User updated: userId=$userId, email=$email")
    }
    
    private fun handleProfileUpdate(name: String, age: Int) {
        Log.d("JSApplication", "Profile updated: name=$name, age=$age")
    }
}
```