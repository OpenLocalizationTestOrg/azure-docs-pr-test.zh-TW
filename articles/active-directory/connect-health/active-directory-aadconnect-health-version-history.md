---
title: "Azure AD Connect Health 版本歷程記錄"
description: "本文件說明 Azure AD Connect Health 的版本和已包含在這些版本中的功能。"
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 8dd4e998-747b-4c52-b8d3-3900fe77d88f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6c990a184d44771c78330f54f518bb4c35a36a35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-health-version-release-history"></a><span data-ttu-id="2387d-103">Azure AD Connect Health︰版本發行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="2387d-103">Azure AD Connect Health: Version Release History</span></span>
<span data-ttu-id="2387d-104">Azure Active Directory 團隊會定期以新的特性和功能更新 Azure AD Connect Health。</span><span class="sxs-lookup"><span data-stu-id="2387d-104">The Azure Active Directory team regularly updates Azure AD Connect Health with new features and functionality.</span></span> <span data-ttu-id="2387d-105">本文列出已發行的版本和功能。</span><span class="sxs-lookup"><span data-stu-id="2387d-105">This article lists the versions and features that have been released.</span></span>

## <a name="october-2016"></a><span data-ttu-id="2387d-106">2016 年 10 月</span><span class="sxs-lookup"><span data-stu-id="2387d-106">October 2016</span></span>
<span data-ttu-id="2387d-107">**代理程式更新：**</span><span class="sxs-lookup"><span data-stu-id="2387d-107">**Agent Update:**</span></span>

* <span data-ttu-id="2387d-108">適用於 AD FS 的 Azure AD Connect Health 代理程式 \(2.6.408.0 版\)</span><span class="sxs-lookup"><span data-stu-id="2387d-108">Azure AD Connect Health agent for AD FS \(version 2.6.408.0\)</span></span>
  1. <span data-ttu-id="2387d-109">改進在驗證要求中偵測用戶端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2387d-109">Improvements in detecting client IP addresses in authentication requests</span></span>
  2. <span data-ttu-id="2387d-110">與警示相關的錯誤修正</span><span class="sxs-lookup"><span data-stu-id="2387d-110">Bug Fixes related to Alerts</span></span>
* <span data-ttu-id="2387d-111">適用於 AD FS 的 Azure AD Connect Health 代理程式 (2.6.408.0 版)</span><span class="sxs-lookup"><span data-stu-id="2387d-111">Azure AD Connect Health agent for AD DS (version 2.6.408.0)</span></span>
  1. <span data-ttu-id="2387d-112">與警示相關的錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="2387d-112">Bug fixes related to Alerts.</span></span>
* <span data-ttu-id="2387d-113">隨著 Azure AD Connect 1.1.281.0 版發行的 Azure AD Connect Health Agent for Sync (2.6.353.0 版)</span><span class="sxs-lookup"><span data-stu-id="2387d-113">Azure AD Connect Health agent for Sync (version 2.6.353.0) released with Azure AD Connect version 1.1.281.0</span></span>
  1. <span data-ttu-id="2387d-114">提供同步處理錯誤報告所需的資料</span><span class="sxs-lookup"><span data-stu-id="2387d-114">Provide the required data for the Synchronization Error Reports</span></span>
  2. <span data-ttu-id="2387d-115">與警示相關的錯誤修正</span><span class="sxs-lookup"><span data-stu-id="2387d-115">Bug fixes related to Alerts</span></span>

<span data-ttu-id="2387d-116">**新的預覽功能：**</span><span class="sxs-lookup"><span data-stu-id="2387d-116">**New preview features:**</span></span>

* <span data-ttu-id="2387d-117">Azure AD Connect 的同步處理錯誤報告</span><span class="sxs-lookup"><span data-stu-id="2387d-117">Synchronization Error Reports for Azure AD Connect</span></span>

<span data-ttu-id="2387d-118">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="2387d-118">**New features:**</span></span>

* <span data-ttu-id="2387d-119">適用於 AD FS 的 Azure AD Connect Health - IP 位址欄位可用於報告中大約前 50 位使用者名稱/密碼不正確的使用者。</span><span class="sxs-lookup"><span data-stu-id="2387d-119">Azure AD Connect Health for AD FS - IP address field is available in the report about top 50 users with bad username/password.</span></span>

## <a name="july-2016"></a><span data-ttu-id="2387d-120">2016 年 7 月</span><span class="sxs-lookup"><span data-stu-id="2387d-120">July 2016</span></span>
<span data-ttu-id="2387d-121">**新的預覽功能：**</span><span class="sxs-lookup"><span data-stu-id="2387d-121">**New preview features:**</span></span>

* <span data-ttu-id="2387d-122">[適用於 AD DS 的 Azure AD Connect Health](active-directory-aadconnect-health-adds.md)。</span><span class="sxs-lookup"><span data-stu-id="2387d-122">[Azure AD Connect Health for AD DS](active-directory-aadconnect-health-adds.md).</span></span>

## <a name="january-2016"></a><span data-ttu-id="2387d-123">2016 年 1 月</span><span class="sxs-lookup"><span data-stu-id="2387d-123">January 2016</span></span>
<span data-ttu-id="2387d-124">**代理程式更新：**</span><span class="sxs-lookup"><span data-stu-id="2387d-124">**Agent Update:**</span></span>

* <span data-ttu-id="2387d-125">適用於 AD FS 的 Azure AD Connect Health 代理程式 (2.6.91.1512 版)</span><span class="sxs-lookup"><span data-stu-id="2387d-125">Azure AD Connect Health agent for AD FS (version 2.6.91.1512)</span></span>

<span data-ttu-id="2387d-126">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="2387d-126">**New features:**</span></span>

