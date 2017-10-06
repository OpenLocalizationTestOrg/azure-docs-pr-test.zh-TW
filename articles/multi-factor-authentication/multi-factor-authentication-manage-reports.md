---
title: "為 Azure MFA 的 aaaAccess 和使用方式報表 |Microsoft 文件"
description: "這說明如何 toouse hello Azure 多重要素驗證功能的報表。"
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
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="d51c8-103">Azure Multi-Factor Authentication 中的報告</span><span class="sxs-lookup"><span data-stu-id="d51c8-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="d51c8-104">Azure Multi-Factor Authentication 提供數個供您和貴組織使用的報告。</span><span class="sxs-lookup"><span data-stu-id="d51c8-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="d51c8-105">這些報表都可以透過 hello Multi-factor Authentication 管理入口網站來存取。</span><span class="sxs-lookup"><span data-stu-id="d51c8-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="d51c8-106">hello 以下是 hello 可用報表的清單：</span><span class="sxs-lookup"><span data-stu-id="d51c8-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="d51c8-107">報告</span><span class="sxs-lookup"><span data-stu-id="d51c8-107">Report</span></span> | <span data-ttu-id="d51c8-108">說明</span><span class="sxs-lookup"><span data-stu-id="d51c8-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d51c8-109">使用量</span><span class="sxs-lookup"><span data-stu-id="d51c8-109">Usage</span></span> |<span data-ttu-id="d51c8-110">hello 使用量報告整體使用量、 使用者摘要和使用者詳細資料的顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="d51c8-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="d51c8-111">伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="d51c8-111">Server Status</span></span> |<span data-ttu-id="d51c8-112">此報告會顯示 hello 的 Multi-factor Authentication Server 與您的帳戶相關聯的狀態。</span><span class="sxs-lookup"><span data-stu-id="d51c8-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="d51c8-113">已封鎖的使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d51c8-113">Blocked User History</span></span> |<span data-ttu-id="d51c8-114">這些報表顯示要求 tooblock hello 歷程記錄，或解除封鎖使用者。</span><span class="sxs-lookup"><span data-stu-id="d51c8-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="d51c8-115">已略過的使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d51c8-115">Bypassed User History</span></span> |<span data-ttu-id="d51c8-116">顯示使用者的電話號碼的要求 toobypass Multi-factor Authentication 的 hello 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d51c8-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="d51c8-117">詐騙警示</span><span class="sxs-lookup"><span data-stu-id="d51c8-117">Fraud Alert</span></span> |<span data-ttu-id="d51c8-118">顯示您所指定的 hello 日期範圍內已提交詐騙警示的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="d51c8-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="d51c8-119">已排入佇列</span><span class="sxs-lookup"><span data-stu-id="d51c8-119">Queued</span></span> |<span data-ttu-id="d51c8-120">列出已排入佇列並等候處理的報告和其狀態。</span><span class="sxs-lookup"><span data-stu-id="d51c8-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="d51c8-121">Hello 報表完成時，會提供連結或檢視表 toodownload hello 報告。</span><span class="sxs-lookup"><span data-stu-id="d51c8-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="d51c8-122">檢視報告</span><span class="sxs-lookup"><span data-stu-id="d51c8-122">View reports</span></span>
1. <span data-ttu-id="d51c8-123">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="d51c8-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d51c8-124">Hello 左側選取 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="d51c8-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="d51c8-125">根據您是否使用驗證提供者來遵循下列兩個選項的其中一個︰</span><span class="sxs-lookup"><span data-stu-id="d51c8-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="d51c8-126">**選項 1**： 按一下 hello Multi-factor Auth 提供者 索引標籤。選取您的 MFA 提供者，然後按一下 hello**管理**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d51c8-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="d51c8-127">**選項 2**： 選取您的目錄，以及移 toohello**設定** 索引標籤。Hello 多因素驗證 區段下，選取**管理服務設定**。</span><span class="sxs-lookup"><span data-stu-id="d51c8-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="d51c8-128">在 hello hello MFA 服務設定 頁面底部，按一下 hello Go toohello 入口網站連結。</span><span class="sxs-lookup"><span data-stu-id="d51c8-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="d51c8-129">在 hello Azure Multi-factor Authentication 管理入口網站，請從 hello 中選取您想要的報表 hello 類型**檢視報表**hello 左瀏覽一節。</span><span class="sxs-lookup"><span data-stu-id="d51c8-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="d51c8-130"><center>![雲端](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="d51c8-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="d51c8-131">**其他資源**</span><span class="sxs-lookup"><span data-stu-id="d51c8-131">**Additional Resources**</span></span>

* [<span data-ttu-id="d51c8-132">適用於使用者</span><span class="sxs-lookup"><span data-stu-id="d51c8-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="d51c8-133">MSDN 上的 Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="d51c8-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
