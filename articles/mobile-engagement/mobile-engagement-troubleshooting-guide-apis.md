---
title: "aaaAzure Mobile Engagement 疑難排解指南-應用程式開發介面"
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
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a><span data-ttu-id="234d8-103">API 問題的疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="234d8-103">Troubleshooting guide for API issues</span></span>
<span data-ttu-id="234d8-104">hello 以下是可能的問題，您可能會遇到與系統管理員的互動方式 Azure Mobile Engagement 透過 hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="234d8-104">hello following are possible issues you may encounter with how administrators interact with Azure Mobile Engagement via hello APIs.</span></span>

## <a name="syntax-issues"></a><span data-ttu-id="234d8-105">語法問題</span><span class="sxs-lookup"><span data-stu-id="234d8-105">Syntax issues</span></span>
### <a name="issue"></a><span data-ttu-id="234d8-106">問題</span><span class="sxs-lookup"><span data-stu-id="234d8-106">Issue</span></span>
* <span data-ttu-id="234d8-107">使用 hello 應用程式開發介面 （或未預期的行為） 的語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="234d8-107">Syntax Errors using hello API (or unexpected behavior).</span></span>

### <a name="causes"></a><span data-ttu-id="234d8-108">原因</span><span class="sxs-lookup"><span data-stu-id="234d8-108">Causes</span></span>
* <span data-ttu-id="234d8-109">語法問題：</span><span class="sxs-lookup"><span data-stu-id="234d8-109">Syntax issues:</span></span>
  * <span data-ttu-id="234d8-110">請確定 toocheck hello hello 特定 API 所使用的語法 hello 選項的 tooconfirm 為止。</span><span class="sxs-lookup"><span data-stu-id="234d8-110">Make sure toocheck hello Syntax of hello specific API you are using tooconfirm that hello option is available.</span></span>
  * <span data-ttu-id="234d8-111">API 使用方式的一般問題是 tooconfuse hello 觸達 API 和 hello 推送應用程式開發介面 （大部分的工作應該執行以 hello 觸達 API 而不是 hello 推送應用程式開發介面）。</span><span class="sxs-lookup"><span data-stu-id="234d8-111">A common issue with API usage is tooconfuse hello Reach API and hello Push API (most tasks should be performed with hello Reach API instead of hello Push API).</span></span> 
  * <span data-ttu-id="234d8-112">另一個常見的問題與 SDK 整合及應用程式開發介面使用方式為 tooconfuse hello SDK 金鑰和 hello API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="234d8-112">Another common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>
  * <span data-ttu-id="234d8-113">連接 toohello Api 的指令碼需要 toosend 資料，至少每隔 10 分鐘或 hello 連接逾時 （特別是通常在接聽資料監視器 API 指令碼）。</span><span class="sxs-lookup"><span data-stu-id="234d8-113">Scripts that connect toohello APIs need toosend data at least every 10 minutes or hello connection will time out (especially common in Monitor API scripts listening for data).</span></span> <span data-ttu-id="234d8-114">tooprevent 逾時，必須將指令碼傳送 XMPP ping 活動與 hello 伺服器每隔 10 分鐘 tookeep hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="234d8-114">tooprevent timeouts, have your script send an XMPP ping every 10 minutes tookeep hello session alive with hello server.</span></span>

