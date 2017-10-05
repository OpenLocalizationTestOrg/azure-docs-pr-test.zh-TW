---
title: "使用應用程式 Proxy 應用程式時發生「無法存取此企業應用程式」錯誤 | Microsoft Docs"
description: "如何解決使用 Azure AD 應用程式 Proxy 應用程式時常見的存取問題。"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 78ff8763a461162cbcfa04c6a86123973271928a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a><span data-ttu-id="42e5c-103">使用 Application Proxy 應用程式時發生「無法存取此企業應用程式」錯誤</span><span class="sxs-lookup"><span data-stu-id="42e5c-103">"Can't Access this Corporate Application" error when using an Application Proxy application</span></span>

<span data-ttu-id="42e5c-104">這篇文章可協助您為在 Azure AD Application Proxy 應用程式上看到「無法存取此企業應用程式」錯誤時所面臨的常見問題疑難排解。</span><span class="sxs-lookup"><span data-stu-id="42e5c-104">This article help you to troubleshoot common issues faced when you see a "This corporate app can't be accessed" error on an Azure AD Application Proxy application.</span></span>

## <a name="overview"></a><span data-ttu-id="42e5c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="42e5c-105">Overview</span></span>
<span data-ttu-id="42e5c-106">當您看見此錯誤時，頁面也會顯示狀態碼。</span><span class="sxs-lookup"><span data-stu-id="42e5c-106">When you see this error, the page also share a status code.</span></span> <span data-ttu-id="42e5c-107">狀態碼可能代表下列其中一種狀態：</span><span class="sxs-lookup"><span data-stu-id="42e5c-107">That code is likely one of the following:</span></span>

-   <span data-ttu-id="42e5c-108">**閘道逾時**：Application Proxy 服務會無法連線到連接器。</span><span class="sxs-lookup"><span data-stu-id="42e5c-108">**Gateway Timeout**: The Application Proxy service is unable to reach the connector.</span></span> <span data-ttu-id="42e5c-109">這通常表示連接器指派、連接器本身，或連接器相關的網路規則有問題。</span><span class="sxs-lookup"><span data-stu-id="42e5c-109">This typically indicates a problem with the connector assignment, connector itself, or the networking rules around the connector.</span></span>

-   <span data-ttu-id="42e5c-110">**不正確的閘道**︰ 連接器無法連線到後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-110">**Bad Gateway**: The connector is unable to reach the backend application.</span></span> <span data-ttu-id="42e5c-111">這表示應用程式的設定不正確。</span><span class="sxs-lookup"><span data-stu-id="42e5c-111">This could indicate a misconfiguration of the application.</span></span>

-   <span data-ttu-id="42e5c-112">**禁止**︰使用者未獲授權存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-112">**Forbidden**: The user is not authorized to access the application.</span></span> <span data-ttu-id="42e5c-113">當未將使用者指派至 Azure Active Directory 中的應用程式，或者使用者在後端沒有存取應用程式的權限，便會發生此狀態。</span><span class="sxs-lookup"><span data-stu-id="42e5c-113">This can happen either when the user is not assigned to the application in Azure Active Directory, or if on the backend the user does not have permission to access the application.</span></span>

<span data-ttu-id="42e5c-114">若要尋找狀態碼，請在錯誤訊息底端的文字中找到「狀態碼」欄位。</span><span class="sxs-lookup"><span data-stu-id="42e5c-114">To find the code, look at the text at the bottom left of the error message for the “Status Code” field.</span></span> <span data-ttu-id="42e5c-115">此外也可以在頁面最底端找到任何有其他秘訣的註解。</span><span class="sxs-lookup"><span data-stu-id="42e5c-115">Also look for any notes at the very bottom of the page with additional tips.</span></span>

   ![閘道逾時錯誤](./media/application-proxy/connection-problem.png)

<span data-ttu-id="42e5c-117">如需如何為這些錯誤的根本原因疑難排解的詳細資訊，以及建議的修正程式詳細資料，請參閱下方對應的章節。</span><span class="sxs-lookup"><span data-stu-id="42e5c-117">For details on how to troubleshoot the root cause of these errors and more details on suggested fixes, see the corresponding section below.</span></span>

## <a name="gateway-timeout-errors"></a><span data-ttu-id="42e5c-118">閘道逾時錯誤</span><span class="sxs-lookup"><span data-stu-id="42e5c-118">Gateway Timeout errors</span></span>

