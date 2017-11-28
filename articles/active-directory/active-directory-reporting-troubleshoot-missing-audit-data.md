---
title: "疑難排解： 遺漏 hello Azure Active Directory 活動記錄檔中的資料 |Microsoft 文件"
description: "列出 Azure Active Directory 的 hello 各種可用的報表"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 7bbec94ab42eb5b54a7e65e124060d057b4a1a34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-hello-azure-active-directory-activity-log"></a><span data-ttu-id="ab21c-103">我找不到我 hello Azure Active Directory 活動記錄檔中執行某些動作</span><span class="sxs-lookup"><span data-stu-id="ab21c-103">I can’t find some actions that I performed in hello Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="ab21c-104">徵兆</span><span class="sxs-lookup"><span data-stu-id="ab21c-104">Symptoms</span></span>

<span data-ttu-id="ab21c-105">我在 hello Azure 入口網站中執行某些動作，而且預期 toosee hello 的稽核記錄，這些動作在 hello`Activity logs > Audit Logs`刀鋒視窗中，但是無法找到它們。</span><span class="sxs-lookup"><span data-stu-id="ab21c-105">I performed some actions in hello Azure portal and expected toosee hello audit logs for those actions in hello `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![報告](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="ab21c-107">原因</span><span class="sxs-lookup"><span data-stu-id="ab21c-107">Cause</span></span>

<span data-ttu-id="ab21c-108">動作不會立即出現 hello 活動稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ab21c-108">Actions don’t appear immediately in hello Activity Audit log.</span></span> <span data-ttu-id="ab21c-109">它可以需要 15 分鐘 tooan 小時 toosee hello 稽核記錄在 hello 入口網站，從 hello hello 作業的時間。</span><span class="sxs-lookup"><span data-stu-id="ab21c-109">It can take anywhere from 15 minutes tooan hour toosee hello audit logs in hello portal from hello time hello operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="ab21c-110">解決方案</span><span class="sxs-lookup"><span data-stu-id="ab21c-110">Resolution</span></span>

<span data-ttu-id="ab21c-111">等候 15 分鐘 tooan 小時，請參閱是否 hello 動作會出現在 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ab21c-111">Wait for 15 minutes tooan hour and see if hello actions appear in hello log.</span></span> <span data-ttu-id="ab21c-112">如果您仍看不到它們，請向我們提出支援票證，我們將探討它。</span><span class="sxs-lookup"><span data-stu-id="ab21c-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ab21c-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab21c-113">Next steps</span></span>
<span data-ttu-id="ab21c-114">請參閱 hello [reporting 常見問題集的 Azure Active Directory](active-directory-reporting-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="ab21c-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

