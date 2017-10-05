---
title: "Azure Mobile Engagement 疑難排解指南 - API"
description: "Azure Mobile Engagement 疑難排解指南 - API"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: a7ae0a83046f2d67b790f672dcd3ae261987357a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="9bd80-103">API 問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="9bd80-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="9bd80-104">以下是您可能遇到，有關系統管理員如何透過 API 與 Azure Mobile Engagement 互動的問題。</span><span class="sxs-lookup"><span data-stu-id="9bd80-104">The following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via the APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="9bd80-105">語法問題</span><span class="sxs-lookup"><span data-stu-id="9bd80-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="9bd80-106">問題</span><span class="sxs-lookup"><span data-stu-id="9bd80-106">Issue</span></span>
* <span data-ttu-id="9bd80-107">使用 API 的語法錯誤 (或非預期的行為)。</span><span class="sxs-lookup"><span data-stu-id="9bd80-107">Syntax Errors using the API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="9bd80-108">原因</span><span class="sxs-lookup"><span data-stu-id="9bd80-108">Causes</span></span>
* <span data-ttu-id="9bd80-109">語法問題：</span><span class="sxs-lookup"><span data-stu-id="9bd80-109">Syntax issues:</span></span>
  * <span data-ttu-id="9bd80-110">請務必檢查您正在使用之特定 API 的語法，以確認該選項可以使用。</span><span class="sxs-lookup"><span data-stu-id="9bd80-110">Make sure to check the Syntax of the specific API you are using to confirm that the option is available.</span></span>
  * <span data-ttu-id="9bd80-111">API 使用方式的一個常見問題是將觸達 API 與推送 API 混淆 (大部分工作應該是使用觸達 API 來執行，而不是使用推送 API 來執行)。</span><span class="sxs-lookup"><span data-stu-id="9bd80-111">A common issue with API usage is to confuse the Reach API and the Push API (most tasks should be performed with the Reach API instead of the Push API).</span></span> 
  * <span data-ttu-id="9bd80-112">SDK 整合與 API 使用方式的另一個常見問題是將 SDK 金鑰和 API 金鑰混淆。</span><span class="sxs-lookup"><span data-stu-id="9bd80-112">Another common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>
  * <span data-ttu-id="9bd80-113">連接到 API 的指令碼必須至少每 10 分鐘傳送一次資料，否則連線會逾時 (這在接聽資料的監視 API 指令碼中特別常見)。</span><span class="sxs-lookup"><span data-stu-id="9bd80-113">Scripts that connect to the APIs need to send data at least every 10 minutes or the connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="9bd80-114">若要避免逾時，請讓您的指令碼每 10 分鐘傳送一個 XMPP ping，以保持伺服器工作階段運作。</span><span class="sxs-lookup"><span data-stu-id="9bd80-114">To prevent timeouts, have your script send an XMPP ping every 10 minutes to keep the session alive with the server.</span></span>

