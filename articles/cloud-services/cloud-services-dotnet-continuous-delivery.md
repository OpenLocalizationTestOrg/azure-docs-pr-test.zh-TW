---
title: "aaaContinuous 傳遞的雲端服務在 Azure 中與 TFS |Microsoft 文件"
description: "深入了解如何註冊 azure 持續傳遞 tooset 雲端應用程式。 MSBuild 命令列陳述式和 PowerShell 指令碼的程式碼範例。"
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Azure 中雲端服務的連續傳遞
hello 本文中所述的程序為您示範如何設定 Azure 雲端應用程式的持續傳遞 tooset。 此程序可讓您自動建立封裝和部署 hello 封裝 tooAzure 之後每個程式碼簽入。 hello 本文中所述的封裝建置程序是相當 toohello**封裝**在 Visual Studio 中的命令，並發行步驟是對等 toohello**發行**Visual Studio 中的命令。
您會使用 MSBuild 命令列陳述式和 Windows PowerShell 指令碼，而且與 toocreate 組建伺服器也 hello 文章涵蓋 hello 方法示範 toooptionally 如何設定 Visual 的 Studio Team Foundation Server-Team Build 定義toouse hello MSBuild 命令和 PowerShell 指令碼。 hello 程序是可自訂的建置環境和 Azure 的目標環境。

您也可以使用 Visual Studio Team Services 的是的 TFS 版本的 Azure 中裝載，toodo 這更容易。 

開始之前，您應該先從 Visual Studio 發佈應用程式。
這可確保所有 hello 資源，都可供使用且初始化當您嘗試 tooautomate hello 發行集的程序。

## <a name="1-configure-hello-build-server"></a>1： 設定組建伺服器 hello
您可以使用 MSBuild 建立 Azure 的封裝之前，您必須 hello 組建伺服器上安裝所需的 hello 軟體和工具。

Visual Studio 不必要的 toobe hello 組建伺服器上安裝。 如果您想 toouse Team Foundation Build Service toomanage 組建伺服器，請遵循 hello 中的 hello 指示[Team Foundation Build Service] [ Team Foundation Build Service]文件。

