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
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0eef5-103">在 Azure AD 網域服務受管理網域上部署 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="0eef5-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="0eef5-104">Azure Active Directory (AD) 應用程式 Proxy 可藉由發佈要透過網際網路存取的內部部署應用程式，協助您支援遠端背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="0eef5-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="0eef5-105">使用 Azure AD 網域服務，您現在可以提升執行內部部署的舊版應用程式並隨即轉移至 Azure 基礎結構服務。</span><span class="sxs-lookup"><span data-stu-id="0eef5-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="0eef5-106">然後，您可以使用 Azure AD 應用程式 Proxy 發佈這些應用程式，為您組織中的使用者提供安全遠端存取。</span><span class="sxs-lookup"><span data-stu-id="0eef5-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="0eef5-107">如果您是 Azure AD 應用程式 Proxy 的新手，可至下列文章：[如何為內部部署應用程式提供安全的遠端存取](../active-directory/active-directory-application-proxy-get-started.md)深入了解這個功能。</span><span class="sxs-lookup"><span data-stu-id="0eef5-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="0eef5-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="0eef5-108">Before you begin</span></span>
<span data-ttu-id="0eef5-109">若要執行本文中所列的工作，您需要︰</span><span class="sxs-lookup"><span data-stu-id="0eef5-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="0eef5-110">有效的 **Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0eef5-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="0eef5-111">**Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。</span><span class="sxs-lookup"><span data-stu-id="0eef5-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="0eef5-112">需要 **Azure AD 基本或進階授權**才能使用 Azure AD 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0eef5-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="0eef5-113">**Azure AD 網域服務** 必須已針對 Azure AD 目錄啟用。</span><span class="sxs-lookup"><span data-stu-id="0eef5-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="0eef5-114">如果還沒有啟用，請按照 [入門指南](active-directory-ds-getting-started.md)所述的所有工作來進行。</span><span class="sxs-lookup"><span data-stu-id="0eef5-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="0eef5-115">工作 1 - 針對您的 Azure AD 目錄啟用 Azure AD 應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="0eef5-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="0eef5-116">執行下列步驟為您的 Azure AD 目錄啟用 Azure AD 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="0eef5-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="0eef5-117">在 [Azure 入口網站](http://portal.azure.com)中，以系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="0eef5-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="0eef5-118">按一下 [Azure Active Directory] 以啟動目錄概觀。</span><span class="sxs-lookup"><span data-stu-id="0eef5-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="0eef5-119">按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0eef5-119">Click **Enterprise applications**.</span></span>

    ![選取 Azure AD 目錄](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="0eef5-121">按一下 [應用程式 Proxy]。</span><span class="sxs-lookup"><span data-stu-id="0eef5-121">Click **Application proxy**.</span></span> <span data-ttu-id="0eef5-122">如果您沒有 Azure AD Basic 或 Azure AD Premium 訂用帳戶，您會看到一個選項可啟用試用版。</span><span class="sxs-lookup"><span data-stu-id="0eef5-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="0eef5-123">將 [啟用應用程式 Proxy？] 切換為 [啟用]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0eef5-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![啟用應用程式 Proxy](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="0eef5-125">若要下載連接器，請按一下 [連接器] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0eef5-125">To download the connector, click the **Connector** button.</span></span>

    ![下載連接器](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="0eef5-127">在下載頁面上，接受授權條款和隱私權合約，並按一下 [下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0eef5-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![確認下載](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="0eef5-129">工作 2 - 佈建已加入網域的 Windows 伺服器來部署 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="0eef5-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="0eef5-130">您需要可安裝 Azure AD 應用程式 Proxy 連接器的已加入網域 Windows Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="0eef5-131">根據發佈的應用程式，您可以選擇佈建已安裝連接器的多部伺服器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="0eef5-132">這個部署選項為您提供更高的可用性，並協助處理更大量的驗證負載。</span><span class="sxs-lookup"><span data-stu-id="0eef5-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="0eef5-133">在相同的虛擬網路 (或連線/對等互連的虛擬網路) 上佈建連接器伺服器，其中已您啟用 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0eef5-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="0eef5-134">同樣地，裝載您透過應用程式 Proxy 發佈之應用程式的伺服器需要安裝在相同的 Azure 虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="0eef5-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="0eef5-135">若要佈建連接器伺服器，請依照名為[將 Windows 虛擬機器加入受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)一文所述的工作進行操作。</span><span class="sxs-lookup"><span data-stu-id="0eef5-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="0eef5-136">工作 3 - 安裝與註冊 Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="0eef5-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="0eef5-137">在過去，您會佈建 Windows Server 虛擬機器，並將它加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0eef5-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="0eef5-138">在這個工作中，您將在此虛擬機器上安裝 Azure AD 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="0eef5-139">將連接器安裝套件複製到安裝 Azure AD Web 應用程式 Proxy 連接器的 VM。</span><span class="sxs-lookup"><span data-stu-id="0eef5-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="0eef5-140">在虛擬機器上執行 **AADApplicationProxyConnectorInstaller.exe**。</span><span class="sxs-lookup"><span data-stu-id="0eef5-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="0eef5-141">接受軟體授權條款。</span><span class="sxs-lookup"><span data-stu-id="0eef5-141">Accept the software license terms.</span></span>

    ![接受安裝的條款](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="0eef5-143">在安裝期間，系統將提示您使用 Azure AD 目錄的應用程式 Proxy 註冊連接器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="0eef5-144">提供您的 **Azure AD 全域管理員認證**。</span><span class="sxs-lookup"><span data-stu-id="0eef5-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="0eef5-145">您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。</span><span class="sxs-lookup"><span data-stu-id="0eef5-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="0eef5-146">用於註冊連接器的系統管理員帳戶必須屬於與您啟用應用程式 Proxy 服務的位置相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="0eef5-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="0eef5-147">例如，如果租用戶網域為 contoso.com，則系統管理員應該是 admin@contoso.com，或該網域上的其他有效別名。</span><span class="sxs-lookup"><span data-stu-id="0eef5-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="0eef5-148">如果 [IE 增強式安全性設定] 在您要安裝連接器的伺服器上開啟，可能會封鎖註冊畫面。</span><span class="sxs-lookup"><span data-stu-id="0eef5-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="0eef5-149">若要允許存取，請依照錯誤訊息中的指示。</span><span class="sxs-lookup"><span data-stu-id="0eef5-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="0eef5-150">請確定已停用 [Internet Explorer 增強式安全性]。</span><span class="sxs-lookup"><span data-stu-id="0eef5-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="0eef5-151">如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](../active-directory/active-directory-application-proxy-troubleshoot.md)。</span><span class="sxs-lookup"><span data-stu-id="0eef5-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![安裝的連接器](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="0eef5-153">若要確保連接器正確運作，請執行 Azure AD 應用程式 Proxy 連接器疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0eef5-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="0eef5-154">執行疑難排解程式之後，您應該看到成功的報告。</span><span class="sxs-lookup"><span data-stu-id="0eef5-154">You should see a successful report after running the troubleshooter.</span></span>

    ![疑難排解程式成功](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="0eef5-156">您應該會在Azure AD 目錄中看到新安裝的連接器列在應用程式 Proxy 頁面上。</span><span class="sxs-lookup"><span data-stu-id="0eef5-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="0eef5-157">您可以選擇在多部伺服器上安裝連接器，以確保驗證透過 Azure AD 應用程式 Proxy 發佈之應用程式的高可用性。</span><span class="sxs-lookup"><span data-stu-id="0eef5-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="0eef5-158">執行上述的相同步驟，以在其他加入您受管理網域的伺服器上安裝連接器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0eef5-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0eef5-159">Next Steps</span></span>
<span data-ttu-id="0eef5-160">您已設定 Azure AD 應用程式 Proxy，並將其與您 Azure AD 網域服務的受管理網域進行整合。</span><span class="sxs-lookup"><span data-stu-id="0eef5-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="0eef5-161">**將您的應用程式移轉到 Azure 虛擬機器︰**您可以從內部部署伺服器提升應用程式並隨即轉移到加入至受管理網域的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0eef5-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="0eef5-162">如此一來，可協助您刪掉執行伺服器內部部署的基礎結構成本。</span><span class="sxs-lookup"><span data-stu-id="0eef5-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="0eef5-163">**使用 Azure AD 應用程式 Proxy 發佈應用程式︰**使用 Azure AD 應用程式 Proxy 發佈您的 Azure 虛擬機器上所執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0eef5-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="0eef5-164">如需詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 發佈應用程式](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0eef5-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="0eef5-165">部署附註 - 使用 Azure AD 應用程式 Proxy 發佈 IWA (整合式 Windows 驗證) 應用程式</span><span class="sxs-lookup"><span data-stu-id="0eef5-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="0eef5-166">授與應用程式 Proxy 連接器權限來模擬使用者並代表其傳送和接收權杖，以使用「整合式 Windows 驗證」(IWA) 啟用應用程式的單一登入。</span><span class="sxs-lookup"><span data-stu-id="0eef5-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="0eef5-167">設定連接器的 Kerberos 限制委派 (KCD)，以授與存取受管理網域上的資源所需的權限。</span><span class="sxs-lookup"><span data-stu-id="0eef5-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="0eef5-168">在受管理的網域上使用資源型 KCD 機制來提高安全性。</span><span class="sxs-lookup"><span data-stu-id="0eef5-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="0eef5-169">針對 Azure AD 應用程式 Proxy 連接器啟用資源型 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="0eef5-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="0eef5-170">應設定 Kerberos 限制委派 (KCD) 的 Azure 應用程式 Proxy 連接器，以便它可以在受管理的網域上模擬使用者。</span><span class="sxs-lookup"><span data-stu-id="0eef5-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="0eef5-171">在 Azure AD 網域服務受管理的網域上，您沒有網域系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0eef5-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="0eef5-172">因此，**無法在受管理的網域上設定傳統帳戶層級 KCD**。</span><span class="sxs-lookup"><span data-stu-id="0eef5-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="0eef5-173">使用本[文章](active-directory-ds-enable-kcd.md)中所述的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="0eef5-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0eef5-174">您必須是「AAD DC 系統管理員」群組的成員，才能使用 AD PowerShell cmdlet 來管理受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="0eef5-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="0eef5-175">使用 Get-adcomputer PowerShell cmdlet 來擷取已安裝 Azure AD 應用程式 Proxy 連接器之電腦的設定。</span><span class="sxs-lookup"><span data-stu-id="0eef5-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="0eef5-176">之後，使用組 Set-ADComputer cmdlet 來設定資源伺服器的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="0eef5-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="0eef5-177">如果您已在受管理的網域上部署多個應用程式 Proxy 連接器，您需要設定每個此類連接器執行個體的資源型 KCD。</span><span class="sxs-lookup"><span data-stu-id="0eef5-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="0eef5-178">相關內容</span><span class="sxs-lookup"><span data-stu-id="0eef5-178">Related Content</span></span>
* [<span data-ttu-id="0eef5-179">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="0eef5-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="0eef5-180">在受管理的網域上設定 Kerberos 限制委派</span><span class="sxs-lookup"><span data-stu-id="0eef5-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="0eef5-181">Kerberos 限制委派概觀</span><span class="sxs-lookup"><span data-stu-id="0eef5-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
