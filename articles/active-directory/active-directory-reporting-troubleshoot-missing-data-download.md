---
title: "疑難排解︰已下載的 Azure Active Directory 活動記錄中的遺漏資料 | Microsoft Docs"
description: "提供您已下載的 Azure Active Directory 活動記錄中遺漏資料的解決方案。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 3d56f89035da4d1a0074256b165663f81fc2b01e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="3d624-103">我在已下載的 Azure Active Directory 活動記錄中找不到任何資料</span><span class="sxs-lookup"><span data-stu-id="3d624-103">I can’t find any data in the Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="3d624-104">徵兆</span><span class="sxs-lookup"><span data-stu-id="3d624-104">Symptoms</span></span>

<span data-ttu-id="3d624-105">我已下載活動記錄 (稽核或登入)，卻沒看到我所選擇時間的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="3d624-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="3d624-106">原因為何？</span><span class="sxs-lookup"><span data-stu-id="3d624-106">Why?</span></span> 

 ![報告](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="3d624-108">原因</span><span class="sxs-lookup"><span data-stu-id="3d624-108">Cause</span></span>

<span data-ttu-id="3d624-109">當您在 Azure 入口網站中下載活動記錄時，我們會將級別限制為 120K 筆記錄，依最新記錄排序。</span><span class="sxs-lookup"><span data-stu-id="3d624-109">When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="3d624-110">解決方案</span><span class="sxs-lookup"><span data-stu-id="3d624-110">Resolution</span></span>

<span data-ttu-id="3d624-111">您可以利用 [Azure AD 報告 API](active-directory-reporting-api-getting-started.md) 在任何指定時間點擷取最多一萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="3d624-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="3d624-112">我們建議的方法是定期執行指令碼，呼叫報告 API 以增量方式來擷取一段時間的記錄 (例如，每天或每週)。</span><span class="sxs-lookup"><span data-stu-id="3d624-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d624-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d624-113">Next steps</span></span>
<span data-ttu-id="3d624-114">請參閱 [Azure Active Directory 報告常見問題集](active-directory-reporting-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="3d624-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

