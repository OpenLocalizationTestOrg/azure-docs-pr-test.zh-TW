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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>啟用遠端偵錯時使用持續傳遞 toopublish tooAzure
您可以啟用遠端偵錯在 Azure 中，針對雲端服務或虛擬機器，當您使用[持續傳遞](cloud-services-dotnet-continuous-delivery.md)toopublish tooAzure，依照下列步驟。

## <a name="enabling-remote-debugging-for-cloud-services"></a>對雲端服務啟用遠端偵錯
1. 在上 hello 組建代理程式，設定初始環境的 hello azure 中所述[為 Azure 命令列建置](http://msdn.microsoft.com/library/hh535755.aspx)。
2. 因為需要 hello 套件 hello 遠端偵錯執行階段 (msvsmon.exe)，請安裝 hello **for Visual Studio 遠端工具**。

    * [Remote Tools for Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Remote Tools for Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Remote Tools for Visual Studio 2013 Update 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    或者，您可以從已安裝的 Visual Studio 有系統複製 hello 遠端偵錯二進位檔案。

3. 建立憑證，如 [Azure 雲端服務憑證概觀](cloud-services-certs-create.md)中所述。 保留 hello.pfx 和 RDP 憑證指紋，並上傳 hello 憑證 toohello 目標雲端服務。
4. 使用下列 hello MSBuild 命令列 toobuild 和封裝中的選項，啟用遠端偵錯的 hello。 （取代實際路徑 tooyour 系統和專案檔 hello 角括號的項目）。
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`這 hello 路徑 toohello 資料夾可以包含 msvsmon.exe hello 遠端工具中的 Visual Studio。
    `RemoteDebuggerConnectorVersion`是雲端服務中的 hello Azure SDK 版本。 它也應該符合 hello 版本與 Visual Studio 一起安裝。
5. 使用產生 hello 上一個步驟中的 hello 封裝和.cscfg 檔，以發行 toohello 目標雲端服務。
6. 匯入具有 Visual Studio 和 Azure SDK for.NET 安裝 hello 憑證 （.pfx 檔案） toohello 機器。 請確定 tooimport toohello`CurrentUser\My`憑證存放區，否則 Visual Studio 中的附加 toohello 偵錯工具將會失敗。

## <a name="enabling-remote-debugging-for-virtual-machines"></a>對虛擬機器啟用遠端偵錯
1. 建立 Azure 虛擬機器。 請參閱[建立執行 Windows Server 的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)或[在 Visual Studio 中建立及管理 Azure 虛擬機器](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
2. 在 hello [Azure 傳統入口網站頁面](http://go.microsoft.com/fwlink/p/?LinkID=269851)，檢視 hello 虛擬機器的儀表板 toosee hello 虛擬機器的**RDP 憑證指紋**。 這個值用於 hello `ServerThumbprint` hello 延伸模組設定中的值。
3. 建立用戶端憑證中所述[Azure 雲端服務憑證概觀](cloud-services-certs-create.md)（保持 hello.pfx 和 RDP 憑證指紋）。
4. 安裝 Azure Powershell (版本為 0.7.4 或更新版本) 中所述[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
5. 執行下列指令碼 tooenable hello RemoteDebug 延伸 hello。 Hello 路徑和個人資料以取代您自己的資源，例如您的訂用帳戶名稱、 服務名稱和指紋。
   
   > [!NOTE]
   > 此指令碼是針對 Visual Studio 2015 所設計。 如果您使用 Visual Studio 2013 或 Visual Studio 2017，修改 hello`$referenceName`和`$extensionName`指派下列太`RemoteDebugVS2013`或`RemoteDebugVS2017`。

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

6. 匯入具有 Visual Studio 和 Azure SDK for.NET 安裝 hello 憑證 (.pfx) toohello 機器。