### <a name="see-also"></a><span data-ttu-id="234d8-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="234d8-115">See also</span></span>
* <span data-ttu-id="234d8-116">[API 文件][Link 4]</span><span class="sxs-lookup"><span data-stu-id="234d8-116">[API Documentation][Link 4]</span></span>
* [<span data-ttu-id="234d8-117">XMPP 通訊協定資訊</span><span class="sxs-lookup"><span data-stu-id="234d8-117">XMPP Protocol Info</span></span>](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a><span data-ttu-id="234d8-118">無法 toouse hello API tooperform hello hello Azure Mobile Engagement UI 中相同的動作</span><span class="sxs-lookup"><span data-stu-id="234d8-118">Unable toouse hello API tooperform hello same action available in hello Azure Mobile Engagement UI</span></span>
### <a name="issue"></a><span data-ttu-id="234d8-119">問題</span><span class="sxs-lookup"><span data-stu-id="234d8-119">Issue</span></span>
* <span data-ttu-id="234d8-120">運作方式與 hello 從 hello 不適用於 Azure Mobile Engagement UI 動作的相關 Azure Mobile Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="234d8-120">An action that works from hello Azure Mobile Engagement UI doesn't work from hello related Azure Mobile Engagement API.</span></span>

### <a name="causes"></a><span data-ttu-id="234d8-121">原因</span><span class="sxs-lookup"><span data-stu-id="234d8-121">Causes</span></span>
* <span data-ttu-id="234d8-122">確認您可以執行相同的動作，從 hello Azure Mobile Engagement UI 會顯示您已正確整合與 Azure Mobile Engagement 的這項功能的 hello hello SDK。</span><span class="sxs-lookup"><span data-stu-id="234d8-122">Confirming that you can perform hello same action from hello Azure Mobile Engagement UI shows that you have correctly integrated this feature of Azure Mobile Engagement with hello SDK.</span></span>

### <a name="see-also"></a><span data-ttu-id="234d8-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="234d8-123">See also</span></span>
* <span data-ttu-id="234d8-124">[UI 文件][Link 1]</span><span class="sxs-lookup"><span data-stu-id="234d8-124">[UI Documentation][Link 1]</span></span>

## <a name="error-messages"></a><span data-ttu-id="234d8-125">錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="234d8-125">Error Messages</span></span>
### <a name="issue"></a><span data-ttu-id="234d8-126">問題</span><span class="sxs-lookup"><span data-stu-id="234d8-126">Issue</span></span>
* <span data-ttu-id="234d8-127">使用顯示在執行階段或記錄檔中的 hello API 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="234d8-127">Error codes using hello API displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="234d8-128">原因</span><span class="sxs-lookup"><span data-stu-id="234d8-128">Causes</span></span>
* <span data-ttu-id="234d8-129">以下是供參考和初步疑難排解使用之一般 API 狀態碼號碼的複合清單：</span><span class="sxs-lookup"><span data-stu-id="234d8-129">Here is a composite list of common API status codes numbers for reference and preliminary troubleshooting:</span></span>
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a><span data-ttu-id="234d8-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="234d8-130">See also</span></span>
* <span data-ttu-id="234d8-131">[API 文件 - 適用於每個特定 API 的詳細錯誤][Link 4]</span><span class="sxs-lookup"><span data-stu-id="234d8-131">[API Documentation - for detailed errors on each specific API][Link 4]</span></span>

## <a name="silent-failures"></a><span data-ttu-id="234d8-132">無訊息失敗</span><span class="sxs-lookup"><span data-stu-id="234d8-132">Silent failures</span></span>
### <a name="issue"></a><span data-ttu-id="234d8-133">問題</span><span class="sxs-lookup"><span data-stu-id="234d8-133">Issue</span></span>
* <span data-ttu-id="234d8-134">API 動作失敗，但執行階段或記錄檔中沒有顯示任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="234d8-134">API action fails with no error message displayed at runtime or in logs.</span></span>

### <a name="causes"></a><span data-ttu-id="234d8-135">原因</span><span class="sxs-lookup"><span data-stu-id="234d8-135">Causes</span></span>
* <span data-ttu-id="234d8-136">多個項目將會停用在 hello Azure Mobile Engagement UI 如果不正確，整合，但將會以無訊息模式失敗從 hello 應用程式開發介面，因此請記住 tootest hello hello UI toosee 從相同的功能，看看是否可行。</span><span class="sxs-lookup"><span data-stu-id="234d8-136">Many items will be disabled in hello Azure Mobile Engagement UI if they aren't integrated correctly, but will fail silently from hello API, so remember tootest hello same functionality from hello UI toosee if it works.</span></span>
* <span data-ttu-id="234d8-137">Azure Mobile Engagement，以及許多進階的功能的 Azure Mobile Engagement 嘗試 toouse，需要 toobe 個別整合到應用程式與 hello SDK 為個別的步驟才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="234d8-137">Azure Mobile Engagement, and many advanced features of Azure Mobile Engagement you are attempting toouse, need toobe individually integrated into your app with hello SDK as separate steps before you can use them.</span></span>

### <a name="see-also"></a><span data-ttu-id="234d8-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="234d8-138">See also</span></span>
* <span data-ttu-id="234d8-139">[疑難排解指南 - SDK][Link 25]</span><span class="sxs-lookup"><span data-stu-id="234d8-139">[Troubleshooting Guide - SDK][Link 25]</span></span>

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