1. Hello 組建伺服器上，安裝 hello [.NET Framework 4.5.2][.NET Framework 4.5.2]，其中包括 MSBuild。
2. 安裝最新的 hello[適用於.NET 的 Azure Authoring Tools](https://azure.microsoft.com/develop/net/)。
3. 安裝 hello [Azure Libraries for.NET](http://go.microsoft.com/fwlink/?LinkId=623519)。
4. 從 Visual Studio 安裝 toohello 複製 hello Microsoft.WebApplication.targets 檔案部署組建伺服器。

   電腦上安裝 Visual Studio，這個檔案位於 hello 目錄 c:\\Program files （x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications。 您應該將它複製 toohello hello 組建伺服器上相同的目錄。
5. 安裝 hello [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)。

## <a name="2-build-a-package-using-msbuild-commands"></a>2：使用 MSBuild 命令來建置封裝
本章節描述如何 tooconstruct MSBuild 命令，建立 Azure 的封裝。 上的所有項目已正確設定，而且 hello MSBuild 命令會是您要它 hello 組建伺服器 tooverify toodo 執行此步驟。 您可以加入這個命令列 tooexisting hello 組建伺服器上，建立指令碼，或者您可以使用 TFS 組建定義中的 hello 命令列 hello 下一節中所述。 如需命令列參數及 MSBuild 的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。

1. 如果在 hello 組建伺服器上安裝 Visual Studio，找出並選擇**Visual Studio 命令提示字元**在 hello **Visual Studio Tools** Windows 中的資料夾。

   如果 hello 組建伺服器上未安裝 Visual Studio，開啟命令提示字元，並確認 MSBuild.exe 路徑上，您可以存取。 MSBuild 會隨 hello.NET Framework 在 hello 路徑 %WINDIR%\\Microsoft.NET\\Framework\\*版本*。 比方說，若要加入 MSBuild.exe toohello PATH 環境變數，當您安裝.NET Framework 4 時，輸入下列命令在 hello 命令提示字元的 hello:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. Hello 命令提示字元，瀏覽 toohello 資料夾包含您想 toobuild Azure 專案檔。
3. 執行 MSBuild 與 hello /target： 發行選項，如 hello 下列範例所示：

       MSBuild /target:Publish

   此選項可以縮寫為 /t:Publish。 不應將在 MSBuild 中的 hello /t:Publish 選項混淆 hello 發行 Visual Studio 中提供的命令，當您擁有的 hello 安裝 Azure SDK。 hello /t： 組建 hello Azure 套件只發佈選項。 它不會部署 hello 封裝 Visual Studio 中的 hello 發行命令一樣。

   （選擇性） 您可以指定 hello 專案名稱做為 MSBuild 參數。 如果未指定，會使用 hello 目前的目錄。 如需 MSBuild 命令列選項的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)。
4. 找出 hello 輸出。 根據預設，此命令會建立一個目錄關聯 toohello 根 hello 專案資料夾，例如*ProjectDir*\\bin\\*組態*\\app.publish\\。 當您建置 Azure 專案時，會產生兩個檔案、 hello 封裝檔本身和伴隨的組態檔的 hello:

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   依預設，每個 Azure 專案都會包含一個服務組態檔 (.cscfg 檔) 用於本機 (偵錯) 組建，以及另一個服務組態檔用於 (預備或生產) 雲端組建，但是您可以視需要新增或移除服務組態檔。 當您建置 Visual Studio 中的封裝時，系統會詢問與 hello 封裝一起哪一個服務組態檔 tooinclude。
5. 指定 hello 服務組態檔。 當您使用 MSBuild 建置封裝時，預設會包含 hello 本機服務組態檔。 tooinclude 不同的服務組態檔，設定如 hello 下列範例所示的 hello MSBuild 命令的 TargetProfile 屬性：

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. 指定 hello hello 輸出的位置。 設定 hello 路徑使用 publishdir =*目錄*\\選項，包括 hello 尾端的反斜線分隔，如 hello 下列範例所示：

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   一旦您建構並測試適當的 MSBuild 命令列 toobuild 您的專案，並將它們結合於 Azure 的封裝，您可以加入這個命令列 tooyour 建置指令碼。 如果您的組建伺服器使用自訂指令碼，則此程序將視您自訂建置流程的特性而定。 如果您使用 TFS 做為建置環境，您可以依照 hello hello 下一個步驟 tooadd hello Azure 封裝組建 tooyour 建置流程中的指示。

## <a name="3-build-a-package-using-tfs-team-build"></a>3：使用 TFS Team Build 建置封裝
如果您有 Team Foundation Server (TFS) 設定組建控制器和 hello 組建伺服器設定為 TFS 組建電腦，然後您可以選擇性地設定自動化建置您的 Azure 套件。 如需有關如何向上 tooset 和做為 Team Foundation server 建置系統，請參閱詳細[向外延展您的建置系統][Scale out your build system]。 特別是，下列程序假設您已設定您的組建伺服器中所述[部署和設定組建伺服器][Deploy and configure a build server]，而且您已建立 team 專案時，建立雲端hello team 專案中的服務專案。

tooconfigure TFS toobuild Azure 封裝，執行下列步驟的 hello:

1. 在 Visual Studio 在開發電腦，hello 檢視 功能表上選擇**Team Explorer**，或選擇 Ctrl +\\，Ctrl + M。 在 Team Explorer 視窗中，展開 hello**建置**節點，或選擇 hello**建置**頁面，然後選擇 **新增組建定義**。

   ![新增組建定義選項][0]
2. 選擇 hello**觸發程序**索引標籤，並指定當您想要的條件 hello 封裝 toobe 建置所需的 hello。 例如，指定**連續整合**toobuild hello 封裝簽入原始檔控制時，就會發生。
3. 選擇 hello**來源設定**索引標籤，然後確認您的專案資料夾會列在 hello**原始檔控制資料夾**資料行，且 hello 狀態為**Active**。
4. 選擇 hello**組建預設值**索引標籤，然後在之下，組建控制器，確認 hello hello 組建伺服器名稱。  而且請選擇 hello 選項**複製組建輸出 toohello 下列置放資料夾**並指定所需的 hello 置放位置。
5. 選擇 hello**程序** 索引標籤。Hello 程序 索引標籤上選擇 hello 預設範本，在**建置**，如果尚未選取，並展開 hello 選擇 hello 專案**進階**> 一節中 hello**建置**hello 方格的區段。
6. 選擇**MSBuild 引數**，並依照上述步驟 2 中所述設定 hello 適當 MSBuild 命令列引數。 例如，輸入**/t： 發行 publishdir =\\\\myserver\\卸除\\** toobuild 封裝並複製 hello 封裝檔案 toohello 位置\\ \\myserver\\卸除\\:

   ![MSBuild 引數][2]

   > [!NOTE]
   > 複製 hello 檔案 tooa 公用共用可讓您更輕鬆 toomanually 部署 hello 封裝從開發電腦。
7. 藉由在變更 tooyour 專案中，檢查測試 hello 成功的建置步驟或佇列新組建。 tooqueue 新的組建，在 Team Explorer 中，以滑鼠右鍵按一下**所有組建定義，** ，然後選擇 **佇列新組建**。

## <a name="4-publish-a-package-using-a-powershell-script"></a>4：使用 PowerShell 指令碼來發佈封裝
本章節描述如何 tooconstruct Windows PowerShell 指令碼會將發佈 hello 雲端應用程式封裝輸出 tooAzure 使用選擇性參數。 在自訂建置自動化中的 hello 建置步驟後，可以呼叫此指令碼。 也可以從 Visual Studio TFS Team Build 中的「流程範本」工作流程活動中呼叫。

1. 安裝 hello [Azure PowerShell cmdlet] [ Azure PowerShell cmdlets] (v0.6.1 或更高版本)。
   在 hello cmdlet 安裝階段中，選擇 tooinstall 嵌入式管理單元。 請注意，雖然 hello 舊版已編號 2.x.x 這個正式支援的版本會取代 hello 透過 CodePlex 提供的舊版。
2. 啟動 Azure PowerShell 中使用 hello [開始] 功能表或起始頁。 如果您在這種方式啟動，就會載入 hello Azure PowerShell cmdlet。
3. Hello PowerShell 命令提示字元中，確認 hello PowerShell 指令程式會載入輸入 hello 部分命令`Get-Azure`，然後按 hello Tab 鍵，以完成陳述式。

   如果您重複按 hello Tab 鍵，您應該會看到不同的 Azure PowerShell 命令。
4. 請確認您可以從 hello.publishsettings 檔案匯入您的訂用帳戶資訊來連接 tooyour Azure 訂用帳戶。

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   然後輸入 hello 命令

   `Get-AzureSubscription`

   如此即會顯示訂用帳戶的相關資訊。 確認一切正確無誤。
5. 儲存在 hello 到您指令碼的資料夾為 c： 本文結尾處提供的 hello 指令碼範本\\指令碼\\WindowsAzure\\**PublishCloudService.ps1**。
6. 檢閱 hello hello 指令碼參數區段。 新增或修改任何預設值。 您永遠可以傳遞明確參數來覆寫這些值。
7. 請確定沒有有效的雲端服務，而且您可以將目標設 hello 的訂閱中建立的儲存體帳戶的發行指令碼。 儲存體帳戶 （blob 儲存） 會使用的 tooupload 並在建立部署時，暫時儲存 hello 部署封裝和組態檔。

   * toocreate 新的雲端服務，您可以呼叫此指令碼或使用 hello [Azure 入口網站](https://portal.azure.com)。 hello 雲端服務名稱會用作中完整的網域名稱的前置詞，因此它必須是唯一的。

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * toocreate 新的儲存體帳戶，您可以呼叫此指令碼或使用 hello [Azure 入口網站](https://portal.azure.com)。 hello 儲存體帳戶名稱會用作中完整的網域名稱的前置詞，因此它必須是唯一的。 您可以嘗試使用名稱相同的 hello 與雲端服務。

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. 直接從 Azure PowerShell，呼叫 hello 指令碼，或連接此指令碼 tooyour 主機組建自動化 toooccur 之後 hello 封裝組建。

   > [!IMPORTANT]
   > hello 指令碼將會永遠刪除，或您現有的部署取代依預設，如果偵測到。 此為不得不的方式，因為如此一來，完全省去使用者互動過程的自動化程序才有辦法進行連續傳遞。
   >
   >

   **範例案例 1:**連續部署 toohello 預備環境的服務：

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   此作業後面通常接著測試執行驗證及 VIP 交換。 hello VIP 交換可透過 hello [Azure 入口網站](https://portal.azure.com)或使用 hello 移動部署 cmdlet。

   **範例案例 2:**連續部署 toohello 實際執行環境的專用的測試服務

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **遠端桌面：**

   遠端桌面已啟用 Azure 專案中，如果您需要 tooperform 額外的單次步驟 tooensure hello 是正確的雲端服務憑證上傳 tooall 雲端服務，此指令碼的目標。

   找出您的角色所預期的 hello 憑證指紋值。 憑證指紋值 hello 的雲端組態檔 (也就是 ServiceConfiguration.Cloud.cscfg) 的憑證 > 一節中會出現的。 您的顯示選項和檢視 hello 選取憑證時，它會也在 Visual Studio 中的 hello 遠端桌面設定對話方塊中顯示。

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   遠端桌面憑證上傳一次設定步驟，使用下列 cmdlet 指令碼的 hello:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   例如：

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   或者，您可以匯出使用私用金鑰和上傳憑證 tooeach 目標雲端服務的 hello 憑證檔案 PFX [Azure 入口網站](https://portal.azure.com)。

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **升級部署以及刪除部署 -\> 新增部署**

   hello 指令碼會根據預設執行升級的部署 ($enableDeploymentUpgrade = 1) 在沒有參數傳遞或明確傳遞的值為 1 時。 對於單一執行個體，這具有比完整部署花費更少時間的優點。 針對需要高可用性，這也有某些情況下執行，而其他則可能會留下 hello 優點的執行個體升級 （查核更新網域），加上將不會刪除您的 VIP。

   升級部署，您可以在 hello 指令碼中停用 ($enableDeploymentUpgrade = 0) 或藉由傳遞*-enableDeploymentUpgrade 0*做為參數，其中改變指令碼行為 toofirst 刪除任何現有的部署，然後建立新的部署。

   > [!IMPORTANT]
   > hello 指令碼將會永遠刪除，或您現有的部署取代依預設，如果偵測到。 此為不得不的方式，因為如此一來，完全省去使用者/作業員互動過程的自動化程序才有辦法進行連續傳遞。
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5：使用 TFS Team Build 發佈封裝
此選擇性步驟中連接的 TFS Team Build toohello 指令碼在步驟 4 中，建立用來處理 hello 封裝組建 tooAzure 發行。 這需要修改 hello 供您的組建定義，使其執行的發佈活動結尾 hello hello 工作流程的流程範本。 hello 發行活動會執行您從 hello 組建傳入參數的 PowerShell 命令。 Hello MSBuild 目標和發行指令碼的輸出會經由管道輸出到 hello 標準的建置輸出。

1. 編輯組建定義負責 hello 連續部署。
2. 選取 hello**程序** 索引標籤。
3. 請遵循[這些指示](http://msdn.microsoft.com/library/dd647551.aspx)tooadd hello 活動專案建置流程範本，請下載 hello 預設範本，將它加入 hello 專案並將它簽入。 請提供新的名稱，例如 AzureBuildProcessTemplate hello 建置流程範本。
4. 傳回 toohello**程序**索引標籤，然後使用**顯示詳細資料**tooshow 可用的建置流程範本的清單。 選擇 hello**新增...**按鈕，然後瀏覽 toohello 專案只需要加入，並簽入。 找出您剛才建立的 hello 範本，然後選擇 **確定**。
5. 開啟 hello 選取流程範本進行編輯。 您可以開啟直接在 hello 工作流程設計工具或 hello XML 編輯器 toowork 以 hello XAML 中。
6. 新增新引數清單後面 hello 的 hello 工作流程設計工具的引數 索引標籤中的個別明細項目為 hello。 所有引數都應該具有 direction=In 及 type=String。 這些會是使用的 tooflow hello 到 hello 流程中，哪些然後 get 使用的 toocall hello 發行指令碼的組建定義的參數。

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![引數清單][3]

   hello 對應 XAML 看起來像這樣：

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. 在代理程式上執行的 hello 結尾處加入新的順序：

   1. 將有效的指令碼檔案的 If 陳述式活動 toocheck 來開始。 設定 hello 條件 toothis 值：

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. 然後在 hello hello If 陳述式的情況下加入新的序列活動。 發行集 hello 顯示名稱 too'Start'
   3. Hello 開始發行仍選取的順序，加入下列新的變數清單為 hello 工作流程設計工具中的 [變數] 索引標籤中的個別明細項目。 所有變數都應該具有 Variable type =String 及 Scope=Start publish。 這些會是使用的 tooflow hello 到哪些然後 get 使用的 toocall hello 發行指令碼的工作流程的組建定義的參數。

      * SubscriptionDataFilePath，型別為 String
      * PublishScriptFilePath，型別為 String

        ![新變數][4]
   4. 如果您使用 TFS 2012 或更早版本，在 hello 開頭加入 ConvertWorkspaceItem 活動 hello 新的順序。 如果您使用 TFS 2013 或更新版本，新增 GetLocalPath 活動 hello hello 新序列開頭。 對於 ConvertWorkspaceItem，設定 hello 屬性，如下所示： 方向 = ServerToLocal，DisplayName = 'Convert 發佈指令碼檔案名稱 輸入 = 'PublishScriptLocation'，結果 = 'PublishScriptFilePath'，工作空間 = '工作區'。 是 GetLocalPath 活動，請設定 hello 屬性 IncomingPath too'PublishScriptLocation'，與 hello 結果 too'PublishScriptFilePath'。 （如果適用），此活動將 hello 路徑 toohello 發行指令碼，從 TFS 伺服器位置 tooa 標準的本機磁碟的路徑。
   5. 如果您使用 TFS 2012 或更早版本，新增另一個 ConvertWorkspaceItem 活動結尾的 hello hello 新的順序。 Direction=ServerToLocal、DisplayName='Convert subscription filename'、Input=' SubscriptionDataFileLocation'、Result= 'SubscriptionDataFilePath'、Workspace='Workspace'。 如果您使用 TFS 2013 或更新版本，請新增另一個 GetLocalPath。 IncomingPath='SubscriptionDataFileLocation'，以及 Result='SubscriptionDataFilePath'。
   6. 加入 InvokeProcess 活動結尾 hello hello 新的順序。
      此活動 PowerShell.exe 具 hello 引數呼叫傳入 hello 組建定義。

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Execute publish script
      + 檔案名稱 ="PowerShell"（包括 hello 引號）
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. 在 hello**處理標準輸出**區段 InvokeProcess 的文字方塊中，將 hello textbox 值 too'data'。 這是變數 toostore hello 標準輸出資料。
   8. 新增正下方 hello WriteBuildMessage 活動**處理標準輸出**> 一節。 設定 hello 重要性 = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' 和 hello 訊息 = 'data'。 這可確保指令碼的 hello 標準輸出會寫入 toohello 組建輸出。
   9. 在 hello**處理錯誤輸出**區段 InvokeProcess 的文字方塊中，將 hello textbox 值 too'data'。 這是變數 toostore hello 標準錯誤資料。
   10. 新增正下方 hello WriteBuildError 活動**處理錯誤輸出**> 一節。 設定 hello 訊息 = 'data'。 這可確保 hello 指令碼的 hello 標準錯誤會寫入 toohello 建置錯誤輸出。
   11. 更正由藍色驚嘆號指出的任何錯誤。 將滑鼠停留在驚歎 tooget hello 錯誤有關的提示。 儲存要清除錯誤 hello 工作流程。

   hello hello 最終結果會發行工作流程活動 hello 設計工具中，看起來像這樣：

   ![工作流程活動][5]

   hello 最終結果的 hello 發行工作流程活動 XAML 中，看起來像這樣：

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. 儲存建置流程範本工作流程 hello 和簽入這個檔案。
9. 編輯 hello 組建定義 （關閉它如果已經開啟），並選取 hello**新增**按鈕，如果您有尚未看到 hello hello 流程範本清單中的新範本。
10. 設定 hello 參數屬性值在 hello 其他區段如下所示：

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' 此值衍生自：($PublishDir)ServiceConfiguration.Cloud.cscfg
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' 此值衍生自：($PublishDir)($ProjectName).cspkg
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename'*使用 hello 適當的雲端服務名稱*
    5. Environment = 'Staging'
    6. StorageAccountName = 'mystorageaccountname'*使用 hello 適當的儲存體帳戶名稱*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![參數屬性值][6]
11. 儲存 hello 變更 toohello 組建定義。
12. 佇列組建 tooexecute 兩者 hello 封裝組建和發行。 如果您有設定 tooContinuous 整合觸發程序，您也會執行這項行為每個簽入。

### <a name="publishcloudserviceps1-script-template"></a>PublishCloudService.ps1 指令碼範本
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>後續步驟
tooenable 遠端偵錯時使用連續的傳遞，請參閱[啟用遠端偵錯時使用持續傳遞 toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)。

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
