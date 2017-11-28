---
title: "aaaAzure Active Directory 報告保留原則 |Microsoft 文件"
description: "Azure Active Directory 中報告資料的保留原則"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="ac850-103">Azure Active Directory 報告保留原則</span><span class="sxs-lookup"><span data-stu-id="ac850-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="ac850-104">本主題提供您的解答 toohello 搭配 hello 資料保留在 Azure Active Directory 中的 hello 不同的活動報表的最常見的問題。</span><span class="sxs-lookup"><span data-stu-id="ac850-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="ac850-105">**問： 如何取得活動資料入門 hello 集合？**</span><span class="sxs-lookup"><span data-stu-id="ac850-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="ac850-106">**答：**</span><span class="sxs-lookup"><span data-stu-id="ac850-106">**A:**</span></span>

| <span data-ttu-id="ac850-107">Azure AD 版本</span><span class="sxs-lookup"><span data-stu-id="ac850-107">Azure AD Edition</span></span> | <span data-ttu-id="ac850-108">開始收集</span><span class="sxs-lookup"><span data-stu-id="ac850-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="ac850-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="ac850-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="ac850-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="ac850-110">Azure AD Premium P2</span></span> | <span data-ttu-id="ac850-111">當您註冊訂用帳戶時</span><span class="sxs-lookup"><span data-stu-id="ac850-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="ac850-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="ac850-112">Azure AD Free</span></span> | <span data-ttu-id="ac850-113">hello 第一次開啟 hello [Azure Active Directory 刀鋒視窗](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)或使用 hello[報告 Api](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="ac850-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="ac850-114">**問： 當有活動資料 hello Azure 入口網站？**</span><span class="sxs-lookup"><span data-stu-id="ac850-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="ac850-115">**答：**</span><span class="sxs-lookup"><span data-stu-id="ac850-115">**A:**</span></span>

- <span data-ttu-id="ac850-116">**立即**-如果您已使用 hello Azure 傳統入口網站中的報表</span><span class="sxs-lookup"><span data-stu-id="ac850-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="ac850-117">**在 2 小時內**-如果您尚未開啟 reporting hello Azure 傳統入口網站中</span><span class="sxs-lookup"><span data-stu-id="ac850-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="ac850-118">**問： 如何取得啟動安全性訊號 hello 集合？**</span><span class="sxs-lookup"><span data-stu-id="ac850-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="ac850-119">**答：**安全性訊號 hello 收集處理程序啟動時您選擇加入的 toouse hello 識別防護中心。</span><span class="sxs-lookup"><span data-stu-id="ac850-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="ac850-120">**問： 多久會 hello 收集的資料儲存？**</span><span class="sxs-lookup"><span data-stu-id="ac850-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="ac850-121">**答：**</span><span class="sxs-lookup"><span data-stu-id="ac850-121">**A:**</span></span>

<span data-ttu-id="ac850-122">**活動報告**</span><span class="sxs-lookup"><span data-stu-id="ac850-122">**Activity reports**</span></span>    

| <span data-ttu-id="ac850-123">報告</span><span class="sxs-lookup"><span data-stu-id="ac850-123">Report</span></span>                 | <span data-ttu-id="ac850-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="ac850-124">Azure AD Free</span></span> | <span data-ttu-id="ac850-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="ac850-125">Azure AD Premium P1</span></span> | <span data-ttu-id="ac850-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="ac850-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="ac850-127">目錄稽核</span><span class="sxs-lookup"><span data-stu-id="ac850-127">Directory Audit</span></span>        | <span data-ttu-id="ac850-128">7 天</span><span class="sxs-lookup"><span data-stu-id="ac850-128">7 days</span></span>        | <span data-ttu-id="ac850-129">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-129">30 days</span></span>             | <span data-ttu-id="ac850-130">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-130">30 days</span></span>             |
| <span data-ttu-id="ac850-131">登入活動</span><span class="sxs-lookup"><span data-stu-id="ac850-131">Sign-in Activity</span></span>       | <span data-ttu-id="ac850-132">7 天</span><span class="sxs-lookup"><span data-stu-id="ac850-132">7 days</span></span>        | <span data-ttu-id="ac850-133">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-133">30 days</span></span>             | <span data-ttu-id="ac850-134">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-134">30 days</span></span>             |

<span data-ttu-id="ac850-135">**安全性訊號**</span><span class="sxs-lookup"><span data-stu-id="ac850-135">**Security Signals**</span></span>

| <span data-ttu-id="ac850-136">報告</span><span class="sxs-lookup"><span data-stu-id="ac850-136">Report</span></span>         | <span data-ttu-id="ac850-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="ac850-137">Azure AD Free</span></span> | <span data-ttu-id="ac850-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="ac850-138">Azure AD Premium P1</span></span> | <span data-ttu-id="ac850-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="ac850-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="ac850-140">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="ac850-140">Users at risk</span></span>  | <span data-ttu-id="ac850-141">7 天</span><span class="sxs-lookup"><span data-stu-id="ac850-141">7 days</span></span>        | <span data-ttu-id="ac850-142">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-142">30 days</span></span>             | <span data-ttu-id="ac850-143">90 天</span><span class="sxs-lookup"><span data-stu-id="ac850-143">90 days</span></span>             |
| <span data-ttu-id="ac850-144">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="ac850-144">Risky sign-ins</span></span> | <span data-ttu-id="ac850-145">7 天</span><span class="sxs-lookup"><span data-stu-id="ac850-145">7 days</span></span>        | <span data-ttu-id="ac850-146">30 天</span><span class="sxs-lookup"><span data-stu-id="ac850-146">30 days</span></span>             | <span data-ttu-id="ac850-147">90 天</span><span class="sxs-lookup"><span data-stu-id="ac850-147">90 days</span></span>             |

---