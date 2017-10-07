---
title: "對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解 | Microsoft Docs"
description: "您提供的錯誤訊息的 hello Azure Active Directory 活動內容組件和步驟 toofix 清單它們。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="3128c-103">對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3128c-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="3128c-104">使用 Azure Active Directory preview hello Power BI 內容套件，它時可能遇到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="3128c-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="3128c-105">重新整理失敗</span><span class="sxs-lookup"><span data-stu-id="3128c-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="3128c-106">失敗的 tooupdate 資料來源認證</span><span class="sxs-lookup"><span data-stu-id="3128c-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="3128c-107">匯入資料的時間太長</span><span class="sxs-lookup"><span data-stu-id="3128c-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="3128c-108">本主題將提供您 hello 的可能原因的相關資訊及如何 toofix 這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="3128c-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="3128c-109">重新整理失敗</span><span class="sxs-lookup"><span data-stu-id="3128c-109">Refresh failed</span></span> 
 
<span data-ttu-id="3128c-110">**此錯誤會顯示如何**： 從 Power BI 或 hello 重新整理記錄中的失敗的狀態的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="3128c-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="3128c-111">原因</span><span class="sxs-lookup"><span data-stu-id="3128c-111">Cause</span></span> | <span data-ttu-id="3128c-112">如何 toofix</span><span class="sxs-lookup"><span data-stu-id="3128c-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3128c-113">重新整理的失敗時已重設 hello hello 連線的使用者 toohello 內容套件的認證，但不是會在 hello hello hello 內容套件的連接設定更新，可能導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="3128c-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="3128c-114">在 Power BI 中，找出 hello 資料集對應 toohello Azure Active Directory 活動記錄檔儀表板 （Azure Active Directory 活動記錄檔），選擇 排程重新整理，然後輸入您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="3128c-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="3128c-115">重新整理可能會在基礎內容套件的 hello toodata 問題而失敗。</span><span class="sxs-lookup"><span data-stu-id="3128c-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="3128c-116">提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="3128c-116">File a support ticket.</span></span> <span data-ttu-id="3128c-117">如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="3128c-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="3128c-118">失敗的 tooupdate 資料來源認證</span><span class="sxs-lookup"><span data-stu-id="3128c-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="3128c-119">**此錯誤會顯示如何**： 在 Power BI 中，當您連線 toohello Azure Active Directory 活動記錄 （預覽） 內容套件。</span><span class="sxs-lookup"><span data-stu-id="3128c-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="3128c-120">原因</span><span class="sxs-lookup"><span data-stu-id="3128c-120">Cause</span></span> | <span data-ttu-id="3128c-121">如何 toofix</span><span class="sxs-lookup"><span data-stu-id="3128c-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3128c-122">hello 連接的使用者是既不是全域管理員也不安全讀取器或安全性管理員。</span><span class="sxs-lookup"><span data-stu-id="3128c-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="3128c-123">使用全域管理員或安全性讀取器或安全性管理員 tooaccess hello 內容套件的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3128c-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="3128c-124">您的租用戶不是 Premium 租用戶，或者沒有任何具備 Premium 授權檔案的使用者。</span><span class="sxs-lookup"><span data-stu-id="3128c-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="3128c-125">提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="3128c-125">File a support ticket.</span></span> <span data-ttu-id="3128c-126">如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="3128c-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="3128c-127">匯入資料的時間太長</span><span class="sxs-lookup"><span data-stu-id="3128c-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="3128c-128">**此錯誤會顯示如何**： 在 Power BI 中，一旦您已經連接您的內容套件 hello 資料匯入程序啟動 tooprepare 儀表板的 Azure Active Directory 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3128c-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="3128c-129">您會看到 hello 訊息: 「*匯入資料...*"</span><span class="sxs-lookup"><span data-stu-id="3128c-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="3128c-130">原因</span><span class="sxs-lookup"><span data-stu-id="3128c-130">Cause</span></span> | <span data-ttu-id="3128c-131">如何 toofix</span><span class="sxs-lookup"><span data-stu-id="3128c-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="3128c-132">取決於您的租用戶的 hello 規模、 此步驟可能需要幾分鐘 too30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3128c-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="3128c-133">請耐心等候。</span><span class="sxs-lookup"><span data-stu-id="3128c-133">Just be patient.</span></span> <span data-ttu-id="3128c-134">如果 hello 訊息不會變更 tooshowing 儀表板在一小時內，請提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="3128c-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="3128c-135">如需詳細資訊，請參閱[tooget 如何支援 Azure Active directory](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="3128c-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="3128c-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3128c-136">Next steps</span></span>

<span data-ttu-id="3128c-137">按一下 tooinstall hello Azure Active Directory 預覽的 Power BI 內容套件[這裡](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/)。</span><span class="sxs-lookup"><span data-stu-id="3128c-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


