---
title: "Azure AD Connect：更新 Active Directory Federation Services (AD FS) 伺服器陣列的 SSL 憑證 | Microsoft Docs"
description: "本文件詳述使用 Azure AD Connect 更新 AD FS 伺服器陣列 SSL 憑證的步驟。"
services: active-directory
keywords: "azure ad connect, adfs ssl 更新, adfs 憑證更新, 變更 adfs 憑證, 新增 adfs 憑證, adfs 憑證, 更新 adfs ssl 憑證, 更新 ssl 憑證 adfs, 設定 adfs ssl 憑證, adfs, ssl, 憑證, adfs 服務通訊憑證, 更新同盟, 設定同盟, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="95847-104">更新 Active Directory Federation Services (AD FS) 伺服器陣列的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="95847-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="95847-105">概觀</span><span class="sxs-lookup"><span data-stu-id="95847-105">Overview</span></span>
<span data-ttu-id="95847-106">本文說明您如何使用 Azure AD Connect 來更新 Active Directory Federation Services (AD FS) 伺服器陣列的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="95847-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="95847-107">即使選取的使用者登入方法不是 AD FS，您也可以使用 Azure AD Connect 工具輕鬆地更新 AD FS 伺服器陣列的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="95847-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="95847-108">只要 3 個簡單步驟，即可跨所有同盟和 Web 應用程式 Proxy (WAP) 伺服器，執行 AD FS 之 SSL 憑證的完整更新作業︰</span><span class="sxs-lookup"><span data-stu-id="95847-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![三個步驟](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="95847-110">若要深入了解 AD FS 所使用的憑證，請參閱[了解 AD FS 所使用的憑證](https://technet.microsoft.com/library/cc730660.aspx)。</span><span class="sxs-lookup"><span data-stu-id="95847-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95847-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="95847-111">Prerequisites</span></span>

