---
title: "aaaAzure AD v2 iOS 入門-測試 |Microsoft 文件"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="aa5d4-103">測試查詢 hello Microsoft Graph API 從 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa5d4-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="aa5d4-104">按`Command`  +  `R` toorun hello 模擬器中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="aa5d4-106">當您準備好 tootest 時，點選*' 呼叫 Microsoft Graph API'*而且您將會提示的 tootype，您的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="aa5d4-107">同意</span><span class="sxs-lookup"><span data-stu-id="aa5d4-107">Consent</span></span>
<span data-ttu-id="aa5d4-108">hello 第一次您登入 tooyour 應用程式，您會看到類似 toohello 下列同意畫面，您需要在 tooexplicitly 接受：</span><span class="sxs-lookup"><span data-stu-id="aa5d4-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![同意畫面](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="aa5d4-110">預期的結果</span><span class="sxs-lookup"><span data-stu-id="aa5d4-110">Expected results</span></span>
<span data-ttu-id="aa5d4-111">您應該會看到在 hello hello Microsoft Graph API 呼叫所傳回的使用者設定檔資訊*記錄*> 一節。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="aa5d4-112">與範圍和委派的權限有關的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="aa5d4-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="aa5d4-113">hello Microsoft Graph API 需要 hello`user.read`範圍 tooread hello 使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="aa5d4-114">根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="aa5d4-115">Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="aa5d4-116">例如，針對 Microsoft Graph hello 範圍`Calendars.Read`是必要的 toolist hello 使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="aa5d4-117">順序 tooaccess hello 使用者的行事曆應用程式的內容中，您需要 tooadd hello`Calendars.Read`委派權限 toohello 應用程式註冊的資訊，然後再加入 hello`Calendars.Read`範圍 toohello`acquireTokenSilent`呼叫。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="aa5d4-118">隨著您增加 hello 範圍數目，可能會提示 hello 使用者輸入其他的同意授權。</span><span class="sxs-lookup"><span data-stu-id="aa5d4-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



