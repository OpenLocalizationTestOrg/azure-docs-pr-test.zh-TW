---
title: "for Excel 和 SOA 叢集 aaaHPC 組件 |Microsoft 文件"
description: "開始在 Azure 中的 HPC Pack 叢集上執行大規模 Excel 和 SOA 工作負載"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>開始在 Azure 中的 HPC Pack 叢集上執行 Excel 和 SOA 工作負載
本文章將示範如何 toodeploy Microsoft HPC Pack 2012 R2 上叢集化 Azure 虛擬機器使用的 Azure 快速入門範本，或選擇性的 Azure PowerShell 部署指令碼。 hello 叢集會使用 Azure Marketplace VM 映像設計 toorun Microsoft Excel 或服務導向架構 (SOA) 工作負載使用 HPC Pack。 您可以使用 hello 叢集 toorun Excel HPC 及 SOA 服務從內部部署用戶端電腦。 hello Excel HPC 服務包括 Excel 活頁簿卸載和 Excel 使用者定義函數或 Udf。

> [!IMPORTANT] 
> 此文章是以 HPC Pack 2012 R2 的功能、範本與指令碼為基礎。 HPC Pack 2016 目前不支援此案例。
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

在高層級，hello 下列圖表顯示 hello HPC Pack 叢集您所建立。

![HPC 叢集與執行 Excel 工作負載的節點][scenario]