<span data-ttu-id="42e5c-119">當服務嘗試連線到連接器時，若無法在逾時時間範圍內連線，即發生閘道逾時。</span><span class="sxs-lookup"><span data-stu-id="42e5c-119">A gateway timeout occurs when the service tries to reach the connector and is unable to within the timeout window.</span></span> <span data-ttu-id="42e5c-120">這通常是因為指派至連接器群組的應用程式沒有運作中的連接器，或連接器所需的某些連接埠並未開啟所造成的。</span><span class="sxs-lookup"><span data-stu-id="42e5c-120">This is typically caused by an application assigned to a Connector Group with no working connectors, or some ports required by the Connector are not open.</span></span>


## <a name="bad-gateway-errors"></a><span data-ttu-id="42e5c-121">閘道錯誤</span><span class="sxs-lookup"><span data-stu-id="42e5c-121">Bad Gateway errors</span></span>

<span data-ttu-id="42e5c-122">不正確的閘道是指連接器無法連線到後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-122">A bad gateway error indicates that the connector is unable to reach the backend application.</span></span> <span data-ttu-id="42e5c-123">請確定您所發佈的是正確的應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-123">make sure that you have published the correct application.</span></span> <span data-ttu-id="42e5c-124">造成此錯誤的常見過失︰</span><span class="sxs-lookup"><span data-stu-id="42e5c-124">Common mistakes that cause this error:</span></span>

-   <span data-ttu-id="42e5c-125">打字錯誤或內部 URL 不正確</span><span class="sxs-lookup"><span data-stu-id="42e5c-125">A typo or mistake in the internal URL</span></span>

-   <span data-ttu-id="42e5c-126">未發佈應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="42e5c-126">Not publishing the root of the application.</span></span> <span data-ttu-id="42e5c-127">例如，發佈的是 <http://expenses/reimbursement>，但嘗試存取 <http://expenses></span><span class="sxs-lookup"><span data-stu-id="42e5c-127">For example, publishing <http://expenses/reimbursement> but trying to access <http://expenses></span></span>

-   <span data-ttu-id="42e5c-128">Kerberos 限制委派 (KCD) 組態有問題</span><span class="sxs-lookup"><span data-stu-id="42e5c-128">Problems with the Kerberos Constrained Delegation (KCD) configuration</span></span>

-   <span data-ttu-id="42e5c-129">後端應用程式有問題</span><span class="sxs-lookup"><span data-stu-id="42e5c-129">Problems with the backend application</span></span>

## <a name="forbidden-errors"></a><span data-ttu-id="42e5c-130">禁止錯誤</span><span class="sxs-lookup"><span data-stu-id="42e5c-130">Forbidden errors</span></span>

<span data-ttu-id="42e5c-131">如果您看到禁止錯誤，則表示使用者尚未指派至該應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-131">If you see a forbidden error, the user has not been assigned to the application.</span></span> <span data-ttu-id="42e5c-132">這可能發生在 Azure Active Directory 或後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-132">This could be either in Azure Active Directory or on the backend application.</span></span>

<span data-ttu-id="42e5c-133">若要了解如何將使用者指派至 Azure 中的應用程式，請參閱[組態文件](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user)。</span><span class="sxs-lookup"><span data-stu-id="42e5c-133">To learn how to assign users to the application in Azure, see the [configuration documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).</span></span>

<span data-ttu-id="42e5c-134">如果您確認使用者已指派至 Azure 中的應用程式，請在後端應用程式中檢查使用者組態。</span><span class="sxs-lookup"><span data-stu-id="42e5c-134">If you confirm the user is assigned to the application in Azure, check the user configuration in the backend application.</span></span> <span data-ttu-id="42e5c-135">如果您使用的是 Kerberos 限制委派/整合式 Windows 驗證，您可以在我們的 [KCD 疑難排解] 頁面上看到部分指導方針。</span><span class="sxs-lookup"><span data-stu-id="42e5c-135">If you are using Kerberos Constrained Delegation/Integrated Windows Authentication, you can see our KCD Troubleshoot page for some guidelines.</span></span>

## <a name="check-the-applications-internal-url"></a><span data-ttu-id="42e5c-136">檢查應用程式的內部 URL</span><span class="sxs-lookup"><span data-stu-id="42e5c-136">Check the application's internal URL</span></span>

