---
title: "在 Azure VM 中使用 PowerShell 設定 Always On 可用性群組 | Microsoft Docs"
description: "本教學課程會使用以傳統部署模型建立的資源。 您使用 PowerShell 在 Azure 中建立 Always On 可用性群組。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: b99cf767fb931d3f7fe14fcbe7990126244613ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="5a5b9-104">在 Azure VM 中使用 PowerShell 設定 Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="5a5b9-104">Configure the Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a5b9-105">傳統：UI</span><span class="sxs-lookup"><span data-stu-id="5a5b9-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="5a5b9-106">[傳統：PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="5a5b9-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="5a5b9-107">在開始之前，請考量您現在可以在 Azure Resource Manager 模型中完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="5a5b9-108">我們建議針對新的部署使用 Azure Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="5a5b9-109">請參閱 [Azure 虛擬機器上的 SQL Server Always On 可用性群組](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a5b9-110">我們建議讓大部分的新部署使用 Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-110">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5a5b9-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5a5b9-112">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-112">This article covers using the classic deployment model.</span></span>

<span data-ttu-id="5a5b9-113">Azure 虛擬機器 (VM) 可協助資料庫管理員降低高可用性 SQL Server 系統的成本。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-113">Azure virtual machines (VMs) can help database administrators to lower the cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="5a5b9-114">本教學課程將示範如何使用 Azure 環境中的 SQL Server Always On 端對端來實作可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-114">This tutorial shows you how to implement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="5a5b9-115">在本教學課程結束時，您 Azure 中的 SQL Server Always On 解決方案將包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-115">At the end of the tutorial, your SQL Server Always On solution in Azure will consist of the following elements:</span></span>

* <span data-ttu-id="5a5b9-116">包含多個子網路 (前端和後端子網路) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="5a5b9-117">具有 Active Directory 網域的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="5a5b9-118">兩個 SQL Server VM 已部署至後端子網路並加入 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-118">Two SQL Server VMs that are deployed to the back-end subnet and joined to the Active Directory domain.</span></span>
* <span data-ttu-id="5a5b9-119">具有節點多數仲裁模型的 3 節點 Windows 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-119">A three-node Windows failover cluster with the Node Majority quorum model.</span></span>
* <span data-ttu-id="5a5b9-120">具有兩份可用性資料庫同步認可複本的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="5a5b9-121">此案例在 Azure 中是好選擇的原因是其單純性，而非因為其具有成本效益或其他因素。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="5a5b9-122">例如，您可以將雙複本可用性群組的 VM 數量減到最少，以縮短 Azure 中的計算時數，方法是在 2 節點的容錯移轉叢集中使用網域控制站作為仲裁檔案共用見證。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-122">For example, you can minimize the number of VMs for a two-replica availability group to save on compute hours in Azure by using the domain controller as the quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="5a5b9-123">此方法可讓上述組態減少一個 VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-123">This method reduces the VM count by one from the above configuration.</span></span>

<span data-ttu-id="5a5b9-124">本教學課程的目的是示範設定上述解決方案所需執行的步驟，但不會闡述每個步驟的細節內容。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-124">This tutorial is intended to show you the steps that are required to set up the described solution above, without elaborating on the details of each step.</span></span> <span data-ttu-id="5a5b9-125">因此，本教學課程會使用 PowerShell 指令碼帶您快速進行每個步驟，但不會提供 GUI 組態步驟。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-125">Therefore, instead of providing the GUI configuration steps, it uses PowerShell scripting to take you quickly through each step.</span></span> <span data-ttu-id="5a5b9-126">本教學課程假設您已句備下列條件：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-126">This tutorial assumes the following:</span></span>

* <span data-ttu-id="5a5b9-127">您已經有訂閱虛擬機器訂用帳戶的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-127">You already have an Azure account with the virtual machine subscription.</span></span>
* <span data-ttu-id="5a5b9-128">您已安裝 [Azure PowerShell Cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-128">You've installed the [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5a5b9-129">您已非常熟悉內部部署解決方案的 Always On 可用性群組的功能。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="5a5b9-130">如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-to-your-azure-subscription-and-create-the-virtual-network"></a><span data-ttu-id="5a5b9-131">連線至您的 Azure 訂用帳戶並建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5a5b9-131">Connect to your Azure subscription and create the virtual network</span></span>
1. <span data-ttu-id="5a5b9-132">在您本機電腦上的 [PowerShell] 視窗中匯入 Azure 模組，再將發佈設定檔案下載至您的電腦，然後透過匯入所下載的發佈設定，將 PowerShell 工作階段連線至您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-132">In a PowerShell window on your local computer, import the Azure module, download the publishing settings file to your machine, and connect your PowerShell session to your Azure subscription by importing the downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="5a5b9-133">**Get-AzurePublishSettingsFile** 命令會自動產生管理憑證，然後讓 Azure 將該憑證下載至您的電腦。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-133">The **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it to your machine.</span></span> <span data-ttu-id="5a5b9-134">瀏覽器會自動開啟，並提示您輸入 Azure 訂用帳戶的 Microsoft 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-134">A browser is automatically opened, and you're prompted to enter the Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="5a5b9-135">所下載的 **.publishsettings** 檔案包含管理 Azure 訂用帳戶的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-135">The downloaded **.publishsettings** file contains all the information that you need to manage your Azure subscription.</span></span> <span data-ttu-id="5a5b9-136">將此檔案儲存至本機目錄之後，再透過 **Import-AzurePublishSettingsFile** 命令將它匯入。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-136">After saving this file to a local directory, import it by using the **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5a5b9-137">.publishsettings 檔案包含用來管理 Azure 訂用帳戶和服務的認證 (未編碼)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-137">The .publishsettings file contains your credentials (unencoded) that are used to administer your Azure subscriptions and services.</span></span> <span data-ttu-id="5a5b9-138">這個檔案的安全性最佳做法是暫時儲存在來源目錄之外 (例如在 Libraries\Documents 資料夾)，然後在匯入完成後予以刪除。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-138">The security best practice for this file is to store it temporarily outside your source directories (for example, in the Libraries\Documents folder), and then delete it after the import has finished.</span></span> <span data-ttu-id="5a5b9-139">惡意使用者若取得 .publishsettings 檔案的存取權，就可以編輯、建立和刪除您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-139">A malicious user who gains access to the .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="5a5b9-140">定義一系列可用來建立雲端 IT 基礎結構的變數。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-140">Define a series of variables that you'll use to create your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="5a5b9-141">請注意下列事項，以確保稍後執行命令時，能成功發揮作用。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-141">Pay attention to the following to ensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="5a5b9-142">**$storageAccountName** 和 **$dcServiceName** 變數必須獨一無二，因為它們將分別作為雲端儲存體帳戶，和雲端伺服器在網際網路上的身分識別。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used to identify your cloud storage account and cloud server, respectively, on the Internet.</span></span>
   * <span data-ttu-id="5a5b9-143">在稍後您將用到的虛擬網路組態文件中為 **$affinityGroupName** 和 **$virtualNetworkName** 變數指定名稱。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-143">The names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in the virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="5a5b9-144">**$sqlImageName** 指定包含 SQL Server 2012 Service Pack 1 Enterprise Edition 之 VM 映像的更新名稱。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-144">**$sqlImageName** specifies the updated name of the VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="5a5b9-145">為降低複雜性，本教學課程一律使用 **Contoso!000** 作為密碼。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-145">For simplicity, **Contoso!000** is the same password that's used throughout the entire tutorial.</span></span>

3. <span data-ttu-id="5a5b9-146">建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="5a5b9-147">匯入組態檔以建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="5a5b9-148">組態檔包含下列 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-148">The configuration file contains the following XML document.</span></span> <span data-ttu-id="5a5b9-149">簡單來說，它會在稱為 **ContosoAG**的同質群組中指定名為 **ContosoNET** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-149">In brief, it specifies a virtual network called **ContosoNET** in the affinity group called **ContosoAG**.</span></span> <span data-ttu-id="5a5b9-150">它有位址空間 **10.10.0.0/16** 及兩個子網路 **10.10.1.0/24** 和 **10.10.2.0/24**，分別是前端子網路和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-150">It has the address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are the front subnet and back subnet, respectively.</span></span> <span data-ttu-id="5a5b9-151">前端子網路是您可以在其中放置例如 Microsoft SharePoint 之用戶端應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-151">The front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="5a5b9-152">後端子網路是您要在其中放置 SQL Server VM 的位置。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-152">The back subnet is where you'll place the SQL Server VMs.</span></span> <span data-ttu-id="5a5b9-153">如果您先前已變更 **$affinityGroupName** 和 **$virtualNetworkName** 變數，則也必須變更下方的對應名稱。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-153">If you change the **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change the corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="5a5b9-154">建立與您所建立之同質群組相關聯的儲存體帳戶，並將其設為訂用帳戶目前的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-154">Create a storage account that's associated with the affinity group that you created, and set it as the current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="5a5b9-155">建立新雲端服務和可用性設定組中的網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-155">Create the domain controller server in the new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="5a5b9-156">這些已輸送的命令可執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-156">These piped commands do the following things:</span></span>

   * <span data-ttu-id="5a5b9-157">**New-AzureVMConfig** 可建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="5a5b9-158">**Add-AzureProvisioningConfig** 可提供獨立 Windows 伺服器的組態參數。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-158">**Add-AzureProvisioningConfig** gives the configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="5a5b9-159">**Add-AzureDataDisk** 可新增將用於儲存 Active Directory 資料的資料磁碟，該快取選項設為 [無]。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-159">**Add-AzureDataDisk** adds the data disk that you'll use for storing Active Directory data, with the caching option set to None.</span></span>
   * <span data-ttu-id="5a5b9-160">**New-AzureVM** 可建立新的雲端服務，以及在新的雲端服務中建立新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-160">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span>

7. <span data-ttu-id="5a5b9-161">等候系統完整佈建新 VM ，並將遠端桌面檔案下載至您的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-161">Wait for the new VM to be fully provisioned, and download the remote desktop file to your working directory.</span></span> <span data-ttu-id="5a5b9-162">因為佈建新的 Azure VM 需要很長的時間，所以 `while` 迴圈會持續輪詢新的 VM 直到該 VM 準備就緒。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-162">Because the new Azure VM takes a long time to provision, the `while` loop continues to poll the new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="5a5b9-163">現在已成功佈建網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-163">The domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="5a5b9-164">接下來，您將在這個網域控制站伺服器上設定 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-164">Next, you'll configure the Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="5a5b9-165">讓 [PowerShell] 視窗在本機電腦上保持開啟。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-165">Leave the PowerShell window open on your local computer.</span></span> <span data-ttu-id="5a5b9-166">稍後需使用用該視窗建立兩個 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-166">You'll use it again later to create the two SQL Server VMs.</span></span>

## <a name="configure-the-domain-controller"></a><span data-ttu-id="5a5b9-167">設定網域控制站</span><span class="sxs-lookup"><span data-stu-id="5a5b9-167">Configure the domain controller</span></span>
1. <span data-ttu-id="5a5b9-168">啟動遠端桌面檔案，以連線至網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-168">Connect to the domain controller server by launching the remote desktop file.</span></span> <span data-ttu-id="5a5b9-169">使用電腦系統管理員的使用者名稱 AzureAdmin，和建立新 VM 時所指定的密碼 **Contoso!000**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-169">Use the machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created the new VM.</span></span>
2. <span data-ttu-id="5a5b9-170">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="5a5b9-171">執行下列 **DCPROMO.EXE** 命令以設定 **corp.contoso.com** 網域，以及 M 磁碟機上的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-171">Run the following **DCPROMO.EXE** command to set up the **corp.contoso.com** domain, with the data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="5a5b9-172">命令完成後，VM 便會自動重新啟動。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-172">After the command finishes, the VM restarts automatically.</span></span>

4. <span data-ttu-id="5a5b9-173">啟動遠端桌面檔案，再次連線至網域控制站伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-173">Connect to the domain controller server again by launching the remote desktop file.</span></span> <span data-ttu-id="5a5b9-174">這次，改用 **CORP\Administrator** 身分登入。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="5a5b9-175">在系統管理員模式中開啟 [PowerShell] 視窗，並透過下列命令匯入 Active Directory PowerShell 模組：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-175">Open a PowerShell window in administrator mode, and import the Active Directory PowerShell module by using the following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="5a5b9-176">執行下列命令以將三個使用者新增至網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-176">Run the following commands to add three users to the domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="5a5b9-177">**CORP\Install** 可用來設定與 SQL Server 服務執行個體、容錯移轉叢集和可用性群組相關的所有項目。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-177">**CORP\Install** is used to configure everything related to the SQL Server service instances, the failover cluster, and the availability group.</span></span> <span data-ttu-id="5a5b9-178">**CORP\SQLSvc1** 和 **CORP\SQLSvc2** 可作為兩個 SQL Server VM 的 SQL Server 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as the SQL Server service accounts for the two SQL Server VMs.</span></span>
7. <span data-ttu-id="5a5b9-179">接下來，執行下列命令以提供 **CORP\Install** 權限在網域中建立電腦物件。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-179">Next, run the following commands to give **CORP\Install** the permissions to create computer objects in the domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="5a5b9-180">上面指定的 GUID 即是電腦物件類型的 GUID。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-180">The GUID specified above is the GUID for the computer object type.</span></span> <span data-ttu-id="5a5b9-181">**CORP\Install** 帳戶需要**讀取全部內容**和**建立電腦物件**權限，才能建立容錯移轉叢集的 Active Directory 物件。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-181">The **CORP\Install** account needs the **Read All Properties** and **Create Computer Objects** permission to create the Active Direct objects for the failover cluster.</span></span> <span data-ttu-id="5a5b9-182">根據預設，系統已將**讀取所有內容**權限授與 CORP\Install，因此，您不需要明確地授與該權限。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-182">The **Read All Properties** permission is already given to CORP\Install by default, so you don't need to grant it explicitly.</span></span> <span data-ttu-id="5a5b9-183">如需建立容錯移轉叢集所需權限的詳細資訊，請參閱[容錯移轉叢集逐步指南：設定 Active Directory 中的帳戶](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-183">For more information on permissions that are needed to create the failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="5a5b9-184">現在 Active Directory 和使用者物件便已設定完畢，請建立兩個 SQL Server VM，並將這些 VM 加入此網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-184">Now that you've finished configuring Active Directory and the user objects, you'll create two SQL Server VMs and join them to this domain.</span></span>

## <a name="create-the-sql-server-vms"></a><span data-ttu-id="5a5b9-185">建立 SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="5a5b9-185">Create the SQL Server VMs</span></span>
1. <span data-ttu-id="5a5b9-186">繼續使用在本機電腦上開啟的 [PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-186">Continue to use the PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="5a5b9-187">定義下列額外變數：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-187">Define the following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="5a5b9-188">IP 位址 **10.10.0.4** 通常會指派給您在 Azure 虛擬網路之子網路 **10.10.0.0/16** 中建立的第一個 VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-188">The IP address **10.10.0.4** is typically assigned to the first VM that you create in the **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="5a5b9-189">請執行 **IPCONFIG**，以驗證該 IP 位址是否為網域控制站伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-189">You should verify that this is the address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="5a5b9-190">執行下列管道命令來建立容錯移轉叢集中的第一個 VM **ContosoQuorum**：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-190">Run the following piped commands to create the first VM in the failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="5a5b9-191">下列資訊為上述命令的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-191">Note the following regarding the command above:</span></span>

   * <span data-ttu-id="5a5b9-192">**New-AzureVMConfig** 可建立 VM 組態，並將其命名為需要的可用性集合名稱。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-192">**New-AzureVMConfig** creates a VM configuration with the desired availability set name.</span></span> <span data-ttu-id="5a5b9-193">系統會使用相同的可用性設定組名稱命名之後建立的 VM，以便將它們加入相同的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-193">The subsequent VMs will be created with the same availability set name so that they're joined to the same availability set.</span></span>
   * <span data-ttu-id="5a5b9-194">**Add-AzureProvisioningConfig** 可將 VM 加入您所建立的 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-194">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="5a5b9-195">**Set-AzureSubnet** 可將 VM 放在後端子網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-195">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="5a5b9-196">**New-AzureVM** 可建立新的雲端服務，以及在新的雲端服務中建立新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-196">**New-AzureVM** creates a new cloud service and creates the new Azure VM in the new cloud service.</span></span> <span data-ttu-id="5a5b9-197">**DnsSettings** 參數表示新雲端服務中的 DNS 伺服器具有 IP 位址 **10.10.0.4**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-197">The **DnsSettings** parameter specifies that the DNS server for the servers in the new cloud service has the IP address **10.10.0.4**.</span></span> <span data-ttu-id="5a5b9-198">這是網域控制站伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-198">This is the IP address of the domain controller server.</span></span> <span data-ttu-id="5a5b9-199">需使用此參數，才能將雲端服務中的新 VM 成功加入 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-199">This parameter is needed to enable the new VMs in the cloud service to join to the Active Directory domain successfully.</span></span> <span data-ttu-id="5a5b9-200">如果不使用此參數，就必須 在 VM 中手動進行 VM IPv4 設定，以在佈建 VM，並將該 VM 加入 Active Directory 網域後，將網域控制站伺服器作為主要的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-200">Without this parameter, you must manually set the IPv4 settings in your VM to use the domain controller server as the primary DNS server after the VM is provisioned, and then join the VM to the Active Directory domain.</span></span>
3. <span data-ttu-id="5a5b9-201">執行下列已輸送命令以建立名為 **ContosoSQL1** 和 **ContosoSQL2** 的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-201">Run the following piped commands to create the SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="5a5b9-202">下列資訊為上述命令的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-202">Note the following regarding the commands above:</span></span>

   * <span data-ttu-id="5a5b9-203">**New-AzureVMConfig** 可將相同的可用性設定組名稱作為網域控制站伺服器，並在虛擬機器資源庫中使用 SQL Server 2012 Service Pack 1 Enterprise Edition 映像。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-203">**New-AzureVMConfig** uses the same availability set name as the domain controller server, and uses the SQL Server 2012 Service Pack 1 Enterprise Edition image in the virtual machine gallery.</span></span> <span data-ttu-id="5a5b9-204">也可將作業系統磁碟設為唯讀快取 (無寫入快取)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-204">It also sets the operating system disk to read-caching only (no write caching).</span></span> <span data-ttu-id="5a5b9-205">建議您將資料庫檔案移轉至連結至 VM 的獨立資料磁碟，並將該磁碟設為無讀取或寫入快取權限。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-205">We recommend that you migrate the database files to a separate data disk that you attach to the VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="5a5b9-206">由於無法移除作業系統磁碟的讀取快取權限，所以另外一個次佳的作法就是，移除作業系統磁碟的寫入快取權限。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-206">However, the next best thing is to remove write caching on the operating system disk because you can't remove read caching on the operating system disk.</span></span>
   * <span data-ttu-id="5a5b9-207">**Add-AzureProvisioningConfig** 可將 VM 加入您所建立的 Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-207">**Add-AzureProvisioningConfig** joins the VM to the Active Directory domain that you created.</span></span>
   * <span data-ttu-id="5a5b9-208">**Set-AzureSubnet** 可將 VM 放在後端子網路。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-208">**Set-AzureSubnet** places the VM in the back subnet.</span></span>
   * <span data-ttu-id="5a5b9-209">**Add-AzureEndpoint** 可新增存取端點，讓用戶端應用程式得以存取網際網路上的 SQL Server 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on the Internet.</span></span> <span data-ttu-id="5a5b9-210">系統會將不同的通訊埠指派給 ContosoSQL1 和 ContosoSQL2。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-210">Different ports are given to ContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="5a5b9-211">**New-AzureVM** 可在相同的雲端服務中建立新的 SQL Server VM：ContosoQuorum。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-211">**New-AzureVM** creates the new SQL Server VM in the same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="5a5b9-212">若想要讓所有 VM 都位於相同的可用性集合中，您必須將 VM 放置到相同的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-212">You must place the VMs in the same cloud service if you want them to be in the same availability set.</span></span>
4. <span data-ttu-id="5a5b9-213">等候系統完整佈建每個 VM，並將其遠端桌面檔案下載至您的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-213">Wait for each VM to be fully provisioned and for each VM to download its remote desktop file to your working directory.</span></span> <span data-ttu-id="5a5b9-214">`for` 迴圈會針對三個新 VM 分別執行，並針對每個 VM 執行最上層大括弧中的命令。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-214">The `for` loop cycles through the three new VMs and executes the commands inside the top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until the VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="5a5b9-215">現在 SQL Server VM 已完成佈建並執行中，但這些 VM 所安裝的是使用預設值的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-215">The SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-the-failover-cluster-vms"></a><span data-ttu-id="5a5b9-216">初始化容錯移轉叢集 VM</span><span class="sxs-lookup"><span data-stu-id="5a5b9-216">Initialize the failover cluster VMs</span></span>
<span data-ttu-id="5a5b9-217">在本節中，您必須修改將用於容錯移轉叢集和 SQL Server 安裝中的三部伺服器。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-217">In this section, you need to modify the three servers that you'll use in the failover cluster and the SQL Server installation.</span></span> <span data-ttu-id="5a5b9-218">具體而言：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-218">Specifically:</span></span>

* <span data-ttu-id="5a5b9-219">所有伺服器：必須安裝 [容錯移轉叢集] 功能。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-219">All servers: You need to install the **Failover Clustering** feature.</span></span>
* <span data-ttu-id="5a5b9-220">所有伺服器：您必須以電腦**系統管理員**的身分新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-220">All servers: You need to add **CORP\Install** as the machine **administrator**.</span></span>
* <span data-ttu-id="5a5b9-221">僅 ContosoSQL1 和 ContosoSQL2：您必須以預設資料庫中的**系統管理員**角色新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-221">ContosoSQL1 and ContosoSQL2 only: You need to add **CORP\Install** as a **sysadmin** role in the default database.</span></span>
* <span data-ttu-id="5a5b9-222">僅 ContosoSQL1 和 ContosoSQL2：您必須以具備下列權限的登入身分新增 **NT AUTHORITY\System**：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-222">ContosoSQL1 and ContosoSQL2 only: You need to add **NT AUTHORITY\System** as a sign-in with the following permissions:</span></span>

  * <span data-ttu-id="5a5b9-223">更改所有可用性群組</span><span class="sxs-lookup"><span data-stu-id="5a5b9-223">Alter any availability group</span></span>
  * <span data-ttu-id="5a5b9-224">連接 SQL</span><span class="sxs-lookup"><span data-stu-id="5a5b9-224">Connect SQL</span></span>
  * <span data-ttu-id="5a5b9-225">檢視伺服器狀態</span><span class="sxs-lookup"><span data-stu-id="5a5b9-225">View server state</span></span>
* <span data-ttu-id="5a5b9-226">僅 ContosoSQL1 和 ContosoSQL2：SQL Server VM 已啟用 **TCP** 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-226">ContosoSQL1 and ContosoSQL2 only: The **TCP** protocol is already enabled on the SQL Server VM.</span></span> <span data-ttu-id="5a5b9-227">但是，還是必須開啟防火牆以供 SQL Server 進行遠端存取。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-227">However, you still need to open the firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="5a5b9-228">您現在即可準備開始。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-228">Now, you're ready to start.</span></span> <span data-ttu-id="5a5b9-229">先從 **ContosoQuorum**開始，依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-229">Beginning with **ContosoQuorum**, follow the steps below:</span></span>

1. <span data-ttu-id="5a5b9-230">啟動遠端桌面檔案，以連接至 **ContosoQuorum** 。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-230">Connect to **ContosoQuorum** by launching the remote desktop files.</span></span> <span data-ttu-id="5a5b9-231">使用電腦系統管理員的使用者名稱 **AzureAdmin**，和建立 VM 時所指定的密碼 **Contoso!000**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-231">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="5a5b9-232">確認電腦已成功加入至 **corp.contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-232">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="5a5b9-233">等候 SQL Server 安裝完成執行之前自動化的初始化工作，再繼續下一步。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-233">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="5a5b9-234">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="5a5b9-235">安裝 [Windows 容錯移轉叢集] 功能。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-235">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="5a5b9-236">以本機系統管理員的身分新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="5a5b9-237">登出 ContosoQuorum。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="5a5b9-238">此伺服器的相關作業完成。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="5a5b9-239">接下來，初始化 **ContosoSQL1** 和 **ContosoSQL2**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="5a5b9-240">針對兩個 SQL Server VM 執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-240">Follow the steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="5a5b9-241">啟動遠端桌面檔案，以連接至兩個 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-241">Connect to the two SQL Server VMs by launching the remote desktop files.</span></span> <span data-ttu-id="5a5b9-242">使用電腦系統管理員的使用者名稱 **AzureAdmin**，和建立 VM 時所指定的密碼 **Contoso!000**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-242">Use the machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created the VMs.</span></span>
2. <span data-ttu-id="5a5b9-243">確認電腦已成功加入至 **corp.contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-243">Verify that the computers have been successfully joined to **corp.contoso.com**.</span></span>
3. <span data-ttu-id="5a5b9-244">等候 SQL Server 安裝完成執行之前自動化的初始化工作，再繼續下一步。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-244">Wait for the SQL Server installation to finish running the automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="5a5b9-245">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="5a5b9-246">安裝 [Windows 容錯移轉叢集] 功能。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-246">Install the Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="5a5b9-247">以本機系統管理員的身分新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="5a5b9-248">匯入 SQL Server PowerShell 提供者。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-248">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="5a5b9-249">以預設 SQL Server 執行個體的系統管理員角色新增 **CORP\Install**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-249">Add **CORP\Install** as the sysadmin role for the default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="5a5b9-250">以具備上述三項權限的登入身分新增 **NT AUTHORITY\System**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-250">Add **NT AUTHORITY\System** as a sign-in with the three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE TO [NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="5a5b9-251">開啟防火牆以供 SQL Server 進行遠端存取。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-251">Open the firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="5a5b9-252">登出兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="5a5b9-253">準備就緒，可以開始設定可用性群組了。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-253">Finally, you're ready to configure the availability group.</span></span> <span data-ttu-id="5a5b9-254">SQL Server PowerShell 提供者將執行 **ContosoSQL1** 上的所有工作。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-254">You'll use the SQL Server PowerShell Provider to perform all of the work on **ContosoSQL1**.</span></span>

## <a name="configure-the-availability-group"></a><span data-ttu-id="5a5b9-255">設定可用性群組</span><span class="sxs-lookup"><span data-stu-id="5a5b9-255">Configure the availability group</span></span>
1. <span data-ttu-id="5a5b9-256">啟動遠端桌面檔案，以連接至 **ContosoSQL1** 。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-256">Connect to **ContosoSQL1** again by launching the remote desktop files.</span></span> <span data-ttu-id="5a5b9-257">以 **CORP\Install** 身分登入，而不要使用電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-257">Instead of signing in by using the machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="5a5b9-258">在系統管理員模式下開啟 [Azure PowerShell] 視窗。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="5a5b9-259">定義下列變數：</span><span class="sxs-lookup"><span data-stu-id="5a5b9-259">Define the following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="5a5b9-260">匯入 SQL Server PowerShell 提供者。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-260">Import the SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="5a5b9-261">將 ContosoSQL1 的 SQL Server 服務帳戶變更為 CORP\SQLSvc1。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-261">Change the SQL Server service account for ContosoSQL1 to CORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="5a5b9-262">將 ContosoSQL2 的 SQL Server 服務帳戶變更為 CORP\SQLSvc2。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-262">Change the SQL Server service account for ContosoSQL2 to CORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="5a5b9-263">從[在 Azure VM 中建立 Always On 可用性群組的容錯移轉叢集 (英文)](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)，將 **CreateAzureFailoverCluster.ps1** 下載至本機工作目錄。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) to the local working directory.</span></span> <span data-ttu-id="5a5b9-264">您將使用此指令碼來協助您建立功能性容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-264">You'll use this script to help you create a functional failover cluster.</span></span> <span data-ttu-id="5a5b9-265">如需 Windows 容錯移轉叢集如何與 Azure 網路互動的重要資訊，請參閱 [Azure 虛擬機器中的 SQL Server 高可用性和災害復原](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-265">For important information on how Windows Failover Clustering interacts with the Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="5a5b9-266">變更您的工作目錄，並利用下載的指令碼建立容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-266">Change to your working directory and create the failover cluster with the downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="5a5b9-267">在 **ContosoSQL1** 和 **ContosoSQL2** 上，為預設 SQL Server 執行個體啟用 Always On 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-267">Enable Always On availability groups for the default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="5a5b9-268">建立備份目錄，並將權限授與 SQL Server 服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-268">Create a backup directory and grant permissions for the SQL Server service accounts.</span></span> <span data-ttu-id="5a5b9-269">此目錄將用來準備次要複本的可用性資料庫。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-269">You'll use this directory to prepare the availability database on the secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="5a5b9-270">在 **ContosoSQL1** 上建立名稱為 **MyDB1** 的資料庫，同時為它建立完整備份和記錄備份，然後透過 [使用 NORECOVERY] 選項將這些備份還原至 **ContosoSQL2**。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with the **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="5a5b9-271">在 SQL Server VM 上建立可用性群組端點，並在端點上設定適當的權限。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-271">Create the availability group endpoints on the SQL Server VMs and set the proper permissions on the endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] TO [$acct1]" -ServerInstance $server2
13. <span data-ttu-id="5a5b9-272">建立可用性複本。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-272">Create the availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="5a5b9-273">最後，建立可用性群組並將次要複本加入可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-273">Finally, create the availability group and join the secondary replica to the availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="5a5b9-274">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a5b9-274">Next steps</span></span>
<span data-ttu-id="5a5b9-275">現在，您已透過在 Azure 中建立可用性群組的方式，成功實作 SQL Server Always On。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="5a5b9-276">若要為此可用性群組設定接聽程式，請參閱[設定 Azure 中 Always On 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-276">To configure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="5a5b9-277">如需在 Azure 中使用 SQL Server 的其他資訊，請參閱 [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5a5b9-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
