---
title: "aaaAzure AD v2 Android 快速入門-使用 |Microsoft 文件"
description: "Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API，或呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="4e93c-103">用於 hello Microsoft Graph API 中的 hello Microsoft 驗證程式庫 (MSAL) tooget 語彙基元</span><span class="sxs-lookup"><span data-stu-id="4e93c-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

1.  <span data-ttu-id="4e93c-104">開啟：`MainActivity` (在 `app` > `java` > `{domain}.{appname}` 底下)</span><span class="sxs-lookup"><span data-stu-id="4e93c-104">Open: `MainActivity` (under `app` > `java` > `{domain}.{appname}`)</span></span>
2.  <span data-ttu-id="4e93c-105">加入下列 imports hello:</span><span class="sxs-lookup"><span data-stu-id="4e93c-105">Add hello following imports:</span></span>

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="4e93c-106">取代 hello`MainActivity`類別如下：</span><span class="sxs-lookup"><span data-stu-id="4e93c-106">Replace hello `MainActivity` class with below:</span></span>
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="4e93c-107">相關資訊</span><span class="sxs-lookup"><span data-stu-id="4e93c-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="4e93c-108">以互動方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="4e93c-108">Getting a user token interactive</span></span>
<span data-ttu-id="4e93c-109">呼叫 hello`AcquireTokenAsync`方法的結果 視窗，提示 hello 使用者 toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="4e93c-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="4e93c-110">應用程式通常需要以互動方式 hello 中的使用者 toosign 第一次需要 tooaccess 受保護的資源，或無訊息作業 tooacquire 權杖就會失敗 （例如 hello 使用者密碼到期時）。</span><span class="sxs-lookup"><span data-stu-id="4e93c-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="4e93c-111">以無訊息方式取得使用者權杖</span><span class="sxs-lookup"><span data-stu-id="4e93c-111">Getting a user token silently</span></span>
<span data-ttu-id="4e93c-112">`AcquireTokenSilentAsync` 會處理權杖取得和更新作業，不需要與使用者進行任何互動。</span><span class="sxs-lookup"><span data-stu-id="4e93c-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="4e93c-113">之後`AcquireTokenAsync`會針對要執行 hello 第一次， `AcquireTokenSilentAsync` hello 方法常用 tooobtain 語彙基元 tooaccess 呼叫 toorequest 的受保護的後續呼叫的資源，或更新權杖會以無訊息模式。</span><span class="sxs-lookup"><span data-stu-id="4e93c-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello method commonly used tooobtain tokens tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="4e93c-114">最後，`AcquireTokenSilentAsync`將會失敗 – 例如 hello 使用者已登出，或已變更其密碼，另一個裝置上的。</span><span class="sxs-lookup"><span data-stu-id="4e93c-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="4e93c-115">當 MSAL 偵測到 hello 問題可透過要求互動的動作來解決時，它就會引發`MsalUiRequiredException`。</span><span class="sxs-lookup"><span data-stu-id="4e93c-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="4e93c-116">您的應用程式可以透過兩種方式處理此例外狀況：</span><span class="sxs-lookup"><span data-stu-id="4e93c-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="4e93c-117">進行呼叫，以針對`AcquireTokenAsync`立即，這會導致提示 toosign 中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="4e93c-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="4e93c-118">此模式通常用於線上應用程式在沒有離線內容 hello 應用程式中可供 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="4e93c-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="4e93c-119">hello 此引導式的安裝程式所產生的範例會使用此模式： 您可以看到它動作 hello 中第一次執行 hello 範例： 沒有任何使用者都用過 hello 應用程式，因為`PublicClientApp.Users.FirstOrDefault`會包含 null 值，和`MsalUiRequiredException`擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="4e93c-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="4e93c-120">hello hello 範例中的程式碼，則控制代碼藉由呼叫 hello 例外狀況`AcquireTokenAsync`導致提示 toosign 中的 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="4e93c-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>
2.  <span data-ttu-id="4e93c-121">應用程式也可以進行互動式登入是必要項目，所以 hello 使用者可以選取 hello 正確的時間 toosign 中，或者 hello 應用程式可以重試的視覺指示 toohello 使用者`AcquireTokenSilentAsync`稍後。</span><span class="sxs-lookup"><span data-stu-id="4e93c-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="4e93c-122">這通常用於 hello 使用者是不被中斷的 hello 應用程式可以 tooaccess 功能-例如，沒有離線內容 hello 應用程式中提供。</span><span class="sxs-lookup"><span data-stu-id="4e93c-122">This is commonly used when hello user is able tooaccess functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="4e93c-123">在此情況下，hello 使用者可以決定當他們想 toosign tooaccess hello 受保護的資源，或 toorefresh hello 過期的資訊，或您的應用程式可以決定 tooretry`AcquireTokenSilentAsync`網路還原之後變成暫時無法使用時。</span><span class="sxs-lookup"><span data-stu-id="4e93c-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="4e93c-124">呼叫 hello Microsoft Graph API，使用您剛取得 hello 語彙基元</span><span class="sxs-lookup"><span data-stu-id="4e93c-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>
1.  <span data-ttu-id="4e93c-125">新增下列方法至 hello hello`MainActivity`類別：</span><span class="sxs-lookup"><span data-stu-id="4e93c-125">Add hello following methods into hello `MainActivity` class:</span></span>

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="4e93c-126">針對受保護 API 進行 REST 呼叫的相關詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4e93c-126">More information about making a REST call against a protected API</span></span>

<span data-ttu-id="4e93c-127">在此範例應用程式，`callGraphAPI`呼叫`getAccessToken`，然後將 HTTP`GET`針對資源需要權杖，並傳回 hello 內容要求。</span><span class="sxs-lookup"><span data-stu-id="4e93c-127">In this sample application, `callGraphAPI` calls `getAccessToken` and then makes an HTTP `GET` request against a resource that requires a token and returns hello content.</span></span> <span data-ttu-id="4e93c-128">這個方法會加入 hello 取得語彙基元中 hello *HTTP 授權標頭*。</span><span class="sxs-lookup"><span data-stu-id="4e93c-128">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="4e93c-129">此範例中，hello 資源為 hello Microsoft Graph API*我*端點 – 顯示 hello 使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="4e93c-129">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="setup-sign-out"></a><span data-ttu-id="4e93c-130">設定登出</span><span class="sxs-lookup"><span data-stu-id="4e93c-130">Setup Sign-out</span></span>

1.  <span data-ttu-id="4e93c-131">新增下列方法至 hello hello`MainActivity`類別：</span><span class="sxs-lookup"><span data-stu-id="4e93c-131">Add hello following methods into hello `MainActivity` class:</span></span>

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="4e93c-132">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4e93c-132">More information</span></span>

<span data-ttu-id="4e93c-133">`onSignOutClicked`移除上述 hello 使用者從 MSAL 使用者快取 – 這會有效地指示 MSAL tooforget hello 目前使用者讓未來的要求 tooacquire 語彙基元才會成功則由 toobe 互動式。</span><span class="sxs-lookup"><span data-stu-id="4e93c-133">`onSignOutClicked` above removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="4e93c-134">雖然此範例中的 hello 應用程式支援單一使用者，但是 MSAL 支援的案例，其中多個帳戶可以是登入在 hello 相同時間 – 範例可以是電子郵件應用程式使用者有多個帳戶的位置。</span><span class="sxs-lookup"><span data-stu-id="4e93c-134">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->
