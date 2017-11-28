---
title: "遠端偵錯持續傳遞 aaaEnable |Microsoft 文件"
description: "深入了解如何 tooenable 遠端偵錯時使用持續傳遞 toodeploy tooAzure"
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
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="250f1-103">啟用遠端偵錯時使用持續傳遞 toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="250f1-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="250f1-104">您可以啟用遠端偵錯在 Azure 中，針對雲端服務或虛擬機器，當您使用[持續傳遞](cloud-services-dotnet-continuous-delivery.md)toopublish tooAzure，依照下列步驟。</span><span class="sxs-lookup"><span data-stu-id="250f1-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="250f1-105">對雲端服務啟用遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="250f1-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="250f1-106">在上 hello 組建代理程式，設定初始環境的 hello azure 中所述[為 Azure 命令列建置](http://msdn.microsoft.com/library/hh535755.aspx)。</span><span class="sxs-lookup"><span data-stu-id="250f1-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="250f1-107">因為需要 hello 套件 hello 遠端偵錯執行階段 (msvsmon.exe)，請安裝 hello **for Visual Studio 遠端工具**。</span><span class="sxs-lookup"><span data-stu-id="250f1-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="250f1-108">Remote Tools for Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="250f1-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="250f1-109">Remote Tools for Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="250f1-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="250f1-110">Remote Tools for Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="250f1-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="250f1-111">或者，您可以從已安裝的 Visual Studio 有系統複製 hello 遠端偵錯二進位檔案。</span><span class="sxs-lookup"><span data-stu-id="250f1-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="250f1-112">建立憑證，如 [Azure 雲端服務憑證概觀](cloud-services-certs-create.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="250f1-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="250f1-113">保留 hello.pfx 和 RDP 憑證指紋，並上傳 hello 憑證 toohello 目標雲端服務。</span><span class="sxs-lookup"><span data-stu-id="250f1-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="250f1-114">使用下列 hello MSBuild 命令列 toobuild 和封裝中的選項，啟用遠端偵錯的 hello。</span><span class="sxs-lookup"><span data-stu-id="250f1-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="250f1-115">（取代實際路徑 tooyour 系統和專案檔 hello 角括號的項目）。</span><span class="sxs-lookup"><span data-stu-id="250f1-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="250f1-116">`VSX64RemoteDebuggerPath`這 hello 路徑 toohello 資料夾可以包含 msvsmon.exe hello 遠端工具中的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="250f1-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="250f1-117">`RemoteDebuggerConnectorVersion`是雲端服務中的 hello Azure SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="250f1-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="250f1-118">它也應該符合 hello 版本與 Visual Studio 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="250f1-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="250f1-119">使用產生 hello 上一個步驟中的 hello 封裝和.cscfg 檔，以發行 toohello 目標雲端服務。</span><span class="sxs-lookup"><span data-stu-id="250f1-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="250f1-120">匯入具有 Visual Studio 和 Azure SDK for.NET 安裝 hello 憑證 （.pfx 檔案） toohello 機器。</span><span class="sxs-lookup"><span data-stu-id="250f1-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="250f1-121">請確定 tooimport toohello`CurrentUser\My`憑證存放區，否則 Visual Studio 中的附加 toohello 偵錯工具將會失敗。</span><span class="sxs-lookup"><span data-stu-id="250f1-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="250f1-122">對虛擬機器啟用遠端偵錯</span><span class="sxs-lookup"><span data-stu-id="250f1-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="250f1-123">建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="250f1-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="250f1-124">請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[在 Visual Studio 中建立及管理 Azure 虛擬機器](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="250f1-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="250f1-125">在 hello [Azure 傳統入口網站頁面](http://go.microsoft.com/fwlink/p/?LinkID=269851)，檢視 hello 虛擬機器的儀表板 toosee hello 虛擬機器的**RDP 憑證指紋**。</span><span class="sxs-lookup"><span data-stu-id="250f1-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="250f1-126">這個值用於 hello `ServerThumbprint` hello 延伸模組設定中的值。</span><span class="sxs-lookup"><span data-stu-id="250f1-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="250f1-127">建立用戶端憑證中所述[Azure 雲端服務憑證概觀](cloud-services-certs-create.md)（保持 hello.pfx 和 RDP 憑證指紋）。</span><span class="sxs-lookup"><span data-stu-id="250f1-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="250f1-128">安裝 Azure Powershell (版本為 0.7.4 或更新版本) 中所述[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="250f1-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="250f1-129">執行下列指令碼 tooenable hello RemoteDebug 延伸 hello。</span><span class="sxs-lookup"><span data-stu-id="250f1-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="250f1-130">Hello 路徑和個人資料以取代您自己的資源，例如您的訂用帳戶名稱、 服務名稱和指紋。</span><span class="sxs-lookup"><span data-stu-id="250f1-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="250f1-131">此指令碼是針對 Visual Studio 2015 所設計。</span><span class="sxs-lookup"><span data-stu-id="250f1-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="250f1-132">如果您使用 Visual Studio 2013 或 Visual Studio 2017，修改 hello`$referenceName`和`$extensionName`指派下列太`RemoteDebugVS2013`或`RemoteDebugVS2017`。</span><span class="sxs-lookup"><span data-stu-id="250f1-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="250f1-133">匯入具有 Visual Studio 和 Azure SDK for.NET 安裝 hello 憑證 (.pfx) toohello 機器。</span><span class="sxs-lookup"><span data-stu-id="250f1-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

