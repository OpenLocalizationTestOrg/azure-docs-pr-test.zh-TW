---
title: "檢視存取和使用情況報告 | Microsoft Docs"
description: "說明如何檢視存取和使用情況報告來深入了解貴組織之目錄完整性和安全性。"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 038ac79ebf61c6429fbf7ca21eefe9414bcfc03a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-your-access-and-usage-reports"></a><span data-ttu-id="71f1b-103">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-103">View your access and usage reports</span></span>
<span data-ttu-id="71f1b-104">*這份文件是 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)的一部分。*</span><span class="sxs-lookup"><span data-stu-id="71f1b-104">*This documentation is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="71f1b-105">您可以使用 Azure Active Directory 的存取和使用情況報告來了解貴組織的目錄完整性和安全性。</span><span class="sxs-lookup"><span data-stu-id="71f1b-105">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="71f1b-106">利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的位置，以便適當地規劃來減輕這些風險。</span><span class="sxs-lookup"><span data-stu-id="71f1b-106">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="71f1b-107">在 Azure 管理入口網站中，報告會以下列方式分類：</span><span class="sxs-lookup"><span data-stu-id="71f1b-107">In the Azure Management Portal, reports are categorized in the following ways:</span></span>

* <span data-ttu-id="71f1b-108">異常報告 – 包含我們發現異常的登入事件。</span><span class="sxs-lookup"><span data-stu-id="71f1b-108">Anomaly reports – Contain sign in events that we found to be anomalous.</span></span> <span data-ttu-id="71f1b-109">我們的目標在於使您注意這類活動，並讓您能夠判斷事件是否可疑。</span><span class="sxs-lookup"><span data-stu-id="71f1b-109">Our goal is to make you aware of such activity and enable you to be able to make a determination about whether an event is suspicious.</span></span>
* <span data-ttu-id="71f1b-110">整合式應用程式報告 – 可供深入了解雲端應用程式在組織中的使用方式。</span><span class="sxs-lookup"><span data-stu-id="71f1b-110">Integrated Application reports – Provides insights into how cloud applications are being used in your organization.</span></span> <span data-ttu-id="71f1b-111">Azure Active Directory 提供與數千個雲端應用程式的整合。</span><span class="sxs-lookup"><span data-stu-id="71f1b-111">Azure Active Directory offers integration with thousands of cloud applications.</span></span>
* <span data-ttu-id="71f1b-112">錯誤報告 – 指出將帳戶佈建至外部應用程式時可能發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="71f1b-112">Error reports – Indicate errors that may occur when provisioning accounts to external applications.</span></span>
* <span data-ttu-id="71f1b-113">使用者特定報告 – 顯示特定使用者的裝置/登入活動資料。</span><span class="sxs-lookup"><span data-stu-id="71f1b-113">User-specific reports – Display device/sign in activity data for a specific user.</span></span>
* <span data-ttu-id="71f1b-114">活動記錄檔 – 包含過去 24 小時、過去 7 天或過去 30 天內所有稽核事件的記錄，以及群組活動變更、密碼重設和登錄活動。</span><span class="sxs-lookup"><span data-stu-id="71f1b-114">Activity logs – Contain a record of all audited events within the last 24 hours, last 7 days, or last 30 days, as well as group activity changes, and password reset and registration activity.</span></span>

