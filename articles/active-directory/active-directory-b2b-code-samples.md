---
title: "aaaAzure Active Directory B2B 共同作業程式碼和 PowerShell 範例 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業的程式碼與 PowerShell 範例"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 8e4f66fcb50d190899304831ea7ccd2203c5468c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a><span data-ttu-id="6f564-103">Azure Active Directory B2B 共同作業程式碼與 PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="6f564-103">Azure Active Directory B2B collaboration code and PowerShell samples</span></span>

## <a name="powershell-example"></a><span data-ttu-id="6f564-104">PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="6f564-104">PowerShell example</span></span>
<span data-ttu-id="6f564-105">您可以大量-邀請外部使用者 tooan 組織從您儲存中的電子郵件地址。CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f564-105">You can bulk-invite external users tooan organization from email addresses that you have stored in a .CSV file.</span></span>

1. <span data-ttu-id="6f564-106">準備 hello。CSV 檔案建立一個新的 CSV 檔案，並將它命名為 invitations.csv。</span><span class="sxs-lookup"><span data-stu-id="6f564-106">Prepare hello .CSV file Create a new CSV file and name it invitations.csv.</span></span> <span data-ttu-id="6f564-107">在此範例中，hello 檔案會儲存在 C:\data，並包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="6f564-107">In this example, hello file is saved in C:\data, and contains hello following information:</span></span>
  
  <span data-ttu-id="6f564-108">名稱</span><span class="sxs-lookup"><span data-stu-id="6f564-108">Name</span></span>                  |  <span data-ttu-id="6f564-109">InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="6f564-109">InvitedUserEmailAddress</span></span>
  --------------------- | --------------------------
  <span data-ttu-id="6f564-110">Gmail B2B 受邀者</span><span class="sxs-lookup"><span data-stu-id="6f564-110">Gmail B2B Invitee</span></span>     | b2binvitee@gmail.com
  <span data-ttu-id="6f564-111">Outlook B2B 受邀者</span><span class="sxs-lookup"><span data-stu-id="6f564-111">Outlook B2B invitee</span></span>   | b2binvitee@outlook.com


