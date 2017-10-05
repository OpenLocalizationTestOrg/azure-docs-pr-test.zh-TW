---
title: "Azure MFA 的存取及使用報告 | Microsoft Docs"
description: "說明如何使用 Azure Multi-Factor Authentication 功能 - 報告。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: f76e726c6a67de4b0472c0e97f9e72c31c14c4f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="f6bd9-103">Azure Multi-Factor Authentication 中的報告</span><span class="sxs-lookup"><span data-stu-id="f6bd9-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="f6bd9-104">Azure Multi-Factor Authentication 提供數個供您和貴組織使用的報告。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="f6bd9-105">這些報告可透過 Multi-Factor Authentication 管理入口網站來存取。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-105">These reports can be accessed through the Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="f6bd9-106">以下是可用報告的清單：</span><span class="sxs-lookup"><span data-stu-id="f6bd9-106">The following is a list of the available reports:</span></span>

| <span data-ttu-id="f6bd9-107">報告</span><span class="sxs-lookup"><span data-stu-id="f6bd9-107">Report</span></span> | <span data-ttu-id="f6bd9-108">說明</span><span class="sxs-lookup"><span data-stu-id="f6bd9-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f6bd9-109">使用量</span><span class="sxs-lookup"><span data-stu-id="f6bd9-109">Usage</span></span> |<span data-ttu-id="f6bd9-110">使用量報告顯示有關整體使用量、使用者摘要和使用者詳細資料等資訊。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-110">The usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="f6bd9-111">伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="f6bd9-111">Server Status</span></span> |<span data-ttu-id="f6bd9-112">此報告會顯示與帳戶相關聯之 Multi-Factor Authentication Server 的狀態。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-112">This report displays the status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="f6bd9-113">已封鎖的使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f6bd9-113">Blocked User History</span></span> |<span data-ttu-id="f6bd9-114">這些報告會顯示要求封鎖或解除封鎖使用者之申請的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-114">These reports show the history of requests to block or unblock users.</span></span> |
| <span data-ttu-id="f6bd9-115">已略過的使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f6bd9-115">Bypassed User History</span></span> |<span data-ttu-id="f6bd9-116">顯示要求略過使用者電話號碼之 Multi-Factor Authentication 的申請歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-116">Shows the history of requests to bypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="f6bd9-117">詐騙警示</span><span class="sxs-lookup"><span data-stu-id="f6bd9-117">Fraud Alert</span></span> |<span data-ttu-id="f6bd9-118">顯示在指定日期範圍內提交之詐騙警示的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-118">Shows a history of fraud alerts submitted during the date range you specified.</span></span> |
| <span data-ttu-id="f6bd9-119">已排入佇列</span><span class="sxs-lookup"><span data-stu-id="f6bd9-119">Queued</span></span> |<span data-ttu-id="f6bd9-120">列出已排入佇列並等候處理的報告和其狀態。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="f6bd9-121">當報告完成時，系統會提供下載或檢視報告的連結。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-121">A link to download or view the report is provided when the report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="f6bd9-122">檢視報告</span><span class="sxs-lookup"><span data-stu-id="f6bd9-122">View reports</span></span>
1. <span data-ttu-id="f6bd9-123">登入 [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-123">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f6bd9-124">在左側選取 [Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-124">On the left, select Active Directory.</span></span>
3. <span data-ttu-id="f6bd9-125">根據您是否使用驗證提供者來遵循下列兩個選項的其中一個︰</span><span class="sxs-lookup"><span data-stu-id="f6bd9-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="f6bd9-126">**選項 1**：按一下 [多因素驗證提供者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-126">**Option 1**: Click the Multi-Factor Auth Providers tab.</span></span> <span data-ttu-id="f6bd9-127">選取您的 MFA 提供者，然後按一下底部的 [管理] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-127">Select your MFA provider and click the **Manage** button at the bottom.</span></span>
   * <span data-ttu-id="f6bd9-128">**選項 2**：選取您的目錄，然後移至 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-128">**Option 2**: Select your directory and go to the **Configure** tab.</span></span> <span data-ttu-id="f6bd9-129">在 [Multi-Factor Authentication] 區段底下，選取 [管理服務設定] 。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-129">Under the multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="f6bd9-130">在 [MFA 服務設定] 頁面底部，按一下 [移至入口網站] 連結。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-130">At the bottom of the MFA Service Settings page, click the Go to the portal link.</span></span>
4. <span data-ttu-id="f6bd9-131">在 Azure Multi-Factor Authentication 管理入口網站的左側導覽中，從 [檢視報告] 區段中選取您要使用的報告類型。</span><span class="sxs-lookup"><span data-stu-id="f6bd9-131">In the Azure Multi-Factor Authentication Management Portal, select the type of report you want from the **View a Report** section in the left navigation.</span></span>

<span data-ttu-id="f6bd9-132"><center>![雲端](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="f6bd9-132"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="f6bd9-133">**其他資源**</span><span class="sxs-lookup"><span data-stu-id="f6bd9-133">**Additional Resources**</span></span>

* [<span data-ttu-id="f6bd9-134">適用於使用者</span><span class="sxs-lookup"><span data-stu-id="f6bd9-134">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="f6bd9-135">MSDN 上的 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="f6bd9-135">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