> [!NOTE]
> * <span data-ttu-id="71f1b-115">某些進階的異常和資源使用情況報告僅適用於您啟用 [Azure Active Directory Premium](active-directory-get-started-premium.md)時。</span><span class="sxs-lookup"><span data-stu-id="71f1b-115">Some advanced anomaly and resource usage reports are only available when you enable [Azure Active Directory Premium](active-directory-get-started-premium.md).</span></span> <span data-ttu-id="71f1b-116">進階報告可協助您改善存取安全性、回應潛在威脅，以及存取裝置存取與應用程式使用情況的分析資料。</span><span class="sxs-lookup"><span data-stu-id="71f1b-116">Advanced reports help you improve access security, respond to potential threats and get access to analytics on device access and application usage.</span></span>
> * <span data-ttu-id="71f1b-117">Azure Active Directory Premium 和 Basic 版本適用於使用 Azure Active Directory 全球執行個體的中國客戶。</span><span class="sxs-lookup"><span data-stu-id="71f1b-117">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="71f1b-118">由 21Vianet 在中國提供的 Microsoft Azure 服務目前不支援 Azure Active Directory Premium 和 Basic 版本。</span><span class="sxs-lookup"><span data-stu-id="71f1b-118">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="71f1b-119">如需詳細資訊，請透過 [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="71f1b-119">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
> 
> 

## <a name="reports"></a><span data-ttu-id="71f1b-120">報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-120">Reports</span></span>
| <span data-ttu-id="71f1b-121">報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-121">Report</span></span> | <span data-ttu-id="71f1b-122">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71f1b-123">**異常活動報告**</span><span class="sxs-lookup"><span data-stu-id="71f1b-123">**Anomalous activity reports**</span></span> | |
| [<span data-ttu-id="71f1b-124">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-124">Sign ins from unknown sources</span></span>](active-directory-reporting-sign-ins-from-unknown-sources.md) |<span data-ttu-id="71f1b-125">可能表示使用者嘗試在不被追蹤的情況下登入。</span><span class="sxs-lookup"><span data-stu-id="71f1b-125">May indicate an attempt to sign in without being traced.</span></span> |
| [<span data-ttu-id="71f1b-126">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-126">Sign ins after multiple failures</span></span>](active-directory-reporting-sign-ins-after-multiple-failures.md) |<span data-ttu-id="71f1b-127">可能表示暴力密碼破解攻擊成功。</span><span class="sxs-lookup"><span data-stu-id="71f1b-127">May indicate a successful brute force attack.</span></span> |
| [<span data-ttu-id="71f1b-128">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md) |<span data-ttu-id="71f1b-129">可能表示多個使用者登入相同帳戶。</span><span class="sxs-lookup"><span data-stu-id="71f1b-129">May indicate that multiple users are signing in with the same account.</span></span> |
| [<span data-ttu-id="71f1b-130">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-130">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |<span data-ttu-id="71f1b-131">可能表示使用者嘗試多次入侵後成功登入。</span><span class="sxs-lookup"><span data-stu-id="71f1b-131">May indicate a successful sign in after a sustained intrusion attempt.</span></span> |
| [<span data-ttu-id="71f1b-132">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-132">Sign ins from possibly infected devices</span></span>](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |<span data-ttu-id="71f1b-133">可能表示使用者嘗試用於登入的裝置可能已受到感染。</span><span class="sxs-lookup"><span data-stu-id="71f1b-133">May indicate an attempt to sign in from possibly infected devices.</span></span> |
| [<span data-ttu-id="71f1b-134">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-134">Irregular sign in activity</span></span>](active-directory-reporting-irregular-sign-in-activity.md) |<span data-ttu-id="71f1b-135">可能表示違背使用者平常登入習慣的事件。</span><span class="sxs-lookup"><span data-stu-id="71f1b-135">May indicate events anomalous to users’ sign in patterns.</span></span> |
| [<span data-ttu-id="71f1b-136">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-136">Users with anomalous sign in activity</span></span>](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |<span data-ttu-id="71f1b-137">指示帳戶可能已受到危害的使用者。</span><span class="sxs-lookup"><span data-stu-id="71f1b-137">Indicates users whose accounts may have been compromised.</span></span> |
| <span data-ttu-id="71f1b-138">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-138">Users with leaked credentials</span></span> |<span data-ttu-id="71f1b-139">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-139">Users with leaked credentials</span></span> |
| <span data-ttu-id="71f1b-140">**活動記錄檔**</span><span class="sxs-lookup"><span data-stu-id="71f1b-140">**Activity logs**</span></span> | |
| <span data-ttu-id="71f1b-141">稽核報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-141">Audit report</span></span> |<span data-ttu-id="71f1b-142">目錄中的已稽核事件</span><span class="sxs-lookup"><span data-stu-id="71f1b-142">Audited events in your directory</span></span> |
| <span data-ttu-id="71f1b-143">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-143">Password reset activity</span></span> |<span data-ttu-id="71f1b-144">提供您組織中所執行之密碼重設的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="71f1b-144">Provides a detailed view of password resets that occur in your organization.</span></span> |
| <span data-ttu-id="71f1b-145">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-145">Password reset registration activity</span></span> |<span data-ttu-id="71f1b-146">提供您組織中所執行之密碼重設登錄的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="71f1b-146">Provides a detailed view of password reset registrations that occur in your organization.</span></span> |
| <span data-ttu-id="71f1b-147">自助服務群組活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-147">Self service groups activity</span></span> |<span data-ttu-id="71f1b-148">提供活動記錄給您目錄中所有的群組自助活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-148">Provides an activity log to all group self service activity in your directory</span></span> |
| <span data-ttu-id="71f1b-149">**整合式應用程式**</span><span class="sxs-lookup"><span data-stu-id="71f1b-149">**Integrated applications**</span></span> | |
| <span data-ttu-id="71f1b-150">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="71f1b-150">Application usage</span></span> |<span data-ttu-id="71f1b-151">針對與您目錄整合的所有 SaaS 應用程式提供使用摘要。</span><span class="sxs-lookup"><span data-stu-id="71f1b-151">Provides a usage summary for all SaaS applications integrated with your directory.</span></span> |
| <span data-ttu-id="71f1b-152">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-152">Account provisioning activity</span></span> |<span data-ttu-id="71f1b-153">提供嘗試將帳戶佈建到外部應用程式的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="71f1b-153">Provides a history of attempts to provision accounts to external applications.</span></span> |
| <span data-ttu-id="71f1b-154">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="71f1b-154">Password rollover status</span></span> |<span data-ttu-id="71f1b-155">提供 SaaS 應用程式自動密碼變換狀態的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="71f1b-155">Provides a detailed overview of automatic password rollover status of SaaS applications.</span></span> |
| <span data-ttu-id="71f1b-156">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="71f1b-156">Account provisioning errors</span></span> |<span data-ttu-id="71f1b-157">指示對使用者的外部應用程式存取造成的影響。</span><span class="sxs-lookup"><span data-stu-id="71f1b-157">Indicates an impact to users’ access to external applications.</span></span> |
| <span data-ttu-id="71f1b-158">**版權管理**</span><span class="sxs-lookup"><span data-stu-id="71f1b-158">**Rights management**</span></span> | |
| <span data-ttu-id="71f1b-159">RMS 使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-159">RMS usage</span></span> |<span data-ttu-id="71f1b-160">提供 Rights Management 使用量的摘要</span><span class="sxs-lookup"><span data-stu-id="71f1b-160">Provides a summary for Rights Management usage</span></span> |
| <span data-ttu-id="71f1b-161">最活躍的 RMS 使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-161">Most active RMS users</span></span> |<span data-ttu-id="71f1b-162">列出已存取受 RMS 保護之檔案的前 1000 名有效使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-162">Lists top 1000 active users who accessed RMS-protected files</span></span> |
| <span data-ttu-id="71f1b-163">RMS 裝置使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-163">RMS device usage</span></span> |<span data-ttu-id="71f1b-164">列出存取受 RMS 保護的檔案所使用的裝置</span><span class="sxs-lookup"><span data-stu-id="71f1b-164">Lists devices used for accessing RMS-protected files</span></span> |
| <span data-ttu-id="71f1b-165">啟用 RMS 的應用程式使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-165">RMS enabled application usage</span></span> |<span data-ttu-id="71f1b-166">提供啟用 RMS 之應用程式的使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-166">Provides usage of RMS enabled applications</span></span> |

## <a name="report-editions"></a><span data-ttu-id="71f1b-167">報告版本</span><span class="sxs-lookup"><span data-stu-id="71f1b-167">Report editions</span></span>
| <span data-ttu-id="71f1b-168">報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-168">Report</span></span> | <span data-ttu-id="71f1b-169">免費</span><span class="sxs-lookup"><span data-stu-id="71f1b-169">Free</span></span> | <span data-ttu-id="71f1b-170">基本</span><span class="sxs-lookup"><span data-stu-id="71f1b-170">Basic</span></span> | <span data-ttu-id="71f1b-171">高級</span><span class="sxs-lookup"><span data-stu-id="71f1b-171">Premium</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71f1b-172">**異常活動報告**</span><span class="sxs-lookup"><span data-stu-id="71f1b-172">**Anomalous activity reports**</span></span> | | | |
| <span data-ttu-id="71f1b-173">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-173">Sign ins from unknown sources</span></span> |<span data-ttu-id="71f1b-174">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-174">✓</span></span> |<span data-ttu-id="71f1b-175">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-175">✓</span></span> |<span data-ttu-id="71f1b-176">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-176">✓</span></span> |
| <span data-ttu-id="71f1b-177">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-177">Sign ins after multiple failures</span></span> |<span data-ttu-id="71f1b-178">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-178">✓</span></span> |<span data-ttu-id="71f1b-179">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-179">✓</span></span> |<span data-ttu-id="71f1b-180">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-180">✓</span></span> |
| <span data-ttu-id="71f1b-181">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-181">Sign ins from multiple geographies</span></span> |<span data-ttu-id="71f1b-182">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-182">✓</span></span> |<span data-ttu-id="71f1b-183">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-183">✓</span></span> |<span data-ttu-id="71f1b-184">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-184">✓</span></span> |
| <span data-ttu-id="71f1b-185">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-185">Sign ins from IP addresses with suspicious activity</span></span> | | |<span data-ttu-id="71f1b-186">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-186">✓</span></span> |
| <span data-ttu-id="71f1b-187">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-187">Sign ins from possibly infected devices</span></span> | | |<span data-ttu-id="71f1b-188">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-188">✓</span></span> |
| <span data-ttu-id="71f1b-189">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-189">Irregular sign in activity</span></span> | | |<span data-ttu-id="71f1b-190">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-190">✓</span></span> |
| <span data-ttu-id="71f1b-191">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-191">Users with anomalous sign in activity</span></span> | | |<span data-ttu-id="71f1b-192">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-192">✓</span></span> |
| <span data-ttu-id="71f1b-193">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-193">Users with leaked credentials</span></span> | | |<span data-ttu-id="71f1b-194">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-194">✓</span></span> |
| <span data-ttu-id="71f1b-195">**活動記錄檔**</span><span class="sxs-lookup"><span data-stu-id="71f1b-195">**Activity logs**</span></span> | | | |
| <span data-ttu-id="71f1b-196">稽核報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-196">Audit report</span></span> |<span data-ttu-id="71f1b-197">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-197">✓</span></span> |<span data-ttu-id="71f1b-198">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-198">✓</span></span> |<span data-ttu-id="71f1b-199">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-199">✓</span></span> |
| <span data-ttu-id="71f1b-200">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-200">Password reset activity</span></span> | | |<span data-ttu-id="71f1b-201">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-201">✓</span></span> |
| <span data-ttu-id="71f1b-202">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-202">Password reset registration activity</span></span> | | |<span data-ttu-id="71f1b-203">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-203">✓</span></span> |
| <span data-ttu-id="71f1b-204">自助服務群組活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-204">Self service groups activity</span></span> | | |<span data-ttu-id="71f1b-205">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-205">✓</span></span> |
| <span data-ttu-id="71f1b-206">**整合式應用程式**</span><span class="sxs-lookup"><span data-stu-id="71f1b-206">**Integrated applications**</span></span> | | | |
| <span data-ttu-id="71f1b-207">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="71f1b-207">Application usage</span></span> | | |<span data-ttu-id="71f1b-208">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-208">✓</span></span> |
| <span data-ttu-id="71f1b-209">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-209">Account provisioning activity</span></span> |<span data-ttu-id="71f1b-210">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-210">✓</span></span> |<span data-ttu-id="71f1b-211">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-211">✓</span></span> |<span data-ttu-id="71f1b-212">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-212">✓</span></span> |
| <span data-ttu-id="71f1b-213">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="71f1b-213">Password rollover status</span></span> | | |<span data-ttu-id="71f1b-214">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-214">✓</span></span> |
| <span data-ttu-id="71f1b-215">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="71f1b-215">Account provisioning errors</span></span> |<span data-ttu-id="71f1b-216">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-216">✓</span></span> |<span data-ttu-id="71f1b-217">✓ </span><span class="sxs-lookup"><span data-stu-id="71f1b-217">✓</span></span> |<span data-ttu-id="71f1b-218">✓</span><span class="sxs-lookup"><span data-stu-id="71f1b-218">✓</span></span> |
| <span data-ttu-id="71f1b-219">**版權管理**</span><span class="sxs-lookup"><span data-stu-id="71f1b-219">**Rights managment**</span></span> | | | |
| <span data-ttu-id="71f1b-220">RMS 使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-220">RMS usage</span></span> | | |<span data-ttu-id="71f1b-221">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="71f1b-221">RMS Only</span></span> |
| <span data-ttu-id="71f1b-222">最活躍的 RMS 使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-222">Most active RMS users</span></span> | | |<span data-ttu-id="71f1b-223">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="71f1b-223">RMS Only</span></span> |
| <span data-ttu-id="71f1b-224">RMS 裝置使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-224">RMS device usage</span></span> | | |<span data-ttu-id="71f1b-225">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="71f1b-225">RMS Only</span></span> |
| <span data-ttu-id="71f1b-226">啟用 RMS 的應用程式使用量</span><span class="sxs-lookup"><span data-stu-id="71f1b-226">RMS enabled application usage</span></span> | | |<span data-ttu-id="71f1b-227">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="71f1b-227">RMS Only</span></span> |

## <a name="anomalous-activity-reports"></a><span data-ttu-id="71f1b-228">異常活動報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-228">Anomalous activity reports</span></span>
<p><span data-ttu-id="71f1b-229">異常登入活動報告會將 Office365、Azure 管理入口網站、Azure AD 存取面板、Sharepoint Online、Dynamics CRM Online 和其他 Microsoft Online Services 的可疑登入活動加上旗標。</span><span class="sxs-lookup"><span data-stu-id="71f1b-229">The anomalous sign in activity reports flag suspicious sign in activity to Office365, Azure Management Portal, Azure AD Access Panel, Sharepoint Online, Dynamics CRM Online, and other Microsoft online services.</span></span></p>

<p><span data-ttu-id="71f1b-230">所有這些報告 (「多次失敗後的登入次數」報告除外) 也會將上述服務的可疑「同盟」<i></i>登入加上旗標，無論同盟提供者是誰。</span><span class="sxs-lookup"><span data-stu-id="71f1b-230">All of these reports, except the "Sign ins after multiple failures" report, also flag suspicious <i>federated</i> sign ins to the aforementioned services, regardless of the federation provider.</span></span> </p>

<p><span data-ttu-id="71f1b-231">以下是可用的報告：</span><span class="sxs-lookup"><span data-stu-id="71f1b-231">The following reports are available:</span></span> </p><ul>

<li><span data-ttu-id="71f1b-232">[從不明來源登入](active-directory-reporting-sign-ins-from-unknown-sources.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-232">[Sign ins from unknown sources](active-directory-reporting-sign-ins-from-unknown-sources.md).</span></span></li>

<li><span data-ttu-id="71f1b-233">[在多次失敗後登入](active-directory-reporting-sign-ins-after-multiple-failures的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-233">[Sign ins after multiple failures](active-directory-reporting-sign-ins-after-multiple-failures.md).</span></span></li>

<li><span data-ttu-id="71f1b-234">[從多個地理區域登入](active-directory-reporting-sign-ins-from-multiple-geographies的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-234">[Sign ins from multiple geographies](active-directory-reporting-sign-ins-from-multiple-geographies.md).</span></span></li>

<li><span data-ttu-id="71f1b-235">[從具有可疑活動的 IP 位址登入](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-235">[Sign ins from IP addresses with suspicious activity](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</span></span></li>

<li><span data-ttu-id="71f1b-236">[異常的登入活動](active-directory-reporting-irregular-sign-in-activity的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-236">[Irregular sign in activity](active-directory-reporting-irregular-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="71f1b-237">[從可能受感染的裝置登入](active-directory-reporting-sign-ins-from-possibly-infected-devices的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-237">[Sign ins from possibly infected devices](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</span></span></li>

<li><span data-ttu-id="71f1b-238">[具有異常登入活動的使用者](active-directory-reporting-users-with-anomalous-sign-in-activity.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="71f1b-238">[Users with anomalous sign in activity](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="71f1b-239">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="71f1b-239">Users with leaked credentials</span></span></li></ul>

## <a name="activity-logs"></a><span data-ttu-id="71f1b-240">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="71f1b-240">Activity logs</span></span>
### <a name="audit-report"></a><span data-ttu-id="71f1b-241">稽核報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-241">Audit report</span></span>
| <span data-ttu-id="71f1b-242">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-242">Description</span></span> | <span data-ttu-id="71f1b-243">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-243">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-244">顯示過去 24 小時、過去 7 天或過去 30 天內的所有稽核事件記錄。</span><span class="sxs-lookup"><span data-stu-id="71f1b-244">Shows a record of all audited events within the last 24 hours, last 7 days, or last 30 days.</span></span> <br /> <span data-ttu-id="71f1b-245">如需詳細資訊，請參閱 [Azure Active Directory 稽核報告事件](active-directory-reporting-audit-events.md)</span><span class="sxs-lookup"><span data-stu-id="71f1b-245">For more information, see [Azure Active Directory Audit Report Events](active-directory-reporting-audit-events.md)</span></span> |<span data-ttu-id="71f1b-246">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-246">Directory > Reports tab</span></span> |

![稽核報告](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a><span data-ttu-id="71f1b-248">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-248">Password reset activity</span></span>
| <span data-ttu-id="71f1b-249">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-249">Description</span></span> | <span data-ttu-id="71f1b-250">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-250">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-251">顯示您的組織中發生的所有密碼重設嘗試</span><span class="sxs-lookup"><span data-stu-id="71f1b-251">Shows all password reset attempts that have occurred in your organization.</span></span> |<span data-ttu-id="71f1b-252">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-252">Directory > Reports tab</span></span> |

![密碼重設活動](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a><span data-ttu-id="71f1b-254">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-254">Password reset registration activity</span></span>
| <span data-ttu-id="71f1b-255">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-255">Description</span></span> | <span data-ttu-id="71f1b-256">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-256">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-257">顯示您的組織中發生的所有密碼重設登錄</span><span class="sxs-lookup"><span data-stu-id="71f1b-257">Shows all password reset registrations that have occurred in your organization</span></span> |<span data-ttu-id="71f1b-258">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-258">Directory > Reports tab</span></span> |

![密碼重設註冊活動](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a><span data-ttu-id="71f1b-260">自助服務群組活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-260">Self service groups activity</span></span>
| <span data-ttu-id="71f1b-261">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-261">Description</span></span> | <span data-ttu-id="71f1b-262">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-262">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-263">顯示您的目錄中自助式管理群組的所有活動。</span><span class="sxs-lookup"><span data-stu-id="71f1b-263">Shows all activity for the self-service managed groups in your directory.</span></span> |<span data-ttu-id="71f1b-264">目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-264">Directory > Users > <i>User</i> > Devices tab</span></span> |

![自助服務群組活動](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a><span data-ttu-id="71f1b-266">整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-266">Integrated applications reports</span></span>
### <a name="application-usage-summary"></a><span data-ttu-id="71f1b-267">應用程式使用情況：摘要</span><span class="sxs-lookup"><span data-stu-id="71f1b-267">Application usage: summary</span></span>
| <span data-ttu-id="71f1b-268">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-268">Description</span></span> | <span data-ttu-id="71f1b-269">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-269">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-270">使用這份報告可以查看您的目錄中所有 SaaS 應用程式的使用情況。</span><span class="sxs-lookup"><span data-stu-id="71f1b-270">Use this report when you want to see usage for all the SaaS applications in your directory.</span></span> <span data-ttu-id="71f1b-271">這份報告是以使用者在 [存取面板] 中點選應用程式的次數為基礎。</span><span class="sxs-lookup"><span data-stu-id="71f1b-271">This report is based on the number of times users have clicked on the application in the Access Panel.</span></span> |<span data-ttu-id="71f1b-272">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-272">Directory > Reports tab</span></span> |

<span data-ttu-id="71f1b-273">這份報告包含您目錄有權存取之「所有」應用程式的登入，包括預先整合的 Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="71f1b-273">This report includes sign ins to *all* applications that your directory has access to, including pre-integrated Microsoft applications.</span></span>

<span data-ttu-id="71f1b-274">預先整合的 Microsoft 應用程式包括 Office 365、Sharepoint、Azure 管理入口網站和其他項目。</span><span class="sxs-lookup"><span data-stu-id="71f1b-274">Pre-integrated Microsoft applications include Office 365, Sharepoint, the Azure Management Portal, and others.</span></span>

![應用程式使用情況摘要](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a><span data-ttu-id="71f1b-276">應用程式使用情況：詳細</span><span class="sxs-lookup"><span data-stu-id="71f1b-276">Application usage: detailed</span></span>
| <span data-ttu-id="71f1b-277">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-277">Description</span></span> | <span data-ttu-id="71f1b-278">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-278">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-279">使用這份報告可以查看特定 SaaS 應用程式目前的使用量。</span><span class="sxs-lookup"><span data-stu-id="71f1b-279">Use this report when you want to see how much a specific SaaS application is being used.</span></span> <span data-ttu-id="71f1b-280">這份報告是以使用者在 [存取面板] 中點選應用程式的次數為基礎。</span><span class="sxs-lookup"><span data-stu-id="71f1b-280">This report is based on the number of times users have clicked on the application in the Access Panel.</span></span> |<span data-ttu-id="71f1b-281">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-281">Directory > Reports tab</span></span> |

### <a name="application-dashboard"></a><span data-ttu-id="71f1b-282">應用程式儀表板</span><span class="sxs-lookup"><span data-stu-id="71f1b-282">Application dashboard</span></span>
| <span data-ttu-id="71f1b-283">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-283">Description</span></span> | <span data-ttu-id="71f1b-284">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-284">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-285">此報告指出在一段選取的時間間隔內，您組織中的使用者對應用程式進行的累計登入。</span><span class="sxs-lookup"><span data-stu-id="71f1b-285">This report indicates cumulative sign ins to the application by users in your organization, over a selected time interval.</span></span> <span data-ttu-id="71f1b-286">儀表板頁面上的圖表可協助您識別該應用程式的所有使用趨勢。</span><span class="sxs-lookup"><span data-stu-id="71f1b-286">The chart on the dashboard page will help you identify trends for all usage of that application.</span></span> |<span data-ttu-id="71f1b-287">目錄 > 應用程式 > 儀表板索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-287">Directory > Application > Dashboard tab</span></span> |

## <a name="error-reports"></a><span data-ttu-id="71f1b-288">錯誤報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-288">Error reports</span></span>
### <a name="account-provisioning-errors"></a><span data-ttu-id="71f1b-289">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="71f1b-289">Account provisioning errors</span></span>
| <span data-ttu-id="71f1b-290">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-290">Description</span></span> | <span data-ttu-id="71f1b-291">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-291">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-292">使用這份報告來監控將帳戶從 SaaS 應用程式同步處理至 Azure Active Directory 期間發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="71f1b-292">Use this to monitor errors that occur during the synchronization of accounts from SaaS applications to Azure Active Directory.</span></span> |<span data-ttu-id="71f1b-293">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-293">Directory > Reports tab</span></span> |

![帳戶佈建錯誤](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a><span data-ttu-id="71f1b-295">特定使用者報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-295">User-specific reports</span></span>
### <a name="devices"></a><span data-ttu-id="71f1b-296">裝置</span><span class="sxs-lookup"><span data-stu-id="71f1b-296">Devices</span></span>
| <span data-ttu-id="71f1b-297">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-297">Description</span></span> | <span data-ttu-id="71f1b-298">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-298">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-299">使用此報告可查看特定使用者用來存取 Azure Active Directory 的 IP 位址和裝置地理位置。</span><span class="sxs-lookup"><span data-stu-id="71f1b-299">Use this report when you want to see the IP address and geographical location of devices that a specific user has used to access Azure Active Directory.</span></span> |<span data-ttu-id="71f1b-300">目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-300">Directory > Users > <i>User</i> > Devices tab</span></span> |

### <a name="activity"></a><span data-ttu-id="71f1b-301">活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-301">Activity</span></span>
| <span data-ttu-id="71f1b-302">說明</span><span class="sxs-lookup"><span data-stu-id="71f1b-302">Description</span></span> | <span data-ttu-id="71f1b-303">報告位置</span><span class="sxs-lookup"><span data-stu-id="71f1b-303">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="71f1b-304">顯示使用者的登入活動。</span><span class="sxs-lookup"><span data-stu-id="71f1b-304">Shows the sign in activity for a user.</span></span> <span data-ttu-id="71f1b-305">此報告包含登入的應用程式、使用的裝置、IP 位址和位置等資訊。</span><span class="sxs-lookup"><span data-stu-id="71f1b-305">The report includes information like the application signed into, device used, IP address, and location.</span></span> <span data-ttu-id="71f1b-306">我們不會收集以 Microsoft 帳戶登入的使用者歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="71f1b-306">We do not collect the history for users that sign in with a Microsoft account.</span></span> |<span data-ttu-id="71f1b-307">目錄 > 使用者 > <i>使用者</i> > 活動索引標籤</span><span class="sxs-lookup"><span data-stu-id="71f1b-307">Directory > Users > <i>User</i> > Activity tab</span></span> |

#### <a name="sign-in-events-included-in-the-user-activity-report"></a><span data-ttu-id="71f1b-308">使用者活動中包含的登入事件報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-308">Sign in events included in the User Activity report</span></span>
<span data-ttu-id="71f1b-309">只有某些類型的登入事件會出現在「使用者活動」報告中。</span><span class="sxs-lookup"><span data-stu-id="71f1b-309">Only certain types of sign in events will appear in the User Activity report.</span></span>

| <span data-ttu-id="71f1b-310">事件類型</span><span class="sxs-lookup"><span data-stu-id="71f1b-310">Event type</span></span> | <span data-ttu-id="71f1b-311">已包含？</span><span class="sxs-lookup"><span data-stu-id="71f1b-311">Included?</span></span> |
| --- | --- |
| <span data-ttu-id="71f1b-312">對 [存取面板](http://myapps.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="71f1b-312">Sign ins to the [Access Panel](http://myapps.microsoft.com/)</span></span> |<span data-ttu-id="71f1b-313">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-313">Yes</span></span> |
| <span data-ttu-id="71f1b-314">對 [Azure 管理入口網站](https://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="71f1b-314">Sign ins to the [Azure Management Portal](https://manage.windowsazure.com/)</span></span> |<span data-ttu-id="71f1b-315">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-315">Yes</span></span> |
| <span data-ttu-id="71f1b-316">對 [Microsoft Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="71f1b-316">Sign ins to the [Microsoft Azure Portal](https://portal.azure.com/)</span></span> |<span data-ttu-id="71f1b-317">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-317">Yes</span></span> |
| <span data-ttu-id="71f1b-318">對 [Office 365 入口網站](http://portal.office.com/)</span><span class="sxs-lookup"><span data-stu-id="71f1b-318">Sign ins to the [Office 365 portal](http://portal.office.com/)</span></span> |<span data-ttu-id="71f1b-319">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-319">Yes</span></span> |
| <span data-ttu-id="71f1b-320">對原生應用程式進行的登入，例如 Outlook (請參閱底下的例外狀況)</span><span class="sxs-lookup"><span data-stu-id="71f1b-320">Sign ins to a native application, like Outlook (see exception below)</span></span> |<span data-ttu-id="71f1b-321">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-321">Yes</span></span> |
| <span data-ttu-id="71f1b-322">透過存取面板 (例如 Salesforce) 對同盟/佈建應用程式進行的登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-322">Sign ins to a federated/provisioned app through the Access Panel, like Salesforce</span></span> |<span data-ttu-id="71f1b-323">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-323">Yes</span></span> |
| <span data-ttu-id="71f1b-324">透過存取面板 (例如 Twitter) 對密碼型應用程式進行進行的登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-324">Sign ins to a password-based app through the Access Panel, like Twitter</span></span> |<span data-ttu-id="71f1b-325">是</span><span class="sxs-lookup"><span data-stu-id="71f1b-325">Yes</span></span> |
| <span data-ttu-id="71f1b-326">對已新增至目錄的自訂商務應用程式進行的登入</span><span class="sxs-lookup"><span data-stu-id="71f1b-326">Sign ins to a custom business app that has been added to the directory</span></span> |<span data-ttu-id="71f1b-327">否 (敬請期待)</span><span class="sxs-lookup"><span data-stu-id="71f1b-327">No (Coming soon)</span></span> |
| <span data-ttu-id="71f1b-328">登入已加入目錄的 Azure AD 應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="71f1b-328">Sign ins to an Azure AD Application Proxy app that has been added to the directory</span></span> |<span data-ttu-id="71f1b-329">否 (敬請期待)</span><span class="sxs-lookup"><span data-stu-id="71f1b-329">No (Coming soon)</span></span> |

> <span data-ttu-id="71f1b-330">注意：為了減少此報告中的雜訊量，不會顯示經由 [Microsoft Online Services 登入小幫手](http://community.office365.com/en-us/w/sso/534.aspx)進行的登入。</span><span class="sxs-lookup"><span data-stu-id="71f1b-330">Note: To reduce the amount of noise in this report, sign ins by the [Microsoft Online Services Sign-In Assistant](http://community.office365.com/en-us/w/sso/534.aspx) are not shown.</span></span>
> 
> 

## <a name="things-to-consider-if-you-suspect-security-breach"></a><span data-ttu-id="71f1b-331">您懷疑有安全性缺口時的考慮事項</span><span class="sxs-lookup"><span data-stu-id="71f1b-331">Things to consider if you suspect security breach</span></span>
<span data-ttu-id="71f1b-332">如果您懷疑使用者帳戶可能遭到入侵，或有任何可能導致雲端中您的目錄資料出現安全性缺口的可疑使用者活動，您可能要考慮下列其中一或多個動作：</span><span class="sxs-lookup"><span data-stu-id="71f1b-332">If you suspect that a user account may be compromised or any kind of suspicious user activity that may lead to a security breach of your directory data in the cloud, you may want to consider one or more of the following actions:</span></span>

* <span data-ttu-id="71f1b-333">連絡使用者來確認活動</span><span class="sxs-lookup"><span data-stu-id="71f1b-333">Contact the user to verify the activity</span></span>
* <span data-ttu-id="71f1b-334">重設使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="71f1b-334">Reset the user's password</span></span>
* <span data-ttu-id="71f1b-335">[啟用多因素驗證](../multi-factor-authentication/multi-factor-authentication-get-started.md) 以提供額外的安全性</span><span class="sxs-lookup"><span data-stu-id="71f1b-335">[Enable multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md) for additional security</span></span>

## <a name="view-or-download-a-report"></a><span data-ttu-id="71f1b-336">檢視或下載報告</span><span class="sxs-lookup"><span data-stu-id="71f1b-336">View or download a report</span></span>
1. <span data-ttu-id="71f1b-337">在 Azure 傳統入口網站中，依序按一下 [Active Directory]、您組織目錄的名稱，然後按一下 [報告]。</span><span class="sxs-lookup"><span data-stu-id="71f1b-337">In the Azure classic portal, click **Active Directory**, click the name of your organization’s directory, and then click **Reports**.</span></span>
2. <span data-ttu-id="71f1b-338">在 [報告] 頁面上，按一下您要檢視和/或下載的報告。</span><span class="sxs-lookup"><span data-stu-id="71f1b-338">On the Reports page, click the report you want to view and/or download.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="71f1b-339">如果這是您第一次使用 Azure Active Directory 的報告功能，您會看到「選擇加入」的訊息。</span><span class="sxs-lookup"><span data-stu-id="71f1b-339">If this is the first time you have used the reporting feature of Azure Active Directory, you will see a message to Opt In.</span></span> <span data-ttu-id="71f1b-340">如果您同意，請按一下核取記號圖示繼續進行。</span><span class="sxs-lookup"><span data-stu-id="71f1b-340">If you agree, click the check mark icon to continue.</span></span>
   > 
   > 
3. <span data-ttu-id="71f1b-341">按一下 [間隔] 旁邊的下拉式功能表，然後選取在產生此報告時所應使用的其中一個時間範圍：</span><span class="sxs-lookup"><span data-stu-id="71f1b-341">Click the drop-down menu next to Interval, and then select one of the following time ranges that should be used when generating this report:</span></span>
   
   * <span data-ttu-id="71f1b-342">過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="71f1b-342">Last 24 hours</span></span>
   * <span data-ttu-id="71f1b-343">過去 7 天</span><span class="sxs-lookup"><span data-stu-id="71f1b-343">Last 7 days</span></span>
   * <span data-ttu-id="71f1b-344">過去 30 天</span><span class="sxs-lookup"><span data-stu-id="71f1b-344">Last 30 days</span></span>
4. <span data-ttu-id="71f1b-345">按一下核取記號圖示來執行報告。</span><span class="sxs-lookup"><span data-stu-id="71f1b-345">Click the check mark icon to run the report.</span></span>
   * <span data-ttu-id="71f1b-346">Azure 傳統入口網站最多會顯示 1000 個事件。</span><span class="sxs-lookup"><span data-stu-id="71f1b-346">Up to 1000 events will be shown in the Azure classic portal.</span></span>
5. <span data-ttu-id="71f1b-347">如果適用的話，按一下 [下載]  可將報告下載為逗號分隔值 (CSV) 格式的壓縮檔，以供離線檢視或封存。</span><span class="sxs-lookup"><span data-stu-id="71f1b-347">If applicable, click **Download** to download the report to a compressed file in comma-separated values (CSV) format for offline viewing or archiving purposes.</span></span>
   * <span data-ttu-id="71f1b-348">最多 75,000 個事件會包含在下載的檔案中。</span><span class="sxs-lookup"><span data-stu-id="71f1b-348">Up to 75,000 events will be included in the downloaded file.</span></span>
   * <span data-ttu-id="71f1b-349">如需更多資料，請參閱 [Azure AD 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="71f1b-349">For more data, check out the [Azure AD Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

## <a name="ignore-an-event"></a><span data-ttu-id="71f1b-350">忽略事件</span><span class="sxs-lookup"><span data-stu-id="71f1b-350">Ignore an event</span></span>
<span data-ttu-id="71f1b-351">如果正在檢視任何異常報告，您可能會注意到您可以忽略顯示在相關報告中的各種事件。</span><span class="sxs-lookup"><span data-stu-id="71f1b-351">If you are viewing any anomaly reports, you may notice that you can ignore various events that show up in related reports.</span></span> <span data-ttu-id="71f1b-352">若要忽略事件，只要將報告中的事件反白，然後按一下 [ **忽略**] 即可。</span><span class="sxs-lookup"><span data-stu-id="71f1b-352">To ignore an event, simply highlight the event in the report and then click **Ignore**.</span></span> <span data-ttu-id="71f1b-353">[ **忽略** ] 按鈕將會永久移除報告中反白顯示的事件，而且只能由獲得授權的全域管理員使用。</span><span class="sxs-lookup"><span data-stu-id="71f1b-353">The **Ignore** button will permanently remove the highlighted event from the report and can only be used by licensed global admins.</span></span>

## <a name="automatic-email-notifications"></a><span data-ttu-id="71f1b-354">自動電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="71f1b-354">Automatic email notifications</span></span>
<span data-ttu-id="71f1b-355">如需有關 Azure AD 的報告通知詳細資訊，請參閱 [Azure Active Directory 報告通知](active-directory-reporting-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="71f1b-355">For more information about Azure AD's reporting notifications, check out [Azure Active Directory Reporting Notifications](active-directory-reporting-notifications.md).</span></span>

## <a name="whats-next"></a><span data-ttu-id="71f1b-356">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71f1b-356">What's next</span></span>
* [<span data-ttu-id="71f1b-357">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="71f1b-357">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="71f1b-358">在登入和存取面板頁面加上公司商標</span><span class="sxs-lookup"><span data-stu-id="71f1b-358">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

