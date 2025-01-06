# Native to JavaScript Communication

## Android to JavaScript

[View Android to JavaScript Code](implementations/android-to-js.md)

## iOS to JavaScript

[View iOS to JavaScript Code](implementations/ios-to-js.md)

## JavaScript Receiver

```javascript
// Setup native event handler
window.onNativeEvent = function(event, data) {
    console.log('Received native event:', event, data);
    
    switch(event) {
        case 'userStatus':
            handleUserStatus(data);
            break;
            
        case 'userData':
            const [firstName, lastName, age] = data;
            handleUserData(firstName, lastName, age);
            break;
            
        case 'userProfile':
            handleUserProfile(data);
            break;
            
        case 'appConfig':
            handleAppConfig(data);
            break;
    }
}

// Implementation of handlers
[View JavaScript Event Handlers](implementations/js-event-handlers.md)
```

## Data Types Examples

[View Native Data Types Examples](implementations/native-data-types.md)