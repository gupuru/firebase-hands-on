
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

# [fit] Authentication

---

# Authentication

- ログイン周り
- メアド, 匿名アカウント, Google, Facebook, Twitter, GitHubなどに対応
- 無料
- FirebaseUIを使えば、uiなども簡単に実装できる
- iOS, Android, Web

---

![inline](img/auth_settings.png)

---

```
compile 'com.firebaseui:firebase-ui-auth:0.6.0'
```

```
 FirebaseAuth auth = FirebaseAuth.getInstance();
        if (auth.getCurrentUser() != null) {
            //ログイン済み
        } else {
          startActivityForResult(
                    AuthUI.getInstance().createSignInIntentBuilder().build(),
                    RC_SIGN_IN);
        }
```

```
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == RC_SIGN_IN) {
            if (resultCode == RESULT_OK) {
                // ログイン成功
            }
        }
    }
```
---

![inline](img/auth_db.png)

---

# [fit] Realtime Database

---

# Realtime Database

- NoSQL JSON データベース
- リアルタイム同期(オフライン対応)
- iOS, Android, Web
- 有料(無料枠あり)

---

![inline](img/database_rule.png)

---

```
pod 'Firebase/Database'
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

```swift
import UIKit
import FirebaseDatabase

class ViewController: UIViewController {

    let rootRef = FIRDatabase.database().reference()

    override func viewDidLoad() {
        super.viewDidLoad()
        
        //読み込み    
        rootRef.observe(.value, with: { snapshot in
            print("\(snapshot.key) -> \(snapshot.value)")
        })
        
        //書き込み
        rootRef.child("food").setValue("りんごさま")

    }

}
```

---

![inline](img/database.png)

---

# [fit]  Storage

---

#  Storage

- ストレージ(S3に近いかも)
- 画像, 動画, 音声などのダウンロード, アップロード
- iOS, Android, Web
- 有料(無料枠あり)

---

```ruby
pod 'Firebase/Storage'
```
### あとは他と同じ
---

## アップロード

```swift
import FirebaseStorage

class ViewController: UIViewController {
    
    let storage = FIRStorage.storage()

    override func viewDidLoad() {
        super.viewDidLoad()
   
        let storageRef = storage.reference(forURL: "gs://fir-handson-ce2a8.appspot.com")

        if let data = UIImagePNGRepresentation(UIImage(named: "ie")!) {
            let riversRef = storageRef.child("images/ie.png")
            riversRef.put(data, metadata: nil, completion: { metaData, error in
                print(metaData)
                print(error)
            })
        }
    }
}
```

---

![inline](img/storage_console.png)

---

## ダウンロード

```swift

import FirebaseStorage

class ViewController: UIViewController {
    
    let storage = FIRStorage.storage()

    override func viewDidLoad() {
        super.viewDidLoad()

        let storageRef = storage.reference(forURL: "gs://fir-handson-ce2a8.appspot.com")

        let ieRef = storageRef.child("images/hogehoge.png")        
        ieRef.data(withMaxSize: 1 * 1024 * 1024) { (data, error) -> Void in
            if (error != nil) {
                print(error)
            } else {
                let image: UIImage! = UIImage(data: data!)
            }
        }
        
    }
}
```

---

![inline](img/storage_ios.png)

---