### <a name="see-also"></a><span data-ttu-id="9bd80-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9bd80-115">See also</span></span>
* <span data-ttu-id="9bd80-116">[API 文件][Link 4]</span><span class="sxs-lookup"><span data-stu-id="9bd80-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="9bd80-117">XMPP 通訊協定資訊</span><span class="sxs-lookup"><span data-stu-id="9bd80-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-to-use-the-api-to-perform-the-same-action-available-in-the-azure-mobile-engagement-ui"></a><span data-ttu-id="9bd80-118">無法使用 API 執行 Azure Mobile Engagement UI 中可用的相同動作</span><span class="sxs-lookup"><span data-stu-id="9bd80-118">Unable to use the API to perform the same action available in the Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="9bd80-119">問題</span><span class="sxs-lookup"><span data-stu-id="9bd80-119">Issue</span></span>
* <span data-ttu-id="9bd80-120">可從 Azure Mobile Engagement UI 運作的動作，無法從相關的 Azure Mobile Engagement API 運作。</span><span class="sxs-lookup"><span data-stu-id="9bd80-120">An action that works from the Azure Mobile Engagement UI doesn't work from the related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="9bd80-121">原因</span><span class="sxs-lookup"><span data-stu-id="9bd80-121">Causes</span></span>
* <span data-ttu-id="9bd80-122">確認您可以從 Azure Mobile Engagement UI 執行相同的動作之後，即表示您已正確地將 Azure Mobile Engagement 的這項功能與 SDK 整合。</span><span class="sxs-lookup"><span data-stu-id="9bd80-122">Confirming that you can perform the same action from the Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with the SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="9bd80-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9bd80-123">See also</span></span>
* <span data-ttu-id="9bd80-124">[UI 文件][Link 1]</span><span class="sxs-lookup"><span data-stu-id="9bd80-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="9bd80-125">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="9bd80-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="9bd80-126">問題</span><span class="sxs-lookup"><span data-stu-id="9bd80-126">Issue</span></span>
* <span data-ttu-id="9bd80-127">使用 API 時在執行階段或記錄檔中顯示的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="9bd80-127">Error codes using the API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="9bd80-128">原因</span><span class="sxs-lookup"><span data-stu-id="9bd80-128">Causes</span></span>
* <span data-ttu-id="9bd80-129">以下是供參考和初步疑難排解使用之一般 API 狀態碼號碼的複合清單：</span><span class="sxs-lookup"><span data-stu-id="9bd80-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from the current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in the response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). The parameters provided to the API or service are invalid. In this case, the HTTP response will embed more details. Make sure to test for the MIME type of the response as the payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check the AppID and SDK key).
        402        Billing lock. The application is either off its quotas or is currently in a bad billing state.
        403        The application is not enabled or the specific API is disabled for this application.
        403        Unauthorized access to the project or application, invalid access key (the key must match the one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), the suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and the campaign’s property named, manual Push must be set to true.
        403        The email address is already associated to another account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        The email address is not associated with an account. Please create or update the account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying to edit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for the first time.
        409        Name already associated to a different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or the period is too large to be displayed (the server didn’t retrieve the analytics because the user request is for a period that is too large).
        503        Analytics not available yet (the requested information is not computed yet for an application).
        504        The server was not able to handle your request in a reasonable time (if you make multiple calls to an API very quickly, try to make one call at a time and spread the calls out over time).

### <a name="see-also"></a><span data-ttu-id="9bd80-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9bd80-130">See also</span></span>
* <span data-ttu-id="9bd80-131">[API 文件 - 適用於每個特定 API 的詳細錯誤][Link 4]</span><span class="sxs-lookup"><span data-stu-id="9bd80-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="9bd80-132">無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="9bd80-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="9bd80-133">問題</span><span class="sxs-lookup"><span data-stu-id="9bd80-133">Issue</span></span>
* <span data-ttu-id="9bd80-134">API 動作失敗，但執行階段或記錄檔中沒有顯示任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="9bd80-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="9bd80-135">原因</span><span class="sxs-lookup"><span data-stu-id="9bd80-135">Causes</span></span>
* <span data-ttu-id="9bd80-136">如果項目整合不正確，Azure Mobile Engagement UI 中的許多項目將會停用，但會從 API 以無訊息方式發生失敗，因此請記得從 UI 測試相同功能，以查看功能是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="9bd80-136">Many items will be disabled in the Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from the API, so remember to test the same functionality from the UI to see if it works.</span></span>
* <span data-ttu-id="9bd80-137">Azure Mobile Engagement 以及許多您嘗試使用的 Azure Mobile Engagement 進階功能，都需要使用 SDK 以獨立步驟方式個別整合到您的應用程式中，您才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="9bd80-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting to use, need to be individually integrated into your app with the SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="9bd80-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9bd80-138">See also</span></span>
* <span data-ttu-id="9bd80-139">[疑難排解指南 - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="9bd80-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

