---
title: "aaaView 存取和使用方式報表 |Microsoft 文件"
description: "說明如何 tooview 存取和使用方式報告 toogain 深入了解 hello 完整性與安全性貴組織的目錄。"
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
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a><span data-ttu-id="95821-103">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="95821-103">View your access and usage reports</span></span>
<span data-ttu-id="95821-104">*這份文件屬於 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。*</span><span class="sxs-lookup"><span data-stu-id="95821-104">*This documentation is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="95821-105">您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。</span><span class="sxs-lookup"><span data-stu-id="95821-105">You can use Azure Active Directory's access and usage reports toogain visibility into hello integrity and security of your organization’s directory.</span></span> <span data-ttu-id="95821-106">利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。</span><span class="sxs-lookup"><span data-stu-id="95821-106">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan toomitigate those risks.</span></span>

<span data-ttu-id="95821-107">Hello Azure 管理入口網站，在報表的分類中 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="95821-107">In hello Azure Management Portal, reports are categorized in hello following ways:</span></span>

* <span data-ttu-id="95821-108">異常報表-包含登入事件，我們發現 toobe 異常。</span><span class="sxs-lookup"><span data-stu-id="95821-108">Anomaly reports – Contain sign in events that we found toobe anomalous.</span></span> <span data-ttu-id="95821-109">我們的目標是 toomake 您注意這類活動，並讓您 toobe 無法 toomake 判斷事件是否可疑。</span><span class="sxs-lookup"><span data-stu-id="95821-109">Our goal is toomake you aware of such activity and enable you toobe able toomake a determination about whether an event is suspicious.</span></span>
* <span data-ttu-id="95821-110">整合式應用程式報告 – 可供深入了解雲端應用程式在組織中的使用方式。</span><span class="sxs-lookup"><span data-stu-id="95821-110">Integrated Application reports – Provides insights into how cloud applications are being used in your organization.</span></span> <span data-ttu-id="95821-111">Azure Active Directory 提供與數千個雲端應用程式的整合。</span><span class="sxs-lookup"><span data-stu-id="95821-111">Azure Active Directory offers integration with thousands of cloud applications.</span></span>
* <span data-ttu-id="95821-112">錯誤報表 – 指出佈建帳戶 tooexternal 應用程式時可能發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="95821-112">Error reports – Indicate errors that may occur when provisioning accounts tooexternal applications.</span></span>
* <span data-ttu-id="95821-113">使用者特定報告 – 顯示特定使用者的裝置/登入活動資料。</span><span class="sxs-lookup"><span data-stu-id="95821-113">User-specific reports – Display device/sign in activity data for a specific user.</span></span>
* <span data-ttu-id="95821-114">活動記錄-hello 內所有稽核事件的記錄包含過去 24 小時、 過去 7 天或過去 30 天內，以及群組活動變更、 和密碼重設和註冊活動。</span><span class="sxs-lookup"><span data-stu-id="95821-114">Activity logs – Contain a record of all audited events within hello last 24 hours, last 7 days, or last 30 days, as well as group activity changes, and password reset and registration activity.</span></span>

