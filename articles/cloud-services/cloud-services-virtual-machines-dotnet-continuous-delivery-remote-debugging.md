---
title: "對持續傳遞啟用遠端偵錯 | Microsoft Docs"
description: "了解在使用連續傳遞來部署至 Azure 時如何啟用遠端偵錯"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="56cf0-103">使用連續傳遞來發行至 Azure 時啟用遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="56cf0-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="56cf0-104">當您使用 [連續傳遞](cloud-services-dotnet-continuous-delivery.md) 來發行至 Azure 時，您可以依照下列步驟在 Azure 中為雲端服務或虛擬機器啟用遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="56cf0-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="56cf0-105">對雲端服務啟用遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="56cf0-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="56cf0-106">在組建代理程式上，設定 Azure 的初始環境，如 [Azure 的命令列建置](http://msdn.microsoft.com/library/hh535755.aspx)所述。</span><span class="sxs-lookup"><span data-stu-id="56cf0-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="56cf0-107">因為封裝需要遠端偵錯執行階段 (msvsmon.exe)，請安裝 **Remote Tools for Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="56cf0-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="56cf0-108">Remote Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="56cf0-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="56cf0-109">Remote Tools for Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="56cf0-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="56cf0-110">Remote Tools for Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="56cf0-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="56cf0-111">或者，您也可以從已安裝 Visual Studio 的系統中複製遠端偵錯二進位檔案。</span><span class="sxs-lookup"><span data-stu-id="56cf0-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="56cf0-112">建立憑證，如 [Azure 雲端服務憑證概觀](cloud-services-certs-create.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="56cf0-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="56cf0-113">保留 .pfx 和 RDP 憑證指紋，並將憑證上傳至目標雲端服務。</span><span class="sxs-lookup"><span data-stu-id="56cf0-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="56cf0-114">在 MSBuild 命令列中使用下列選項，指定啟用遠端偵測來建置和封裝</span><span class="sxs-lookup"><span data-stu-id="56cf0-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="56cf0-115">(以系統和專案檔案的實際路徑替代角括弧括住的項目)。</span><span class="sxs-lookup"><span data-stu-id="56cf0-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="56cf0-116">`VSX64RemoteDebuggerPath` 是存放 Visual Studio 遠端工具中 msvsmon.exe 的資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="56cf0-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="56cf0-117">`RemoteDebuggerConnectorVersion` 是雲端服務中的 Azure SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="56cf0-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="56cf0-118">它也應符合隨 Visual Studio 一起安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="56cf0-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="56cf0-119">使用前一個步驟中產生的封裝和 .cscfg 檔案來發行至目標雲端服務。</span><span class="sxs-lookup"><span data-stu-id="56cf0-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="56cf0-120">將憑證匯入 (.pfx file) 已安裝包含 Azure SDK for .NET 的 Visual Studio  的機器。</span><span class="sxs-lookup"><span data-stu-id="56cf0-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="56cf0-121">請務必匯入至 `CurrentUser\My` 憑證存放區，否則附加至 Visual Studio 中的偵錯工具將會失敗。</span><span class="sxs-lookup"><span data-stu-id="56cf0-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="56cf0-122">對虛擬機器啟用遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="56cf0-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="56cf0-123">建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="56cf0-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="56cf0-124">請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[在 Visual Studio 中建立及管理 Azure 虛擬機器](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="56cf0-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="56cf0-125">在 [Azure 傳統入口網站頁面](http://go.microsoft.com/fwlink/p/?LinkID=269851)，檢視虛擬機器儀表板來查看虛擬機器的 **RDP 憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="56cf0-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="56cf0-126">此值是用於延伸模組組態中的 `ServerThumbprint` 值。</span><span class="sxs-lookup"><span data-stu-id="56cf0-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="56cf0-127">建立用戶端憑證，如 [Azure 雲端服務憑證概觀](cloud-services-certs-create.md) 中所述 (保留 .pfx 和 RDP 憑證指紋)。</span><span class="sxs-lookup"><span data-stu-id="56cf0-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="56cf0-128">如 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)中所述安裝 Azure Powershell (0.7.4 版或更新版本)</span><span class="sxs-lookup"><span data-stu-id="56cf0-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="56cf0-129">執行下列指令碼來啟用 RemoteDebug 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="56cf0-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="56cf0-130">將路徑和個人資料替換成您自己的路徑和個人資料，例如您的訂用帳戶、服務名稱和指紋。</span><span class="sxs-lookup"><span data-stu-id="56cf0-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="56cf0-131">此指令碼是針對 Visual Studio 2015 所設計。</span><span class="sxs-lookup"><span data-stu-id="56cf0-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="56cf0-132">如果您使用 Visual Studio 2013 或 Visual Studio 2017，請將以下的 `$referenceName` 和 `$extensionName` 指派修改為 `RemoteDebugVS2013` 或 `RemoteDebugVS2017`。</span><span class="sxs-lookup"><span data-stu-id="56cf0-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="56cf0-133">將憑證 (.pfx) 匯入已安裝 Visual Studio with Azure SDK for .NET 的機器。</span><span class="sxs-lookup"><span data-stu-id="56cf0-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