## <a name="prerequisites"></a>必要條件
* **用戶端電腦**-您需要 Windows 架構的用戶端電腦 toosubmit 範例 Excel 和 SOA 工作 toohello 叢集。 您也需要 Windows 電腦 toorun hello Azure PowerShell 叢集部署指令碼 （如果您選擇的部署方法）。
* **Azure 訂用帳戶** - 如果您沒有 Azure 訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/) 。
* **核心配額**-您可能需要的核心，tooincrease hello 配額，特別是當您部署具有多核心的 VM 大小的數個叢集節點。 如果您使用 Azure 快速入門範本，資源管理員 中的 hello 核心配額為每個 Azure 區域。 在此情況下，您可能需要在特定地區的 tooincrease hello 配額。 請參閱 [Azure 訂用帳戶限制、配額與限制](../../azure-subscription-service-limits.md)。 tooincrease 配額限制時，[開啟線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)不收費。
* **Microsoft Office 授權** - 如果您使用包含 Microsoft Excel 的 Marketplace HPC Pack 2012 R2 VM 映像部署計算節點，會安裝 Microsoft Excel Professional Plus 2013 的 30 天評估版。 之後 hello 評估期間，您需要 tooprovide 有效 Microsoft Office 授權 tooactivate Excel toocontinue toorun 工作負載。 請參閱在本文章稍候的 [啟用 Excel](#excel-activation) 。 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>步驟 1. 在 Azure 中設定 HPC Pack 叢集
我們顯示 hello HPC Pack 2012 R2 叢集的兩個選項 tooset： 首先，使用 Azure 快速入門的範本和 hello Azure 入口網站。與第二個，使用 Azure PowerShell 部署指令碼。

### <a name="option-1-use-a-quickstart-template"></a>選項 1。 使用快速入門範本
使用 Azure 快速入門範本 tooquickly 部署 HPC Pack 叢集 hello Azure 入口網站中。 當您開啟 hello 範本 hello 入口網站中時，您會取得您輸入 hello 設定叢集的簡單 UI。 以下是 hello 步驟。 

> [!TIP]
> 如果您願意的話，可以使用 [Azure Marketplace 範本](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) 來專為 Excel 工作負載建立類似的叢集。 hello 步驟稍有不同 hello 下列。
> 
> 

1. 請瀏覽 hello [GitHub 上的建立 HPC 叢集 [範本] 頁面](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)。 如果您想，檢閱 hello 範本和 hello 原始程式碼的相關資訊。
2. 按一下**部署 tooAzure** toostart hello Azure 入口網站中的 hello 範本部署。
   
   ![部署範本 tooAzure][github]
3. 在 hello 入口網站中，遵循這些步驟 tooenter hello 參數的 hello HPC 叢集的範本。
   
   a. 在 hello**參數**頁面上，輸入或修改 hello 範本參數的值。 （按一下 hello 圖示下一個 tooeach 設定的說明資訊）。Hello 遵循畫面中會顯示範例值。 這個範例會建立名為叢集*hpc01*在 hello *hpc.local*前端節點和 2 組成網域的計算節點。 hello 運算節點會建立從 HPC Pack VM 映像，其中包含 Microsoft Excel。
   
   ![輸入參數][parameters-new-portal]
   
   > [!NOTE]
   > hello 前端節點 VM 會自動建立從 hello[最新的 Marketplace 映像](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)的 HPC Pack 2012 R2，Windows Server 2012 R2 上。 目前 hello 映像為基礎 HPC Pack 2012 R2 更新 3。
   > 
   > 運算節點 Vm 會建立從 hello hello 選取計算節點系列的最新映像。 選取 hello **ComputeNodeWithExcel** hello 最新 HPC Pack 計算節點映像，其中包含 Microsoft Excel Professional Plus 2013 評估版的選項。 toodeploy 叢集一般 SOA 工作階段或 Excel UDF 卸載，選擇 hello **ComputeNode**選項 （不需安裝 Excel）。
   > 
   > 
   
   b. 選擇 hello 訂用帳戶。
   
   c. 建立 hello 叢集資源群組，例如*hpc01RG*。
   
   d. 選擇 hello 資源群組，例如美國中部的位置。
   
   e. 在 hello**法律條款**頁面上，檢閱 hello 條款。 如果您同意，請按一下 [購買]。 當您完成設定 hello hello 範本的值，然後按一下**建立**。
4. Hello 部署完成時 （通常可以花大約 30 分鐘），從 hello 叢集前端節點匯出 hello 叢集憑證檔案。 在稍後步驟中，您匯入這個 hello 的用戶端電腦 tooprovide hello 伺服器端驗證安全的 HTTP 繫結上的公開憑證。
   
   a. 在 hello Azure 入口網站，移 toohello 儀表板，選取 hello 前端節點，然後按一下 **連接**頂端 hello hello 頁面 tooconnect 使用遠端桌面。
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. 使用具 hello 私密金鑰的憑證管理員 tooexport hello 前端節點憑證 （位於 Cert: \LocalMachine\My） 中的標準程序。 在此範例中，匯出 *CN = hpc01.eastus.cloudapp.azure.com*。
   
   ![匯出 hello 憑證][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>選項 2。 使用 hello HPC Pack IaaS 部署指令碼
hello HPC Pack IaaS 部署指令碼會提供其他的靈活方式 toodeploy HPC Pack 叢集。 建立叢集的 hello 傳統部署模型，而 hello 範本使用 hello Azure Resource Manager 部署模型。 此外，hello 指令碼是與 hello Azure Global 或 Azure China 服務中的訂閱。

**其他必要條件**

* **Azure PowerShell** - [安裝和設定 Azure PowerShell](/powershell/azure/overview) (0.8.10 版或更新版本)。
* **HPC Pack IaaS 部署指令碼**-下載及解壓縮 hello 最新版 hello 指令碼從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949)。 執行檢查 hello hello 指令碼版本`New-HPCIaaSCluster.ps1 –Version`。 這篇文章根據 4.5.0 版本或更新版本的 hello 指令碼。

**建立 hello 設定檔**

 hello HPC Pack IaaS 部署指令碼會使用 XML 組態檔，做為輸入描述 hello hello HPC 叢集基礎結構。 toodeploy 前端節點和 18 所組成的叢集計算節點建立 hello 計算節點映像，包括 Microsoft Excel 中，替換成下列範例組態檔的 hello 環境的值。 如需 hello 設定檔的詳細資訊，請參閱 hello 指令碼資料夾中的 hello Manual.rtf 檔案和[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Hello 設定檔的相關注意事項**

* hello **VMName** hello 前端節點的**必須**是為 hello hello 相同**ServiceName**，SOA 工作失敗 toorun 或。
* 請確定您指定**EnableWebPortal**以便 hello 前端節點的憑證會產生並匯出。
* hello 檔案會指定組態後 PowerShell 指令碼 PostConfig.ps1 hello 前端節點上執行。 下列範例指令碼的 hello 設定 hello Azure 儲存體連接字串、 hello 運算節點角色移除 hello 前端節點之後，並在部署時，使所有節點上線。 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**執行 hello 指令碼**

1. 系統管理員身分開啟 hello hello 用戶端電腦上的 PowerShell 主控台。
2. 變更目錄 toohello 指令碼資料夾 (在此範例中 E:\IaaSClusterScript)。
   
   ```
   cd E:\IaaSClusterScript
   ```
3. toodeploy hello HPC Pack 叢集，請執行下列命令的 hello。 這個範例假設 hello 設定檔位於 E:\HPCDemoConfig.xml。
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

hello HPC Pack 部署指令碼會執行一些時間。 一件事 hello 指令碼會執行為 tooexport 和下載 hello 叢集憑證並將它儲存在 hello 目前使用者的文件 資料夾中 hello 用戶端電腦上。 hello 指令碼會產生類似 toohello 後的訊息。 在下列步驟中，您匯入 hello 適當的憑證存放區中的 hello 憑證。    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>步驟 2. 卸載 Excel 活頁簿並從內部部署用戶端執行 UDF
### <a name="excel-activation"></a>啟用 Excel
當使用 hello ComputeNodeWithExcel VM 映像以生產工作負載時，您需要 tooprovide 有效 Microsoft Office 授權金鑰 tooactivate Excel hello 計算節點上。 否則，Excel hello 評估版到期後 30 天，並執行 Excel 活頁簿以 hello COMException (0x800AC472) 將會失敗。 

您可以重設授權狀態 Excel 的評估時間延長 30 天： 登入 toohello 前端節點和 clusrun`%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe`上所有的 Excel 計算節點透過 HPC 叢集管理員。 您最多可以重新取得兩次。 之後，您就必須提供有效的 Office 授權金鑰。

hello Office Professional Plus 2013 hello VM 映像上安裝為的大量授權版本含一般大量授權金鑰 (GVLK)。 您可以透過金鑰管理服務 (KMS)/Active Directory 型啟用 (AD-BA) 或多重啟用金鑰 (MAK) 來啟用它。 

    * toouse KMS/AD-BA 使用現有的 KMS 伺服器，或設定一個新使用 hello Microsoft Office 2013 的磁碟區的授權封包。 （如果您要設定 hello 伺服器 hello 前端節點上。）然後，啟用 hello KMS 主機金鑰透過 hello 網際網路或電話。 然後 clusrun `ospp.vbs` tooset hello KMS 伺服器和連接埠，並在所有 hello Excel 計算節點上啟用 Office。 

    * toouse MAK，第一個 clusrun `ospp.vbs` tooinput hello 索引鍵，然後啟用 透過 hello 網際網路或電話所有 hello Excel 計算節點。 

> [!NOTE]
> Office Professsional Plus 2013 的零售產品金鑰不適用於此 VM 映像。 如果您擁有非此 Office Professional Plus 2013 大量授權版本之 Office 或 Excel 版本的有效金鑰和安裝媒體，您也可以改用它們。 第一次解除安裝這個磁碟區版本並安裝您所擁有的 hello 版本。 hello 重新安裝計算節點可以擷取成自訂 VM 映像 toouse 大規模的部署中的 Excel。
> 
> 

### <a name="offload-excel-workbooks"></a>卸載 Excel 活頁簿
請遵循這些步驟 toooffload Excel 活頁簿，使其在 Azure 中的 hello HPC Pack 叢集上執行。 toodo，您必須擁有 Excel 2010 或 2013 hello 用戶端電腦上已安裝。

1. 使用步驟 1 toodeploy HPC Pack 叢集以 hello Excel 中的 hello 選項的其中一個計算節點映像。 取得 hello 叢集憑證檔案 (.cer) 以及叢集使用者名稱和密碼。
2. Hello 用戶端電腦上，匯入憑證： \CurrentUser\Root hello 叢集憑證。
3. 請確定已安裝 Excel。 建立具有下列內容在 hello hello 位檔案與 Excel.exe hello 用戶端電腦上相同的資料夾。 這個步驟可確保該 hello HPC Pack 2012 R2 Excel COM 增益集成功載入。
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. 設定 hello 用戶端 toosubmit 作業 toohello HPC Pack 叢集。 其中一個選項是完整的 toodownload hello [HPC Pack 2012 R2 Update 3 安裝](http://www.microsoft.com/download/details.aspx?id=49922)並安裝 hello HPC Pack 用戶端。 或者，下載並安裝 hello [HPC Pack 2012 R2 更新 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)和 hello 適當 Visual c + + 2010 可轉散發套件為您的電腦 ([x64](http://www.microsoft.com/download/details.aspx?id=14632)， [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. 在此範例中，我們使用名為 ConvertiblePricing_Complete.xlsb 的範例 Excel 活頁簿。 您可以從 [這裡](https://www.microsoft.com/en-us/download/details.aspx?id=2939)下載。
6. 將複製 hello Excel 活頁簿 tooa 工作資料夾 D:\Excel\Run 等。
7. 開啟 hello Excel 活頁簿。 在 hello**開發**功能區中，按一下  **COM 增益集**並確認該 hello HPC Pack Excel COM 增益集已順利載入。
   
   ![HPC Pack 的 Excel 增益集][addin]
8. 編輯 hello VBA 巨集會在 Excel 中 HPCControlMacros 藉由變更 hello 註解行 hello 下列指令碼所示。 請將您的環境取代為適當的值。
   
   ![HPC Pack 的 Excel 巨集][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. 將複製 hello Excel 活頁簿 tooan 上載目錄例如 D:\Excel\Upload。 Hello HPC_DependsFiles 常數中 hello VBA 巨集會指定這個目錄。
10. 在 Azure 中的 hello 叢集上 toorun hello 活頁簿按一下 hello**叢集**hello 工作表上的按鈕。

### <a name="run-excel-udfs"></a>執行 Excel UDF
toorun Excel Udf 遵循 hello 先前步驟 1-3 tooset hello 用戶端電腦。 對於 Excel Udf，您不需要計算節點上安裝的 toohave hello Excel 應用程式。 因此，當建立您的叢集計算節點，您可以選擇標準的計算節點映像，而不是 hello 計算節點映像與 Excel。

> [!NOTE]
> 沒有 34 字元限制在 hello Excel 2010 和 2013年叢集連接器 對話方塊。 您使用這個對話方塊方塊 toospecify hello 叢集來執行 hello Udf。 如果 hello 完整的叢集名稱的長度 (例如，hpcexcelhn01.southeastasia.cloudapp.azure.com)，無法容納在 hello 對話方塊。 hello 因應措施是 tooset 全機器變數，例如*CCP_IAASHN* hello 的 hello 長叢集名稱的值。 然後，輸入*%ccp_iaashn* hello 對話方塊中做為 hello 叢集前端節點名稱。 
> 
> 

Hello 叢集已成功部署之後，繼續執行下列步驟 toorun hello 範例內建 Excel UDF。 自訂 Excel Udf，請參閱這些[資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx)toobuild hello Xll，並將其部署 hello IaaS 叢集上。

1. 開啟新的 Excel 活頁簿。 在 hello**開發**功能區中，按一下 **增益集**。然後，在 hello 對話方塊中，按一下**瀏覽**，瀏覽 toohello %CCP_HOME%Bin\XLL32 資料夾，並選取 hello 範例 ClusterUDF32.xll。 如果 hello ClusterUDF32 不存在 hello 用戶端電腦上，請將其複製 hello 前端節點上的 hello %CCP_HOME%Bin\XLL32 資料夾中。
   
   ![選取 hello UDF][udf]
2. 按一下 [檔案] > [選項] > [進階]。 在下**公式**，檢查**運算叢集可讓使用者定義 XLL 函式 toorun**。 然後按一下 **選項**，然後輸入 hello 完整的叢集名稱中**叢集前端節點名稱**。 （如所述先前這個輸入的方塊是有限的 too34 字元，因此長叢集名稱可能不適合。 您在這裡可以對完整叢集名稱使用電腦全域變數。)
   
   ![設定 hello UDF][options]
3. toorun hello UDF 計算 hello 在叢集上，按一下值 =XllGetComputerNameC() hello 儲存格，然後按 Enter。 hello 函式只會擷取 hello UDF 執行哪些 hello hello 運算節點名稱。 第一次執行的 hello，認證對話方塊會提示輸入 hello 使用者名稱和密碼 tooconnect toohello IaaS 叢集中。
   
   ![執行 UDF][run]
   
   當有許多儲存格 toocalculate 時，按下 Alt Shift Ctrl + F9 toorun hello 計算所有資料格上。

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>步驟 3. 從內部部署用戶端執行 SOA 工作負載
toorun 一般 SOA 應用程式在 hello HPC Pack IaaS 叢集中，先使用其中一種 hello 方法步驟 1 toodeploy hello 叢集中。 在此情況下，指定泛型計算節點映像，因為您不需要 Excel hello 計算節點上。 接著，遵循下列步驟。

1. 擷取後 hello 叢集憑證，請將它匯入憑證： \CurrentUser\Root hello 用戶端電腦。
2. 安裝 hello [HPC Pack 2012 R2 更新 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921)和[HPC Pack 2012 R2 更新 3 用戶端公用程式](https://www.microsoft.com/download/details.aspx?id=49923)。 這些工具讓您 toodevelop，並執行 SOA 用戶端應用程式。
3. 下載 hello HelloWorldR2[範例程式碼](https://www.microsoft.com/download/details.aspx?id=41633)。 開啟 Visual Studio 2010 中的 HelloWorldR2.sln hello 或 2012年。 (此範例目前與較新的 Visual Studio 版本不相容。)
4. 第一次建置 hello EchoService 專案。 接著，將部署 hello 服務 toohello IaaS 叢集中 hello 中相同的方式部署 tooan 內部部署叢集。 如需詳細步驟，請參閱 hello Readme.doc HelloWordR2 中。 修改及建置 hello HellWorldR2 和其他專案中下列區段 toogenerate hello SOA 用戶端應用程式在 Azure IaaS 叢集中執行的 hello 所述。

### <a name="use-http-binding-with-azure-storage-queue"></a>搭配使用 Http 繫結和 Azure 儲存體佇列
使用 Azure 儲存體佇列，toouse Http 繫結進行一些變更 toohello 範例程式碼。

* 更新 hello 叢集名稱。
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* 選擇性地用於 SessionStartInfo hello 預設 TransportScheme 或明確設定 tooHttp。

```
    info.TransportScheme = TransportScheme.Http;
```

* Hello BrokerClient 使用預設繫結。
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    或明確地使用 hello basicHttpBinding 設定。
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* （選擇性） 設定 hello UseAzureQueue 旗標 tootrue SessionStartInfo 中。 如果沒有設定，它就會設定 tootrue 預設 hello 叢集名稱已 Azure 網域尾碼和 hello TransportScheme 是 Http 時。
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>使用 Http 繫結而不使用 Azure 儲存體佇列
沒有 Azure 儲存體佇列中，明確地設定 hello UseAzureQueue 旗標 toofalse 在 hello SessionStartInfo toouse Http 繫結。

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>使用 NetTcp 繫結
toouse NetTcp 繫結，hello 組態是類似 tooconnecting tooan 在內部部署叢集。 您需要 tooopen hello 前端節點 VM 上的幾個端點。 如果您使用 hello HPC Pack IaaS 部署指令碼 toocreate hello 叢集時，例如，集合中的 hello 端點 hello Azure 入口網站，如下所示。

1. 停止 hello VM。
2. 將 hello TCP 連接埠 9090，9087，9091，9094 hello 工作階段中，為 Broker，分別 Broker 背景工作與資料服務
   
    ![設定端點][endpoint-new-portal]
3. 啟動 hello VM。

hello SOA 用戶端應用程式不需要變更除了改變 hello 前端名稱 toohello IaaS 叢集完整名稱。

## <a name="next-steps"></a>後續步驟
* 請參閱 [這些資源](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) 以取得使用 HPC Pack 執行 Excel 工作負載的詳細資訊。
* 請參閱 [管理 Microsoft HPC Pack 中的 SOA 服務](https://technet.microsoft.com/library/ff919412.aspx) 以取得使用 HPC Pack 部署和管理 SOA 服務的詳細資訊。

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
