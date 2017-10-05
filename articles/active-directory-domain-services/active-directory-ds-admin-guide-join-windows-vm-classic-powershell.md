---
title: "Azure Active Directory Domain Services：管理指南 | Microsoft Docs"
description: "使用 Azure PowerShell 與傳統部署模型將 Windows 虛擬機器加入受管理的網域。"
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
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="f3cec-103">使用 PowerShell 將 Windows Server 虛擬機器加入受管理的網域</span><span class="sxs-lookup"><span data-stu-id="f3cec-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3cec-104">Azure 傳統入口網站 - Windows</span><span class="sxs-lookup"><span data-stu-id="f3cec-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="f3cec-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="f3cec-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="f3cec-106">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="f3cec-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f3cec-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="f3cec-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f3cec-108">Azure AD 網域服務目前不支援 Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="f3cec-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="f3cec-109">下列步驟將示範如何使用建置組塊自訂一組 Azure PowerShell 命令，建立和預先設定以 Windows 為基礎的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3cec-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="f3cec-110">這些步驟可協助您建置 Windows 型 Azure 虛擬機器，並將它加入 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="f3cec-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="f3cec-111">這些步驟遵循建立 Azure PowerShell 命令集合的填空方法。</span><span class="sxs-lookup"><span data-stu-id="f3cec-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="f3cec-112">如果您是 PowerShell 的新手或想知道可指定哪些值來成功設定組態，這個方法相當實用。</span><span class="sxs-lookup"><span data-stu-id="f3cec-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="f3cec-113">進階的 PowerShell 使用者可以使用命令並取代本身的變數值 (以「$」為開頭的行)。</span><span class="sxs-lookup"><span data-stu-id="f3cec-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="f3cec-114">如果您尚未這樣做，請按照 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 中的操作方法，在本機電腦安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f3cec-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="f3cec-115">然後，開啟 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f3cec-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="f3cec-116">步驟 1︰加入您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f3cec-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="f3cec-117">在 PowerShell 提示字元中，輸入 **Add-AzureAccount**，然後按一下 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="f3cec-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="f3cec-118">輸入與您 Azure 訂用帳戶相關聯的電子郵件地址，並按一下 [繼續] 。</span><span class="sxs-lookup"><span data-stu-id="f3cec-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="f3cec-119">輸入您帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="f3cec-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="f3cec-120">按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="f3cec-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="f3cec-121">步驟 2：設定您的訂用帳戶和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f3cec-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="f3cec-122">在 Windows PowerShell 命令提示字元處執行這些命令，來設定您的 Azure 訂用帳戶與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3cec-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="f3cec-123">以正確的名稱取代括號中 (包括 < 和 > 字元) 的所有內容。</span><span class="sxs-lookup"><span data-stu-id="f3cec-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="f3cec-124">您可以從 **Get-AzureSubscription** 命令輸出的 SubscriptionName 屬性，取得正確的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f3cec-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f3cec-125">執行 **Select-AzureSubscription** 命令後，您就能從 **Get-AzureStorageAccount** 命令輸出的標籤屬性取得正確的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f3cec-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="f3cec-126">步驟 3︰逐步解說 - 佈建虛擬機器並將它加入受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="f3cec-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="f3cec-127">以下是建立這個虛擬機器的相對應 Azure PowerShell 命令集，各個區塊之間均有空白行，以求編排清晰。</span><span class="sxs-lookup"><span data-stu-id="f3cec-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="f3cec-128">指定要佈建的 Windows 虛擬機器相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3cec-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="f3cec-129">如需 D、DS 或 G 系列虛擬機器的 InstanceSize 值，請參閱 [Azure 的虛擬機器和雲端服務大小](https://msdn.microsoft.com/library/azure/dn197896.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3cec-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="f3cec-130">提供受管理網域的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f3cec-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="f3cec-131">指定雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="f3cec-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="f3cec-132">指定 VM 應該加入的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="f3cec-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="f3cec-133">請確定這個虛擬網路中有 AAD-DS 受管理的網域可用。</span><span class="sxs-lookup"><span data-stu-id="f3cec-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="f3cec-134">選取要用來佈建 VM 的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f3cec-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="f3cec-135">設定 VM - 設定 VM 名稱、執行個體大小和要使用的映像。</span><span class="sxs-lookup"><span data-stu-id="f3cec-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="f3cec-136">取得 VM 的本機系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f3cec-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="f3cec-137">選擇本機系統管理員的強式密碼。</span><span class="sxs-lookup"><span data-stu-id="f3cec-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="f3cec-138">取得屬於「AAD DC 系統管理員」群組的使用者帳戶認證，將 VM 加入受管理的網域中。</span><span class="sxs-lookup"><span data-stu-id="f3cec-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="f3cec-139">不指定網域名稱 - 例如，我們在範例中指定 'bob' 為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f3cec-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="f3cec-140">設定 VM - 指定網域聯結需求和所需的認證。</span><span class="sxs-lookup"><span data-stu-id="f3cec-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="f3cec-141">設定 VM 的子網路。</span><span class="sxs-lookup"><span data-stu-id="f3cec-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="f3cec-142">選擇性︰指向網域的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f3cec-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="f3cec-143">如果 Azure AD 網域服務受管理網域的 IP 位址設定成虛擬網路的 DNS 伺服器，就不需要這個步驟。</span><span class="sxs-lookup"><span data-stu-id="f3cec-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="f3cec-144">現在，佈建已加入網域的 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="f3cec-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="f3cec-145">佈建 Windows VM 並自動將它聯結至 AAD 網域服務受管理網域的指令碼</span><span class="sxs-lookup"><span data-stu-id="f3cec-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="f3cec-146">這個 PowerShell 命令集建立企業營運伺服器的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="f3cec-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="f3cec-147">使用 Windows Server 2012 R2 Datacenter 映像。</span><span class="sxs-lookup"><span data-stu-id="f3cec-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f3cec-148">是超小的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f3cec-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="f3cec-149">名稱為 Contoso100-test。</span><span class="sxs-lookup"><span data-stu-id="f3cec-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="f3cec-150">會自動加入 contoso100 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="f3cec-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="f3cec-151">和受管理的網域加入相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f3cec-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="f3cec-152">以下的完整範例指令碼，可建立 Windows 虛擬機器，並自動將它加入 Azure AD 網域服務受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="f3cec-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="f3cec-153">相關內容</span><span class="sxs-lookup"><span data-stu-id="f3cec-153">Related Content</span></span>
* [<span data-ttu-id="f3cec-154">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="f3cec-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f3cec-155">Administer an Azure AD Domain Services managed domain (管理 Azure AD 網域服務受管理的網域)</span><span class="sxs-lookup"><span data-stu-id="f3cec-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
