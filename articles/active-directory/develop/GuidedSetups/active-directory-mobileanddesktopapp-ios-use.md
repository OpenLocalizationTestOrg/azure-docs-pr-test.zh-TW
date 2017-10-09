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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="2665f-103">用於 hello Microsoft Graph API 中的 hello Microsoft 驗證程式庫 (MSAL) tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="2665f-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="2665f-104">開啟`ViewController.swift`並取代與 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="2665f-104">Open `ViewController.swift` and replace hello code with:</span></span>

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
### <a name="more-information"></a><span data-ttu-id="2665f-105">相關資訊</span><span class="sxs-lookup"><span data-stu-id="2665f-105">More Information</span></span>
#### <a name="getting-a-user-token-interactively"></a><span data-ttu-id="2665f-106">以互動方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="2665f-106">Getting a user token interactively</span></span>
<span data-ttu-id="2665f-107">呼叫 hello`acquireToken`方法的結果，在瀏覽器視窗，提示 hello 使用者 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="2665f-107">Calling hello `acquireToken` method results in a browser window prompting hello user toosign in.</span></span> <span data-ttu-id="2665f-108">應用程式通常需要以互動方式 hello 中的使用者 toosign 第一次需要 tooaccess 受保護的資源，或無訊息作業 tooacquire 權杖就會失敗 （例如 hello 使用者密碼到期時）。</span><span class="sxs-lookup"><span data-stu-id="2665f-108">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="2665f-109">以無訊息方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="2665f-109">Getting a user token silently</span></span>
<span data-ttu-id="2665f-110">hello`acquireTokenSilent`方法會處理語彙基元收購並沒有任何使用者互動的更新。</span><span class="sxs-lookup"><span data-stu-id="2665f-110">hello `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="2665f-111">之後`acquireToken`會針對要執行 hello 第一次， `acquireTokenSilent` hello 方法常用 tooobtain 權杖 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="2665f-111">After `acquireToken` is executed for hello first time, `acquireTokenSilent` is hello method commonly used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>

<span data-ttu-id="2665f-112">最後，`acquireTokenSilent`將會失敗 – 例如 hello 使用者已登出，或已變更其密碼，另一個裝置上的。</span><span class="sxs-lookup"><span data-stu-id="2665f-112">Eventually, `acquireTokenSilent` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="2665f-113">當 MSAL 偵測到 hello 問題可透過要求互動的動作來解決時，它就會引發`MSALErrorCode.interactionRequired`例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2665f-113">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MSALErrorCode.interactionRequired` exception.</span></span> <span data-ttu-id="2665f-114">您的應用程式可以透過兩種方式處理此例外狀況：</span><span class="sxs-lookup"><span data-stu-id="2665f-114">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="2665f-115">進行呼叫，以針對`acquireToken`立即，而這會造成提示 hello 使用者 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="2665f-115">Make a call against `acquireToken` immediately, which results in prompting hello user toosign in.</span></span> <span data-ttu-id="2665f-116">此模式通常用於線上應用程式在沒有離線內容 hello 應用程式中可供 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2665f-116">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="2665f-117">此 「 引導式的安裝程式所產生的 hello 範例應用程式會使用此模式： 您可以看到它在動作 hello 執行 hello 應用程式的第一次。</span><span class="sxs-lookup"><span data-stu-id="2665f-117">hello sample application generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello application.</span></span> <span data-ttu-id="2665f-118">因為沒有使用者曾使用 hello 應用程式，`applicationContext.users().first`會包含 null 值，和` MSALErrorCode.interactionRequired `擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="2665f-118">Because no user ever used hello application, `applicationContext.users().first` will contain a null value, and an ` MSALErrorCode.interactionRequired ` exception will be thrown.</span></span> <span data-ttu-id="2665f-119">hello hello 範例中的程式碼，則控制代碼藉由呼叫 hello 例外狀況`acquireToken`導致提示中的 hello 使用者 toosign。</span><span class="sxs-lookup"><span data-stu-id="2665f-119">hello code in hello sample then handles hello exception by calling `acquireToken` resulting in prompting hello user toosign in.</span></span>

