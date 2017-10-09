---
title: "aaaAzure 自動化 DSC 連續部署 Chocolatey |Microsoft 文件"
description: "使用 Azure 自動化 DSC 和 Chocolatey 封裝管理員執行 DevOps 持續部署。  具有完整 JSON ARM 範本與 PowerShell 原始檔的範例。"
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: c0baa411-eb76-4f91-8d14-68f68b4805b6
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/29/2016
ms.author: golive
ms.openlocfilehash: 60af52af5f834fd48e3a0dc4677919397b53f0f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="usage-example-continuous-deployment-toovirtual-machines-using-automation-dsc-and-chocolatey"></a>使用範例： 連續部署 tooVirtual 的電腦上使用 Automation DSC 和 Chocolatey
DevOps 世界中有許多工具 tooassist 與 hello 連續整合管線中的各種點。  Azure 自動化 Desired State Configuration (DSC) 是  褖畫惎新加法 toohello 選項可以採用 DevOps 小組。  本文示範如何為 Windows 電腦設定持續部署 (CD)。  您可以輕鬆地擴充 hello 技術 tooinclude 視 hello 角色 （該網站，例如），並從該處 tooadditional 一樣多的 Windows 電腦以及角色。

![IaaS VM 的持續部署](./media/automation-dsc-cd-chocolatey/cdforiaasvm.png)

## <a name="at-a-high-level"></a>概括而言
這裡要進行的事項很多，幸好，大致上可分成兩個主要程序： 

* 撰寫程式碼以及測試、 建立和發行 hello 系統的主要和次要版本的安裝套件。 
* 建立和管理 Vm 將安裝及執行 hello 封裝中的 hello 程式碼。  

一旦這些核心程序都備妥，就會是簡短步驟 tooautomatically 更新 hello 封裝建立和部署新版本時，任何特定 VM 上執行。

