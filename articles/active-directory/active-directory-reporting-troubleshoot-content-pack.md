---
title: "對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解 | Microsoft Docs"
description: "為您提供 Azure Active Directory 活動內容套件的錯誤訊息清單以及修正它們的步驟。"
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
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="9dd00-103">對 Azure Active Directory 活動記錄內容套件錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="9dd00-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="9dd00-104">使用適用於 Azure Active Directory 預覽版的 Power BI 內容套件時，可能會遇到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="9dd00-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="9dd00-105">重新整理失敗</span><span class="sxs-lookup"><span data-stu-id="9dd00-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="9dd00-106">無法更新資料來源認證</span><span class="sxs-lookup"><span data-stu-id="9dd00-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="9dd00-107">匯入資料的時間太長</span><span class="sxs-lookup"><span data-stu-id="9dd00-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="9dd00-108">本主題為您提供可能的原因以及如何修正這些錯誤的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9dd00-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="9dd00-109">重新整理失敗</span><span class="sxs-lookup"><span data-stu-id="9dd00-109">Refresh failed</span></span> 
 
<span data-ttu-id="9dd00-110">**此錯誤的呈現方式**：從 Power BI 寄送電子郵件，或是重新整理記錄中的失敗狀態。</span><span class="sxs-lookup"><span data-stu-id="9dd00-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="9dd00-111">原因</span><span class="sxs-lookup"><span data-stu-id="9dd00-111">Cause</span></span> | <span data-ttu-id="9dd00-112">修正方式</span><span class="sxs-lookup"><span data-stu-id="9dd00-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9dd00-113">若連線到內容套件的使用者認證已重設，但卻未在內容套件的連線設定中加以更新，即會導致重新整理失敗錯誤。</span><span class="sxs-lookup"><span data-stu-id="9dd00-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="9dd00-114">在 Power BI 中，找出對應到 Azure Active Directory 活動記錄儀表板 (Azure Active Directory 活動記錄) 的資料集、選擇 [排程重新整理]，然後輸入您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="9dd00-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="9dd00-115">重新整理可能會因為基礎內容套件中的資料問題而失敗。</span><span class="sxs-lookup"><span data-stu-id="9dd00-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="9dd00-116">提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="9dd00-116">File a support ticket.</span></span> <span data-ttu-id="9dd00-117">如需詳細資訊，請參閱[如何取得 Azure Active Directory 支援](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="9dd00-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="9dd00-118">無法更新資料來源認證</span><span class="sxs-lookup"><span data-stu-id="9dd00-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="9dd00-119">**此錯誤的呈現方式**：在 Power BI 中，當您連線到 Azure Active Directory 活動記錄 (預覽) 內容套件時。</span><span class="sxs-lookup"><span data-stu-id="9dd00-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="9dd00-120">原因</span><span class="sxs-lookup"><span data-stu-id="9dd00-120">Cause</span></span> | <span data-ttu-id="9dd00-121">修正方式</span><span class="sxs-lookup"><span data-stu-id="9dd00-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9dd00-122">連線的使用者既不是全域系統管理員，也不是安全性讀取者或安全性系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9dd00-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="9dd00-123">使用非全域系統管理員或安全性讀取者或安全性系統管理員的帳戶來存取內容套件。</span><span class="sxs-lookup"><span data-stu-id="9dd00-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="9dd00-124">您的租用戶不是 Premium 租用戶，或者沒有任何具備 Premium 授權檔案的使用者。</span><span class="sxs-lookup"><span data-stu-id="9dd00-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="9dd00-125">提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="9dd00-125">File a support ticket.</span></span> <span data-ttu-id="9dd00-126">如需詳細資訊，請參閱[如何取得 Azure Active Directory 支援](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="9dd00-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="9dd00-127">匯入資料的時間太長</span><span class="sxs-lookup"><span data-stu-id="9dd00-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="9dd00-128">**此錯誤的呈現方式**：在 Power BI 中，一旦連線到內容套件之後，資料匯入程序就會開始準備您的儀表板以用於 Azure Active Directory 活動記錄。</span><span class="sxs-lookup"><span data-stu-id="9dd00-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="9dd00-129">您會看見下列訊息：「正在匯入資料...」</span><span class="sxs-lookup"><span data-stu-id="9dd00-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="9dd00-130">原因</span><span class="sxs-lookup"><span data-stu-id="9dd00-130">Cause</span></span> | <span data-ttu-id="9dd00-131">修正方式</span><span class="sxs-lookup"><span data-stu-id="9dd00-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="9dd00-132">根據您的租用戶大小而定，此步驟所需的時間可能從數分鐘到 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9dd00-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="9dd00-133">請耐心等候。</span><span class="sxs-lookup"><span data-stu-id="9dd00-133">Just be patient.</span></span> <span data-ttu-id="9dd00-134">如果訊息未在一小時內變更以顯示您的儀表板，請提出支援票證。</span><span class="sxs-lookup"><span data-stu-id="9dd00-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="9dd00-135">如需詳細資訊，請參閱[如何取得 Azure Active Directory 支援](active-directory-troubleshooting-support-howto.md)。</span><span class="sxs-lookup"><span data-stu-id="9dd00-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="9dd00-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dd00-136">Next steps</span></span>

<span data-ttu-id="9dd00-137">若要安裝適用於 Azure Active Directory 預覽版的 Power BI 內容套件，請按一下[這裡](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="9dd00-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