<span data-ttu-id="42e5c-137">第一個快速步驟就是反覆檢查內部 URL 並加以修正，做法是透過 [企業應用程式] 開啟應用程式，然後選取 [Application Proxy] 功能表。</span><span class="sxs-lookup"><span data-stu-id="42e5c-137">As a first quick step, double check check and fix the internal URL by opening the application through **Enterprise Applications**, then selecting the **Application Proxy** menu.</span></span> <span data-ttu-id="42e5c-138">確認內部 URL 正確無誤，亦即從您的內部網路用於存取應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="42e5c-138">Verify this is the correct internal URL, the one used from your on-prem network to access the application.</span></span>

## <a name="check-the-application-is-assigned-to-a-working-connector-group"></a><span data-ttu-id="42e5c-139">確認應用程式已指派至運作中的連接器群組</span><span class="sxs-lookup"><span data-stu-id="42e5c-139">Check the application is assigned to a working Connector Group</span></span>

<span data-ttu-id="42e5c-140">若要確認應用程式已指派至運作中的連接器群組：</span><span class="sxs-lookup"><span data-stu-id="42e5c-140">To verify the application is assigned to a working Connector Group:</span></span>

1.  <span data-ttu-id="42e5c-141">移至 [Azure Active Directory]，然後依序按一下 [企業應用程式]、[所有應用程式]，以開啟入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-141">Open the application in the portal by going to **Azure Active Directory**, clicking on **Enterprise Applications**, then **All Applications.**</span></span> <span data-ttu-id="42e5c-142">開啟應用程式，然後選取左側功能表中的 [Application Proxy]。</span><span class="sxs-lookup"><span data-stu-id="42e5c-142">Open the application, then select **Application Proxy** from the left menu.</span></span>

2.  <span data-ttu-id="42e5c-143">找到 [連接器群組] 欄位。</span><span class="sxs-lookup"><span data-stu-id="42e5c-143">Look at the Connector Group field.</span></span> <span data-ttu-id="42e5c-144">如果群組中沒有作用中的連接器，您會看到一則警告。</span><span class="sxs-lookup"><span data-stu-id="42e5c-144">If there are no active connectors in the group, you see a warning.</span></span> <span data-ttu-id="42e5c-145">如果您沒有看到任何警告，請進一步「確認所有必要的連接埠皆在允許清單中」。</span><span class="sxs-lookup"><span data-stu-id="42e5c-145">If you don’t see any warnings, move on to “verify all required ports are whitelisted”.</span></span>

3.  <span data-ttu-id="42e5c-146">如果這是錯誤的連接器群組，請使用下拉清單選取正確的群組，並確認未再出現任何警告。</span><span class="sxs-lookup"><span data-stu-id="42e5c-146">If this is the wrong Connector Group, use the drop down to select the correct group, and confirm you no longer see any warnings.</span></span> <span data-ttu-id="42e5c-147">如果這是所需的連接器群組，請按一下警告訊息以開啟含連接器管理資訊的頁面。</span><span class="sxs-lookup"><span data-stu-id="42e5c-147">If this is the intended Connector Group, click the warning message to open the page with Connector management.</span></span>

