---
title: "aaaAzure AD v2 iOS 入門-使用 |Microsoft 文件"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 22e67850e2e0b14b6d68815d8f23e18ce2e878ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>用於 hello Microsoft Graph API 中的 hello Microsoft 驗證程式庫 (MSAL) tooget 語彙基元

開啟`ViewController.swift`並取代與 hello 程式碼：

```swift
import UIKit
import MSAL

class ViewController: UIViewController, UITextFieldDelegate, URLSessionDelegate {
    
    let kClientID = "Your_Application_Id_Here"
    let kAuthority = "https://login.microsoftonline.com/common/v2.0"

    let kGraphURI = "https://graph.microsoft.com/v1.0/me/"
    let kScopes: [String] = ["https://graph.microsoft.com/user.read"]
    
    var accessToken = String()
    var applicationContext = MSALPublicClientApplication.init()

    @IBOutlet weak var loggingText: UITextView!
    @IBOutlet weak var signoutButton: UIButton!

     // This button will invoke hello call toohello Microsoft Graph API. It uses the
     // built in Swift libraries toocreate a connection.
    
    @IBAction func callGraphButton(_ sender: UIButton) {
        
        
        do {
            
            // We check toosee if we have a current logged in user. If we don't, then we need toosign someone in.
            // We throw an interactionRequired so that we trigger hello interactive signin.
            
            if  try self.applicationContext.users().isEmpty {
                throw NSError.init(domain: "MSALErrorDomain", code: MSALErrorCode.interactionRequired.rawValue, userInfo: nil)
            } else {
            
            // Acquire a token for an existing user silently
            
            try self.applicationContext.acquireTokenSilent(forScopes: self.kScopes, user: applicationContext.users().first) { (result, error) in
    
                    if error == nil {
                        self.accessToken = (result?.accessToken)!
                        self.loggingText.text = "Refreshing token silently)"
                        self.loggingText.text = "Refreshed Access token is \(self.accessToken)"
                        
                        self.signoutButton.isEnabled = true;
                        self.getContentWithToken()
    
                    } else {
                        self.loggingText.text = "Could not acquire token silently: \(error ?? "No error information" as! Error)"
    
                    }
                }
            }
        }  catch let error as NSError {
            
            // interactionRequired means we need tooask hello user toosign-in. This usually happens
            // when hello user's Refresh Token is expired or if hello user has changed their password
            // among other possible reasons.
            
            if error.code == MSALErrorCode.interactionRequired.rawValue {
                
                self.applicationContext.acquireToken(forScopes: self.kScopes) { (result, error) in
                        if error == nil {
                            self.accessToken = (result?.accessToken)!
                            self.loggingText.text = "Access token is \(self.accessToken)"
                            self.signoutButton.isEnabled = true;
                            self.getContentWithToken()
                            
                        } else  {
                            self.loggingText.text = "Could not acquire token: \(error ?? "No error information" as! Error)"
                        }
                }
                
            }
            
        } catch {
            
            // This is hello catch all error.
            
            self.loggingText.text = "Unable tooacquire token. Got error: \(error)"
            
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        do {
             // Initialize a MSALPublicClientApplication with a given clientID and authority
            self.applicationContext = try MSALPublicClientApplication.init(clientId: kClientID, authority: kAuthority)
        } catch {
            self.loggingText.text = "Unable toocreate Application Context. Error: \(error)"
        }
    }


    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        
        if self.accessToken.isEmpty {
            signoutButton.isEnabled = false; 
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a>相關資訊
#### <a name="getting-a-user-token-interactively"></a>以互動方式取得使用者權杖
呼叫 hello`acquireToken`方法的結果，在瀏覽器視窗，提示 hello 使用者 toosign 中的。 應用程式通常需要以互動方式 hello 中的使用者 toosign 第一次需要 tooaccess 受保護的資源，或無訊息作業 tooacquire 權杖就會失敗 （例如 hello 使用者密碼到期時）。

#### <a name="getting-a-user-token-silently"></a>以無訊息方式取得使用者權杖
hello`acquireTokenSilent`方法會處理語彙基元收購並沒有任何使用者互動的更新。 之後`acquireToken`會針對要執行 hello 第一次， `acquireTokenSilent` hello 方法常用 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。

最後，`acquireTokenSilent`將會失敗 – 例如 hello 使用者已登出，或已變更其密碼，另一個裝置上的。 當 MSAL 偵測到 hello 問題可透過要求互動的動作來解決時，它就會引發`MSALErrorCode.interactionRequired`例外狀況。 您的應用程式可以透過兩種方式處理此例外狀況：

1.  進行呼叫，以針對`acquireToken`立即，而這會造成提示 hello 使用者 toosign 中的。 此模式通常用於線上應用程式在沒有離線內容 hello 應用程式中可供 hello 使用者。 此 「 引導式的安裝程式所產生的 hello 範例應用程式會使用此模式： 您可以看到它在動作 hello 執行 hello 應用程式的第一次。 因為沒有使用者曾使用 hello 應用程式，`applicationContext.users().first`會包含 null 值，和` MSALErrorCode.interactionRequired `擲回例外狀況。 hello hello 範例中的程式碼，則控制代碼藉由呼叫 hello 例外狀況`acquireToken`導致提示中的 hello 使用者 toosign。

2.  應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`acquireTokenSilent`稍後。 這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，沒有離線內容 hello 應用程式中提供。 在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊，或您的應用程式可以決定 tooretry`acquireTokenSilent`網路還原之後變成暫時無法使用時。

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元

新增下列 hello 新方法太`ViewController.swift`。 這個方法是使用的 toomake`GET`對 hello Microsoft Graph API 使用要求*HTTP 授權標頭*:

```swift
func getContentWithToken() {
    
    let sessionConfig = URLSessionConfiguration.default
    
    // Specify hello Graph API endpoint
    let url = URL(string: kGraphURI)
    var request = URLRequest(url: url!)
    
    // Set hello Authorization header for hello request. We use Bearer tokens, so we specify Bearer + hello token we got from hello result
    request.setValue("Bearer \(self.accessToken)", forHTTPHeaderField: "Authorization")
    let urlSession = URLSession(configuration: sessionConfig, delegate: self, delegateQueue: OperationQueue.main)
    
    urlSession.dataTask(with: request) { data, response, error in
        let result = try? JSONSerialization.jsonObject(with: data!, options: [])
                    if result != nil {
                
                self.loggingText.text = result.debugDescription
            }
        }.resume()
}
```

<!--start-collapse-->
### <a name="making-a-rest-call-against-a-protected-api"></a>針對受保護 API 進行 REST 呼叫

在此範例應用程式，hello`getContentWithToken()`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。 這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。 此範例中，hello 資源為 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。
<!--end-collapse-->

## <a name="set-up-sign-out"></a>設定登出

新增下列方法太 hello`ViewController.swift` toosign 出 hello 使用者：

```swift 
@IBAction func signoutButton(_ sender: UIButton) {

    do {
        
        // Removes all tokens from hello cache for this application for hello provided user
        // first parameter:   hello user tooremove from hello cache
        
        try self.applicationContext.remove(self.applicationContext.users().first)
        self.signoutButton.isEnabled = false;
        
    } catch let error {
        self.loggingText.text = "Received error signing user out: \(error)"
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a>關於登出的詳細資訊

hello`signoutButton`方法 hello 使用者移除 hello MSAL 使用者快取 – 這會有效地指示 MSAL tooforget hello 目前使用者讓未來的要求 tooacquire 語彙基元才會成功則由 toobe 互動式。

雖然此範例中的 hello 應用程式支援單一使用者，但是 MSAL 支援的案例，其中多個帳戶可以登入在 hello 相同時間 – 範例可以是電子郵件應用程式使用者有多個帳戶的位置。
<!--end-collapse-->

## <a name="register-hello-callback"></a>註冊 hello 回呼

Hello 使用者進行驗證時，一旦 hello 瀏覽器重新導向 hello 使用者回復 toohello 應用程式。 請遵循以下 tooregister 的 hello 步驟這個回呼：

1.  開啟 `AppDelegate.swift` 並匯入 MSAL：

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
新增下列方法 tooyour hello<code>AppDelegate</code>類別 toohandle 回呼：
</li>
</ol>

```swift
// @brief Handles inbound URLs. Checks if hello URL matches hello redirect URI for a pending AppAuth
// authorization request and if so, will look for hello code in hello response.

func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    
    print("Received callback!")
    
    MSALPublicClientApplication.handleMSALResponse(url)
    
    return true
}
```

