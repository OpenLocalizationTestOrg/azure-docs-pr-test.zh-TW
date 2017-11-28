---
title: "Azure Active Directory Domain Services：管理指南 | Microsoft Docs"
description: "加入 Windows 虛擬機器 tooa 受管理的網域使用 Azure PowerShell 及 hello 傳統部署模型。"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="aa5a1-103">加入 Windows Server 虛擬機器 tooa 受管理的網域使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa5a1-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa5a1-104">Azure 傳統入口網站 - Windows</span><span class="sxs-lookup"><span data-stu-id="aa5a1-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="aa5a1-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="aa5a1-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="aa5a1-106">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="aa5a1-107">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="aa5a1-108">Azure AD 網域服務目前不支援 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="aa5a1-109">這些步驟顯示如何 toocustomize 一組的 Azure PowerShell 命令，建立並預先設定 windows Azure 虛擬機器使用的建置組塊方法。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="aa5a1-110">這些步驟可協助您建立 windows Azure 虛擬機器，並將其加入 tooan Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="aa5a1-111">這些步驟遵循建立 Azure PowerShell 命令集合的填空方法。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="aa5a1-112">如果您是新 tooPowerShell 或想 tooknow 哪些值 toospecify 成功的組態，這種方法十分有用。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="aa5a1-113">進階的 PowerShell 使用者可以採取 hello 命令，並以取代其值為 hello 變數 （hello 行開頭為"$"）。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="aa5a1-114">如果還沒有這麼做，使用中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell，在本機電腦上的。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="aa5a1-115">然後，開啟 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="aa5a1-116">步驟 1︰加入您的帳戶</span><span class="sxs-lookup"><span data-stu-id="aa5a1-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="aa5a1-117">在 hello PowerShell 提示字元中輸入**Add-azureaccount**按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="aa5a1-118">輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="aa5a1-119">輸入 hello 您帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="aa5a1-120">按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="aa5a1-121">步驟 2：設定您的訂用帳戶和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="aa5a1-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="aa5a1-122">Hello Windows PowerShell 命令提示字元中執行這些命令來設定您的 Azure 訂用帳戶和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="aa5a1-123">Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確名稱。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="aa5a1-124">您可以從 hello 的 hello hello 輸出的訂用帳戶名稱屬性來取得 hello 正確的訂用帳戶名稱**Get-azuresubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="aa5a1-125">您可以從 hello Label 屬性的 hello hello 輸出取得 hello 正確的儲存體帳戶名稱**Get AzureStorageAccount**命令之後執行 hello **Select-azuresubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="aa5a1-126">步驟 3： 逐步解說-佈建 hello 虛擬機器，並將其聯結 toohello 受管理的網域</span><span class="sxs-lookup"><span data-stu-id="aa5a1-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="aa5a1-127">以下是 hello 對應 Azure PowerShell 命令集 toocreate 之間可讀性的每個區塊的空白行與此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="aa5a1-128">指定 hello Windows 虛擬機器 toobe 佈建的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="aa5a1-129">D、 DS 或 G 系列虛擬機器的 hello InstanceSize 值，請參閱[虛擬機器和 Azure 的雲端服務大小](https://msdn.microsoft.com/library/azure/dn197896.aspx)。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="aa5a1-130">提供有關 hello 受管理的網域資訊。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="aa5a1-131">指定 hello hello 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="aa5a1-132">指定 hello VM 應加入的虛擬網路 toowhich hello hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="aa5a1-133">確定此虛擬網路中有該 hello AAD DS 受管理網域。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="aa5a1-134">選取 VM 映像使用 toobe tooprovision hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="aa5a1-135">設定 hello VM-組 VM 名稱，使用的執行個體大小及影像 toobe。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="aa5a1-136">取得 hello VM 的本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="aa5a1-137">選擇本機系統管理員的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="aa5a1-138">取得屬於 too'AAD DC Administrators' 群組 toojoin VM toohello 受管理的網域使用者帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="aa5a1-139">請勿指定 hello 網域名稱-的執行個體，在本例中，我們在此指定 'bob' hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="aa5a1-140">設定 hello VM-指定網域聯結需求 （& s） 所需的認證。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="aa5a1-141">設定 hello VM 子網路。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="aa5a1-142">選擇性： 點 toohello 的 hello 網域的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="aa5a1-143">如果您設定 hello IP 位址的 hello Azure AD 網域服務受管理的網域 toobe hello hello 虛擬網路的 DNS 伺服器，就不需要此步驟。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="aa5a1-144">現在，佈建 hello 已加入網域的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="aa5a1-145">指令碼 tooprovision Windows VM，並自動將其加入 tooan AAD 網域服務受管理的網域</span><span class="sxs-lookup"><span data-stu-id="aa5a1-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="aa5a1-146">這個 PowerShell 命令集建立企業營運伺服器的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="aa5a1-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="aa5a1-147">使用 hello Windows Server 2012 R2 Datacenter 映像。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="aa5a1-148">是超小的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="aa5a1-149">具有 hello Contoso100 測試的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="aa5a1-150">會自動網域聯結的 toohello contoso100 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="aa5a1-151">加入 toohello hello 與相同虛擬網路管理網域。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="aa5a1-152">以下是 hello 完整的範例指令碼 toocreate hello Windows 虛擬機器，並自動將其加入 toohello Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="aa5a1-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="aa5a1-153">相關內容</span><span class="sxs-lookup"><span data-stu-id="aa5a1-153">Related Content</span></span>
* [<span data-ttu-id="aa5a1-154">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="aa5a1-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="aa5a1-155">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="aa5a1-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