4.  <span data-ttu-id="42e5c-148">此頁面提供數種方法可進一步向下切入：</span><span class="sxs-lookup"><span data-stu-id="42e5c-148">From here, there are a few ways to drill in further:</span></span>

  * <span data-ttu-id="42e5c-149">將作用中連接器移至群組中：如果您有應該屬於群組的作用中連接器，而且能直接看到目標後端應用程式，您就可以將連接器移入指派的群組。</span><span class="sxs-lookup"><span data-stu-id="42e5c-149">Move an active Connector into the group: If you have an active Connector that should belong to this group and has line of sight to the target backend application, you can move the Connector into the assigned group.</span></span> <span data-ttu-id="42e5c-150">若要這麼做，請按一下連接器。</span><span class="sxs-lookup"><span data-stu-id="42e5c-150">To do so, click the Connector.</span></span> <span data-ttu-id="42e5c-151">在 [連接器群組] 欄位中，使用下拉式清單選取正確的群組，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="42e5c-151">In the “Connector Group” field, use the drop-down to select the correct group, and click save.</span></span>

  * <span data-ttu-id="42e5c-152">下載該群組的新連接器：此頁面上有連結可讓您[下載新連接器](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download)。</span><span class="sxs-lookup"><span data-stu-id="42e5c-152">Download a new Connector for that group: From this page, you can get the link to [download a new Connector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download).</span></span> <span data-ttu-id="42e5c-153">連接器必須安裝在可直接看到後端應用程式的電腦上，而且通常會位於與應用程式相同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="42e5c-153">The Connector needs to be installed on a machine with direct line of sight to the backend application, and is typically placed on the same server as the application.</span></span> <span data-ttu-id="42e5c-154">使用下載連接器連結，將連接器下載到目標電腦上。</span><span class="sxs-lookup"><span data-stu-id="42e5c-154">Use the download Connector link to download a connector onto the target machine.</span></span> <span data-ttu-id="42e5c-155">接著按一下連接器，然後使用 [連接器群組] 下拉式清單確定它屬於正確的群組。</span><span class="sxs-lookup"><span data-stu-id="42e5c-155">Next, click the Connector, and use the “Connector Group” drop-down to make sure it belongs to the right group.</span></span>

  * <span data-ttu-id="42e5c-156">調查非作用中連接器︰如果連接器會顯示為非作用中，則表示它無法連線到服務。</span><span class="sxs-lookup"><span data-stu-id="42e5c-156">Investigate an inactive Connector: If a connector shows as inactive, it is unable to reach the service.</span></span> <span data-ttu-id="42e5c-157">這通常是因為某些必要連接埠遭到封鎖造成的。</span><span class="sxs-lookup"><span data-stu-id="42e5c-157">This is typically due to some required ports being blocked.</span></span> <span data-ttu-id="42e5c-158">若要解決此問題，請進一步「確認所有必要的連接埠皆在允許清單中」。</span><span class="sxs-lookup"><span data-stu-id="42e5c-158">To solve this issue, move on to “verify all required ports are whitelisted”.</span></span>

<span data-ttu-id="42e5c-159">在使用這些步驟確認應用程式已指派至有運作中連接器的群組後，請再次測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-159">After using these steps to ensure the application is assigned to a group with working Connectors, test the application again.</span></span> <span data-ttu-id="42e5c-160">如果仍然無法運作，繼續進行下一節。</span><span class="sxs-lookup"><span data-stu-id="42e5c-160">If it is still not working, continue to the next section.</span></span>

## <a name="check-all-required-ports-are-whitelisted"></a><span data-ttu-id="42e5c-161">檢查所有必要連接埠皆在允許清單中</span><span class="sxs-lookup"><span data-stu-id="42e5c-161">Check all required ports are whitelisted</span></span>

<span data-ttu-id="42e5c-162">若要確認所有必要連接埠皆已開啟，請參閱我們有關開啟連接埠的文件。</span><span class="sxs-lookup"><span data-stu-id="42e5c-162">To verify that all required ports are open, see our documentation on opening ports.</span></span> <span data-ttu-id="42e5c-163">如果所有必要連接埠皆已開啟，請移至下一節。</span><span class="sxs-lookup"><span data-stu-id="42e5c-163">If all the required ports are open, move to the next section.</span></span>

## <a name="check-for-other-connector-errors"></a><span data-ttu-id="42e5c-164">檢查有無其他連接器錯誤</span><span class="sxs-lookup"><span data-stu-id="42e5c-164">Check for other Connector Errors</span></span>

<span data-ttu-id="42e5c-165">如果上述方法都無法解決此問題，下一步就是找出連接器本身的問題或錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-165">If none of the above resolve the issue, the next step is to look for issues or errors with the Connector itself.</span></span> <span data-ttu-id="42e5c-166">您可以在[疑難排解文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors)中看見一些常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-166">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span></span> 

<span data-ttu-id="42e5c-167">您也可以直接查看連接器記錄檔，以找出任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-167">You can also look directly at the Connector logs to identify any errors.</span></span> <span data-ttu-id="42e5c-168">我們的錯誤訊息中有許多能夠分享更具體的修正程式建議。</span><span class="sxs-lookup"><span data-stu-id="42e5c-168">Many of our error messages be able to share more specific recommendations for fixes.</span></span> <span data-ttu-id="42e5c-169">若要了解如何檢視記錄檔，請參閱[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood)。</span><span class="sxs-lookup"><span data-stu-id="42e5c-169">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span></span>

## <a name="additional-resolutions"></a><span data-ttu-id="42e5c-170">其他解決方式</span><span class="sxs-lookup"><span data-stu-id="42e5c-170">Additional Resolutions</span></span>

<span data-ttu-id="42e5c-171">如果上述方法皆無法修正問題，有幾個不同的可能原因。</span><span class="sxs-lookup"><span data-stu-id="42e5c-171">If the above didn’t fix the problem, there are a few different possible causes.</span></span> <span data-ttu-id="42e5c-172">若要找出問題︰</span><span class="sxs-lookup"><span data-stu-id="42e5c-172">To identify the issue:</span></span>