2.  <span data-ttu-id="2665f-120">應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`acquireTokenSilent`稍後。</span><span class="sxs-lookup"><span data-stu-id="2665f-120">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `acquireTokenSilent` at a later time.</span></span> <span data-ttu-id="2665f-121">這通常用於 hello 使用者可以使用 hello 應用程式的其他功能，而不被中斷-例如，沒有離線內容 hello 應用程式中提供。</span><span class="sxs-lookup"><span data-stu-id="2665f-121">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="2665f-122">在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊，或您的應用程式可以決定 tooretry`acquireTokenSilent`網路還原之後變成暫時無法使用時。</span><span class="sxs-lookup"><span data-stu-id="2665f-122">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `acquireTokenSilent` when network is restored after being unavailable temporarily.</span></span>

<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="2665f-123">呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元</span><span class="sxs-lookup"><span data-stu-id="2665f-123">Call hello Microsoft Graph API using hello token you just obtained</span></span>

<span data-ttu-id="2665f-124">新增下列 hello 新方法太`ViewController.swift`。</span><span class="sxs-lookup"><span data-stu-id="2665f-124">Add hello new method below too`ViewController.swift`.</span></span> <span data-ttu-id="2665f-125">這個方法是使用的 toomake`GET`對 hello Microsoft Graph API 使用要求*HTTP 授權標頭*:</span><span class="sxs-lookup"><span data-stu-id="2665f-125">This method is used toomake a `GET` request against hello Microsoft Graph API using an *HTTP Authorization header*:</span></span>

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
### <a name="making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="2665f-126">針對受保護 API 進行 REST 呼叫</span><span class="sxs-lookup"><span data-stu-id="2665f-126">Making a REST call against a protected API</span></span>

<span data-ttu-id="2665f-127">在此範例應用程式，hello`getContentWithToken()`方法是使用的 toomake HTTP`GET`針對受保護的資源需要權杖，然後再回到 hello 內容 toohello 呼叫端要求。</span><span class="sxs-lookup"><span data-stu-id="2665f-127">In this sample application, hello `getContentWithToken()` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="2665f-128">這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。</span><span class="sxs-lookup"><span data-stu-id="2665f-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="2665f-129">此範例中，hello 資源為 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="2665f-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="set-up-sign-out"></a><span data-ttu-id="2665f-130">設定登出</span><span class="sxs-lookup"><span data-stu-id="2665f-130">Set up sign-out</span></span>

<span data-ttu-id="2665f-131">新增下列方法太 hello`ViewController.swift` toosign 出 hello 使用者：</span><span class="sxs-lookup"><span data-stu-id="2665f-131">Add hello following method too`ViewController.swift` toosign out hello user:</span></span>

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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="2665f-132">關於登出的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2665f-132">More info on sign-out</span></span>

<span data-ttu-id="2665f-133">hello`signoutButton`方法 hello 使用者移除 hello MSAL 使用者快取 – 這會有效地指示 MSAL tooforget hello 目前使用者讓未來的要求 tooacquire 語彙基元才會成功則由 toobe 互動式。</span><span class="sxs-lookup"><span data-stu-id="2665f-133">hello `signoutButton` method removes hello user from hello MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>

<span data-ttu-id="2665f-134">雖然此範例中的 hello 應用程式支援單一使用者，但是 MSAL 支援的案例，其中多個帳戶可以登入在 hello 相同時間 – 範例可以是電子郵件應用程式使用者有多個帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="2665f-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="register-hello-callback"></a><span data-ttu-id="2665f-135">註冊 hello 回呼</span><span class="sxs-lookup"><span data-stu-id="2665f-135">Register hello callback</span></span>

<span data-ttu-id="2665f-136">Hello 使用者進行驗證時，一旦 hello 瀏覽器重新導向 hello 使用者回復 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2665f-136">Once hello user authenticates, hello browser redirects hello user back toohello application.</span></span> <span data-ttu-id="2665f-137">請遵循以下 tooregister 的 hello 步驟這個回呼：</span><span class="sxs-lookup"><span data-stu-id="2665f-137">Follow hello steps below tooregister this callback:</span></span>

1.  <span data-ttu-id="2665f-138">開啟 `AppDelegate.swift` 並匯入 MSAL：</span><span class="sxs-lookup"><span data-stu-id="2665f-138">Open `AppDelegate.swift` and import MSAL:</span></span>

```swift
import MSAL
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2665f-139">新增下列方法 tooyour hello<code>AppDelegate</code>類別 toohandle 回呼：</span><span class="sxs-lookup"><span data-stu-id="2665f-139">Add hello following method tooyour <code>AppDelegate</code> class toohandle callbacks:</span></span>
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

