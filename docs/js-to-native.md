# JavaScript to Native Communication

## JavaScript Implementation

```javascript
function sendEvent(event, ...data) {
    if (!event || typeof event !== 'string') {
        console.error('Event name is required and must be a string');
        return false;
    }

    try {
        // iOS
        if (window?.webkit?.messageHandlers?.JSApplication) {
            window.webkit.messageHandlers.JSApplication.postMessage({
                event,
                data
            });
            return true;
        }

        // Android
        if (typeof JSApplication !== 'undefined') {
            JSApplication.sendEvent(event, JSON.stringify(data));
            return true;
        }

        console.warn('Native interface not found');
        return false;

    } catch (error) {
        console.error('Failed to send event:', {
            event,
            data,
            error: error.message
        });
        return false;
    }
}
```

## Android Implementation

[View Android Implementation Code](implementations/android-implementation.md)

## iOS Implementation

[View iOS Implementation Code](implementations/ios-implementation.md)

## Data Types Examples

```javascript
// Single value
sendEvent('userClick', 'button1');

// Multiple values
sendEvent('formSubmit', 'john_doe', 'john@example.com', true);

// Array
const userData = ['user123', 'john@example.com'];
sendEvent('userUpdate', ...userData);

// Object
sendEvent('profileUpdate', { name: 'John', age: 30 });
```