* [<span data-ttu-id="2387d-127">Azure AD Connect Health 代理程式的測試連線工具</span><span class="sxs-lookup"><span data-stu-id="2387d-127">Test Connectivity Tool for Azure AD Connect Health Agents</span></span>](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service)

## <a name="november-2015"></a><span data-ttu-id="2387d-128">2015 年 11 月</span><span class="sxs-lookup"><span data-stu-id="2387d-128">November 2015</span></span>
<span data-ttu-id="2387d-129">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="2387d-129">**New features:**</span></span>

* <span data-ttu-id="2387d-130">支援 [角色型存取控制](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)</span><span class="sxs-lookup"><span data-stu-id="2387d-130">Support for [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control)</span></span>

<span data-ttu-id="2387d-131">**新的預覽功能：**</span><span class="sxs-lookup"><span data-stu-id="2387d-131">**New preview features:**</span></span>

* <span data-ttu-id="2387d-132">[適用於同步的 Azure AD Connect Health](active-directory-aadconnect-health-sync.md)。</span><span class="sxs-lookup"><span data-stu-id="2387d-132">[Azure AD Connect Health for sync](active-directory-aadconnect-health-sync.md).</span></span>

<span data-ttu-id="2387d-133">**已修正的問題：**</span><span class="sxs-lookup"><span data-stu-id="2387d-133">**Fixed issues:**</span></span>

* <span data-ttu-id="2387d-134">針對代理程式註冊期間看到的錯誤進行修正。</span><span class="sxs-lookup"><span data-stu-id="2387d-134">Bug fixes for errors seen during agent registrations.</span></span>

## <a name="september-2015"></a><span data-ttu-id="2387d-135">2015 年 9 月</span><span class="sxs-lookup"><span data-stu-id="2387d-135">September 2015</span></span>
<span data-ttu-id="2387d-136">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="2387d-136">**New features:**</span></span>

* <span data-ttu-id="2387d-137">AD FS 的錯誤使用者名稱密碼報告</span><span class="sxs-lookup"><span data-stu-id="2387d-137">Wrong Username password report for AD FS</span></span>
* <span data-ttu-id="2387d-138">支援設定未經驗證的 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="2387d-138">Support to configure Unauthenticated HTTP Proxy</span></span>
* <span data-ttu-id="2387d-139">支援在伺服器核心上設定代理程式</span><span class="sxs-lookup"><span data-stu-id="2387d-139">Support to configure agent on Server core</span></span>
* <span data-ttu-id="2387d-140">改善 AD FS 的警示</span><span class="sxs-lookup"><span data-stu-id="2387d-140">Improvements to Alerts for AD FS</span></span>
* <span data-ttu-id="2387d-141">在適用於 AD FS 的 Azure AD Connect Health 代理程式中改善連線和資料上傳。</span><span class="sxs-lookup"><span data-stu-id="2387d-141">Improvements in Azure AD Connect Health Agent for AD FS for connectivity and data upload.</span></span>

<span data-ttu-id="2387d-142">**已修正的問題：**</span><span class="sxs-lookup"><span data-stu-id="2387d-142">**Fixed issues:**</span></span>

* <span data-ttu-id="2387d-143">AD FS 使用量詳細資料錯誤類型的錯誤修正。</span><span class="sxs-lookup"><span data-stu-id="2387d-143">Bug fixes in Usage Insights for AD FS Error types.</span></span>

## <a name="june-2015"></a><span data-ttu-id="2387d-144">2015 年 6 月</span><span class="sxs-lookup"><span data-stu-id="2387d-144">June 2015</span></span>
<span data-ttu-id="2387d-145">**適用於 AD FS 和 AD FS Proxy 的 Azure AD Connect Health 初始版本。**</span><span class="sxs-lookup"><span data-stu-id="2387d-145">**Initial release of Azure AD Connect Health for AD FS and AD FS Proxy.**</span></span>

<span data-ttu-id="2387d-146">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="2387d-146">**New features:**</span></span>

* <span data-ttu-id="2387d-147">監視 AD FS 與 AD FS Proxy 伺服器時以電子郵件通知發出警示。</span><span class="sxs-lookup"><span data-stu-id="2387d-147">Alerts for monitoring AD FS and AD FS Proxy servers with email notifications.</span></span>
* <span data-ttu-id="2387d-148">在 AD FS 效能計數器中輕鬆存取 AD FS 拓撲和模式。</span><span class="sxs-lookup"><span data-stu-id="2387d-148">Easy access to AD FS topology and patterns in AD FS Performance Counters.</span></span>
* <span data-ttu-id="2387d-149">依應用程式、驗證方法、要求網路位置等分組，顯示 AD FS 伺服器上成功權杖要求的趨勢。</span><span class="sxs-lookup"><span data-stu-id="2387d-149">Trend in successful token requests on AD FS servers grouped by Applications, Authentication Methods, Request Network Location etc.</span></span>
* <span data-ttu-id="2387d-150">依應用程式、錯誤類型等分組，顯示 AD FS 伺服器上失敗要求的趨勢。</span><span class="sxs-lookup"><span data-stu-id="2387d-150">Trends in failed request on AD FS servers grouped by Applications, Error Types etc.</span></span>
* <span data-ttu-id="2387d-151">使用 Azure AD 全域管理員認證更輕鬆部署代理程式。</span><span class="sxs-lookup"><span data-stu-id="2387d-151">Simpler Agent Deployment using Azure AD Global Admin credentials.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2387d-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2387d-152">Next steps</span></span>
<span data-ttu-id="2387d-153">深入了解 [在雲端中監視內部部署身分識別基礎結構和同步處理服務](active-directory-aadconnect-health.md)。</span><span class="sxs-lookup"><span data-stu-id="2387d-153">Learn more about [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>

