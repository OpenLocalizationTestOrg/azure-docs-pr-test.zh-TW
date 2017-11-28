---
title: "Azure AD Connect： 更新 hello 的 Active Directory Federation Services (AD FS) 伺服陣列的 SSL 憑證 |Microsoft 文件"
description: "此文件詳細資料 hello 步驟 tooupdate hello SSL 憑證 AD FS 伺服器陣列使用 Azure AD Connect。"
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
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="fa4ce-104">更新 Active Directory Federation Services (AD FS) 伺服陣列的 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="fa4ce-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="fa4ce-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fa4ce-105">Overview</span></span>
<span data-ttu-id="fa4ce-106">本文說明如何使用 Azure AD Connect tooupdate hello SSL 憑證，以及在 Active Directory Federation Services (AD FS) 伺服陣列。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="fa4ce-107">即使 hello 使用者登入時選取方法並不是 AD FS，您可以使用 hello Azure AD Connect 工具 tooeasily 更新 hello SSL 憑證的 hello AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="fa4ce-108">您可以執行跨所有同盟和三個簡單步驟中的 Web 應用程式 Proxy (WAP) 伺服器更新 hello AD FS 伺服器陣列的 SSL 憑證的 hello 整個作業：</span><span class="sxs-lookup"><span data-stu-id="fa4ce-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![三個步驟](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="fa4ce-110">toolearn 進一步了解憑證所使用的 AD FS，請參閱[使用的 AD FS 的了解憑證](https://technet.microsoft.com/library/cc730660.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa4ce-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="fa4ce-111">Prerequisites</span></span>

