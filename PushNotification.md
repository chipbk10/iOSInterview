# Push Notification

## How does Push Notification work under the hood?

- In the case, there is a new change from back-end side, we want to inform iOS apps. The server will call APNs service. The request (push notification payload) contains device token, the content of the notification, and any custom data you want to include
- Based on device tokens in the payload, APNs knows to which devices to deliver the notification.

## Device Token

- APNs does not maintain a centralized registry of device tokens associated with individual apps.
- Our server needs to manage and maintain the device tokens associated with our app's users. Whenever a user logs out or uninstalls the app, you should remove their device token from your server's records.

### How is the device token generated?

- When a user grants permission for your iOS app to receive push notifications, your app calls the `registerForRemoteNotifications()` method. This method actually sends a request to APNs.
- APNs will generate a unique device token, and sends back to our app
- Our app will send this device token to our server for storage and later use

### How do we send push notificaiton to all devices?

- Apple provides a `Bulk API` feature to handle sending notifications to multiple devices efficiently.
- Instead of sending individual requests per device token, you can create a single request that includes multiple device tokens in a bulk format.
- The request payload should contain the notification content, custom data, and an array of device tokens to which the notification will be sent.
- Due to limitations on the maximum payload size and rate limits, you may need to break down the device tokens into smaller batches or chunks.
- Send multiple requests, each containing a batch of device tokens, until you have processed all the tokens.
- By using the Bulk API and batching device tokens, you can efficiently send notifications to a large number of devices without having to include all the tokens in a single payload.

## How does APNs recognize our server?

- When setting up communication with APNs, we generate an SSL certificate through the Apple Developer portal, specifically for push notifications.
- During the initial connection setup, our server presents the SSL certificate to APNs as part of the TLS handshake process.
- The SSL certificate serves as a form of authentication, proving that our server is authorized to send push notifications for our specific app.
