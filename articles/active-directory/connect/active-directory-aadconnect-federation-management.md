---
title: "aaaActive Directory Federation Services 管理和使用 Azure AD Connect 自訂 |Microsoft 文件"
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
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="afd99-104">使用 Azure AD Connect 管理和自訂 Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="afd99-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="afd99-105">本文說明如何 toomanage 和自訂 Active Directory Federation Services (AD FS)，藉由使用 Azure Active Directory (Azure AD) 連線。</span><span class="sxs-lookup"><span data-stu-id="afd99-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="afd99-106">它也包含其他常見的 AD FS 工作，您可能需要 toodo 完成 AD FS 伺服器陣列組態。</span><span class="sxs-lookup"><span data-stu-id="afd99-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="afd99-107">主題</span><span class="sxs-lookup"><span data-stu-id="afd99-107">Topic</span></span> | <span data-ttu-id="afd99-108">涵蓋內容</span><span class="sxs-lookup"><span data-stu-id="afd99-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="afd99-109">**管理 AD FS**</span><span class="sxs-lookup"><span data-stu-id="afd99-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="afd99-110">修復 hello 信任</span><span class="sxs-lookup"><span data-stu-id="afd99-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="afd99-111">如何 toorepair hello 同盟信任與 Office 365。</span><span class="sxs-lookup"><span data-stu-id="afd99-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="afd99-112">使用替代登入識別碼與 Azure AD 建立同盟關係</span><span class="sxs-lookup"><span data-stu-id="afd99-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="afd99-113">使用替代登入識別碼設定同盟</span><span class="sxs-lookup"><span data-stu-id="afd99-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="afd99-114">新增 AD FS 伺服器</span><span class="sxs-lookup"><span data-stu-id="afd99-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="afd99-115">如何 tooexpand AD FS 伺服器與其他的 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="afd99-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="afd99-116">新增 AD FS Web 應用程式 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="afd99-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="afd99-117">如何 tooexpand AD FS 伺服器陣列與其他 Web 應用程式 Proxy (WAP) 伺服器。</span><span class="sxs-lookup"><span data-stu-id="afd99-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="afd99-118">新增同盟網域</span><span class="sxs-lookup"><span data-stu-id="afd99-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="afd99-119">如何 tooadd 同盟網域。</span><span class="sxs-lookup"><span data-stu-id="afd99-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="afd99-120">Hello SSL 憑證更新</span><span class="sxs-lookup"><span data-stu-id="afd99-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="afd99-121">如何 tooupdate hello SSL 憑證的 AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="afd99-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="afd99-122">**自訂 AD FS**</span><span class="sxs-lookup"><span data-stu-id="afd99-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="afd99-123">新增自訂公司標誌或圖例</span><span class="sxs-lookup"><span data-stu-id="afd99-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="afd99-124">如何 toocustomize AD FS 登入頁面上的公司標誌與插圖。</span><span class="sxs-lookup"><span data-stu-id="afd99-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="afd99-125">新增登入說明</span><span class="sxs-lookup"><span data-stu-id="afd99-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="afd99-126">如何 tooadd 登入頁面描述。</span><span class="sxs-lookup"><span data-stu-id="afd99-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="afd99-127">修改 AD FS 宣告規則</span><span class="sxs-lookup"><span data-stu-id="afd99-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="afd99-128">如何 toomodify AD FS 宣告各種同盟案例。</span><span class="sxs-lookup"><span data-stu-id="afd99-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="afd99-129">管理 AD FS</span><span class="sxs-lookup"><span data-stu-id="afd99-129">Manage AD FS</span></span>
<span data-ttu-id="afd99-130">您可以使用 hello Azure AD Connect 精靈，而需要最少使用者介入的 Azure AD Connect 中執行各種不同的 AD FS 相關工作。</span><span class="sxs-lookup"><span data-stu-id="afd99-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="afd99-131">安裝 Azure AD Connect 執行 hello 精靈完成之後，您可以執行 hello 精靈一次 tooperform 其他工作。</span><span class="sxs-lookup"><span data-stu-id="afd99-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="afd99-132">修復 hello 信任<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="afd99-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="afd99-133">您可以使用 Azure AD Connect toocheck hello 的目前健全狀況 hello AD FS 與 Azure AD 信任，並採取適當動作 toorepair hello 信任。</span><span class="sxs-lookup"><span data-stu-id="afd99-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="afd99-134">請遵循這些步驟 toorepair 您的 Azure AD 與 AD FS 信任。</span><span class="sxs-lookup"><span data-stu-id="afd99-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="afd99-135">選取**修復 AAD 與 ADFS 信任**hello 清單中的其他工作。</span><span class="sxs-lookup"><span data-stu-id="afd99-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="afd99-136">![](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="afd99-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="afd99-137">在 hello**連接 tooAzure AD**頁面上，提供 Azure AD 全域管理員認證，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="afd99-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="afd99-138">![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="afd99-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="afd99-139">在 hello**遠端存取認證**頁面上，輸入 hello 認證 hello 網域系統管理員。</span><span class="sxs-lookup"><span data-stu-id="afd99-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="afd99-141">在按 [下一步] 之後，Azure AD Connect 會檢查憑證健康情況並顯示任何問題。</span><span class="sxs-lookup"><span data-stu-id="afd99-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![憑證的狀態](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="afd99-143">hello**準備 tooconfigure**頁面顯示 hello 的動作清單將會執行 toorepair hello 信任。</span><span class="sxs-lookup"><span data-stu-id="afd99-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="afd99-145">按一下**安裝**toorepair hello 信任。</span><span class="sxs-lookup"><span data-stu-id="afd99-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="afd99-146">Azure AD Connect 只可以對自我簽署的憑證進行修復或採取動作。</span><span class="sxs-lookup"><span data-stu-id="afd99-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="afd99-147">Azure AD Connect 無法修復第三方憑證。</span><span class="sxs-lookup"><span data-stu-id="afd99-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="afd99-148">使用替代識別碼與 Azure AD 建立同盟關係<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="afd99-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="afd99-149">建議的 hello 內部部署使用者主體 Name(UPN) 和 hello 雲端使用者主體名稱會保留 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="afd99-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="afd99-150">如果 hello 內部部署 UPN 會使用非路由傳送的網域 （例如。</span><span class="sxs-lookup"><span data-stu-id="afd99-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="afd99-151">Contoso.local) 無法變更或到期 toolocal 應用程式相依性，我們建議您設定替代的登入識別碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="afd99-152">替代的登入識別碼，可讓您 tooconfigure 登入體驗，使用者可以使用登入其 UPN，例如 mail 以外的屬性。</span><span class="sxs-lookup"><span data-stu-id="afd99-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="afd99-153">hello 選項使用者主體名稱在 Azure AD Connect 的預設值 toohello Active Directory 中的 userPrincipalName 屬性。</span><span class="sxs-lookup"><span data-stu-id="afd99-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="afd99-154">如果您選擇任何其他屬性來作為使用者主體名稱，而且您使用 AD FS 來建立同盟，則 Azure AD Connect 會就替代登入識別碼對 AD FS 進行設定。</span><span class="sxs-lookup"><span data-stu-id="afd99-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="afd99-155">選擇不同屬性來作為使用者主體名稱的範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="afd99-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![替代識別碼屬性的選擇](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="afd99-157">AD FS 替代登入識別碼的設定作業包含兩個主要步驟︰</span><span class="sxs-lookup"><span data-stu-id="afd99-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="afd99-158">**設定 hello 正確的發行宣告集**: hello 發行宣告規則，在 hello Azure AD 信賴憑證者的合作對象信任是修改的 toouse hello 選取 UserPrincipalName 屬性，如 hello 替代 hello 使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="afd99-159">**啟用 hello AD FS 組態中的替代登入識別碼**: hello AD FS 設定會更新，讓 AD FS 可以查閱 hello 替代識別碼 hello 適當樹系中的使用者</span><span class="sxs-lookup"><span data-stu-id="afd99-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="afd99-160">此設定支援 Windows Server 2012 R2 (含 KB2919355) 或更新版本上的 AD FS。</span><span class="sxs-lookup"><span data-stu-id="afd99-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="afd99-161">如果 hello AD FS 伺服器 2012 R2，hello hello 存在的 Azure AD Connect 檢查需要 KB。</span><span class="sxs-lookup"><span data-stu-id="afd99-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="afd99-162">如果 hello 無法偵測 KB，將會顯示警告之後完成組態，如下所示：</span><span class="sxs-lookup"><span data-stu-id="afd99-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![2012 R2 上缺少 KB 的警告](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="afd99-164">發生遺漏 KB，toorectify hello 組態安裝所需的 hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) ，然後修復 hello 信任使用[修復 AAD 與 AD FS 信任](#repairthetrust)。</span><span class="sxs-lookup"><span data-stu-id="afd99-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="afd99-165">如需有關 alternateID 和步驟 toomanually 設定，請閱讀[設定替代的登入識別碼](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="afd99-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="afd99-166">新增 AD FS 伺服器 <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="afd99-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="afd99-167">tooadd AD FS 伺服器，Azure AD Connect 需要 hello PFX 憑證。</span><span class="sxs-lookup"><span data-stu-id="afd99-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="afd99-168">因此，您可以執行這項作業，只有當您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列中。</span><span class="sxs-lookup"><span data-stu-id="afd99-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="afd99-169">選取 [部署其他同盟伺服器]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="afd99-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![其他同盟伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="afd99-171">在 hello**連接 tooAzure AD**頁面上，輸入 Azure AD 全域管理員認證，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="afd99-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="afd99-173">提供 hello 網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="afd99-173">Provide hello domain administrator credentials.</span></span>

   ![網域系統管理員認證](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="afd99-175">Azure AD Connect 會要求您使用 Azure AD Connect 設定新的 AD FS 伺服器陣列時所提供的 hello PFX 檔案的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="afd99-176">按一下**輸入密碼**tooprovide hello hello PFX 檔案密碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![憑證密碼](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="afd99-179">在 hello **AD FS 伺服器**頁面上，輸入 hello 伺服器名稱或 IP 位址 toobe 加入 toohello AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="afd99-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![AD FS 伺服器](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="afd99-181">按一下**下一步**，並瀏覽 hello 最終**設定**頁面。</span><span class="sxs-lookup"><span data-stu-id="afd99-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="afd99-182">Azure AD Connect 已完成將加入 hello 伺服器 toohello AD FS 伺服器陣列之後，您會獲得 hello 選項 tooverify hello 連線。</span><span class="sxs-lookup"><span data-stu-id="afd99-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![安裝完成](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="afd99-185">新增 AD FS WAP 伺服器 <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="afd99-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="afd99-186">tooadd WAP 伺服器，Azure AD Connect 需要 hello PFX 憑證。</span><span class="sxs-lookup"><span data-stu-id="afd99-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="afd99-187">因此，您只可以執行這項作業，如果您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="afd99-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="afd99-188">選取**部署 Web 應用程式 Proxy**從 hello 可用工作的清單。</span><span class="sxs-lookup"><span data-stu-id="afd99-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![部署 Web 應用程式 Proxy](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="afd99-190">提供 hello Azure 全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="afd99-190">Provide hello Azure global administrator credentials.</span></span>

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="afd99-192">在 hello**指定 SSL 憑證**頁面上，您使用 Azure AD Connect 設定 hello AD FS 伺服器陣列時所提供的 hello PFX 檔案提供 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="afd99-193">![憑證密碼](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="afd99-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![指定 SSL 憑證](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="afd99-195">新增 hello 伺服器 toobe 加入做為 WAP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="afd99-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="afd99-196">Hello WAP 伺服器可能不是聯結的 toohello 網域，因為 hello 精靈即會詢問要新增的系統管理認證 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="afd99-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![管理伺服器認證](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="afd99-198">在 hello **Proxy 信任認證**頁面上，提供系統管理認證 tooconfigure hello proxy 信任及存取 hello 主要伺服器 hello AD FS 伺服器陣列中的。</span><span class="sxs-lookup"><span data-stu-id="afd99-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Proxy 信任憑證](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="afd99-200">在 [hello**準備 tooconfigure** ] 頁面上，hello 精靈會顯示 hello 將執行的動作清單。</span><span class="sxs-lookup"><span data-stu-id="afd99-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="afd99-202">按一下**安裝**toofinish hello 組態。</span><span class="sxs-lookup"><span data-stu-id="afd99-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="afd99-203">Hello 設定完成之後，hello 精靈 」 提供 hello 選項 tooverify hello 連線 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="afd99-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="afd99-204">按一下**確認**toocheck 連線。</span><span class="sxs-lookup"><span data-stu-id="afd99-204">Click **Verify** toocheck connectivity.</span></span>

   ![安裝完成](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="afd99-206">新增同盟網域 <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="afd99-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="afd99-207">它是簡單 tooadd 網域 toobe 同盟與 Azure AD 使用 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="afd99-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="afd99-208">Azure AD Connect 新增 hello 同盟網域，並修改 hello 宣告規則 toocorrectly 反映 hello 簽發者，如果您有多個網域與 Azure AD 建立同盟。</span><span class="sxs-lookup"><span data-stu-id="afd99-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="afd99-209">tooadd 同盟網域，選取 hello 工作**新增其他 Azure AD 網域**。</span><span class="sxs-lookup"><span data-stu-id="afd99-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![其他 Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="afd99-211">在 hello hello 精靈的下一個頁面上，提供 Azure AD 中的 hello 全域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="afd99-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![連接 tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="afd99-213">在 hello**遠端存取認證**頁面上，提供 hello 網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="afd99-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![遠端存取認證](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="afd99-215">在 hello 下一個頁面上，hello 精靈會提供您可以建立與您在內部部署目錄同盟的 Azure AD 網域的清單。</span><span class="sxs-lookup"><span data-stu-id="afd99-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="afd99-216">Hello 清單中選擇 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="afd99-216">Choose hello domain from hello list.</span></span>

   ![Azure AD 網域](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="afd99-218">選擇 hello 網域之後，請 hello 精靈會提供您與 hello 精靈的進一步動作的適當資訊將會接受並 hello hello 設定的影響。</span><span class="sxs-lookup"><span data-stu-id="afd99-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="afd99-219">在某些情況下，如果您選取的網域，不尚未驗證在 Azure AD 中 hello 精靈為您提供資訊 toohelp 會確認 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="afd99-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="afd99-220">請參閱[加入您的自訂網域名稱 tooAzure Active Directory](../active-directory-add-domain.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="afd99-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="afd99-221">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="afd99-221">Click **Next**.</span></span> <span data-ttu-id="afd99-222">hello**準備 tooconfigure**頁面會顯示 hello Azure AD Connect 會執行的動作清單。</span><span class="sxs-lookup"><span data-stu-id="afd99-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="afd99-223">按一下**安裝**toofinish hello 組態。</span><span class="sxs-lookup"><span data-stu-id="afd99-223">Click **Install** toofinish hello configuration.</span></span>

   ![準備好 tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="afd99-225">使用者從 hello 加入之前，會先無法 toologin tooAzure AD 同盟的網域必須進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="afd99-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="afd99-226">AD FS 自訂</span><span class="sxs-lookup"><span data-stu-id="afd99-226">AD FS customization</span></span>
<span data-ttu-id="afd99-227">hello 下列各節提供有關一些 hello 常見工作的詳細資料，當您自訂 AD FS 登入頁面上，您可能必須 tooperform。</span><span class="sxs-lookup"><span data-stu-id="afd99-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="afd99-228">新增自訂公司標誌或圖例 <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="afd99-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="afd99-229">會顯示在 hello hello 公司 toochange hello 標誌**登入**頁面上，使用下列 Windows PowerShell cmdlet 和語法的 hello。</span><span class="sxs-lookup"><span data-stu-id="afd99-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="afd99-230">hello 建議維度 hello 標誌為 260 x 35 @ 96 dpi，檔案大小不超過 10 KB。</span><span class="sxs-lookup"><span data-stu-id="afd99-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="afd99-231">hello *TargetName*參數是必要項。</span><span class="sxs-lookup"><span data-stu-id="afd99-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="afd99-232">釋放與 AD FS 的 hello 預設佈景主題是名為 Default。</span><span class="sxs-lookup"><span data-stu-id="afd99-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="afd99-233">新增登入說明 <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="afd99-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="afd99-234">登入頁面描述 toohello tooadd**登入頁面**，使用下列 Windows PowerShell cmdlet 和語法的 hello。</span><span class="sxs-lookup"><span data-stu-id="afd99-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="afd99-235">修改 AD FS 宣告規則 <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="afd99-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="afd99-236">AD FS 支援豐富的宣告語言，您可以使用 toocreate 自訂宣告規則。</span><span class="sxs-lookup"><span data-stu-id="afd99-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="afd99-237">如需詳細資訊，請參閱[hello hello 宣告規則語言的角色](https://technet.microsoft.com/library/dd807118.aspx)。</span><span class="sxs-lookup"><span data-stu-id="afd99-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="afd99-238">hello 下列章節說明如何撰寫自訂規則，在某些情況下讓 tooAzure AD 和 AD FS 同盟產生關聯。</span><span class="sxs-lookup"><span data-stu-id="afd99-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="afd99-239">條件式出現在 hello 屬性中的值上的固定 ID</span><span class="sxs-lookup"><span data-stu-id="afd99-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="afd99-240">Azure AD Connect 可讓您指定做為來源錨點的物件時進行同步處理 tooAzure AD 屬性 toobe。</span><span class="sxs-lookup"><span data-stu-id="afd99-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="afd99-241">如果 hello 自訂屬性中的 hello 值不是空的您可能想 tooissue 不可變的識別碼宣告。</span><span class="sxs-lookup"><span data-stu-id="afd99-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="afd99-242">例如，您可能會選取**ms-ds-consistencyguid**為 hello 來源錨點和問題的 hello 屬性**ImmutableID**為**ms-ds-consistencyguid**中案例的 hello屬性有對它的值。</span><span class="sxs-lookup"><span data-stu-id="afd99-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="afd99-243">如果沒有針對 hello 屬性值，發出**objectGuid**為 hello 不可變的識別碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="afd99-244">Hello 之後 > 一節中所述，您可以建構 hello 自訂宣告規則集。</span><span class="sxs-lookup"><span data-stu-id="afd99-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="afd99-245">**規則 1：查詢屬性**</span><span class="sxs-lookup"><span data-stu-id="afd99-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="afd99-246">這項規則，在您要查詢的 hello 值**ms-ds-consistencyguid**和**objectGuid** hello 從 Active Directory 的使用者。</span><span class="sxs-lookup"><span data-stu-id="afd99-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="afd99-247">Hello 存放區名稱 tooan 適當的存放區中變更名稱 AD FS 部署。</span><span class="sxs-lookup"><span data-stu-id="afd99-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="afd99-248">也 hello 宣告型別 tooa 適當的宣告類型變更為您的同盟，為所定義的**objectGuid**和**ms-ds-consistencyguid**。</span><span class="sxs-lookup"><span data-stu-id="afd99-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="afd99-249">此外，藉由使用**新增**而非**問題**，避免加入 hello 實體的連出問題，並可以使用 hello 值作為中間值。</span><span class="sxs-lookup"><span data-stu-id="afd99-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="afd99-250">您將發行更新版本的規則中的 hello 宣告之後您建立哪些值 toouse hello 不可變的識別碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="afd99-251">**規則 2： 檢查 ms-ds-consistencyguid 存在 hello 使用者**</span><span class="sxs-lookup"><span data-stu-id="afd99-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="afd99-252">此規則會定義稱為暫存旗標**idflag**太設定**useguid**如果沒有任何**ms-ds-consistencyguid** hello 使用者填入。</span><span class="sxs-lookup"><span data-stu-id="afd99-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="afd99-253">這背後的 hello 邏輯是 hello 事實 AD FS 不允許空的宣告。</span><span class="sxs-lookup"><span data-stu-id="afd99-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="afd99-254">因此當您新增宣告 http://contoso.com/ws/2016/02/identity/claims/objectguid 和 http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid 規則 1 」 中，您得到**msdsconsistencyguid**宣告才hello 使用者會填入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="afd99-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="afd99-255">如果未填入，AD FS 會看到它將具有空值，並因此立即捨棄。</span><span class="sxs-lookup"><span data-stu-id="afd99-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="afd99-256">所有物件都會有 **objectGuid**，因此執行規則 1 之後，宣告一律會在該處。</span><span class="sxs-lookup"><span data-stu-id="afd99-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="afd99-257">**規則 3：發出 ms-ds-consistencyguid 為固定 ID (如果有的話)**</span><span class="sxs-lookup"><span data-stu-id="afd99-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="afd99-258">這是隱含的 **存在** 檢查。</span><span class="sxs-lookup"><span data-stu-id="afd99-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="afd99-259">如果 hello hello 宣告值存在，然後發出，做為不可變的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="afd99-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="afd99-260">hello 上一個範例使用 hello **nameidentifier**宣告。</span><span class="sxs-lookup"><span data-stu-id="afd99-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="afd99-261">您必須 toochange 此 toohello 適當的宣告類型 hello 不可變的識別碼在您的環境中。</span><span class="sxs-lookup"><span data-stu-id="afd99-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="afd99-262">**規則 4：發出 objectGuid 做為固定 ID，如果未出現 ms-ds-consistencyGuid**</span><span class="sxs-lookup"><span data-stu-id="afd99-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="afd99-263">在這項規則，只會檢查 hello 暫存旗標**idflag**。</span><span class="sxs-lookup"><span data-stu-id="afd99-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="afd99-264">您可以決定是否要根據 tooissue hello 宣告於它的值。</span><span class="sxs-lookup"><span data-stu-id="afd99-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="afd99-265">這些規則 hello 順序十分重要。</span><span class="sxs-lookup"><span data-stu-id="afd99-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="afd99-266">使用子網域 UPN 的 SSO</span><span class="sxs-lookup"><span data-stu-id="afd99-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="afd99-267">您可以加入多個網域 toobe 中所述，使用 Azure AD Connect，同盟[加入新的同盟的網域](active-directory-aadconnect-federation-management.md#addfeddomain)。</span><span class="sxs-lookup"><span data-stu-id="afd99-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="afd99-268">您必須修改 hello 使用者主要名稱 (UPN) 宣告，讓 hello 簽發者 ID 對應 toohello 根網域和不 hello 子網域，因為 hello 同盟的根網域也涵蓋 hello 子系。</span><span class="sxs-lookup"><span data-stu-id="afd99-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="afd99-269">根據預設，hello 會簽發者識別碼設定為宣告規則：</span><span class="sxs-lookup"><span data-stu-id="afd99-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![預設簽發者識別碼宣告](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="afd99-271">hello 預設規則只會採用 hello UPN 尾碼，並會在 hello 簽發者 ID 宣告中。</span><span class="sxs-lookup"><span data-stu-id="afd99-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="afd99-272">比方說，John 是 sub.contoso.com 中的使用者，而 contoso.com 與 Azure AD 同盟。</span><span class="sxs-lookup"><span data-stu-id="afd99-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="afd99-273">John 進入john@sub.contoso.com為 hello 時 tooAzure AD 在登入的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="afd99-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="afd99-274">hello 預設簽發者 ID 宣告規則中 AD FS 中 hello 下列方式處理它：</span><span class="sxs-lookup"><span data-stu-id="afd99-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="afd99-275">**宣告值：**http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="afd99-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="afd99-276">toohave 唯一 hello 根網域中 hello 簽發者宣告值，變更 hello 宣告規則 toomatch hello 下列：</span><span class="sxs-lookup"><span data-stu-id="afd99-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="afd99-277">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afd99-277">Next steps</span></span>
<span data-ttu-id="afd99-278">深入了解 [使用者登入選項](active-directory-aadconnect-user-signin.md)。</span><span class="sxs-lookup"><span data-stu-id="afd99-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