<span data-ttu-id="42e5c-173">如果您的應用程式是設定為使用整合式 Windows 驗證 (IWA)，請在未單一登入的情況下測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-173">If your application is configured to use Integrated Windows Authentication (IWA), test the application without single sign-on.</span></span> <span data-ttu-id="42e5c-174">如果不是，請移至下一段。</span><span class="sxs-lookup"><span data-stu-id="42e5c-174">If not, move to the next paragraph.</span></span> <span data-ttu-id="42e5c-175">若要在未單一登入的情況下檢查應用程式，請透過 [企業應用程式] 開啟您的應用程式，然後移至 [單一登入] 功能表。</span><span class="sxs-lookup"><span data-stu-id="42e5c-175">To check the application without single sign-on, open your application through **Enterprise Applications,** and go to the **Single Sign-On** menu.</span></span> <span data-ttu-id="42e5c-176">將下拉式清單從 [整合式 Windows 驗證] 變更為 [Azure AD single sign-on disabled (Azure AD 單一登入已停用)]。</span><span class="sxs-lookup"><span data-stu-id="42e5c-176">Change the drop down from “Integrated Windows Authentication” to “Azure AD single sign-on disabled”.</span></span> 

<span data-ttu-id="42e5c-177">現在開啟瀏覽器，然後再次嘗試存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-177">Now open a browser and try to access the application again.</span></span> <span data-ttu-id="42e5c-178">系統應該會提示您輸入驗證並進入應用程式。</span><span class="sxs-lookup"><span data-stu-id="42e5c-178">You should be prompted for authentication and get into the application.</span></span> <span data-ttu-id="42e5c-179">如果可進入，則問題出在啟用單一登入的 Kerberos 限制委派 (KCD) 組態。</span><span class="sxs-lookup"><span data-stu-id="42e5c-179">If this works, the problem is with the Kerberos Constrained Delegation (KCD) configuration that enables the single sign-on.</span></span> <span data-ttu-id="42e5c-180">請參閱 [KCD 疑難排解] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42e5c-180">see the KCD Troubleshoot page.</span></span>

<span data-ttu-id="42e5c-181">如果您繼續看到此錯誤，請移到已安裝連接器的電腦，開啟瀏覽器，並嘗試連線到應用程式使用的內部 URL。</span><span class="sxs-lookup"><span data-stu-id="42e5c-181">If you continue to see the error, go to the machine where the Connector is installed, open a browser and attempt to reach the internal URL used for the application.</span></span> <span data-ttu-id="42e5c-182">連接器就像同一台電腦中的另一個用戶端。</span><span class="sxs-lookup"><span data-stu-id="42e5c-182">The Connector acts like another client from the same machine.</span></span> <span data-ttu-id="42e5c-183">如果您無法連線到應用程式，請調查為何該電腦無法連線到應用程式，或使用能夠存取應用程式之伺服器上的連接器。</span><span class="sxs-lookup"><span data-stu-id="42e5c-183">If you can’t reach the application, investigate why that machine is unable to reach the application, or use a connector on a server that is able to access the application.</span></span>

<span data-ttu-id="42e5c-184">如果您可以從電腦連線到應用程式，請找出連接器本身的問題或錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-184">If you can reach the application from that machine, to look for issues or errors with the Connector itself.</span></span> <span data-ttu-id="42e5c-185">您可以在[疑難排解文件](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors)中看見一些常見錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-185">You can see some common errors in the [Troubleshoot document](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors).</span></span> <span data-ttu-id="42e5c-186">您也可以直接查看連接器記錄檔，以找出任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="42e5c-186">You can also look directly at the Connector logs to identify any errors.</span></span> <span data-ttu-id="42e5c-187">我們的錯誤訊息中有許多能夠分享更具體的修正程式建議。</span><span class="sxs-lookup"><span data-stu-id="42e5c-187">Many of our error messages be able to share more specific recommendations for fixes.</span></span> <span data-ttu-id="42e5c-188">若要了解如何檢視記錄檔，請參閱[連接器文件](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood)。</span><span class="sxs-lookup"><span data-stu-id="42e5c-188">To learn how to view the logs, see [our connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42e5c-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42e5c-189">Next steps</span></span>
[<span data-ttu-id="42e5c-190">了解 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="42e5c-190">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
