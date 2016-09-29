
![fit](img/firebase.png)

---

# About me

**新見 晃平**

福岡にある株式会社セフリという会社で、[YAMAP](https://yamap.co.jp/)のAndroidアプリを作っている**iOS**エンジニアです。
最近は、Docker, TensorFlow, Angular 2などやっていてiOS全然できてない（泣）

- Twitter: @gupuru
- GitHub: gupuru

---

# [fit] Firebaseって、何？

---

- mBaaS
- Googleが運営しているサービス
- 2011年スタート(2014年後半にGoogleが買収)
- アプリやWeb開発に必要なものを数多く提供
- 無料でつかえるものが多い

---

![fit](img/firebase_features.png)

---

![fit](img/firebase_price.png)

---

#  [fit] 時間が許す限り、紹介していくよー

---

# [fit] Analytics

---

- モバイルアプリに特化した Google アナリティクスみたいなものです。
- イベント型分析ツール
- 無料
- iOS, Android

---

```
pod 'Firebase/Core'
```

```
import UIKit
import Firebase

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {

    var window: UIWindow?

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        //追加
        FIRApp.configure()
        return true
    }

}

```

--- 

![inline](img/analytics.png)

---

# Cloud Messaging

---

- プッシュ通知
- iOS, Android, Web
- 無料
- Notification MessageとData Messageの２種類

---

```
apply plugin: 'com.android.application'

dependencies {
    compile 'com.google.firebase:firebase-messaging:9.6.0'
}
apply plugin: 'com.google.gms.google-services'
```

--- 

## token取得

```
FirebaseInstanceId.getInstance().getToken();
```

---

## Notification Message

```
{
  "to" : "HHwgIpoDKCIZvvDMExUdFQ3P1...",
  "notification" : {
    "body" : "ぼでい",
    "title" : "たいとる",
    "icon" : "myicon"
  }
}
```

```
curl --header "Authorization: key=AIzaSyDGrPny1Cfb2m4cXzrSUoeguQidTc7xzs8" \
     --header Content-Type:"application/json" \
     https://fcm.googleapis.com/fcm/send \
     -d "{\"to\": \"...ifS-oaJevN_VwU0Y\",\"priority\":\"high\",\"notification\": {\"title\": \"this is title\", \"body\": \"this is body\"}}"
```

---

## Data Message

```
{
  "to" : "xUdFQ3P1...",
  "data" : {
    "name" : "fox",
    "body" : "neko",
    "Place" : "horaana"
  },
}
```

```
curl --header "Authorization: key=AIzaSyDGrPny1Cfb2m4cXzrSUoeguQidTc7xzs8" \
     --header Content-Type:"application/json" \
     https://fcm.googleapis.com/fcm/send \
     -d "{\"to\": \"...aJevN_VwU0Y\",\"priority\":\"high\",\"data\": {\"custom_title\": \"this is custom title\", \"custom_body\": \"this is custom body\", \"icon\": \"ic_stat_ic_notification\"}}"

```

---

# Notifications

- プッシュ通知
- Webコンソールから使う(コードを書く必要なし)
- 無料
- iOS, Android

---

![inline](img/notifications.png)

---