---
title: "Azure Active Directory 網域服務︰部署 Azure Active Directory 應用程式 Proxy | Microsoft Docs"
description: "在 Active Directory Domain Services 受管理網域上使用 Azure AD 應用程式"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="9bd6a-103">在 Azure AD 網域服務受管理網域上部署 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bd6a-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="9bd6a-104">Azure Active Directory (AD) 應用程式 Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="9bd6a-105">使用 Azure AD 網域服務中，您可以執行內部 tooAzure 基礎結構服務現在增益集和-shift 舊版應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises tooAzure Infrastructure Services.</span></span> <span data-ttu-id="9bd6a-106">然後，您可以發行這些應用程式使用 Azure AD Application Proxy，您組織中的 tooprovide 安全遠端存取 toousers hello。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-106">You can then publish these applications using hello Azure AD Application Proxy, tooprovide secure remote access toousers in your organization.</span></span>

<span data-ttu-id="9bd6a-107">如果您是新 toohello Azure AD Application Proxy，深入了解這項功能以 hello 下列文章：[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](../active-directory/active-directory-application-proxy-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-107">If you're new toohello Azure AD Application Proxy, learn more about this feature with hello following article: [How tooprovide secure remote access tooon-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="9bd6a-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="9bd6a-108">Before you begin</span></span>
<span data-ttu-id="9bd6a-109">本文所列 tooperform hello 工作，您必須：</span><span class="sxs-lookup"><span data-stu-id="9bd6a-109">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="9bd6a-110">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="9bd6a-111">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="9bd6a-112">**Azure AD Basic 或 Premium 授權**是必要的 toouse hello Azure AD Application Proxy。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-112">An **Azure AD Basic or Premium license** is required toouse hello Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="9bd6a-113">**Azure AD 網域服務**必須啟用 hello Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-113">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="9bd6a-114">如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-114">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="9bd6a-115">工作 1 - 針對您的 Azure AD 目錄啟用 Azure AD 應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="9bd6a-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="9bd6a-116">執行下列步驟 tooenable hello Azure AD Application Proxy 為您的 Azure AD 目錄的 hello。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-116">Perform hello following steps tooenable hello Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="9bd6a-117">Hello 中的系統管理員身分登入[Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-117">Sign in as an administrator in hello [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="9bd6a-118">按一下**Azure Active Directory** toobring 向上 hello directory 概觀。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-118">Click **Azure Active Directory** toobring up hello directory overview.</span></span> <span data-ttu-id="9bd6a-119">按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-119">Click **Enterprise applications**.</span></span>

    ![選取 Azure AD 目錄](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="9bd6a-121">按一下 [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-121">Click **Application proxy**.</span></span> <span data-ttu-id="9bd6a-122">如果您沒有 Azure AD Basic 或 Azure AD Premium 訂用帳戶，您會看到選項 tooenable 試用版。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option tooenable a trial.</span></span> <span data-ttu-id="9bd6a-123">切換**啟用應用程式 Proxy？**太**啟用**按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-123">Toggle **Enable Application Proxy?** too**Enable** and click **Save**.</span></span>

    ![啟用應用程式 Proxy](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="9bd6a-125">toodownload hello 連接器，請按一下 hello**連接器** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-125">toodownload hello connector, click hello **Connector** button.</span></span>

    ![下載連接器](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="9bd6a-127">Hello 下載頁面上，接受 hello 授權條款及隱私權合約，並按一下 hello**下載** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-127">On hello download page, accept hello license terms and privacy agreement and click hello **Download** button.</span></span>

    ![確認下載](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="9bd6a-129">工作 2-佈建已加入網域的 Windows 伺服器 toodeploy hello Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="9bd6a-129">Task 2 - Provision domain-joined Windows servers toodeploy hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="9bd6a-130">您需要已加入網域的 Windows Server 虛擬機器，您可以在其安裝 hello Azure AD 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-130">You need domain-joined Windows Server virtual machines on which you can install hello Azure AD Application Proxy connector.</span></span> <span data-ttu-id="9bd6a-131">根據發行的 hello 應用程式，您可以選擇 tooprovision hello 連接器安裝所在的多部伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-131">Depending on hello applications being published, you may choose tooprovision multiple servers on which hello connector is installed.</span></span> <span data-ttu-id="9bd6a-132">這個部署選項為您提供更高的可用性，並協助處理更大量的驗證負載。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="9bd6a-133">Hello 連接器的伺服器上佈建 hello 相同虛擬網路 （或連接/所以的虛擬網路），在您已啟用您 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-133">Provision hello connector servers on hello same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="9bd6a-134">同樣地，hello 伺服器裝載 hello 您透過 hello 應用程式 Proxy 發佈的應用程式需要 toobe hello 上安裝相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-134">Similarly, hello servers hosting hello applications you publish via hello Application Proxy need toobe installed on hello same Azure virtual network.</span></span>

<span data-ttu-id="9bd6a-135">tooprovision 連接器的伺服器，請遵循 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-135">tooprovision connector servers, follow hello tasks outlined in hello article titled [Join a Windows virtual machine tooa managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="9bd6a-136">工作 3-安裝和註冊 hello Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="9bd6a-136">Task 3 - Install and register hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="9bd6a-137">先前，您要佈建 Windows Server 虛擬機器，並加入 toohello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-137">Previously, you provisioned a Windows Server virtual machine and joined it toohello managed domain.</span></span> <span data-ttu-id="9bd6a-138">在這項工作，您將此虛擬機器上安裝 hello Azure AD 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-138">In this task, you will install hello Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="9bd6a-139">將複製 hello 連接器安裝封裝 toohello VM 安裝 hello Azure AD Web 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-139">Copy hello connector installation package toohello VM on which you install hello Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="9bd6a-140">執行**AADApplicationProxyConnectorInstaller.exe** hello 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-140">Run **AADApplicationProxyConnectorInstaller.exe** on hello virtual machine.</span></span> <span data-ttu-id="9bd6a-141">接受 hello 軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-141">Accept hello software license terms.</span></span>

    ![接受安裝的條款](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="9bd6a-143">在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 目錄的應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-143">During installation, you are prompted tooregister hello connector with hello Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="9bd6a-144">提供您的 **Azure AD 全域管理員認證**。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="9bd6a-145">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="9bd6a-146">hello 系統管理員使用帳戶 tooregister hello 連接器必須屬於 toohello 相同的目錄啟用 hello 應用程式 Proxy 服務的位置。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-146">hello administrator account used tooregister hello connector must belong toohello same directory where you enabled hello Application Proxy service.</span></span> <span data-ttu-id="9bd6a-147">例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或任何其他有效的別名在該網域上。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-147">For example, if hello tenant domain is contoso.com, hello admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="9bd6a-148">如果 IE 增強式安全性設定已開啟 hello 伺服器要在其中安裝 hello 連接器，hello 註冊畫面可能會封鎖。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-148">If IE Enhanced Security Configuration is turned on for hello server where you are installing hello connector, hello registration screen might be blocked.</span></span> <span data-ttu-id="9bd6a-149">tooallow 存取權，遵循 hello hello 錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-149">tooallow access, follow hello instructions in hello error message.</span></span> <span data-ttu-id="9bd6a-150">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="9bd6a-151">如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](../active-directory/active-directory-application-proxy-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![安裝的連接器](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="9bd6a-153">tooensure hello 連接器正常執行，執行的 hello Azure AD 應用程式 Proxy 連接器疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-153">tooensure hello connector works properly, run hello Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="9bd6a-154">執行 hello 疑難排解之後，您應該看到成功的報表。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-154">You should see a successful report after running hello troubleshooter.</span></span>

    ![疑難排解程式成功](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="9bd6a-156">您應該會看到 Azure AD 目錄中的 hello 應用程式 proxy 頁面上所列的 hello 新安裝的連接器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-156">You should see hello newly installed connector listed on hello Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="9bd6a-157">您可以選擇多部伺服器上的 tooinstall 連接器 tooguarantee 驗證透過 hello Azure AD Application Proxy 發行應用程式的高可用性。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-157">You may choose tooinstall connectors on multiple servers tooguarantee high availability for authenticating applications published through hello Azure AD Application Proxy.</span></span> <span data-ttu-id="9bd6a-158">執行的 hello 上列 tooinstall hello 連接器，在其他伺服器聯結的 tooyour 受管理的網域上的相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-158">Perform hello same steps listed above tooinstall hello connector on other servers joined tooyour managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="9bd6a-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bd6a-159">Next Steps</span></span>
<span data-ttu-id="9bd6a-160">您擁有 hello Azure AD Application Proxy 設定，並且整合與您 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-160">You have set up hello Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="9bd6a-161">**移轉應用程式 tooAzure 虛擬機器：**增益 shift 您可以將應用程式從內部部署伺服器 tooAzure 虛擬機器聯結的 tooyour 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-161">**Migrate your applications tooAzure virtual machines:** You can lift-and-shift your applications from on-premises servers tooAzure virtual machines joined tooyour managed domain.</span></span> <span data-ttu-id="9bd6a-162">這樣可協助您移除 hello 的內部部署執行伺服器上的基礎結構成本。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-162">Doing so helps you get rid of hello infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="9bd6a-163">**使用 Azure AD Application Proxy 發行應用程式：**發行應用程式使用 Azure AD Application Proxy hello Azure 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using hello Azure AD Application Proxy.</span></span> <span data-ttu-id="9bd6a-164">如需詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 發佈應用程式](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9bd6a-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="9bd6a-165">部署附註 - 使用 Azure AD 應用程式 Proxy 發佈 IWA (整合式 Windows 驗證) 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bd6a-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="9bd6a-166">啟用單一登入 tooyour 應用程式使用整合式 Windows 驗證 (IWA) 應用程式 Proxy 連接器權限授與 tooimpersonate 使用者，以及傳送和接收代表語彙基元。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-166">Enable single sign-on tooyour applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission tooimpersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="9bd6a-167">設定 kerberos 限制委派 (KCD) hello 連接器 toogrant hello 所需的權限 tooaccess 上的資源 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-167">Configure kerberos constrained delegation (KCD) for hello connector toogrant hello required permissions tooaccess resources on hello managed domain.</span></span> <span data-ttu-id="9bd6a-168">使用受管理的網域上的 hello 資源型 KCD 機制，以提高安全性。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-168">Use hello resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="9bd6a-169">啟用 hello Azure AD 應用程式 Proxy 連接器的資源型 kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="9bd6a-169">Enable resource-based kerberos constrained delegation for hello Azure AD Application Proxy connector</span></span>
<span data-ttu-id="9bd6a-170">hello Azure 應用程式 Proxy 連接器應該進行 kerberos 限制委派 (KCD)，讓它可以模擬使用者上設定 hello 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-170">hello Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on hello managed domain.</span></span> <span data-ttu-id="9bd6a-171">在 Azure AD Domain Services 受管理的網域上，您沒有網域系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="9bd6a-172">因此，**無法在受管理的網域上設定傳統帳戶層級 KCD**。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="9bd6a-173">使用本[文章](active-directory-ds-enable-kcd.md)中所述的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9bd6a-174">您需要 toobe 成員 hello ' AAD DC Administrators' 群組的 tooadminister hello 管理網域使用 AD PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-174">You need toobe a member of hello 'AAD DC Administrators' group, tooadminister hello managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="9bd6a-175">將 hello Get-adcomputer PowerShell cmdlet tooretrieve hello 設定用於 hello 的 hello Azure AD 應用程式 Proxy 連接器安裝的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-175">Use hello Get-ADComputer PowerShell cmdlet tooretrieve hello settings for hello computer on which hello Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="9bd6a-176">之後，使用向上資源型 KCD hello Set-adcomputer cmdlet tooset hello 資源伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-176">Thereafter, use hello Set-ADComputer cmdlet tooset up resource-based KCD for hello resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="9bd6a-177">如果您已在受管理的網域部署多個應用程式 Proxy 連接器，您需要 tooconfigure 資源型 KCD 每個這類連接器執行個體。</span><span class="sxs-lookup"><span data-stu-id="9bd6a-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need tooconfigure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="9bd6a-178">相關內容</span><span class="sxs-lookup"><span data-stu-id="9bd6a-178">Related Content</span></span>
* [<span data-ttu-id="9bd6a-179">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="9bd6a-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="9bd6a-180">在受管理的網域上設定 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="9bd6a-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="9bd6a-181">Kerberos 限制委派概觀</span><span class="sxs-lookup"><span data-stu-id="9bd6a-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