* <span data-ttu-id="95847-112">**AD FS 伺服器陣列**︰請確定您的 AD FS 伺服器陣列是 Windows Server 2012 R2 型或更新版本。</span><span class="sxs-lookup"><span data-stu-id="95847-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="95847-113">**Azure AD Connect**︰請確定 Azure AD Connect 版本為 1.1.443.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="95847-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="95847-114">您會使用工作「更新 AD FS SSL 憑證」。</span><span class="sxs-lookup"><span data-stu-id="95847-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![更新 SSL 工作](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="95847-116">步驟 1︰提供 AD FS 伺服器陣列資訊</span><span class="sxs-lookup"><span data-stu-id="95847-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="95847-117">Azure AD Connect 會透過下列方式，嘗試自動取得 AD FS 伺服器陣列的相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="95847-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="95847-118">自 AD FS (Windows Server 2016 或更新版本) 查詢伺服器陣列資訊。</span><span class="sxs-lookup"><span data-stu-id="95847-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="95847-119">參照來自前次執行的資訊 (使用 Azure AD Connect 儲存在本機)。</span><span class="sxs-lookup"><span data-stu-id="95847-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="95847-120">您可以修改所顯示之伺服器的清單，方法是新增或移除伺服器以反映 AD FS 伺服器陣列的目前組態。</span><span class="sxs-lookup"><span data-stu-id="95847-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="95847-121">只要提供了伺服器資訊，Azure AD Connect 會顯示連線和目前的 SSL 憑證狀態。</span><span class="sxs-lookup"><span data-stu-id="95847-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![AD FS 伺服器資訊](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="95847-123">如果清單包含不再屬於 AD FS 伺服器陣列的伺服器，則按一下 [移除] 可從 AD FS 伺服器陣列中的伺服器清單刪除伺服器。</span><span class="sxs-lookup"><span data-stu-id="95847-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![清單中的離線伺服器](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="95847-125">在 Azure AD Connect 中從 AD FS 伺服器陣列的伺服器清單中移除伺服器是本機作業，並且會更新 Azure AD Connect 在本機維護之 AD FS 伺服器陣列的資訊。</span><span class="sxs-lookup"><span data-stu-id="95847-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="95847-126">Azure AD Connect 不會修改 AD FS 上的組態以反映變更。</span><span class="sxs-lookup"><span data-stu-id="95847-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="95847-127">步驟 2︰提供新的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="95847-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="95847-128">確認 AD FS 伺服器陣列伺服器的相關資訊之後，Azure AD Connect 會要求新的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="95847-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="95847-129">提供使用密碼保護的 PFX 憑證以繼續安裝。</span><span class="sxs-lookup"><span data-stu-id="95847-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL 憑證](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="95847-131">您提供憑證之後，Azure AD Connect 會經歷一系列的必要條件。</span><span class="sxs-lookup"><span data-stu-id="95847-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="95847-132">確認憑證以確定憑證對於 AD FS 伺服器陣列是正確的︰</span><span class="sxs-lookup"><span data-stu-id="95847-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="95847-133">憑證的主體名稱/替代主體名稱與同盟服務名稱相同，或者是萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="95847-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="95847-134">憑證有效期限為 30 天以上。</span><span class="sxs-lookup"><span data-stu-id="95847-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="95847-135">憑證信任鏈結有效。</span><span class="sxs-lookup"><span data-stu-id="95847-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="95847-136">憑證使用密碼保護。</span><span class="sxs-lookup"><span data-stu-id="95847-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="95847-137">步驟 3︰選取用於更新的伺服器</span><span class="sxs-lookup"><span data-stu-id="95847-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="95847-138">在下一個步驟中，選取 SSL 憑證需要更新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="95847-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="95847-139">無法選取離線的伺服器進行更新。</span><span class="sxs-lookup"><span data-stu-id="95847-139">Servers that are offline can't be selected for the update.</span></span>

![選取要更新的伺服器](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="95847-141">組態完成之後，Azure AD Connect 會顯示訊息，指出更新的狀態，並且會提供一個選項來驗證 AD FS 登入。</span><span class="sxs-lookup"><span data-stu-id="95847-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![組態完成](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="95847-143">常見問題集</span><span class="sxs-lookup"><span data-stu-id="95847-143">FAQs</span></span>

* <span data-ttu-id="95847-144">**新 AD FS SSL 憑證之憑證的主體名稱應該是什麼？**</span><span class="sxs-lookup"><span data-stu-id="95847-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="95847-145">Azure AD Connect 會檢查憑證的主體名稱/替代主體名稱是否包含同盟服務名稱。</span><span class="sxs-lookup"><span data-stu-id="95847-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="95847-146">例如，如果同盟服務名稱為 fs.contoso.com，則主體名稱/替代主體名稱必須是 fs.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="95847-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="95847-147">也接受萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="95847-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="95847-148">**為什麼會要求我於 WAP 伺服器頁面上再次輸入認證？**</span><span class="sxs-lookup"><span data-stu-id="95847-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="95847-149">如果提供用於連線至 AD FS 伺服器的認證也不具備管理 WAP 伺服器的權限，Azure AD Connect 會要求提供在 WAP 伺服器上具有系統管理權限的認證。</span><span class="sxs-lookup"><span data-stu-id="95847-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="95847-150">**伺服器顯示為離線。我該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="95847-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="95847-151">如果伺服器已離線，Azure AD Connect 即無法執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="95847-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="95847-152">如果伺服器是 AD FS 伺服器陣列的一部分，請檢查伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="95847-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="95847-153">在解決問題之後，按下 [重新整理] 圖示，以更新精靈中的狀態。</span><span class="sxs-lookup"><span data-stu-id="95847-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="95847-154">如果伺服器稍早是伺服器陣列的一部分，但現在已不存在，請按一下 [移除]，以將它從 Azure AD Connect 維護的伺服器清單中刪除。</span><span class="sxs-lookup"><span data-stu-id="95847-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="95847-155">從 Azure AD Connect 的清單中移除伺服器並不會改變 AD FS 組態本身。</span><span class="sxs-lookup"><span data-stu-id="95847-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="95847-156">如果您在 Windows Server 2016 或更新版本中使用 AD FS，則伺服器會保持在組態設定，並且會在下一次執行工作再次顯示。</span><span class="sxs-lookup"><span data-stu-id="95847-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="95847-157">**可以使用新的 SSL 憑證更新我的伺服器陣列伺服器子集嗎？**</span><span class="sxs-lookup"><span data-stu-id="95847-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="95847-158">是。</span><span class="sxs-lookup"><span data-stu-id="95847-158">Yes.</span></span> <span data-ttu-id="95847-159">您永遠可以再次執行工作「更新 SSL 憑證」來更新其餘的伺服器。</span><span class="sxs-lookup"><span data-stu-id="95847-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="95847-160">在 [選取要進行 SSL 憑證更新的伺服器] 頁面上，您可以依「SSL 到期日」來排序伺服器清單，以便輕鬆地存取尚未更新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="95847-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="95847-161">**我在上一次執行中移除了伺服器，但它仍然顯示為離線，並且列在 [AD FS 伺服器] 頁面。為何即使在移除後，離線的伺服器還在？**</span><span class="sxs-lookup"><span data-stu-id="95847-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="95847-162">從 Azure AD Connect 的清單中移除伺服器並不會在 AD FS 組態中將它移除。</span><span class="sxs-lookup"><span data-stu-id="95847-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="95847-163">Azure AD Connect 會參考 AD FS (Windows Server 2016 或更新版本) 以取得伺服器陣列的任何相關資訊。</span><span class="sxs-lookup"><span data-stu-id="95847-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="95847-164">如果伺服器仍然出現在 AD FS 組態中，它會列回到清單中。</span><span class="sxs-lookup"><span data-stu-id="95847-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="95847-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="95847-165">Next steps</span></span>

- [<span data-ttu-id="95847-166">Azure AD Connect 和同盟</span><span class="sxs-lookup"><span data-stu-id="95847-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="95847-167">使用 Azure AD Connect 管理和自訂 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="95847-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
