---
title: "使用 Azure AD Connect 管理和自訂 Active Directory Federation Services | Microsoft Docs"
description: "使用 Azure AD Connect 進行 AD FS 管理，以及使用 Azure AD Connect 和 PowerShell 的使用者 AD FS 登入經驗的自訂。"
keywords: "AD FS, ADFS, AD FS 管理, AAD Connect, 連線, 登入, AD FS 自訂, 修復信任, O365, 同盟, 信賴憑證者"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="21790-104">使用 Azure AD Connect 管理和自訂 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="21790-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="21790-105">本文說明如何使用 Azure Active Directory (Azure AD) Connect 管理及自訂 Active Directory Federation Services (AD FS)。</span><span class="sxs-lookup"><span data-stu-id="21790-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="21790-106">它也包含您可能需要進行以完整設定 AD FS 伺服器陣列的其他常見 AD FS 工作。</span><span class="sxs-lookup"><span data-stu-id="21790-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="21790-107">主題</span><span class="sxs-lookup"><span data-stu-id="21790-107">Topic</span></span> | <span data-ttu-id="21790-108">涵蓋內容</span><span class="sxs-lookup"><span data-stu-id="21790-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="21790-109">**管理 AD FS**</span><span class="sxs-lookup"><span data-stu-id="21790-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="21790-110">修復信任</span><span class="sxs-lookup"><span data-stu-id="21790-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="21790-111">如何修復與 Office 365 的同盟信任。</span><span class="sxs-lookup"><span data-stu-id="21790-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="21790-112">使用替代登入識別碼與 Azure AD 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="21790-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="21790-113">使用替代登入識別碼設定同盟</span><span class="sxs-lookup"><span data-stu-id="21790-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="21790-114">新增 AD FS 伺服器</span><span class="sxs-lookup"><span data-stu-id="21790-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="21790-115">如何使用額外的 AD FS 伺服器擴充 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="21790-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="21790-116">新增 AD FS Web 應用程式 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="21790-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="21790-117">如何使用其他 Web 應用程式 Proxy (WAP) 伺服器展開 AD FS 陣列。</span><span class="sxs-lookup"><span data-stu-id="21790-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="21790-118">新增同盟網域</span><span class="sxs-lookup"><span data-stu-id="21790-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="21790-119">如何新增同盟網域。</span><span class="sxs-lookup"><span data-stu-id="21790-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="21790-120">更新 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="21790-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="21790-121">如何更新 AD FS 伺服器陣列的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="21790-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="21790-122">**自訂 AD FS**</span><span class="sxs-lookup"><span data-stu-id="21790-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="21790-123">新增自訂公司標誌或圖例</span><span class="sxs-lookup"><span data-stu-id="21790-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="21790-124">如何使用公司標誌與圖例自訂 AD FS 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="21790-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="21790-125">新增登入說明</span><span class="sxs-lookup"><span data-stu-id="21790-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="21790-126">如何新增登入頁面說明。</span><span class="sxs-lookup"><span data-stu-id="21790-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="21790-127">修改 AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="21790-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="21790-128">如何修改各種同盟案例的 AD FS 宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="21790-129">管理 AD FS</span><span class="sxs-lookup"><span data-stu-id="21790-129">Manage AD FS</span></span>
<span data-ttu-id="21790-130">您可以使用 Azure AD Connect 精靈，以最少使用者介入的形式執行各種 AD FS 相關工作。</span><span class="sxs-lookup"><span data-stu-id="21790-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="21790-131">執行精靈來完成安裝 Azure AD Connect 之後，您可以再次執行精靈，以執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="21790-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="21790-132">修復信任 <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="21790-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="21790-133">您可以使用 Azure AD Connect 檢查 AD FS 和 Azure AD trust 目前的健全狀況，並採取適當的動作來修復信任。</span><span class="sxs-lookup"><span data-stu-id="21790-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="21790-134">請遵循下列步驟來修復您的 Azure AD 和 AD FS 信任。</span><span class="sxs-lookup"><span data-stu-id="21790-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="21790-135">從其他工作的清單中選取 [修復 AAD 和 ADFS 信任]  。</span><span class="sxs-lookup"><span data-stu-id="21790-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="21790-136">![](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="21790-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="21790-137">在 [連線到 Azure AD] 頁面上，提供 Azure AD 的全域系統管理員認證，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="21790-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="21790-138">![連接至 Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="21790-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="21790-139">在 [遠端存取認證]  頁面上，輸入網域系統管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="21790-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="21790-141">在按 [下一步] 之後，Azure AD Connect 會檢查憑證健康情況並顯示任何問題。</span><span class="sxs-lookup"><span data-stu-id="21790-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![憑證的狀態](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="21790-143">[準備設定] 頁面會顯示為了修復信任，將執行的動作清單。</span><span class="sxs-lookup"><span data-stu-id="21790-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![準備設定](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="21790-145">按一下 [安裝]  以修復信任。</span><span class="sxs-lookup"><span data-stu-id="21790-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="21790-146">Azure AD Connect 只可以對自我簽署的憑證進行修復或採取動作。</span><span class="sxs-lookup"><span data-stu-id="21790-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="21790-147">Azure AD Connect 無法修復第三方憑證。</span><span class="sxs-lookup"><span data-stu-id="21790-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="21790-148">使用替代識別碼與 Azure AD 建立同盟關係<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="21790-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="21790-149">建議您讓內部部署使用者主體名稱 (UPN) 和雲端使用者主體名稱保持相同。</span><span class="sxs-lookup"><span data-stu-id="21790-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="21790-150">如果內部部署 UPN 使用無法路由傳送的網域 (例如︰</span><span class="sxs-lookup"><span data-stu-id="21790-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="21790-151">Contoso.local)，或是由於本機應用程式相依性而無法變更，我們會建議您設定替代登入識別碼。</span><span class="sxs-lookup"><span data-stu-id="21790-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="21790-152">替代登入識別碼可讓您設定登入體驗，讓使用者可以透過其 UPN 以外的屬性 (例如 mail) 來進行登入。</span><span class="sxs-lookup"><span data-stu-id="21790-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="21790-153">Azure AD Connect 預設會選擇 Active Directory 中的 userPrincipalName 屬性來作為使用者主體名稱。</span><span class="sxs-lookup"><span data-stu-id="21790-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="21790-154">如果您選擇任何其他屬性來作為使用者主體名稱，而且您使用 AD FS 來建立同盟，則 Azure AD Connect 會就替代登入識別碼對 AD FS 進行設定。</span><span class="sxs-lookup"><span data-stu-id="21790-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="21790-155">選擇不同屬性來作為使用者主體名稱的範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="21790-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![替代識別碼屬性的選擇](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="21790-157">AD FS 替代登入識別碼的設定作業包含兩個主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="21790-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="21790-158">**設定正確的發行宣告集**︰Azure AD 信賴憑證者信任中的發行宣告規則，會修改為使用選取的 UserPrincipalName 屬性來作為使用者的替代識別碼。</span><span class="sxs-lookup"><span data-stu-id="21790-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="21790-159">**在 AD FS 設定中啟用替代登入識別碼**︰AD FS 設定會進行更新，讓 AD FS 可以使用替代識別碼在適當樹系中查詢使用者。</span><span class="sxs-lookup"><span data-stu-id="21790-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="21790-160">此設定支援 Windows Server 2012 R2 (含 KB2919355) 或更新版本上的 AD FS。</span><span class="sxs-lookup"><span data-stu-id="21790-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="21790-161">如果 AD FS 伺服器是 2012 R2，Azure AD Connect 會檢查是否有必要的 KB 存在。</span><span class="sxs-lookup"><span data-stu-id="21790-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="21790-162">如果未偵測到必要 KB，則系統會在設定完成之後顯示警告，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="21790-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![2012 R2 上缺少 KB 的警告](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="21790-164">若要在缺少 KB 時修正設定，請安裝必要的 [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590)，然後使用[修復 AAD 與 AD FS 信任](#repairthetrust)來修復信任。</span><span class="sxs-lookup"><span data-stu-id="21790-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="21790-165">如需替代識別碼以及手動設定步驟的詳細資訊，請閱讀[設定替代登入識別碼](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="21790-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="21790-166">新增 AD FS 伺服器 <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="21790-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="21790-167">若要新增 AD FS 伺服器，Azure AD Connect 需要 PFX 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="21790-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="21790-168">因此，只有當您使用 Azure AD Connect 來設定 AD FS 伺服器陣列時，才可以執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="21790-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="21790-169">選取 [部署其他同盟伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="21790-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![其他同盟伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="21790-171">在 [連線到 Azure AD] 頁面上，輸入 Azure AD 的全域系統管理員認證，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="21790-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![連接至 Azure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="21790-173">提供網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="21790-173">Provide the domain administrator credentials.</span></span>

   ![網域系統管理員認證](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="21790-175">Azure AD Connect 會要求您提供您在使用 Azure AD Connect 設定您的新 AD FS 伺服器陣列時所提供的 PFX 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="21790-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="21790-176">按一下 [輸入密碼]  以提供 PFX 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="21790-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![憑證密碼](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="21790-179">在 [AD FS 伺服器]  頁面上，輸入要新增到 AD FS 伺服器陣列的伺服器名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="21790-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![AD FS 伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="21790-181">按 [下一步]，並逐步進行到最終的 [設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="21790-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="21790-182">Azure AD Connect 完成將伺服器新增至 AD FS 伺服器陣列之後，將提供您選項來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="21790-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![準備設定](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![安裝完成](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="21790-185">新增 AD FS WAP 伺服器 <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="21790-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="21790-186">若要新增 WAP 伺服器，Azure AD Connect 需要 PFX 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="21790-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="21790-187">因此，只有當您使用 Azure AD Connect 來設定 AD FS 伺服器陣列時，才可以執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="21790-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="21790-188">從可用的工作清單中選取 [部署 Web 應用程式 Proxy]  。</span><span class="sxs-lookup"><span data-stu-id="21790-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![部署 Web 應用程式 Proxy](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="21790-190">提供 Azure 全域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="21790-190">Provide the Azure global administrator credentials.</span></span>

   ![連接至 Azure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="21790-192">在 [指定 SSL 憑證] 頁面上，提供您在使用 Azure AD Connect 設定 AD FS 伺服器陣列時所提供之 PFX 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="21790-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="21790-193">![憑證密碼](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="21790-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="21790-195">新增要做為 WAP 伺服器的伺服器。</span><span class="sxs-lookup"><span data-stu-id="21790-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="21790-196">因為 WAP 伺服器可能不會加入網域，精靈會要求要新增之伺服器的系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="21790-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![管理伺服器認證](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="21790-198">在 [Proxy 信任憑證]  頁面上，提供系統管理認證，以設定 Proxy 信任和存取 AD FS 伺服器陣列中的主要伺服器。</span><span class="sxs-lookup"><span data-stu-id="21790-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Proxy 信任憑證](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="21790-200">在 [準備設定]  頁面上，精靈會顯示將執行的動作清單。</span><span class="sxs-lookup"><span data-stu-id="21790-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![準備設定](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="21790-202">按一下 [安裝]  以完成組態。</span><span class="sxs-lookup"><span data-stu-id="21790-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="21790-203">組態完成之後，精靈會提供您選項，來驗證與伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="21790-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="21790-204">按一下 [驗證]  來檢查連線能力。</span><span class="sxs-lookup"><span data-stu-id="21790-204">Click **Verify** to check connectivity.</span></span>

   ![安裝完成](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="21790-206">新增同盟網域 <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="21790-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="21790-207">您可以使用 Azure AD Connect 輕鬆地新增要與 Azure AD 同盟的網域。</span><span class="sxs-lookup"><span data-stu-id="21790-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="21790-208">Azure AD Connect 會新增同盟的網域並修改宣告規則，以在您有與 Azure AD 同盟的多個網域時正確反映發行者。</span><span class="sxs-lookup"><span data-stu-id="21790-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="21790-209">若要新增同盟網域，請選取工作 [新增其他 Azure AD 網域] 。</span><span class="sxs-lookup"><span data-stu-id="21790-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![其他 Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="21790-211">在精靈的下一個頁面上，提供 Azure AD 全域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="21790-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![連接至 Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="21790-213">在 [遠端存取認證]  頁面上，提供網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="21790-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="21790-215">在下一個頁面上，精靈會提供 Azure AD 網域的清單，以供您用來同盟您的內部部署目錄。</span><span class="sxs-lookup"><span data-stu-id="21790-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="21790-216">從清單選擇網域。</span><span class="sxs-lookup"><span data-stu-id="21790-216">Choose the domain from the list.</span></span>

   ![Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="21790-218">選擇網域之後，精靈會提供您關於精靈將採取的進一步動作和組態影響的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="21790-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="21790-219">在某些情況下，如果您選取尚未在 Azure AD 中驗證的網域，精靈將提供資訊協助您驗證網域。</span><span class="sxs-lookup"><span data-stu-id="21790-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="21790-220">如需詳細資訊，請參閱 [將您的自訂網域名稱新增至 Azure Active Directory](../active-directory-add-domain.md) 。</span><span class="sxs-lookup"><span data-stu-id="21790-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="21790-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="21790-221">Click **Next**.</span></span> <span data-ttu-id="21790-222">按 [下一步]，然後 [準備設定] 頁面就會顯示 Azure AD Connect 將會執行的動作清單。</span><span class="sxs-lookup"><span data-stu-id="21790-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="21790-223">按一下 [安裝]  以完成組態。</span><span class="sxs-lookup"><span data-stu-id="21790-223">Click **Install** to finish the configuration.</span></span>

   ![準備設定](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="21790-225">所新增同盟網域的使用者必須保持同步，才能夠登入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="21790-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="21790-226">AD FS 自訂</span><span class="sxs-lookup"><span data-stu-id="21790-226">AD FS customization</span></span>
<span data-ttu-id="21790-227">下列各節提供在自訂 AD FS 登入頁面時，可能必須執行之某些常見工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="21790-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="21790-228">新增自訂公司標誌或圖例 <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="21790-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="21790-229">若要變更 [登入] 頁面上顯示的公司標誌，請使用下列 Windows PowerShell Cmdlet 和語法。</span><span class="sxs-lookup"><span data-stu-id="21790-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="21790-230">建議的標誌尺寸為 260 x 35 @ 96 dpi，檔案大小不超過 10 KB。</span><span class="sxs-lookup"><span data-stu-id="21790-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="21790-231">*TargetName* 是必要參數。</span><span class="sxs-lookup"><span data-stu-id="21790-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="21790-232">隨著 AD FS 釋出的預設佈景主題為指定的預設值。</span><span class="sxs-lookup"><span data-stu-id="21790-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="21790-233">新增登入說明 <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="21790-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="21790-234">若要在 [登入] 頁面中新增登入頁面描述，請使用下列 Windows PowerShell Cmdlet 和語法。</span><span class="sxs-lookup"><span data-stu-id="21790-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="21790-235">修改 AD FS 宣告規則 <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="21790-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="21790-236">AD FS 支援豐富的宣告語言，您可以用它來建立自訂宣告規則。</span><span class="sxs-lookup"><span data-stu-id="21790-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="21790-237">如需詳細資訊，請參閱 [宣告規則語言的角色](https://technet.microsoft.com/library/dd807118.aspx)。</span><span class="sxs-lookup"><span data-stu-id="21790-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="21790-238">下列各節說明如何為關於 Azure AD 和 AD FS 同盟的一些案例撰寫自訂規則。</span><span class="sxs-lookup"><span data-stu-id="21790-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="21790-239">屬性中的值出現固定 ID 條件</span><span class="sxs-lookup"><span data-stu-id="21790-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="21790-240">Azure AD Connect 可在將物件同步處理至 Azure AD 時，讓您指定要做為來源錨點的屬性。</span><span class="sxs-lookup"><span data-stu-id="21790-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="21790-241">如果自訂屬性中的值未空白，您可能會想要發出固定 ID 宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="21790-242">例如，您可能會選取 **ms-ds-consistencyguid** 做為來源錨點的屬性，並且在該屬性具有值時發出 **ImmutableID** 做為 **ms-ds-consistencyguid**。</span><span class="sxs-lookup"><span data-stu-id="21790-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="21790-243">如果沒有該屬性的值，則發出 **objectGuid** 做為固定 ID。</span><span class="sxs-lookup"><span data-stu-id="21790-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="21790-244">您可以如下一節所述建構自訂宣告規則的集合。</span><span class="sxs-lookup"><span data-stu-id="21790-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="21790-245">**規則 1：查詢屬性**</span><span class="sxs-lookup"><span data-stu-id="21790-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="21790-246">在此規則中，您會從 Active Directory 查詢使用者的 **ms-ds-consistencyguid** 和 **objectGuid** 值。</span><span class="sxs-lookup"><span data-stu-id="21790-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="21790-247">在 AD FS 部署中，將存放區名稱變更為適當的存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="21790-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="21790-248">另外，也將依照針對 **objectGuid** 和 **ms-ds-consistencyguid** 所定義的，將宣告類型變更為您的同盟適用的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="21790-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="21790-249">此外，使用**新增**而非**發出**，您可以避免為實體新增傳出發出，而可以使用這些值做為中間值。</span><span class="sxs-lookup"><span data-stu-id="21790-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="21790-250">在您建立要做為固定 ID 的值之後，您將在後續的規則中發出宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="21790-251">**規則 2：檢查使用者是否存在 ms-ds-consistencyguid**</span><span class="sxs-lookup"><span data-stu-id="21790-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="21790-252">此規則會定義稱為 **idflag** 的暫時旗標，如果沒有為使用者填入 **ms-ds-concistencyguid**，則此旗標會設為 **useguid**。</span><span class="sxs-lookup"><span data-stu-id="21790-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="21790-253">背後邏輯是實際上 AD FS 不允許空的宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="21790-254">所以，在規則 1 中新增宣告 http://contoso.com/ws/2016/02/identity/claims/objectguid 和 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid 時，只有在已為使用者填入該值時，您才會得到 **msdsconsistencyguid** 宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="21790-255">如果未填入，AD FS 會看到它將具有空值，並因此立即捨棄。</span><span class="sxs-lookup"><span data-stu-id="21790-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="21790-256">所有物件都會有 **objectGuid**，因此執行規則 1 之後，宣告一律會在該處。</span><span class="sxs-lookup"><span data-stu-id="21790-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="21790-257">**規則 3：發出 ms-ds-consistencyguid 為固定 ID (如果有的話)**</span><span class="sxs-lookup"><span data-stu-id="21790-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="21790-258">這是隱含的 **存在** 檢查。</span><span class="sxs-lookup"><span data-stu-id="21790-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="21790-259">如果宣告的值存在，則發出做為固定 ID。</span><span class="sxs-lookup"><span data-stu-id="21790-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="21790-260">上述範例使用 **nameidentifier** 宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="21790-261">您必須為您的環境中的固定 ID 將此宣告變更為適當的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="21790-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="21790-262">**規則 4：發出 objectGuid 做為固定 ID，如果未出現 ms-ds-consistencyGuid**</span><span class="sxs-lookup"><span data-stu-id="21790-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="21790-263">在這項規則中，您只會檢查暫存旗標 **idflag**。</span><span class="sxs-lookup"><span data-stu-id="21790-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="21790-264">您必須根據宣告值來決定是否要發出宣告。</span><span class="sxs-lookup"><span data-stu-id="21790-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="21790-265">這些規則的順序很重要。</span><span class="sxs-lookup"><span data-stu-id="21790-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="21790-266">使用子網域 UPN 的 SSO</span><span class="sxs-lookup"><span data-stu-id="21790-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="21790-267">您可以使用 Azure AD Connect 新增多個要同盟的網域，如 [新增新的同盟網域](active-directory-aadconnect-federation-management.md#addfeddomain)所述。</span><span class="sxs-lookup"><span data-stu-id="21790-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="21790-268">您必須修改使用者主要名稱 (UPN) 宣告，讓簽發者識別碼對應至根網域，而不是子網域，因為同盟根網域也涵蓋子系。</span><span class="sxs-lookup"><span data-stu-id="21790-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="21790-269">根據預設，簽發者識別碼的宣告規則會設定為︰</span><span class="sxs-lookup"><span data-stu-id="21790-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![預設簽發者識別碼宣告](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="21790-271">預設規則只是取得 UPN 尾碼，並用在簽發者識別碼宣告中。</span><span class="sxs-lookup"><span data-stu-id="21790-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="21790-272">比方說，John 是 sub.contoso.com 中的使用者，而 contoso.com 與 Azure AD 同盟。</span><span class="sxs-lookup"><span data-stu-id="21790-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="21790-273">John 在登入 Azure AD 時輸入 john@sub.contoso.com 做為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="21790-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="21790-274">AD FS 中的預設簽發者識別碼宣告規則依下列方法處理︰</span><span class="sxs-lookup"><span data-stu-id="21790-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="21790-275">**宣告值：**http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="21790-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="21790-276">為了讓簽發者宣告值中只有根網域，請變更宣告規則以符合下列內容︰</span><span class="sxs-lookup"><span data-stu-id="21790-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="21790-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21790-277">Next steps</span></span>
<span data-ttu-id="21790-278">深入了解 [使用者登入選項](active-directory-aadconnect-user-signin.md)。</span><span class="sxs-lookup"><span data-stu-id="21790-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
