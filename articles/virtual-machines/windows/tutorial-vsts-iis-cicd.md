---
title: "aaaCreate CI/CD 中的管線 Team Services 與 Azure |Microsoft 文件"
description: "了解 toocreate Visual Studio Team Services 的持續整合及部署 web 應用程式 tooIIS Windows VM 上的傳送管線的方式"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a>使用 Visual Studio Team Services 和 IIS 建立持續整合管線
tooautomate hello 建置、 測試及部署應用程式開發階段，您可以使用持續整合和部署 (CI/CD) 管線。 在本教學課程中，您可以使用 Visual Studio Team Services 以及 Azure 中執行 IIS 的 Windows 虛擬機器 (VM) 建立 CI/CD 管線。 您會了解如何：

> [!div class="checklist"]
> * 發佈 ASP.NET web 應用程式 tooa Team Services 專案
> * 建立以程式碼認可所觸發的組建定義
> * 在 Azure 的虛擬機器上安裝和設定 IIS
> * 在 Team Services 中加入 hello IIS 執行個體 tooa 部署群組
> * 建立發行定義 toopublish 新 web 部署套件 tooIIS
> * 測試 hello CI/CD 管線

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行`Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。


## <a name="create-project-in-team-services"></a>在 Team Services 中建立專案
Visual Studio Team Services 可讓您進行簡單的共同作業與開發，不需要維護內部部署的程式碼管理解決方案。 Team Services 提供雲端的程式碼測試、組建和 Application Insights。 您可以選擇版本控制存放庫和最符合您的程式碼開發的整合式開發環境 (IDE)。 此教學課程中，您可以使用免費帳戶 toocreate 基本的 ASP.NET web 應用程式和 CI/CD 管線。 如果您還沒有 Team Services 帳戶，請[建立帳戶](http://go.microsoft.com/fwlink/?LinkId=307137)。

toomanage hello 程式碼認可程序，組建定義，並發行定義建立專案、 Team Services 中，如下所示：

1. 在 Web 瀏覽器中開啟 Team Services 儀表板，選擇 [新增專案]。
2. 輸入*myWebApp* hello**專案名稱**。 保留所有其他預設值 toouse *Git*版本控制和*Agile*工作項目處理序。
3. 選擇 hello 太**分享***小組成員*，然後選取**建立**。
5. 一旦建立您的專案，選擇 hello 選項太**初始化與讀我檔案或 gitignore**，然後**初始化**。
6. 在新專案，選擇 **儀表板**hello 頂端，然後選取**Visual Studio 中開啟**。


## <a name="create-aspnet-web-application"></a>建立 ASP.NET Web 應用程式
在 hello 先前步驟中，您可以建立 Team Services 中的專案。 hello 最後一個步驟會在 Visual Studio 中開啟新的專案。 管理您的程式碼中的認可 hello **Team Explorer**視窗。 建立新專案的本機副本，然後從範本建立 ASP.NET web 應用程式，如下所示︰

1. 選取**複製**toocreate Team Services 專案的本機 git 儲存機制。
    
    ![從 Team Services 專案複製存放庫](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. 在 [解決方案] 下，選取 [新增]。

    ![建立 Web 應用程式解決方案](media/tutorial-vsts-iis-cicd/new_solution.png)

3. 選取**Web**範本，然後選擇 hello **ASP.NET Web 應用程式**範本。
    1. 輸入您的應用程式的名稱，例如*myWebApp*，並取消核取方塊 hello**為方案建立目錄**。
    2. Hello 選項是否可用，取消核取方塊 hello 太**加入 Application Insights tooproject**。 Application Insights 需要您 tooauthorize Azure Application Insights web 應用程式。 tookeep 簡單在本教學課程中，它略過此程序。
    3. 選取 [確定] 。
4. 選擇**MVC** hello 範本清單中。
    1. 選擇 [變更驗證]，選擇 [不需要驗證]，然後選取 [確定]。
    2. 選取**確定**toocreate 您的方案。
5. 在 hello **Team Explorer**視窗中，選擇**變更**。

    ![認可本機變更 tooTeam 服務 git 儲存機制](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. 在 hello [認可] 文字方塊中輸入訊息例如*初始認可*。 選擇**全部認可並同步處理**從 hello 下拉式選單。


## <a name="create-build-definition"></a>建立組建定義
在 Team Services 中，您可以使用組建定義 toooutline 建置您的應用程式的方式。 在本教學課程中，我們會建立基本的定義會使用我們的原始程式碼，建置 hello 的解決方案，然後建立 web 部署套件，我們可以在 IIS 伺服器上使用 toorun hello web 應用程式。

1. 在您的 Team Services 專案，選擇 **建置和發行**hello 頂端，然後選取**建置**。
3. 選取 [+新增定義]。
4. 選擇 hello **ASP.NET （預覽）**範本，然後選取**套用**。
5. 保留所有 hello 預設工作的值。 在下**取得來源**，確保該 hello *myWebApp*儲存機制和*主要*會選取分支。

    ![在 Visual Studio Team Services 中建立組建定義](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. 在 hello**觸發程序**索引標籤上，移動 hello 滑桿**啟用此觸發程序**太*啟用*。
7. 儲存 hello 組建定義和佇列新組建選取**儲存，並佇列**，然後**儲存，並佇列**一次。 保留 hello 預設值，然後選取**佇列**。

監看式當 hello 建置排定在託管的代理程式，然後開始 toobuild。 hello 輸出是 toohello 類似下列範例程式碼：

![Team Services 專案的成功組建](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a>Create virtual machine
平台 toorun tooprovide ASP.NET web 應用程式，您需要執行 IIS 的 Windows 虛擬機器。 Team Services 會使用代理程式 toointeract hello IIS 執行個體認可程式碼，並觸發組建。

使用[此指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json)建立 Windows Server 2016 VM。 它會採用 hello 指令碼 toorun 幾分鐘，並建立 hello VM。 一旦建立 hello VM 之後，開啟的通訊埠 80 web 流量[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) ，如下所示：

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

tooconnect tooyour VM，取得與 hello 公用 IP 位址[Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) ，如下所示：

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

建立遠端桌面工作階段 tooyour VM:

```cmd
mstsc /v:<publicIpAddress>
```

開啟 hello VM，**系統管理員 PowerShell**命令提示字元。 安裝 IIS 和所需的 .NET 功能，如下所示︰

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a>建立部署群組
toopush 出 hello web 部署封裝 toohello IIS 伺服器，您在 Team Services 中定義部署群組。 此群組可讓您的伺服器是新組建的 hello 目標認可完成服務和組建的程式碼 tooTeam toospecify。

1. 在 Team Services 中，選擇 [組建及發行]，然後選取 [部署群組]。
2. 選擇 [新增部署群組]。
3. 輸入 hello 群組的名稱，例如*myIIS*，然後選取**建立**。
4. 在 hello**登錄機器**區段中，確定*Windows*選取，則核取 hello 方塊太**hello 指令碼中的個人存取權杖用於驗證**。
5. 選取**複製指令碼 tooclipboard**。


### <a name="add-iis-vm-toohello-deployment-group"></a>新增 IIS VM toohello 部署群組
透過建立 hello 部署群組，將每個 IIS 執行個體 toohello 群組。 Team Services 產生的指令碼下載並設定代理程式上 hello VM 接收新的 web 部署封裝，然後將它套用 tooIIS。

1. 在 hello**系統管理員 PowerShell**貼上您的 VM 上的工作階段，並執行 Team Services 從複製的 hello 指令碼。
2. 當提示的 tooconfigure 標記 hello 代理程式，選擇*Y*輸入*web*。
3. 當提示 hello 使用者帳戶，請按*傳回*tooaccept hello 預設值。
4. 等候 hello 訊息的指令碼 toofinish *vstsagent.account.computername 服務已順利啟動*。
5. 在 hello**部署群組**頁面 hello**建置和發行**功能表中，開啟 hello *myIIS*部署群組。 在 hello**機器**索引標籤上，確認已列出您的 VM。

    ![VM 成功加入 tooTeam 服務部署群組](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a>建立發行定義
toopublish 組建，您的發行定義中建立 Team Services。 您的應用程式的成功組建會自動觸發此定義。 您選擇 hello 部署群組 toopush 您的 web deploy 封裝，並定義 hello 適當的 IIS 設定。

1. 選擇 [組建及發行]，然後選取 [組建]。 選擇 hello 先前步驟中建立的組建定義。
2. 在下**最近完成**，請選擇 hello 最新的組建，然後選取**發行**。
3. 選擇**是**toocreate 發行定義。
4. 選擇 hello**空**範本，然後選取**下一步**。
5. 請確認 hello 專案和來源組建定義就會填入您的專案。
6. 選取 hello**連續部署**核取方塊，然後選取 **建立**。
7. 選取 hello 下拉式方塊旁邊太**+ 加入工作**選擇*新增部署群組階段*。
    
    ![在 Team Services 中加入工作 toorelease 定義](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. 選擇**新增**下一步太**IIS Web 應用程式 Deploy(Preview)**，然後選取**關閉**。
9. 選取 hello**部署群組上執行**父工作。
    1. 如**部署群組**，選取 hello 部署群組，您建立更早版本，例如*myIIS*。
    2. 在 hello**機器標記**方塊中，選取**新增**選擇 hello *web*標記。
    
    ![用於 IIS 的發行定義部署群組工作](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. 選取 hello**部署： IIS Web 應用程式部署**工作 tooconfigure IIS 執行個體的設定，如下所示：
    1. 在 [網站名稱] 輸入 Default Web Site。
    2. 保留所有 hello 其他預設設定。
12. 選擇 [儲存]，然後選取 [確定] 兩次。


## <a name="create-a-release-and-publish"></a>建立發行並發佈
您現在可以將您的 Web 部署套件當做新發行加以推送。 此步驟中進行通訊的每個執行個體是 hello 部署群組的一部分，將推入 hello web hello 代理程式部署套件，然後設定 IIS toorun hello 更新 web 應用程式。

1. 在您的發行定義中，選取 [+ 發行]，然後選擇 [建立發行]。
2. 確認 hello 最新組建在 hello 下拉式清單中，選取連同**自動部署： 建立版本之後**。 選取 [ **建立**]。
3. 小型橫幅會顯示您的發行定義的 hello 頂端像是*發行 ' Release 1' 已建立*。 選取 hello 發行連結。
4. 開啟 hello**記錄**toowatch hello 發行進度索引標籤上。
    
    ![成功的 Team Services 發行和 Web 部署封裝推送](media/tutorial-vsts-iis-cicd/successful_release.png)

5. Hello 發行完成之後，請開啟網頁瀏覽器，並輸入您的 VM hello 公用 IIP 位址。 您的 ASP.NET Web 應用程式正在執行。

    ![IIS VM 上執行的 ASP.NET Web 應用程式](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a>測試 hello 整個 CI/CD 管線
在 IIS 上執行您 web 應用程式，現在請 hello 整個 CI/CD 管線。 您在 Visual Studio 和認可您的程式碼，組建就會觸發然後觸發更新 web 的版本進行變更後將部署套件 tooIIS:

1. 在 Visual Studio 中，開啟 [hello**方案總管] 中**視窗。
2. 瀏覽 tooand 開啟*myWebApp |檢視 |首頁 |Index.cshtml*
3. 編輯第 6 行 tooread:

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. 儲存 hello 檔案。
5. 開啟 hello **Team Explorer**視窗中，選取 hello *myWebApp*專案，然後選擇 **變更**。
6. 輸入 「 認可 」 訊息，例如*測試 CI/CD 管線*，然後選擇 **認可所有和同步處理**從 hello 下拉式選單。
7. Team Services 工作區中，則會從 hello 程式碼認可觸發新組建。 
    - 選擇 [組建及發行]，然後選取 [組建]。 
    - 選擇您的組建定義，然後選取 hello**排入佇列 （&) 執行**hello 為組建 toowatch 建置進行時。
9. Hello 建置成功之後，就會觸發新的版本。
    - 選擇**建置和發行**，然後**版本**toosee hello web deploy 封裝推入 tooyour IIS VM。 
    - 選取 hello**重新整理**圖示 tooupdate hello 狀態。 當 hello*環境*欄會顯示綠色的核取記號，hello 版本已成功部署 tooIIS。
11. toosee 套用您的變更，請重新整理您的瀏覽器中的 IIS 網站。

    ![從 CI/CD 管線在 IIS VM 上執行的 ASP.NET Web 應用程式](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a>後續步驟

在本教學課程中，您在 Team Services 中建立 ASP.NET web 應用程式和設定的組建和發行定義 toodeploy 新 web deploy 封裝 tooIIS 在每個程式碼認可。 您已了解如何︰

> [!div class="checklist"]
> * 發佈 ASP.NET web 應用程式 tooa Team Services 專案
> * 建立以程式碼認可所觸發的組建定義
> * 在 Azure 的虛擬機器上安裝和設定 IIS
> * 在 Team Services 中加入 hello IIS 執行個體 tooa 部署群組
> * 建立發行定義 toopublish 新 web 部署套件 tooIIS
> * 測試 hello CI/CD 管線

如何前進 toohello 下一個教學課程 toolearn toosecure web 伺服器使用 SSL 憑證。

> [!div class="nextstepaction"]
> [使用 SSL 保護網路伺服器](tutorial-secure-web-server.md)