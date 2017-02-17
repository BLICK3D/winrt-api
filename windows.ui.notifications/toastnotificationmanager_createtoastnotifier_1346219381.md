---
-api-id: M:Windows.UI.Notifications.ToastNotificationManager.CreateToastNotifier
-api-type: winrt method
---

<!-- Method syntax
public Windows.UI.Notifications.ToastNotifier CreateToastNotifier()
-->

# Windows.UI.Notifications.ToastNotificationManager.CreateToastNotifier

## -description
Creates and initializes a new instance of the [ToastNotification](toastnotification.md), bound to the calling application, that lets you raise a toast notification to that app.

## -returns
The object you will use to send the toast notification to the app.

## -remarks
Do not use this overload when creating a toast notifier for a desktop app. Use [CreateToastNotifier(appID)](toastnotificationmanager_createtoastnotifier_163337301.md) to supply the required [AppUserModelID](http://msdn.microsoft.com/library/ebce2d99-6f20-4545-9f12-d79cd8d0828f).

If your app uses a [background voice-over-Internet protocol (VOIP) agent](XREF:TODO:405cff28-3276-49d8-ab73-87c01ce0258d), it must specify the app ID to show a toast. Use the [CreateToastNotifier(appID)](toastnotificationmanager_createtoastnotifier_163337301.md) method overload.

## -examples
The following example shows how to create and send a toast notification that includes text and images, including the use of the [CreateToastNotifier](toastnotificationmanager_createtoastnotifier_1346219381.md) method.

```javascript

var notifications = Windows.UI.Notifications;

// Get the toast notification manager for the current app.
var notificationManager = notifications.ToastNotificationManager;

// The getTemplateContent method returns a Windows.Data.Xml.Dom.XmlDocument object
// that contains the toast notification XML content.
var template = notifications.toastTemplateType.toastImageAndText01;
var toastXml = notificationManager.getTemplateContent(notifications.ToastTemplateType[template]);

// You can use the methods from the XML document to specify the required elements for the toast.
var images = toastXml.getElementsByTagName("image");
images[0].setAttribute("src", "images/toastImageAndText.png");

var textNodes = toastXml.getElementsByTagName("text");
textNodes.forEach(function (value, index) {
    var textNumber = index + 1;
    var text = "";
    for (var j = 0; j < 10; j++) {
        text += "Text input " + /*@static_cast(String)*/textNumber + " ";
    }
    value.appendChild(toastXml.createTextNode(text));
});

// Create a toast notification from the XML, then create a ToastNotifier object
// to send the toast.
var toast = new notifications.ToastNotification(toastXml);

notificationManager.createToastNotifier().show(toast);
```



## -see-also
[CreateToastNotifier(String)](toastnotificationmanager_createtoastnotifier_163337301.md), [Toast notifications sample](http://go.microsoft.com/fwlink/p/?linkid=231503), [Sending toast notifications from desktop apps sample](http://go.microsoft.com/fwlink/p/?linkid=231503), [Toast XML schema](XREF:TODO:toast.Schema_Root), [Toast notification overview](http://msdn.microsoft.com/library/14a07fce-d631-4bad-ab99-305b703713e6), [Quickstart: Sending a toast notification](http://msdn.microsoft.com/library/098df37c-4d40-4499-b809-ccb651da1cba), [Quickstart: Sending a toast push notification](XREF:TODO:m_ui_tiles.quickstart_sending_a_toast_push), [Quickstart: Sending a toast notification from the desktop](http://msdn.microsoft.com/library/1d20ed75-e24a-4e60-91ab-cfcbe902a68e), [Guidelines and checklist for toast notifications](XREF:TODO:m_ui_tiles.guidelines_and_checklist_for_toast), [How to handle activation from a toast notification](http://msdn.microsoft.com/library/74ba3513-0a52-46a0-8769-ed58abe7c05a), [How to opt in for toast notifications](http://msdn.microsoft.com/library/809cdd36-6de1-4de0-88b2-62b46cafdb28), [How to schedule a toast notification](http://msdn.microsoft.com/library/18a09413-1679-4606-8175-346f4fe6a4f8), [How to enable desktop toast notifications through an AppUserModelID](http://msdn.microsoft.com/library/bb32cd0a-99e6-47dc-a913-39a7b3027314), [The toast template catalog](http://msdn.microsoft.com/library/1a437614-4259-426b-8e3f-ca57368b2e7a), [Toast audio options](http://msdn.microsoft.com/library/12185879-1f9b-4bdc-99e7-a6f2f62806cb)