## <a name="component-overview"></a>元件概觀
例如，封裝管理員[apt get](https://en.wikipedia.org/wiki/Advanced_Packaging_Tool)位於相當已知 hello Linux 世界中，但卻未這麼 hello Windows 世界中。  [Chocolatey](https://chocolatey.org/)是這類的作業和 Scott Hanselman[部落格](http://www.hanselman.com/blog/IsTheWindowsUserReadyForAptget.aspx)hello 上主題是絕佳的簡介。  簡而言之，Chocolatey 可讓您 tooinstall 套件從套件的中央儲存機制使用 hello 命令列的 Windows 系統。  您可以建立和管理您自己的儲存機制，而 Chocolatey 可以從您指定的任何數量的儲存機制來安裝封裝。

預期狀態設定 (DSC) ([概觀](https://technet.microsoft.com/library/dn249912.aspx)) 是一種 PowerShell 工具，可讓您 toodeclare hello 組態所要的電腦。  例如，您可以說「我想要安裝 Chocolatey、我想要安裝 IIS、我想要開啟連接埠 80、我想要安裝網站 1.0.0 版」。  hello DSC 本機設定管理員 (LCM) 實作該組態。 DSC 提取伺服器有一個儲存機制保存您電腦的組態。 如果其組態符合 hello 儲存的組態中定期 toosee 會檢查每部機器上的 LCM hello。 它可以報告的狀態，或嘗試 toobring hello 機器回負有 hello 儲存的組態。 您可以編輯 hello 預存的組態在 hello 提取伺服器 toocause 機器或機器 toocome 一組負有 hello 變更組態。

Azure 自動化是 Microsoft azure 可讓您 tooautomate 各種工作，使用 runbook、 節點、 認證、 資源和資產，例如排程和全域變數中受管理的服務。 Azure 自動化 DSC 擴充功能 tooinclude PowerShell DSC 工具的這項自動化。  以下提供清楚的 [概觀](automation-dsc-overview.md)。

DSC 資源是具有特定功能的程式碼模組，例如管理網路、Active Directory 或 SQL Server。  hello Chocolatey DSC 資源知道如何 tooaccess NuGet 伺服器 （和其他項目），下載的封裝、 安裝封裝，等等。  Hello 中有許多其他的 DSC 資源[PowerShell 資源庫](http://www.powershellgallery.com/packages?q=dsc+resources&prerelease=&sortOrder=package-title)。  這些模組安裝到您的 Azure 自動化 DSC 提取伺服器 (由您安裝)，供您的組態使用。

Resource Manager 範本以宣告方式產生基礎結構，例如網路、子網路、網路安全性和路由、負載平衡器、NIC、VM...等等。  以下是[文章](../azure-resource-manager/resource-manager-deployment-model.md)比較 hello Resource Manager 部署模型 （宣告式），以 hello Azure 服務管理 （ASM 或傳統） 部署模型 （必要），並討論 hello 核心資源提供者、 計算，儲存體和網路。

資源管理員範本的一項重要功能已佈建為其能力 tooinstall 到 hello VM 的 VM 延伸模組。  VM 延伸模組具有特定功能，例如執行自訂指令碼、安裝防毒軟體或執行 DSC 組態指令碼。  有許多其他類型的 VM 延伸模組。

## <a name="quick-trip-around-hello-diagram"></a>快速路線 hello 圖表
在 hello 最上方開始，撰寫程式碼、 建置及測試，然後建立安裝套件。  Chocolatey 可以處理各種類型的安裝封裝，例如 MSI、MSU、ZIP 等。  而且您擁有 hello 的 PowerShell toodo hello 實際安裝的完整功能，如果 Chocolatey 的原生功能相當不 tooit。  將 hello 封裝放入某個位置連線 – 封裝儲存機制。  這個使用範例使用 Azure blob 儲存體帳戶中的公用資料夾，但可以是任何位置。  Chocolatey 可自然搭配 NuGet 伺服器和其他一些工具，一起管理封裝中繼資料。  [這篇文章](https://github.com/chocolatey/choco/wiki/How-To-Host-Feed)描述 hello 選項。  這個使用範例使用 NuGet。  Nuspec 是封裝的中繼資料。  hello Nuspec"編譯 」 成 NuPkg 的而且儲存在 NuGet 伺服器。  當您的設定要求套件的名稱，參考的 NuGet 伺服器 hello Chocolatey DSC 資源 （現在在 hello VM) grabs 示範的 hello 封裝，並將它安裝為您。  您也可以要求特定版本的封裝。

Hello 左下方 hello 圖片，在沒有 Azure 資源管理員 (ARM) 範本。  在此使用方式範例中，hello VM 延伸模組會註冊 hello VM 以 hello Azure Automation DSC 提取伺服器 （也就是提取伺服器） 做為節點。  hello 組態儲存在 hello 提取伺服器。  實際上儲存兩次：一次儲存為純文字，另一次編譯成 MOF 檔案 (適用於對此有所瞭解的人。)在 hello 入口網站 hello MOF 為 「 節點設定 」 （相對於 toosimply 「 設定 」)。  它的 hello 成品所知 hello 節點將其設定與節點相關聯。  下列詳細資料會顯示如何 tooassign hello 節點組態 toohello 節點。

假定您已進行 hello 元 hello 頂端或大部分。  小型的項目是建立 hello nuspec、 編譯，以及將其儲存至 NuGet 伺服器。  您已經在管理 VM。  取得下一個步驟 toocontinuous 部署 hello 需要設定 hello 提取伺服器 （一次），註冊您的節點與其 （一次），並建立及儲存 hello 組態那里 （一開始）。  然後當升級封裝，而且部署 toohello 儲存機制上，重新整理 hello 組態和節點組態 hello 提取伺服器 （視需要重複）。

如果不是從 ARM 範本開始，也沒關係。  有 PowerShell cmdlet 設計 toohelp hello 提取伺服器與所有 hello rest 中都註冊您的 Vm。 如需祥氣資訊，請參閱下列文章： [上架由 Azure 自動化 DSC 管理的機器](automation-dsc-onboarding.md)

## <a name="step-1-setting-up-hello-pull-server-and-automation-account"></a>步驟 1： 設定 hello 提取伺服器與自動化帳戶
在已驗證的 (新增 AzureRmAccount) PowerShell 命令列: （可能需要幾分鐘的時間 hello 提取伺服器設定時）

    New-AzureRmResourceGroup –Name MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES
    New-AzureRmAutomationAccount –ResourceGroupName MY-AUTOMATION-RG –Location MY-RG-LOCATION-IN-QUOTES –Name MY-AUTOMATION-ACCOUNT 

您可以將您的自動化帳戶的下列區域 （也稱為位置） 的 hello 任何： 美國東部 2、 美國中南部、 美國 Gov 維吉尼亞州、 西歐、 東南亞、 日本東部、 印度中部和澳洲東南部，加拿大的中央，北歐。

## <a name="step-2-vm-extension-tweaks-toohello-arm-template"></a>步驟 2: VM 延伸模組做調整 toohello ARM 範本
VM 註冊 （使用 hello PowerShell DSC VM 延伸模組） 在此提供詳細資料[Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates/tree/master/dsc-extension-azure-automation-pullserver)。  此步驟中使用 DSC 節點 hello 清單中的 hello 提取伺服器註冊新的 VM。  此登錄的一部分指定 hello 節點組態套用的 toobe toohello 節點。  此節點設定 tooexist 尚未具有在 hello 提取伺服器，因此它的步驟 4，這基於 hello 第一次 [確定]。  不過，這裡在步驟 2 中您需要 toohave 決定的 hello hello 節點名稱和 hello hello 組態名稱。  在此使用範例，hello 節點是 'isvbox' 而 hello 組態是 'ISVBoxConfig'。  Hello 節點設定名稱 (toobe DeploymentTemplate.json 中指定) 是 'ISVBoxConfig.isvbox'。  

## <a name="step-3-adding-required-dsc-resources-toohello-pull-server"></a>步驟 3： 加入必要的 DSC 資源 toohello 提取伺服器
hello PowerShell 資源庫是已經過檢測的 tooinstall DSC 資源到您的 Azure 自動化帳戶。  瀏覽 toohello 資源，然後按一下 hello 」 部署 tooAzure 自動化 」 按鈕。

![PowerShell 資源庫範例](./media/automation-dsc-cd-chocolatey/xNetworking.PNG)

另一種技術最近才新增 toohello Azure 入口網站可讓您 toopull 新模組或更新現有模組中。 按一下瀏覽 hello 自動化帳戶資源、 hello 資產磚，以及最後 hello 模組磚。  hello 瀏覽圖庫圖示可讓您 toosee hello hello 圖庫中的模組清單、 向下鑽研到詳細資料和最終匯入您的自動化帳戶。 這是很好的方法 tookeep 總時間 tootime 從 toodate 模組。 此外，hello 匯入功能會檢查以執行任何動作取得同步的其他模組 tooensure 的相依性。

或者，如果沒有 hello 手動方法。  適用於 Windows 電腦 PowerShell 整合模組 hello 資料夾結構與稍有不同 hello Azure 自動化所預期的 hello 資料夾結構。  您需要稍微調整一下。  但是它並不難，而且每個資源一次處理完成 (除非您想 tooupgrade 它在未來。)如需關於撰寫 PowerShell 整合模組的詳細資訊，請參閱下列文章：[撰寫 Azure 自動化的整合模組](https://azure.microsoft.com/blog/authoring-integration-modules-for-azure-automation/)

* 安裝 hello 模組，您需要在您的工作站，如下所示：
  * 安裝 [Windows Management Framework v5](http://aka.ms/wmf5latest) (Windows 10 不需安裝)
  * `Install-Module –Name MODULE-NAME`<-grabs hello hello PowerShell 資源庫模組 
* 從複製 hello 模組資料夾`c:\Program Files\WindowsPowerShell\Modules\MODULE-NAME`tooa 暫存資料夾 
* 範例與文件刪除 hello 的 main 資料夾 
* Zip hello 主資料夾命名 hello ZIP 檔案完全相同 hello 與 hello 資料夾 
* Hello ZIP 檔案放入連線到 HTTP 位置，例如 Azure 儲存體帳戶中的 blob 儲存體。
* 執行此 PowerShell：
  
      New-AzureRmAutomationModule `
          -ResourceGroupName MY-AUTOMATION-RG -AutomationAccountName MY-AUTOMATION-ACCOUNT `
          -Name MODULE-NAME –ContentLink "https://STORAGE-URI/CONTAINERNAME/MODULE-NAME.zip"

包含 hello 範例 cChoco 和 xNetworking 執行這些步驟。 請參閱 hello[備忘稿](#notes)cChoco 的特殊處理。

## <a name="step-4-adding-hello-node-configuration-toohello-pull-server"></a>步驟 4： 加入 hello 節點設定 toohello 提取伺服器
沒有任何特殊 hello 有關您匯入您的組態 hello 提取伺服器和編譯的第一次。  匯入編譯所有後續的 hello 相同的組態外觀完全 hello 相同。  每次您更新您的封裝，並需要 toopush tooproduction 出您執行此步驟之後 hello 設定檔是封裝的正確 – 包括 hello 新版本，您。  以下是 hello 設定檔與 PowerShell:

ISVBoxConfig.ps1：

    Configuration ISVBoxConfig 
    { 
        Import-DscResource -ModuleName cChoco 
        Import-DscResource -ModuleName xNetworking

        Node "isvbox" {   

            cChocoInstaller installChoco 
            { 
                InstallDir = "C:\choco" 
            }

            WindowsFeature installIIS 
            { 
                Ensure="Present" 
                Name="Web-Server" 
            }

            xFirewall WebFirewallRule 
            { 
                Direction = "Inbound" 
                Name = "Web-Server-TCP-In" 
                DisplayName = "Web Server (TCP-In)" 
                Description = "IIS allow incoming web site traffic." 
                DisplayGroup = "IIS Incoming Traffic" 
                State = "Enabled" 
                Access = "Allow" 
                Protocol = "TCP" 
                LocalPort = "80" 
                Ensure = "Present" 
            }

            cChocoPackageInstaller trivialWeb 
            {            
                Name = "trivialweb" 
                Version = "1.0.0" 
                Source = “MY-NUGET-V2-SERVER-ADDRESS” 
                DependsOn = "[cChocoInstaller]installChoco", 
                "[WindowsFeature]installIIS" 
            } 
        }    
    }

New-ConfigurationScript.ps1：

    Import-AzureRmAutomationDscConfiguration ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -SourcePath C:\temp\AzureAutomationDsc\ISVBoxConfig.ps1 ` 
        -Published –Force

    $jobData = Start-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -ConfigurationName ISVBoxConfig 

    $compilationJobId = $jobData.Id

    Get-AzureRmAutomationDscCompilationJob ` 
        -ResourceGroupName MY-AUTOMATION-RG –AutomationAccountName MY-AUTOMATION-ACCOUNT ` 
        -Id $compilationJobId

這些步驟會導致新的節點設定名為"ISVBoxConfig.isvbox"hello 提取伺服器上要放置。  會建立 「 configurationName.nodeName"hello 節點設定名稱。

## <a name="step-5-creating-and-maintaining-package-metadata"></a>步驟 5：建立和維護封裝中繼資料
您放入 hello 封裝儲存機制的每一個封裝，您需要說明該 nuspec。  該 nuspec 必須編譯並儲存在 NuGet 伺服器中。 此程序的說明請參閱 [這裡](http://docs.nuget.org/create/creating-and-publishing-a-package)。  您可以使用 MyGet.org 做為 NuGet 伺服器。  他們銷售這項服務，但有免費的入門 SKU。  在 NuGet.org，您可以找到為私人封裝來安裝 NuGet 伺服器的指示。

## <a name="step-6-tying-it-all-together"></a>步驟 6：整合一切
部署中，每次的版本會傳遞 QA 及核准建立 hello 封裝、 nuspec nupkg 更新和部署 toohello NuGet 伺服器。  此外，hello 組態 (上述步驟 4) 都必須更新的 tooagree hello 新的版本號碼。  它必須傳送 toohello 提取伺服器和編譯。  從該點上，是由 toohello Vm，取決於該組態 toopull hello 更新並安裝它。  這些更新內容很簡單 - 只有一兩行 PowerShell。  在 Visual Studio Team Services 的 hello 情況下，其中部分都會封裝在可鏈結在一起在組建中建置工作。  [本文](https://www.visualstudio.com/en-us/docs/alm-devops-feature-index#continuous-delivery)將詳加說明。  這[GitHub 儲存機制](https://github.com/Microsoft/vso-agent-tasks)詳細資料 hello 各種可用的組建工作。

## <a name="notes"></a>注意事項
此使用範例開頭將 VM 從 hello Azure 組件庫中的一般 Windows Server 2012 R2 映像。  您可以開始從任何預存的映像，然後再從該處 hello DSC 設定的變更。  不過，將映像變更為燒的組態是比動態更新使用 DSC 的 hello 組態困難得多。

您沒有 toouse ARM 範本和 hello VM 延伸模組 toouse 這項技術與您的 Vm。  而且您的 Vm 沒有 toobe 上 Azure toobe CD 管理下。  所有的是該 Chocolatey 會安裝並 hello LCM 設定 hello VM 上，才會知道其中 hello 提取伺服器是必要的。  

當然，當您更新處於生產環境的 VM 上的封裝，您需要 tootake 離輪替循環該 VM hello 更新安裝時。  視情況而定，作法會有很大的差異。  例如，如果 VM 在 Azure 負載平衡器後方，您可以加入自訂探查。  在更新 hello VM，具有 hello 探查端點傳回 400。  hello 調整必要 toocause 這項變更可以是在您的設定，可以 hello 調整 tooswitch 回 tooreturning 200 一旦 hello 更新已完成。

此使用範例的完整原始檔位於 GitHub 上的 [Visual Studio 專案](https://github.com/sebastus/ARM/tree/master/CDIaaSVM) 。

## <a name="related-articles"></a>相關文章
* [Azure 自動化 DSC 概觀](automation-dsc-overview.md)
* [Azure 自動化 DSC Cmdlet](https://msdn.microsoft.com/library/mt244122.aspx)
* [上架由 Azure 自動化 DSC 管理的機器](automation-dsc-onboarding.md)