2. <span data-ttu-id="6f564-112">取得最新 Azure AD PowerShell toouse hello hello 新的 cmdlet，您必須安裝更新的 hello Azure AD PowerShell 模組，您可以從下載[hello Powershell 模組版本頁面](https://www.powershellgallery.com/packages/AzureADPreview)</span><span class="sxs-lookup"><span data-stu-id="6f564-112">Get hello latest Azure AD PowerShell toouse hello new cmdlets, you must install hello updated Azure AD PowerShell module, which you can download from [hello Powershell module's release page](https://www.powershellgallery.com/packages/AzureADPreview)</span></span>

3. <span data-ttu-id="6f564-113">登入 tooyour 租用戶</span><span class="sxs-lookup"><span data-stu-id="6f564-113">Sign in tooyour tenancy</span></span>

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. <span data-ttu-id="6f564-114">執行 hello PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="6f564-114">Run hello PowerShell cmdlet</span></span>

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

<span data-ttu-id="6f564-115">這個指令程式會傳送邀請 toohello 電子郵件地址 invitations.csv。</span><span class="sxs-lookup"><span data-stu-id="6f564-115">This cmdlet sends an invitation toohello email addresses in invitations.csv.</span></span> <span data-ttu-id="6f564-116">此 Cmdlet 的其他功能包括︰</span><span class="sxs-lookup"><span data-stu-id="6f564-116">Additional features of this cmdlet include:</span></span>
- <span data-ttu-id="6f564-117">Hello 電子郵件訊息中的自訂的文字</span><span class="sxs-lookup"><span data-stu-id="6f564-117">Customized text in hello email message</span></span>
- <span data-ttu-id="6f564-118">包括 hello 的顯示名稱受邀使用者</span><span class="sxs-lookup"><span data-stu-id="6f564-118">Including a display name for hello invited user</span></span>
- <span data-ttu-id="6f564-119">傳送訊息 tooCCs 或完全隱藏電子郵件訊息</span><span class="sxs-lookup"><span data-stu-id="6f564-119">Sending messages tooCCs or suppressing email messages altogether</span></span>

## <a name="code-sample"></a><span data-ttu-id="6f564-120">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6f564-120">Code sample</span></span>
<span data-ttu-id="6f564-121">這裡，我們將說明如何 toocall hello 邀請應用程式開發介面，在 「 應用程式-僅限 」 模式中的，您邀請的 hello 資源 toowhich tooget hello 兌換 URL hello B2B 使用者。</span><span class="sxs-lookup"><span data-stu-id="6f564-121">Here we illustrate how toocall hello invitation API, in "app-only" mode, tooget hello redemption URL for hello resource toowhich you are inviting hello B2B user.</span></span> <span data-ttu-id="6f564-122">hello 目標是 toosend 自訂邀請電子郵件。</span><span class="sxs-lookup"><span data-stu-id="6f564-122">hello goal is toosend a custom invitation email.</span></span> <span data-ttu-id="6f564-123">可以使用 HTTP 用戶端中，撰寫 hello 電子郵件，讓您可以自訂其外觀，並將它傳送到 Graph API。</span><span class="sxs-lookup"><span data-stu-id="6f564-123">hello email can be composed with an HTTP client, so you can customize how it looks and send it through Graph API.</span></span>

```
namespace SampleInviteApp
{
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    class Program
    {
        /// <summary>
        /// Microsoft graph resource.
        /// </summary>
        static readonly string GraphResource = "https://graph.microsoft.com";
 
        /// <summary>
        /// Microsoft graph invite endpoint.
        /// </summary>
        static readonly string InviteEndPoint = "https://graph.microsoft.com/v1.0/invitations";
 
        /// <summary>
        ///  Authentication endpoint tooget token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is hello tenantid of hello tenant you want tooinvite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is hello application id of hello application that is registered in hello above tenant.
        /// hello required scopes are available in hello below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of hello application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is hello email address of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is hello display name of hello user you want tooinvite.
        /// </summary>
        private static readonly string InvitedUserDisplayName = @"";
 
        /// <summary>
        /// Main method.
        /// </summary>
        /// <param name="args">Optional arguments</param>
        static void Main(string[] args)
        {
            Invitation invitation = CreateInvitation();
            SendInvitation(invitation);
        }
 
        /// <summary>
        /// Create hello invitation object.
        /// </summary>
        /// <returns>Returns hello invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set hello invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send hello guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make hello invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get hello HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns hello Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for hello request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get hello access token for our application tootalk toomicrosoft graph.
        /// </summary>
        /// <returns>Returns hello access token for our application tootalk toomicrosoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get hello access token for our application tootalk toomicrosoft graph.
            try
            {
                AuthenticationContext testAuthContext =
                    new AuthenticationContext(string.Format("{0}/{1}", EstsLoginEndpoint, TenantID));
                AuthenticationResult testAuthResult = testAuthContext.AcquireTokenAsync(
                    GraphResource,
                    new ClientCredential(TestAppClientId, TestAppClientSecret)).Result;
                accessToken = testAuthResult.AccessToken;
            }
            catch (AdalException ex)
            {
                Console.WriteLine("An exception was thrown while fetching hello token: {0}.", ex);
                throw;
            }
 
            return accessToken;
        }
 
        /// <summary>
        /// Invitation class.
        /// </summary>
        public class Invitation
        {
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserDisplayName { get; set; }
 
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserEmailAddress { get; set; }
 
            /// <summary>
            /// Gets or sets a value indicating whether Invitation Manager should send hello email tooInvitedUser.
            /// </summary>
            public bool SendInvitationMessage { get; set; }
 
            /// <summary>
            /// Gets or sets invitation redirect URL
            /// </summary>
            public string InviteRedirectUrl { get; set; }
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="6f564-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f564-124">Next steps</span></span>

<span data-ttu-id="6f564-125">請瀏覽有關 Azure AD B2B 共同作業的其他文章：</span><span class="sxs-lookup"><span data-stu-id="6f564-125">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6f564-126">何謂 Azure AD B2B 共同作業？</span><span class="sxs-lookup"><span data-stu-id="6f564-126">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6f564-127">B2B 共同作業使用者屬性</span><span class="sxs-lookup"><span data-stu-id="6f564-127">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="6f564-128">新增 B2B 共同作業使用者 tooa 角色</span><span class="sxs-lookup"><span data-stu-id="6f564-128">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="6f564-129">委派 B2B 共同作業邀請</span><span class="sxs-lookup"><span data-stu-id="6f564-129">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="6f564-130">動態群組和 B2B 共同作業</span><span class="sxs-lookup"><span data-stu-id="6f564-130">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="6f564-131">設定適用於 B2B 共同作業的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f564-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="6f564-132">B2B 共同作業使用者權杖</span><span class="sxs-lookup"><span data-stu-id="6f564-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="6f564-133">B2B 共同作業使用者宣告對應</span><span class="sxs-lookup"><span data-stu-id="6f564-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="6f564-134">Office 365 外部共用</span><span class="sxs-lookup"><span data-stu-id="6f564-134">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="6f564-135">B2B 共同作業目前的限制</span><span class="sxs-lookup"><span data-stu-id="6f564-135">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