> [!NOTE]
> * <span data-ttu-id="95821-115">某些進階的異常和資源使用情況報告僅適用於您啟用 [Azure Active Directory Premium](active-directory-get-started-premium.md)時。</span><span class="sxs-lookup"><span data-stu-id="95821-115">Some advanced anomaly and resource usage reports are only available when you enable [Azure Active Directory Premium](active-directory-get-started-premium.md).</span></span> <span data-ttu-id="95821-116">進階的報表可協助您改善存取安全性，回應 toopotential 威脅，並取得存取 tooanalytics 裝置存取與應用程式使用量。</span><span class="sxs-lookup"><span data-stu-id="95821-116">Advanced reports help you improve access security, respond toopotential threats and get access tooanalytics on device access and application usage.</span></span>
> * <span data-ttu-id="95821-117">Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。</span><span class="sxs-lookup"><span data-stu-id="95821-117">Azure Active Directory Premium and Basic editions are available for customers in China using hello worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="95821-118">Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。</span><span class="sxs-lookup"><span data-stu-id="95821-118">Azure Active Directory Premium and Basic editions are not currently supported in hello Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="95821-119">如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="95821-119">For more information, contact us at hello [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
> 
> 

## <a name="reports"></a><span data-ttu-id="95821-120">報告</span><span class="sxs-lookup"><span data-stu-id="95821-120">Reports</span></span>
| <span data-ttu-id="95821-121">報告</span><span class="sxs-lookup"><span data-stu-id="95821-121">Report</span></span> | <span data-ttu-id="95821-122">說明</span><span class="sxs-lookup"><span data-stu-id="95821-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="95821-123">**異常活動報告**</span><span class="sxs-lookup"><span data-stu-id="95821-123">**Anomalous activity reports**</span></span> | |
| [<span data-ttu-id="95821-124">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="95821-124">Sign ins from unknown sources</span></span>](active-directory-reporting-sign-ins-from-unknown-sources.md) |<span data-ttu-id="95821-125">可能表示在嘗試 toosign 不被追蹤。</span><span class="sxs-lookup"><span data-stu-id="95821-125">May indicate an attempt toosign in without being traced.</span></span> |
| [<span data-ttu-id="95821-126">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="95821-126">Sign ins after multiple failures</span></span>](active-directory-reporting-sign-ins-after-multiple-failures.md) |<span data-ttu-id="95821-127">可能表示暴力密碼破解攻擊成功。</span><span class="sxs-lookup"><span data-stu-id="95821-127">May indicate a successful brute force attack.</span></span> |
| [<span data-ttu-id="95821-128">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="95821-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md) |<span data-ttu-id="95821-129">可能表示多位使用者所登入 hello 相同帳戶。</span><span class="sxs-lookup"><span data-stu-id="95821-129">May indicate that multiple users are signing in with hello same account.</span></span> |
| [<span data-ttu-id="95821-130">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="95821-130">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |<span data-ttu-id="95821-131">可能表示使用者嘗試多次入侵後成功登入。</span><span class="sxs-lookup"><span data-stu-id="95821-131">May indicate a successful sign in after a sustained intrusion attempt.</span></span> |
| [<span data-ttu-id="95821-132">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="95821-132">Sign ins from possibly infected devices</span></span>](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |<span data-ttu-id="95821-133">可能表示嘗試 toosign 中，從可能受感染的裝置。</span><span class="sxs-lookup"><span data-stu-id="95821-133">May indicate an attempt toosign in from possibly infected devices.</span></span> |
| [<span data-ttu-id="95821-134">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="95821-134">Irregular sign in activity</span></span>](active-directory-reporting-irregular-sign-in-activity.md) |<span data-ttu-id="95821-135">可能表示事件異常 toousers' 登入模式。</span><span class="sxs-lookup"><span data-stu-id="95821-135">May indicate events anomalous toousers’ sign in patterns.</span></span> |
| [<span data-ttu-id="95821-136">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-136">Users with anomalous sign in activity</span></span>](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |<span data-ttu-id="95821-137">指示帳戶可能已受到危害的使用者。</span><span class="sxs-lookup"><span data-stu-id="95821-137">Indicates users whose accounts may have been compromised.</span></span> |
| <span data-ttu-id="95821-138">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-138">Users with leaked credentials</span></span> |<span data-ttu-id="95821-139">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-139">Users with leaked credentials</span></span> |
| <span data-ttu-id="95821-140">**活動記錄檔**</span><span class="sxs-lookup"><span data-stu-id="95821-140">**Activity logs**</span></span> | |
| <span data-ttu-id="95821-141">稽核報告</span><span class="sxs-lookup"><span data-stu-id="95821-141">Audit report</span></span> |<span data-ttu-id="95821-142">目錄中的已稽核事件</span><span class="sxs-lookup"><span data-stu-id="95821-142">Audited events in your directory</span></span> |
| <span data-ttu-id="95821-143">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="95821-143">Password reset activity</span></span> |<span data-ttu-id="95821-144">提供您組織中所執行之密碼重設的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="95821-144">Provides a detailed view of password resets that occur in your organization.</span></span> |
| <span data-ttu-id="95821-145">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="95821-145">Password reset registration activity</span></span> |<span data-ttu-id="95821-146">提供您組織中所執行之密碼重設登錄的詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="95821-146">Provides a detailed view of password reset registrations that occur in your organization.</span></span> |
| <span data-ttu-id="95821-147">自助群組活動</span><span class="sxs-lookup"><span data-stu-id="95821-147">Self service groups activity</span></span> |<span data-ttu-id="95821-148">提供活動記錄 tooall 群組自助活動，在您的目錄</span><span class="sxs-lookup"><span data-stu-id="95821-148">Provides an activity log tooall group self service activity in your directory</span></span> |
| <span data-ttu-id="95821-149">**整合式應用程式**</span><span class="sxs-lookup"><span data-stu-id="95821-149">**Integrated applications**</span></span> | |
| <span data-ttu-id="95821-150">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="95821-150">Application usage</span></span> |<span data-ttu-id="95821-151">針對與您目錄整合的所有 SaaS 應用程式提供使用摘要。</span><span class="sxs-lookup"><span data-stu-id="95821-151">Provides a usage summary for all SaaS applications integrated with your directory.</span></span> |
| <span data-ttu-id="95821-152">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="95821-152">Account provisioning activity</span></span> |<span data-ttu-id="95821-153">提供嘗試的歷程記錄 tooprovision 帳戶 tooexternal 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95821-153">Provides a history of attempts tooprovision accounts tooexternal applications.</span></span> |
| <span data-ttu-id="95821-154">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="95821-154">Password rollover status</span></span> |<span data-ttu-id="95821-155">提供 SaaS 應用程式自動密碼變換狀態的詳細概觀。</span><span class="sxs-lookup"><span data-stu-id="95821-155">Provides a detailed overview of automatic password rollover status of SaaS applications.</span></span> |
| <span data-ttu-id="95821-156">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="95821-156">Account provisioning errors</span></span> |<span data-ttu-id="95821-157">表示影響 toousers' 存取 tooexternal 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95821-157">Indicates an impact toousers’ access tooexternal applications.</span></span> |
| <span data-ttu-id="95821-158">**版權管理**</span><span class="sxs-lookup"><span data-stu-id="95821-158">**Rights management**</span></span> | |
| <span data-ttu-id="95821-159">RMS 使用量</span><span class="sxs-lookup"><span data-stu-id="95821-159">RMS usage</span></span> |<span data-ttu-id="95821-160">提供 Rights Management 使用量的摘要</span><span class="sxs-lookup"><span data-stu-id="95821-160">Provides a summary for Rights Management usage</span></span> |
| <span data-ttu-id="95821-161">最活躍的 RMS 使用者</span><span class="sxs-lookup"><span data-stu-id="95821-161">Most active RMS users</span></span> |<span data-ttu-id="95821-162">列出已存取受 RMS 保護之檔案的前 1000 名有效使用者</span><span class="sxs-lookup"><span data-stu-id="95821-162">Lists top 1000 active users who accessed RMS-protected files</span></span> |
| <span data-ttu-id="95821-163">RMS 裝置使用量</span><span class="sxs-lookup"><span data-stu-id="95821-163">RMS device usage</span></span> |<span data-ttu-id="95821-164">列出存取受 RMS 保護的檔案所使用的裝置</span><span class="sxs-lookup"><span data-stu-id="95821-164">Lists devices used for accessing RMS-protected files</span></span> |
| <span data-ttu-id="95821-165">啟用 RMS 的應用程式使用量</span><span class="sxs-lookup"><span data-stu-id="95821-165">RMS enabled application usage</span></span> |<span data-ttu-id="95821-166">提供啟用 RMS 之應用程式的使用量</span><span class="sxs-lookup"><span data-stu-id="95821-166">Provides usage of RMS enabled applications</span></span> |

## <a name="report-editions"></a><span data-ttu-id="95821-167">報告版本</span><span class="sxs-lookup"><span data-stu-id="95821-167">Report editions</span></span>
| <span data-ttu-id="95821-168">報告</span><span class="sxs-lookup"><span data-stu-id="95821-168">Report</span></span> | <span data-ttu-id="95821-169">免費</span><span class="sxs-lookup"><span data-stu-id="95821-169">Free</span></span> | <span data-ttu-id="95821-170">基本</span><span class="sxs-lookup"><span data-stu-id="95821-170">Basic</span></span> | <span data-ttu-id="95821-171">高級</span><span class="sxs-lookup"><span data-stu-id="95821-171">Premium</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="95821-172">**異常活動報告**</span><span class="sxs-lookup"><span data-stu-id="95821-172">**Anomalous activity reports**</span></span> | | | |
| <span data-ttu-id="95821-173">從不明來源登入</span><span class="sxs-lookup"><span data-stu-id="95821-173">Sign ins from unknown sources</span></span> |<span data-ttu-id="95821-174">✓</span><span class="sxs-lookup"><span data-stu-id="95821-174">✓</span></span> |<span data-ttu-id="95821-175">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-175">✓</span></span> |<span data-ttu-id="95821-176">✓</span><span class="sxs-lookup"><span data-stu-id="95821-176">✓</span></span> |
| <span data-ttu-id="95821-177">在多次失敗後登入</span><span class="sxs-lookup"><span data-stu-id="95821-177">Sign ins after multiple failures</span></span> |<span data-ttu-id="95821-178">✓</span><span class="sxs-lookup"><span data-stu-id="95821-178">✓</span></span> |<span data-ttu-id="95821-179">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-179">✓</span></span> |<span data-ttu-id="95821-180">✓</span><span class="sxs-lookup"><span data-stu-id="95821-180">✓</span></span> |
| <span data-ttu-id="95821-181">從多個地理區域登入</span><span class="sxs-lookup"><span data-stu-id="95821-181">Sign ins from multiple geographies</span></span> |<span data-ttu-id="95821-182">✓</span><span class="sxs-lookup"><span data-stu-id="95821-182">✓</span></span> |<span data-ttu-id="95821-183">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-183">✓</span></span> |<span data-ttu-id="95821-184">✓</span><span class="sxs-lookup"><span data-stu-id="95821-184">✓</span></span> |
| <span data-ttu-id="95821-185">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="95821-185">Sign ins from IP addresses with suspicious activity</span></span> | | |<span data-ttu-id="95821-186">✓</span><span class="sxs-lookup"><span data-stu-id="95821-186">✓</span></span> |
| <span data-ttu-id="95821-187">從可能受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="95821-187">Sign ins from possibly infected devices</span></span> | | |<span data-ttu-id="95821-188">✓</span><span class="sxs-lookup"><span data-stu-id="95821-188">✓</span></span> |
| <span data-ttu-id="95821-189">異常的登入活動</span><span class="sxs-lookup"><span data-stu-id="95821-189">Irregular sign in activity</span></span> | | |<span data-ttu-id="95821-190">✓</span><span class="sxs-lookup"><span data-stu-id="95821-190">✓</span></span> |
| <span data-ttu-id="95821-191">具有異常登入活動的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-191">Users with anomalous sign in activity</span></span> | | |<span data-ttu-id="95821-192">✓</span><span class="sxs-lookup"><span data-stu-id="95821-192">✓</span></span> |
| <span data-ttu-id="95821-193">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-193">Users with leaked credentials</span></span> | | |<span data-ttu-id="95821-194">✓</span><span class="sxs-lookup"><span data-stu-id="95821-194">✓</span></span> |
| <span data-ttu-id="95821-195">**活動記錄檔**</span><span class="sxs-lookup"><span data-stu-id="95821-195">**Activity logs**</span></span> | | | |
| <span data-ttu-id="95821-196">稽核報告</span><span class="sxs-lookup"><span data-stu-id="95821-196">Audit report</span></span> |<span data-ttu-id="95821-197">✓</span><span class="sxs-lookup"><span data-stu-id="95821-197">✓</span></span> |<span data-ttu-id="95821-198">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-198">✓</span></span> |<span data-ttu-id="95821-199">✓</span><span class="sxs-lookup"><span data-stu-id="95821-199">✓</span></span> |
| <span data-ttu-id="95821-200">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="95821-200">Password reset activity</span></span> | | |<span data-ttu-id="95821-201">✓</span><span class="sxs-lookup"><span data-stu-id="95821-201">✓</span></span> |
| <span data-ttu-id="95821-202">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="95821-202">Password reset registration activity</span></span> | | |<span data-ttu-id="95821-203">✓</span><span class="sxs-lookup"><span data-stu-id="95821-203">✓</span></span> |
| <span data-ttu-id="95821-204">自助服務群組活動</span><span class="sxs-lookup"><span data-stu-id="95821-204">Self service groups activity</span></span> | | |<span data-ttu-id="95821-205">✓</span><span class="sxs-lookup"><span data-stu-id="95821-205">✓</span></span> |
| <span data-ttu-id="95821-206">**整合式應用程式**</span><span class="sxs-lookup"><span data-stu-id="95821-206">**Integrated applications**</span></span> | | | |
| <span data-ttu-id="95821-207">應用程式使用情況</span><span class="sxs-lookup"><span data-stu-id="95821-207">Application usage</span></span> | | |<span data-ttu-id="95821-208">✓</span><span class="sxs-lookup"><span data-stu-id="95821-208">✓</span></span> |
| <span data-ttu-id="95821-209">帳戶佈建活動</span><span class="sxs-lookup"><span data-stu-id="95821-209">Account provisioning activity</span></span> |<span data-ttu-id="95821-210">✓</span><span class="sxs-lookup"><span data-stu-id="95821-210">✓</span></span> |<span data-ttu-id="95821-211">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-211">✓</span></span> |<span data-ttu-id="95821-212">✓</span><span class="sxs-lookup"><span data-stu-id="95821-212">✓</span></span> |
| <span data-ttu-id="95821-213">密碼變換狀態</span><span class="sxs-lookup"><span data-stu-id="95821-213">Password rollover status</span></span> | | |<span data-ttu-id="95821-214">✓</span><span class="sxs-lookup"><span data-stu-id="95821-214">✓</span></span> |
| <span data-ttu-id="95821-215">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="95821-215">Account provisioning errors</span></span> |<span data-ttu-id="95821-216">✓</span><span class="sxs-lookup"><span data-stu-id="95821-216">✓</span></span> |<span data-ttu-id="95821-217">✓ </span><span class="sxs-lookup"><span data-stu-id="95821-217">✓</span></span> |<span data-ttu-id="95821-218">✓</span><span class="sxs-lookup"><span data-stu-id="95821-218">✓</span></span> |
| <span data-ttu-id="95821-219">**版權管理**</span><span class="sxs-lookup"><span data-stu-id="95821-219">**Rights managment**</span></span> | | | |
| <span data-ttu-id="95821-220">RMS 使用量</span><span class="sxs-lookup"><span data-stu-id="95821-220">RMS usage</span></span> | | |<span data-ttu-id="95821-221">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="95821-221">RMS Only</span></span> |
| <span data-ttu-id="95821-222">最活躍的 RMS 使用者</span><span class="sxs-lookup"><span data-stu-id="95821-222">Most active RMS users</span></span> | | |<span data-ttu-id="95821-223">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="95821-223">RMS Only</span></span> |
| <span data-ttu-id="95821-224">RMS 裝置使用量</span><span class="sxs-lookup"><span data-stu-id="95821-224">RMS device usage</span></span> | | |<span data-ttu-id="95821-225">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="95821-225">RMS Only</span></span> |
| <span data-ttu-id="95821-226">啟用 RMS 的應用程式使用量</span><span class="sxs-lookup"><span data-stu-id="95821-226">RMS enabled application usage</span></span> | | |<span data-ttu-id="95821-227">僅 RMS</span><span class="sxs-lookup"><span data-stu-id="95821-227">RMS Only</span></span> |

## <a name="anomalous-activity-reports"></a><span data-ttu-id="95821-228">異常活動報告</span><span class="sxs-lookup"><span data-stu-id="95821-228">Anomalous activity reports</span></span>
<p><span data-ttu-id="95821-229">hello 異常登入活動報表可疑活動 tooOffice365、 Azure 管理入口網站、 Azure AD 存取面板、 Sharepoint Online、 Dynamics CRM Online，及其他 Microsoft online services 中的旗標。</span><span class="sxs-lookup"><span data-stu-id="95821-229">hello anomalous sign in activity reports flag suspicious sign in activity tooOffice365, Azure Management Portal, Azure AD Access Panel, Sharepoint Online, Dynamics CRM Online, and other Microsoft online services.</span></span></p>

<p><span data-ttu-id="95821-230">所有這些報表，除了 hello 」 多次失敗後的登入 」 的報表，還加上旗標可疑<i>同盟</i>登入 toohello 上述服務，不論 hello 同盟提供者。</span><span class="sxs-lookup"><span data-stu-id="95821-230">All of these reports, except hello "Sign ins after multiple failures" report, also flag suspicious <i>federated</i> sign ins toohello aforementioned services, regardless of hello federation provider.</span></span> </p>

<p><span data-ttu-id="95821-231">hello 下列報表可用：</span><span class="sxs-lookup"><span data-stu-id="95821-231">hello following reports are available:</span></span> </p><ul>

<li><span data-ttu-id="95821-232">[從不明來源登入](active-directory-reporting-sign-ins-from-unknown-sources的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-232">[Sign ins from unknown sources](active-directory-reporting-sign-ins-from-unknown-sources.md).</span></span></li>

<li><span data-ttu-id="95821-233">[在多次失敗後登入](active-directory-reporting-sign-ins-after-multiple-failures的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-233">[Sign ins after multiple failures](active-directory-reporting-sign-ins-after-multiple-failures.md).</span></span></li>

<li><span data-ttu-id="95821-234">[從多個地理區域登入](active-directory-reporting-sign-ins-from-multiple-geographies的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-234">[Sign ins from multiple geographies](active-directory-reporting-sign-ins-from-multiple-geographies.md).</span></span></li>

<li><span data-ttu-id="95821-235">[從具有可疑活動的 IP 位址登入](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-235">[Sign ins from IP addresses with suspicious activity](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</span></span></li>

<li><span data-ttu-id="95821-236">[異常的登入活動](active-directory-reporting-irregular-sign-in-activity的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-236">[Irregular sign in activity](active-directory-reporting-irregular-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="95821-237">[從可能受感染的裝置登入](active-directory-reporting-sign-ins-from-possibly-infected-devices的一部分。md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-237">[Sign ins from possibly infected devices](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</span></span></li>

<li><span data-ttu-id="95821-238">[具有異常登入活動的使用者](active-directory-reporting-users-with-anomalous-sign-in-activity.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="95821-238">[Users with anomalous sign in activity](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</span></span></li>

<li><span data-ttu-id="95821-239">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="95821-239">Users with leaked credentials</span></span></li></ul>

## <a name="activity-logs"></a><span data-ttu-id="95821-240">活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="95821-240">Activity logs</span></span>
### <a name="audit-report"></a><span data-ttu-id="95821-241">稽核報告</span><span class="sxs-lookup"><span data-stu-id="95821-241">Audit report</span></span>
| <span data-ttu-id="95821-242">說明</span><span class="sxs-lookup"><span data-stu-id="95821-242">Description</span></span> | <span data-ttu-id="95821-243">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-243">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-244">顯示 hello 過去 24 小時、 過去 7 天或過去 30 天內所有稽核事件的記錄。</span><span class="sxs-lookup"><span data-stu-id="95821-244">Shows a record of all audited events within hello last 24 hours, last 7 days, or last 30 days.</span></span> <br /> <span data-ttu-id="95821-245">如需詳細資訊，請參閱 [Azure Active Directory 稽核報告事件](active-directory-reporting-audit-events.md)</span><span class="sxs-lookup"><span data-stu-id="95821-245">For more information, see [Azure Active Directory Audit Report Events](active-directory-reporting-audit-events.md)</span></span> |<span data-ttu-id="95821-246">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-246">Directory > Reports tab</span></span> |

![稽核報告](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a><span data-ttu-id="95821-248">密碼重設活動</span><span class="sxs-lookup"><span data-stu-id="95821-248">Password reset activity</span></span>
| <span data-ttu-id="95821-249">說明</span><span class="sxs-lookup"><span data-stu-id="95821-249">Description</span></span> | <span data-ttu-id="95821-250">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-250">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-251">顯示您的組織中發生的所有密碼重設嘗試</span><span class="sxs-lookup"><span data-stu-id="95821-251">Shows all password reset attempts that have occurred in your organization.</span></span> |<span data-ttu-id="95821-252">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-252">Directory > Reports tab</span></span> |

![密碼重設活動](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a><span data-ttu-id="95821-254">密碼重設註冊活動</span><span class="sxs-lookup"><span data-stu-id="95821-254">Password reset registration activity</span></span>
| <span data-ttu-id="95821-255">說明</span><span class="sxs-lookup"><span data-stu-id="95821-255">Description</span></span> | <span data-ttu-id="95821-256">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-256">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-257">顯示您的組織中發生的所有密碼重設登錄</span><span class="sxs-lookup"><span data-stu-id="95821-257">Shows all password reset registrations that have occurred in your organization</span></span> |<span data-ttu-id="95821-258">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-258">Directory > Reports tab</span></span> |

![密碼重設註冊活動](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a><span data-ttu-id="95821-260">自助服務群組活動</span><span class="sxs-lookup"><span data-stu-id="95821-260">Self service groups activity</span></span>
| <span data-ttu-id="95821-261">說明</span><span class="sxs-lookup"><span data-stu-id="95821-261">Description</span></span> | <span data-ttu-id="95821-262">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-262">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-263">在您的目錄中顯示 hello 自助服務受管理群組的所有活動。</span><span class="sxs-lookup"><span data-stu-id="95821-263">Shows all activity for hello self-service managed groups in your directory.</span></span> |<span data-ttu-id="95821-264">目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-264">Directory > Users > <i>User</i> > Devices tab</span></span> |

![自助服務群組活動](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a><span data-ttu-id="95821-266">整合式應用程式報告</span><span class="sxs-lookup"><span data-stu-id="95821-266">Integrated applications reports</span></span>
### <a name="application-usage-summary"></a><span data-ttu-id="95821-267">應用程式使用情況：摘要</span><span class="sxs-lookup"><span data-stu-id="95821-267">Application usage: summary</span></span>
| <span data-ttu-id="95821-268">說明</span><span class="sxs-lookup"><span data-stu-id="95821-268">Description</span></span> | <span data-ttu-id="95821-269">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-269">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-270">當您想 toosee 使用量所有 hello SaaS 應用程式目錄中時，請使用這份報表。</span><span class="sxs-lookup"><span data-stu-id="95821-270">Use this report when you want toosee usage for all hello SaaS applications in your directory.</span></span> <span data-ttu-id="95821-271">這份報表會根據使用者已按一下 hello hello 存取面板中的應用程式的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="95821-271">This report is based on hello number of times users have clicked on hello application in hello Access Panel.</span></span> |<span data-ttu-id="95821-272">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-272">Directory > Reports tab</span></span> |

<span data-ttu-id="95821-273">這份報表包含登入太*所有*您目錄具有應用程式存取，包括預先整合的 Microsoft 應用程式。</span><span class="sxs-lookup"><span data-stu-id="95821-273">This report includes sign ins too*all* applications that your directory has access to, including pre-integrated Microsoft applications.</span></span>

<span data-ttu-id="95821-274">預先整合的 Microsoft 應用程式包括 Office 365、 Sharepoint、 hello Azure 管理入口網站和其他項目。</span><span class="sxs-lookup"><span data-stu-id="95821-274">Pre-integrated Microsoft applications include Office 365, Sharepoint, hello Azure Management Portal, and others.</span></span>

![應用程式使用情況摘要](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a><span data-ttu-id="95821-276">應用程式使用情況：詳細</span><span class="sxs-lookup"><span data-stu-id="95821-276">Application usage: detailed</span></span>
| <span data-ttu-id="95821-277">說明</span><span class="sxs-lookup"><span data-stu-id="95821-277">Description</span></span> | <span data-ttu-id="95821-278">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-278">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-279">當您想的 toosee 正在使用多少特定 SaaS 應用程式時，請使用這份報表。</span><span class="sxs-lookup"><span data-stu-id="95821-279">Use this report when you want toosee how much a specific SaaS application is being used.</span></span> <span data-ttu-id="95821-280">這份報表會根據使用者已按一下 hello hello 存取面板中的應用程式的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="95821-280">This report is based on hello number of times users have clicked on hello application in hello Access Panel.</span></span> |<span data-ttu-id="95821-281">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-281">Directory > Reports tab</span></span> |

### <a name="application-dashboard"></a><span data-ttu-id="95821-282">應用程式儀表板</span><span class="sxs-lookup"><span data-stu-id="95821-282">Application dashboard</span></span>
| <span data-ttu-id="95821-283">說明</span><span class="sxs-lookup"><span data-stu-id="95821-283">Description</span></span> | <span data-ttu-id="95821-284">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-284">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-285">此報表指出累計登單元 toohello 應用程式中選取的時間間隔內，組織的使用者。</span><span class="sxs-lookup"><span data-stu-id="95821-285">This report indicates cumulative sign ins toohello application by users in your organization, over a selected time interval.</span></span> <span data-ttu-id="95821-286">hello 儀表板頁面上的 hello 圖表可協助您識別該應用程式的所有使用量的趨勢。</span><span class="sxs-lookup"><span data-stu-id="95821-286">hello chart on hello dashboard page will help you identify trends for all usage of that application.</span></span> |<span data-ttu-id="95821-287">目錄 > 應用程式 > 儀表板索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-287">Directory > Application > Dashboard tab</span></span> |

## <a name="error-reports"></a><span data-ttu-id="95821-288">錯誤報告</span><span class="sxs-lookup"><span data-stu-id="95821-288">Error reports</span></span>
### <a name="account-provisioning-errors"></a><span data-ttu-id="95821-289">帳戶佈建錯誤</span><span class="sxs-lookup"><span data-stu-id="95821-289">Account provisioning errors</span></span>
| <span data-ttu-id="95821-290">說明</span><span class="sxs-lookup"><span data-stu-id="95821-290">Description</span></span> | <span data-ttu-id="95821-291">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-291">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-292">使用從 SaaS 應用程式 tooAzure Active Directory 的帳戶 hello 同步處理期間發生此 toomonitor 錯誤。</span><span class="sxs-lookup"><span data-stu-id="95821-292">Use this toomonitor errors that occur during hello synchronization of accounts from SaaS applications tooAzure Active Directory.</span></span> |<span data-ttu-id="95821-293">目錄 > 報告索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-293">Directory > Reports tab</span></span> |

![帳戶佈建錯誤](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a><span data-ttu-id="95821-295">特定使用者報告</span><span class="sxs-lookup"><span data-stu-id="95821-295">User-specific reports</span></span>
### <a name="devices"></a><span data-ttu-id="95821-296">裝置</span><span class="sxs-lookup"><span data-stu-id="95821-296">Devices</span></span>
| <span data-ttu-id="95821-297">說明</span><span class="sxs-lookup"><span data-stu-id="95821-297">Description</span></span> | <span data-ttu-id="95821-298">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-298">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-299">當您想 toosee hello IP 位址和地理位置的特定使用者已使用 tooaccess Azure Active Directory 的裝置時，請使用這份報表。</span><span class="sxs-lookup"><span data-stu-id="95821-299">Use this report when you want toosee hello IP address and geographical location of devices that a specific user has used tooaccess Azure Active Directory.</span></span> |<span data-ttu-id="95821-300">目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-300">Directory > Users > <i>User</i> > Devices tab</span></span> |

### <a name="activity"></a><span data-ttu-id="95821-301">活動</span><span class="sxs-lookup"><span data-stu-id="95821-301">Activity</span></span>
| <span data-ttu-id="95821-302">說明</span><span class="sxs-lookup"><span data-stu-id="95821-302">Description</span></span> | <span data-ttu-id="95821-303">報告位置</span><span class="sxs-lookup"><span data-stu-id="95821-303">Report location</span></span> |
|:--- |:--- |
| <span data-ttu-id="95821-304">顯示 hello 登入使用者的活動。</span><span class="sxs-lookup"><span data-stu-id="95821-304">Shows hello sign in activity for a user.</span></span> <span data-ttu-id="95821-305">hello 報表包含 hello 登入的應用程式、 使用的裝置、 IP 位址和位置等資訊。</span><span class="sxs-lookup"><span data-stu-id="95821-305">hello report includes information like hello application signed into, device used, IP address, and location.</span></span> <span data-ttu-id="95821-306">我們不會收集使用 Microsoft 帳戶登入的使用者的 hello 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="95821-306">We do not collect hello history for users that sign in with a Microsoft account.</span></span> |<span data-ttu-id="95821-307">目錄 > 使用者 > <i>使用者</i> > 活動索引標籤</span><span class="sxs-lookup"><span data-stu-id="95821-307">Directory > Users > <i>User</i> > Activity tab</span></span> |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a><span data-ttu-id="95821-308">登入 hello 使用者活動報表中所含事件</span><span class="sxs-lookup"><span data-stu-id="95821-308">Sign in events included in hello User Activity report</span></span>
<span data-ttu-id="95821-309">只有某些類型的登入事件會出現在 hello 使用者活動報表。</span><span class="sxs-lookup"><span data-stu-id="95821-309">Only certain types of sign in events will appear in hello User Activity report.</span></span>

| <span data-ttu-id="95821-310">事件類型</span><span class="sxs-lookup"><span data-stu-id="95821-310">Event type</span></span> | <span data-ttu-id="95821-311">已包含？</span><span class="sxs-lookup"><span data-stu-id="95821-311">Included?</span></span> |
| --- | --- |
| <span data-ttu-id="95821-312">登入 toohello[存取面板](http://myapps.microsoft.com/)</span><span class="sxs-lookup"><span data-stu-id="95821-312">Sign ins toohello [Access Panel](http://myapps.microsoft.com/)</span></span> |<span data-ttu-id="95821-313">是</span><span class="sxs-lookup"><span data-stu-id="95821-313">Yes</span></span> |
| <span data-ttu-id="95821-314">登入 toohello [Azure 管理入口網站](https://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="95821-314">Sign ins toohello [Azure Management Portal](https://manage.windowsazure.com/)</span></span> |<span data-ttu-id="95821-315">是</span><span class="sxs-lookup"><span data-stu-id="95821-315">Yes</span></span> |
| <span data-ttu-id="95821-316">登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="95821-316">Sign ins toohello [Microsoft Azure Portal](https://portal.azure.com/)</span></span> |<span data-ttu-id="95821-317">是</span><span class="sxs-lookup"><span data-stu-id="95821-317">Yes</span></span> |
| <span data-ttu-id="95821-318">登入 toohello [Office 365 入口網站](http://portal.office.com/)</span><span class="sxs-lookup"><span data-stu-id="95821-318">Sign ins toohello [Office 365 portal](http://portal.office.com/)</span></span> |<span data-ttu-id="95821-319">是</span><span class="sxs-lookup"><span data-stu-id="95821-319">Yes</span></span> |
| <span data-ttu-id="95821-320">登入 tooa 原生應用程式，例如 Outlook （請參閱底下的例外狀況）</span><span class="sxs-lookup"><span data-stu-id="95821-320">Sign ins tooa native application, like Outlook (see exception below)</span></span> |<span data-ttu-id="95821-321">是</span><span class="sxs-lookup"><span data-stu-id="95821-321">Yes</span></span> |
| <span data-ttu-id="95821-322">登入 tooa 同盟/佈建應用程式透過存取面板，例如 Salesforce hello</span><span class="sxs-lookup"><span data-stu-id="95821-322">Sign ins tooa federated/provisioned app through hello Access Panel, like Salesforce</span></span> |<span data-ttu-id="95821-323">是</span><span class="sxs-lookup"><span data-stu-id="95821-323">Yes</span></span> |
| <span data-ttu-id="95821-324">登入 tooa 密碼為基礎的應用程式透過存取面板，例如 Twitter hello</span><span class="sxs-lookup"><span data-stu-id="95821-324">Sign ins tooa password-based app through hello Access Panel, like Twitter</span></span> |<span data-ttu-id="95821-325">是</span><span class="sxs-lookup"><span data-stu-id="95821-325">Yes</span></span> |
| <span data-ttu-id="95821-326">登入 tooa 自訂商務應用程式已新增 toohello 目錄</span><span class="sxs-lookup"><span data-stu-id="95821-326">Sign ins tooa custom business app that has been added toohello directory</span></span> |<span data-ttu-id="95821-327">否 (敬請期待)</span><span class="sxs-lookup"><span data-stu-id="95821-327">No (Coming soon)</span></span> |
| <span data-ttu-id="95821-328">登入 tooan Azure AD Application Proxy 應用程式已新增 toohello 目錄</span><span class="sxs-lookup"><span data-stu-id="95821-328">Sign ins tooan Azure AD Application Proxy app that has been added toohello directory</span></span> |<span data-ttu-id="95821-329">否 (敬請期待)</span><span class="sxs-lookup"><span data-stu-id="95821-329">No (Coming soon)</span></span> |

> <span data-ttu-id="95821-330">注意： 這份報表，雜訊 tooreduce hello 數量的登入的 hello [Microsoft Online Services 登入小幫手](http://community.office365.com/en-us/w/sso/534.aspx)不會顯示。</span><span class="sxs-lookup"><span data-stu-id="95821-330">Note: tooreduce hello amount of noise in this report, sign ins by hello [Microsoft Online Services Sign-In Assistant](http://community.office365.com/en-us/w/sso/534.aspx) are not shown.</span></span>
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a><span data-ttu-id="95821-331">如果您懷疑安全性缺口的事情 tooconsider</span><span class="sxs-lookup"><span data-stu-id="95821-331">Things tooconsider if you suspect security breach</span></span>
<span data-ttu-id="95821-332">如果您懷疑可能危害的使用者帳戶，或任何一種可能會導致 tooa 的目錄資料的安全性缺口 hello 雲端中的可疑的使用者活動，您可能會想 tooconsider 一或多個 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="95821-332">If you suspect that a user account may be compromised or any kind of suspicious user activity that may lead tooa security breach of your directory data in hello cloud, you may want tooconsider one or more of hello following actions:</span></span>

* <span data-ttu-id="95821-333">請連絡 hello 使用者 tooverify hello 活動</span><span class="sxs-lookup"><span data-stu-id="95821-333">Contact hello user tooverify hello activity</span></span>
* <span data-ttu-id="95821-334">重設 hello 使用者密碼</span><span class="sxs-lookup"><span data-stu-id="95821-334">Reset hello user's password</span></span>
* <span data-ttu-id="95821-335">[啟用多因素驗證](../multi-factor-authentication/multi-factor-authentication-get-started.md) 以提供額外的安全性</span><span class="sxs-lookup"><span data-stu-id="95821-335">[Enable multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md) for additional security</span></span>

## <a name="view-or-download-a-report"></a><span data-ttu-id="95821-336">檢視或下載報告</span><span class="sxs-lookup"><span data-stu-id="95821-336">View or download a report</span></span>
1. <span data-ttu-id="95821-337">在 hello Azure 傳統入口網站，按一下  **Active Directory**，按一下 hello 貴組織的目錄名稱，然後按一下**報表**。</span><span class="sxs-lookup"><span data-stu-id="95821-337">In hello Azure classic portal, click **Active Directory**, click hello name of your organization’s directory, and then click **Reports**.</span></span>
2. <span data-ttu-id="95821-338">在 hello 報表頁面上，按一下您想要 tooview hello 報表和 （或) 下載。</span><span class="sxs-lookup"><span data-stu-id="95821-338">On hello Reports page, click hello report you want tooview and/or download.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95821-339">如果這是 hello 您已使用 hello 報告功能的 Azure Active Directory 的第一次，您會看到訊息 tooOpt 中。</span><span class="sxs-lookup"><span data-stu-id="95821-339">If this is hello first time you have used hello reporting feature of Azure Active Directory, you will see a message tooOpt In.</span></span> <span data-ttu-id="95821-340">如果您同意，請按一下 hello 核取記號圖示 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="95821-340">If you agree, click hello check mark icon toocontinue.</span></span>
   > 
   > 
3. <span data-ttu-id="95821-341">按一下 下拉式選單下一步 tooInterval hello，，然後選取其中一個 hello 後應該產生此報表時使用的時間範圍：</span><span class="sxs-lookup"><span data-stu-id="95821-341">Click hello drop-down menu next tooInterval, and then select one of hello following time ranges that should be used when generating this report:</span></span>
   
   * <span data-ttu-id="95821-342">過去 24 小時</span><span class="sxs-lookup"><span data-stu-id="95821-342">Last 24 hours</span></span>
   * <span data-ttu-id="95821-343">過去 7 天</span><span class="sxs-lookup"><span data-stu-id="95821-343">Last 7 days</span></span>
   * <span data-ttu-id="95821-344">過去 30 天</span><span class="sxs-lookup"><span data-stu-id="95821-344">Last 30 days</span></span>
4. <span data-ttu-id="95821-345">按一下 hello 核取記號圖示 toorun hello 報表。</span><span class="sxs-lookup"><span data-stu-id="95821-345">Click hello check mark icon toorun hello report.</span></span>
   * <span data-ttu-id="95821-346">向上 too1000 hello Azure 傳統入口網站中會顯示事件。</span><span class="sxs-lookup"><span data-stu-id="95821-346">Up too1000 events will be shown in hello Azure classic portal.</span></span>
5. <span data-ttu-id="95821-347">如果適用的話，按一下**下載**toodownload hello 報表 tooa 壓縮的檔案以逗號分隔值 (CSV) 格式離線檢視或封存。</span><span class="sxs-lookup"><span data-stu-id="95821-347">If applicable, click **Download** toodownload hello report tooa compressed file in comma-separated values (CSV) format for offline viewing or archiving purposes.</span></span>
   * <span data-ttu-id="95821-348">向上 too75，000 事件將會包含在 hello 下載檔案。</span><span class="sxs-lookup"><span data-stu-id="95821-348">Up too75,000 events will be included in hello downloaded file.</span></span>
   * <span data-ttu-id="95821-349">如需詳細資料，查看 hello [Azure AD 報告 API](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="95821-349">For more data, check out hello [Azure AD Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

## <a name="ignore-an-event"></a><span data-ttu-id="95821-350">忽略事件</span><span class="sxs-lookup"><span data-stu-id="95821-350">Ignore an event</span></span>
<span data-ttu-id="95821-351">如果正在檢視任何異常報告，您可能會注意到您可以忽略顯示在相關報告中的各種事件。</span><span class="sxs-lookup"><span data-stu-id="95821-351">If you are viewing any anomaly reports, you may notice that you can ignore various events that show up in related reports.</span></span> <span data-ttu-id="95821-352">tooignore 事件，只要醒目提示 hello 報表中的 hello 事件，然後按一下**忽略**。</span><span class="sxs-lookup"><span data-stu-id="95821-352">tooignore an event, simply highlight hello event in hello report and then click **Ignore**.</span></span> <span data-ttu-id="95821-353">hello**忽略**按鈕將會永久移除 hello 報表中的 hello 反白顯示的事件，只用於授權全域管理員。</span><span class="sxs-lookup"><span data-stu-id="95821-353">hello **Ignore** button will permanently remove hello highlighted event from hello report and can only be used by licensed global admins.</span></span>

## <a name="automatic-email-notifications"></a><span data-ttu-id="95821-354">自動電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="95821-354">Automatic email notifications</span></span>
<span data-ttu-id="95821-355">如需有關 Azure AD 的報告通知詳細資訊，請參閱 [Azure Active Directory 報告通知](active-directory-reporting-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="95821-355">For more information about Azure AD's reporting notifications, check out [Azure Active Directory Reporting Notifications](active-directory-reporting-notifications.md).</span></span>

## <a name="whats-next"></a><span data-ttu-id="95821-356">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95821-356">What's next</span></span>
* [<span data-ttu-id="95821-357">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="95821-357">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="95821-358">新增公司品牌 tooyour 登入及存取面板頁面</span><span class="sxs-lookup"><span data-stu-id="95821-358">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