* <span data-ttu-id="fa4ce-112">**AD FS 伺服器陣列**︰請確定您的 AD FS 伺服器陣列是 Windows Server 2012 R2 型或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="fa4ce-113">**Azure AD Connect**： 請確定該 hello Azure AD Connect 的版本是 1.1.443.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="fa4ce-114">您將使用 hello 工作**更新 AD FS SSL 憑證**。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![更新 SSL 工作](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="fa4ce-116">步驟 1︰提供 AD FS 伺服器陣列資訊</span><span class="sxs-lookup"><span data-stu-id="fa4ce-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="fa4ce-117">Azure AD Connect 會自動嘗試 tooobtain hello AD FS 伺服器陣列的資訊：</span><span class="sxs-lookup"><span data-stu-id="fa4ce-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="fa4ce-118">查詢 hello 伺服陣列資訊從 AD FS (Windows Server 2016 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="fa4ce-119">從儲存在本機使用 Azure AD Connect 中的上一個回合參考 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="fa4ce-120">您可以修改 hello 清單顯示透過加入或移除 hello 伺服器 tooreflect hello 目前組態 hello AD FS 伺服器陣列的伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="fa4ce-121">只要提供 hello 伺服器資訊，Azure AD Connect 會顯示 hello 連線和目前的 SSL 憑證狀態。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![AD FS 伺服器資訊](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="fa4ce-123">如果 hello 清單包含已不再 hello AD FS 伺服器陣列一部分的伺服器，按一下**移除**toodelete hello 伺服器從 AD FS 伺服器陣列中伺服器 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![清單中的離線伺服器](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="fa4ce-125">從 hello 清單移除伺服器的 AD FS 伺服器陣列在 Azure AD Connect 是本機作業，並更新 hello hello Azure AD Connect 會在本機維護的 AD FS 伺服器陣列的資訊。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="fa4ce-126">Azure AD Connect 無法修改 AD FS tooreflect hello 變更 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="fa4ce-127">步驟 2︰提供新的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="fa4ce-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="fa4ce-128">您已確認 AD FS 伺服器陣列伺服器的 hello 資訊之後，會要求 Azure AD Connect hello 新的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="fa4ce-129">提供的密碼保護 PFX 憑證 toocontinue hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![SSL 憑證](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="fa4ce-131">您提供 hello 憑證之後，Azure AD Connect 會經歷一系列的必要條件。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="fa4ce-132">請確認 hello hello 憑證的憑證 tooensure 是正確的 hello AD FS 伺服器陣列：</span><span class="sxs-lookup"><span data-stu-id="fa4ce-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="fa4ce-133">hello hello 憑證的主體名稱/替代主體名稱為相同 hello 與 hello federation service 名稱，或它是萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="fa4ce-134">超過 30 天，hello 憑證有效。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="fa4ce-135">hello 憑證信賴鏈結是有效的。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="fa4ce-136">hello 憑證有密碼保護。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="fa4ce-137">步驟 3： 選取 hello 更新伺服器</span><span class="sxs-lookup"><span data-stu-id="fa4ce-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="fa4ce-138">在 hello 下一個步驟中，選取需要更新 toohave hello SSL 憑證的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="fa4ce-139">無法針對 hello 更新選取離線的伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-139">Servers that are offline can't be selected for hello update.</span></span>

![選取伺服器 tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="fa4ce-141">您完成 hello 組態之後，Azure AD Connect 會顯示 hello 訊息，指出 hello hello 更新狀態，並提供選項 tooverify hello AD FS 登入。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![組態完成](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="fa4ce-143">常見問題集</span><span class="sxs-lookup"><span data-stu-id="fa4ce-143">FAQs</span></span>

* <span data-ttu-id="fa4ce-144">**應有 hello 憑證主體名稱 hello hello 新的 AD FS SSL 憑證？**</span><span class="sxs-lookup"><span data-stu-id="fa4ce-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="fa4ce-145">Azure AD Connect 檢查 hello 憑證 hello 主旨名稱/替代主體名稱是否包含 hello federation service 名稱。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="fa4ce-146">例如，如果您的同盟服務名稱為 fs.contoso.com，hello 主旨名稱/替代主體名稱必須是 fs.contoso.com。也接受萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="fa4ce-147">**為什麼詢問認證再次 hello WAP 伺服器 頁面上？**</span><span class="sxs-lookup"><span data-stu-id="fa4ce-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="fa4ce-148">如果您提供 tooAD FS 伺服器的連線的 hello 認證也沒有 hello 權限 toomanage hello WAP 伺服器，Azure AD Connect 會要求在 hello WAP 伺服器上擁有系統管理權限的認證。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="fa4ce-149">**hello 伺服器顯示為離線。我該怎麼辦？**</span><span class="sxs-lookup"><span data-stu-id="fa4ce-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="fa4ce-150">如果 hello 伺服器處於離線狀態，azure AD Connect 無法執行任何作業。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="fa4ce-151">如果 hello 伺服器是 hello AD FS 伺服器陣列的一部分，請檢查 hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="fa4ce-152">在解決 hello 問題之後，按 hello 精靈 hello 重新整理圖示 tooupdate hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="fa4ce-153">如果 hello 伺服器是一部分的 hello 伺服器陣列之前，但現在不再存在，請按一下**移除**toodelete 它從 Azure AD Connect 的伺服器 hello 清單會保留。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="fa4ce-154">從 Azure AD Connect 中的 hello 清單移除 hello 伺服器不會改變 hello 本身的 AD FS 設定。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="fa4ce-155">如果您使用 AD FS 在 Windows Server 2016 或更新版本，hello 伺服器仍會留在 hello 組態設定，並會顯示一次 hello 下次 hello 工作會執行。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="fa4ce-156">**可以更新我的伺服器陣列伺服器子集 hello 新的 SSL 憑證嗎？**</span><span class="sxs-lookup"><span data-stu-id="fa4ce-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="fa4ce-157">是。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-157">Yes.</span></span> <span data-ttu-id="fa4ce-158">您可以固定執行 hello 工作**更新 SSL 憑證**再次 tooupdate hello，剩餘的伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="fa4ce-159">在 hello**選取的伺服器 ssl 憑證更新** 頁面上，您可以依據伺服器 hello 清單**SSL 到期日**不尚未更新的 tooeasily hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="fa4ce-160">**我移除 hello 伺服器 hello 先前中的執行，但它仍然正在顯示為離線，列出您在 hello AD FS 伺服器 頁面。我已經將它移除，即使為何仍有 hello 離線的伺服器？**</span><span class="sxs-lookup"><span data-stu-id="fa4ce-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="fa4ce-161">從 Azure AD Connect 中的 hello 清單移除 hello 伺服器並不會移除它在 hello AD FS 設定。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="fa4ce-162">Azure AD Connect 參考任何資訊 hello 伺服陣列的 AD 的 FS (Windows Server 2016 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="fa4ce-163">如果 hello 伺服器仍會出現在 hello AD FS 設定時，將列出在 [hello] 清單。</span><span class="sxs-lookup"><span data-stu-id="fa4ce-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="fa4ce-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa4ce-164">Next steps</span></span>

- [<span data-ttu-id="fa4ce-165">Azure AD Connect 和同盟</span><span class="sxs-lookup"><span data-stu-id="fa4ce-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="fa4ce-166">使用 Azure AD Connect 管理和自訂 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="fa4ce-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
