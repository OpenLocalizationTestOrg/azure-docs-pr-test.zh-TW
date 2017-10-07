---
title: "aaaSQL Server Business Intelligence |Microsoft 文件"
description: "本主題會使用與 hello 傳統部署模型，建立的資源，並描述執行 Azure 虛擬機器 (Vm) 上的 SQL Server 的 hello 商業智慧 (BI) 功能。"
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server Business Intelligence
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

hello Microsoft Azure 虛擬機器資源庫含有包含 SQL Server 安裝映像。 hello hello 圖庫映像中支援的版本是 SQL Server hello tooon 內部部署電腦與虛擬機器，您可以安裝的安裝檔案相同。 本主題摘要說明 SQL Server Business Intelligence (BI) hello hello 映像上安裝的功能和之後佈建虛擬機器所需的設定步驟。 本主題也描述 BI 功能支援的部署拓撲和最佳做法。

## <a name="license-considerations"></a>授權考量
有兩種方式 toolicense Microsoft Azure 虛擬機器中 SQL Server:

1. 屬於軟體保證的授權機動性優點。 如需詳細資訊，請參閱 [Azure 上透過軟體保證的授權機動性](https://azure.microsoft.com/pricing/license-mobility/)。
2. 支付安裝了 SQL Server 的 Azure 虛擬機器每小時的費用。 請參閱 < SQL Server > 一節中的 hello[虛擬機器定價](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql)。

如需有關授權和目前費率的詳細資訊，請參閱 [虛擬機器授權常見問題集](https://azure.microsoft.com/pricing/licensing-faq/%20/)。

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Azure 虛擬機器資源庫中提供 SQL Server 映像
hello Microsoft Azure 虛擬機器資源庫含有包含 Microsoft SQL Server 的數個映像。 hello hello 虛擬機器映像上安裝的軟體依據 hello hello 作業系統版本和 hello 的 SQL Server 版本而異。 hello 在 hello Azure 的虛擬機器映像庫映像清單經常變更。

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Azure VM 資源庫中的 SQL 映像](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) hello 下列 PowerShell 指令碼傳回 hello 在 hello ImageName 包含"SQL Server"的 Azure 映像清單：

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

如需有關版本和 SQL Server 支援功能的詳細資訊，請參閱 hello 下列：

* [SQL Server 版本](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [由 hello SQL Server 2016 版本的功能支援](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Hello SQL Server 虛擬機器圖庫映像上安裝的 BI 功能
hello 下表摘要說明 hello common Microsoft Azure 虛擬機器圖庫映像上安裝 SQL server 的 hello 商業智慧功能：

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| SQL Server BI 功能 | Hello 資源庫映像上安裝 | 注意事項 |
| --- | --- | --- |
| **Reporting Services 原生模式** |是 |安裝，但需要組態，包括 hello 報表管理員 URL。 請參閱 hello 節[設定 Reporting Services](#configure-reporting-services)。 |
| **Reporting Services SharePoint 模式** |否 |hello Microsoft Azure 虛擬機器資源庫映像不包含 SharePoint 或 SharePoint 安裝檔案。 <sup>1</sup> |
| **Analysis Services 多維度和資料採礦 (OLAP)** |是 |安裝和設定為 hello 預設 Analysis Services 執行個體 |
| **Analysis Services 表格式** |否 |SQL Server 2012、2014 和 2016 映像中支援，但預設不會安裝。 安裝另一個執行個體的 Analysis Services。 請參閱 hello 節安裝本主題中的其他 SQL Server 服務和功能。 |
| **適用於 SharePoint 的 Analysis Services Power Pivot** |否 |hello Microsoft Azure 虛擬機器資源庫映像不包含 SharePoint 或 SharePoint 安裝檔案。 <sup>1</sup> |

<sup>1</sup> 如需有關 SharePoint 和 Azure 虛擬機器的詳細資訊，請參閱[適用於 SharePoint 2013 的 Microsoft Azure 架構](https://technet.microsoft.com/library/dn635309.aspx)和 [Microsoft Azure 虛擬機器上的 SharePoint 部署](https://www.microsoft.com/download/details.aspx?id=34598)。

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) 在 hello 服務名稱中執行下列 PowerShell 命令 tooget hello 一份已安裝包含"SQL"的服務。

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>一般建議和最佳作法
* hello 最小的建議大小為虛擬機器**A3**時使用 SQL Server Enterprise Edition。 hello **A4**虛擬機器大小建議用於 SQL Server BI 部署的 Analysis Services 和 Reporting Services。
  
    如需目前 VM 大小 hello 資訊，請參閱[的 Azure 虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 磁碟管理的最佳作法是 toostore 資料、 記錄與磁碟機上的備份檔案**C**： 和**D**:。 例如，建立資料磁碟 **E**: 和 **F**:。
  
  * hello 快取原則 hello 預設磁碟機的磁碟機**C**： 不是使用資料的最佳選項。
  * hello **D**： 磁碟機是主要用於 hello 分頁檔的暫存磁碟機。 hello **D**： 磁碟機不會一直保存，並不會儲存在 blob 儲存體。 管理工作，例如變更 toohello 虛擬機器大小重設 hello **D**： 磁碟機。 建議太**不**使用 hello **D**： 資料庫檔案，包括 tempdb 磁碟機。
    
    如需有關建立及連接磁碟的詳細資訊，請參閱[如何 tooAttach 虛擬機器的資料磁碟 tooa](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
* 停止或解除安裝您不打算 toouse 的服務。 範例中，如果 hello 虛擬機器僅用於 Reporting Services，停止或解除安裝 Analysis Services 和 SQL Server Integration Services。 hello 圖是根據預設會啟動的 hello 服務的範例。
  
    ![SQL Server 服務](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > 中支援的 hello BI 案例需要 hello SQL Server database engine。 在單一伺服器 VM 拓撲中，是需要 hello 資料庫引擎上執行的 toobe hello 相同的 VM。
  
    如需詳細資訊，請參閱 hello 下列：[解除安裝 Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx)和[解除安裝的 Analysis Services 執行個體](https://msdn.microsoft.com/library/ms143687.aspx)。
* 檢查 **Windows Update** 以取得新的「重要更新」。 hello Microsoft Azure 虛擬機器映像經常在重新整理。不過，重要的更新無法成為可從**Windows Update**上次重新整理 hello VM 映像之後。

## <a name="example-deployment-topologies"></a>部署拓撲範例
hello 下面是使用 Microsoft Azure 虛擬機器的範例部署。 這些圖表中的 hello 拓撲只是一些 hello 可能的拓撲，您可以使用 SQL Server BI 功能和 Microsoft Azure 虛擬機器。

### <a name="single-virtual-machine"></a>單一虛擬機器
Analysis Services、Reporting Services、SQL Server Database Engine 和資料來源在單一虛擬機器上。

![具有 1 部虛擬機器的 BI IaaS 案例](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>兩部虛擬機器
* Analysis Services、 Reporting Services，並且單一的虛擬機器上的 SQL Server Database Engine hello。 此部署包含 hello 報表伺服器資料庫。
* 資料來源在第二部 VM 上。 hello 第二部 VM 包含 SQL Server Database Engine 做為資料來源。

![具有 2 部虛擬機器的 BI IaaS 案例](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>混合的 Azure - 資料在 Azure SQL 資料庫上
* Analysis Services、 Reporting Services，並且單一的虛擬機器上的 SQL Server Database Engine hello。 此部署包含 hello 報表伺服器資料庫。
* 資料來源是 Azure SQL 資料庫。

![BI IaaS 案例 VM 以及 AzureSQL 做為資料來源](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>混合 - 資料內部部署
* 此範例部署中 Analysis Services、 Reporting Services 和 SQL Server Database Engine hello 單一虛擬機器上執行。 hello 虛擬機器主機 hello 報表伺服器資料庫。 hello 虛擬機器是聯結的 tooan 透過 Azure 虛擬網路，在內部部署網域或一些其他 VPN 通道方案。
* 資料來源是在內部部署。

![BI IaaS 案例 VM 以及內部部署資料來源](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Reporting Services 原生模式組態
hello for SQL Server 虛擬機器資源庫映像包含 Reporting Services 原生模式安裝，不過 hello 報表伺服器未設定。 本節中的 hello 步驟 hello Reporting Services 報表伺服器的設定。 如需有關詳細設定 Reporting Services 原生模式的詳細資訊，請參閱 [安裝 Reporting Services 原生模式報表伺服器 (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx)。

> [!NOTE]
> 如需使用 Windows PowerShell 指令碼 tooconfigure hello 報表伺服器的類似內容，請參閱[使用 PowerShell tooCreate Azure VM 具有原生模式報表伺服器](../classic/ps-sql-report.md)。

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>連接 toohello 虛擬機器並啟動 Reporting Services 組態管理員 hello
有兩個連接 tooan Azure 虛擬機器的一般工作流程：

* 在 hello，tooconnect 按一下 hello hello 虛擬機器名稱，然後按一下**連接**。 遠端桌面連線開啟，並會自動填入 hello 電腦名稱。
  
    ![tooazure 虛擬機器連線](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* 使用 Windows 遠端桌面連線連接 toohello 虛擬機器。 在 hello hello 遠端桌面的使用者介面：
  
  1. 型別 hello**雲端服務名稱**作為 hello 電腦名稱。
  2. 輸入冒號 （:），然後 hello hello TCP 遠端桌面端點設定的公用連接埠號碼。
     
      Myservice.cloudapp.net:63133
     
      如需詳細資訊，請參閱 [什麼是雲端服務？](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/)。


**啟動 Reporting Services 組態管理員**

在 **Windows Server 2012/2016** 中：

1. 從 hello**啟動**畫面上，輸入**Reporting Services** toosee 應用程式清單。
2. 以滑鼠右鍵按一下 [Reporting Services 組態管理員]，然後按一下 [以系統管理員身分執行]。

在 **Windows Server 2008 R2**中：

1. 按一下 開始，然後按一下所有程式。
2. 按一下 [Microsoft SQL Server 2016] 。
3. 按一下 [組態工具] 。
4. 以滑鼠右鍵按一下 [Reporting Services 組態管理員]，然後按一下 [以系統管理員身分執行]。

或：

1. 按一下 [啟動] 。
2. 在 hello**搜尋程式及檔案**對話方塊類型**reporting services**。 Hello VM 正在執行 Windows Server 2012，如果輸入**reporting services** hello Windows Server 2012 [開始] 畫面上。
3. 以滑鼠右鍵按一下 [Reporting Services 組態管理員]，然後按一下 [以系統管理員身分執行]。
   
    ![搜尋 ssrs 組態管理員](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>設定 Reporting Services
**服務帳戶及 Web 服務 URL：**

1. 確認 hello**伺服器名稱**是 hello 本機伺服器名稱，然後按一下**連接**。
2. 請注意 hello 空白**報表伺服器資料庫名稱**。 hello 組態完成時，會建立 hello 資料庫。
3. 確認 hello**報表伺服器狀態**是**已啟動**。 如果您想 tooverify hello 服務在 Windows 伺服器管理員，hello 服務為 hello **SQL Server Reporting Services** Windows 服務。
4. 按一下**服務帳戶**並視需要變更 hello 帳戶。 如果在非網域的網域環境中使用 hello 虛擬機器，hello 內建**ReportServer**帳戶即足夠。 如需有關 hello 服務帳戶的詳細資訊，請參閱[服務帳戶](https://msdn.microsoft.com/library/ms189964.aspx)。
5. 按一下**Web 服務 URL** hello 左窗格中。
6. 按一下**套用**tooconfigure hello 預設值。
7. 請注意 hello**報表伺服器 Web 服務 Url**。 請注意，hello 預設 TCP 通訊埠為 80，並且是 hello URL 的一部分。 在稍後步驟中，您可以建立 hello 連接埠的 Microsoft Azure 虛擬機器端點。
8. 在 [hello**結果**] 窗格中，確認已順利完成的 hello 動作。

**資料庫：**

1. 按一下**資料庫**hello 左窗格中。
2. 按一下 [變更資料庫] 。
3. 確認 [建立新的報表伺服器資料庫]  選取，然後按 [下一步]。
4. 確認 [伺服器名稱]，然後按一下 [測試連接]。
5. 如果 hello 結果為**連接測試成功**，按一下**確定**，然後按一下**下一步**。
6. 注意 hello 資料庫名稱是**ReportServer**和 hello**報表伺服器模式**是**原生**然後按一下 **下一步**。
7. 按一下**下一步**上 hello**認證**頁面。
8. 按一下**下一步**上 hello**摘要**頁面。
9. 按一下**下一步**上 hello**進度和完成**頁面。

**入口網站 URL 或 2012 和 2014 版的報表管理員 URL：**

1. 按一下**入口網站 URL**，或**報表管理員 URL** 2014年和 2012，hello 左窗格中的。
2. 按一下 [Apply (套用)] 。
3. 在 [hello**結果**] 窗格中，確認已順利完成的 hello 動作。
4. 按一下 [結束] 。

如需報表伺服器權限的詳細資訊，請參閱 [在原生模式報表伺服器上授與權限](https://msdn.microsoft.com/library/ms156014.aspx)。

### <a name="browse-toohello-local-report-manager"></a>瀏覽 toohello 本機報表管理員
在 hello VM 上瀏覽 tooreport 管理員 tooverify hello 組態。

1. 在 hello VM，請使用系統管理員權限啟動 Internet Explorer。
2. 瀏覽 toohttp://localhost/reports hello VM 上。

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>tooConnect tooRemote 入口網站或 2014年和 2012年的報表管理員
如果您想 tooconnect toohello 入口網站或報表管理員 2014年和 2012，從遠端電腦，hello 虛擬機器上的建立新的虛擬機器 TCP 端點。 根據預設，hello 報表伺服器會接聽 HTTP 要求上**連接埠 80**。 如果您設定 hello 報表伺服器 Url toouse 不同的通訊埠，您必須在下列指示的 hello 指定該通訊埠編號。

1. 建立 hello TCP 連接埠 80 的虛擬機器的端點。 如需詳細資訊，請參閱 hello[虛擬機器端點和防火牆連接埠](#virtual-machine-endpoints-and-firewall-ports)這份文件中的一節。
2. Hello 虛擬機器的防火牆中開啟通訊埠 80。
3. 瀏覽 toohello 入口網站或報表管理員中，使用 Azure 虛擬機器**DNS 名稱**做為 hello hello URL 中的伺服器名稱。 例如：
   
    **報表伺服器**：http://uebi.cloudapp.net/reportserver **Web 入口網站**：http://uebi.cloudapp.net/reports
   
    [為報表伺服器存取設定防火牆](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate 和發行報表 toohello Azure 虛擬機器
hello 下表將摘要列出一些 hello Microsoft Azure 虛擬機器上裝載在內部部署電腦 toohello 報表伺服器中的 hello 選項可用 toopublish 現有報表：

* **報表產生器**: hello 虛擬機器包含 hello 按一下-click-once 版本的 Microsoft SQL Server 報表產生器適用於 SQL 2014 和 2012年。 toostart 報表產生器 hello hello SQL 2016 的虛擬機器上的第一次：
  
  1. 以管理權限啟動瀏覽器。
  2. 瀏覽 toohello web 入口網站上 hello 虛擬機器，並選取 hello**下載**hello 右上角的圖示。
  3. 選取 [報表產生器] 。
     
     如需詳細資訊，請參閱 [啟動報表產生器](https://msdn.microsoft.com/library/ms159221.aspx)。
* **SQL Server Data Tools**: VM: SQL Server Data Tools 安裝在 hello 虛擬機器上，而且可以是使用的 toocreate**報表伺服器專案**和 hello 虛擬機器上的報表。 SQL Server Data Tools 可以發佈 hello 報表 toohello hello 虛擬機器上的報表伺服器。
* **SQL Server Data Tools：遠端**：在本機電腦上，以 SQL Server Data Tools 建立含有 Reporting Services 報告的 Reporting Services 專案。 設定 hello 專案 tooconnect toohello web 服務 URL。
  
    ![SSRS 專案的 ssdt 專案屬性](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* 建立。VHD 硬碟包含報表，然後上傳並附加 hello 磁碟機。
  
  1. 在您的本機電腦上建立包含報表的 .VHD 硬碟機。
  2. 建立及安裝管理憑證。
  3. 上傳使用 hello Add-azurevhd cmdlet hello VHD 檔案 tooAzure[建立並上傳 Windows Server VHD tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
  4. 附加 hello 磁碟 toohello 虛擬機器。

## <a name="install-other-sql-server-services-and-features"></a>安裝其他 SQL Server 服務和功能
tooinstall 其他 SQL Server 服務，例如 Analysis Services 表格式模式中執行 hello SQL server 安裝精靈。 hello 安裝程式檔案位於 hello 虛擬機器的本機磁碟上。

1. 按一下 開始，然後按一下所有程式。
2. 按一下 Microsoft SQL Server 2016、Microsoft SQL Server 2014 或 Microsoft SQL Server 2012，然後按一下組態工具。
3. 按一下 [SQL Server 安裝中心] 。

或執行 C:\SQLServer_13.0_full\setup.exe、C:\SQLServer_12.0_full\setup.exe 或 C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> hello 第一次執行 SQL Server 安裝程式，可能會下載檔案，且需要重新開機的 hello 虛擬機器，並重新啟動 SQL Server 安裝程式的詳細安裝程式。
> 
> 如果您需要 toorepeatedly 自訂 hello hello Microsoft Azure 虛擬機器從選取的映像，請考慮建立您自己的 SQL Server 映像。 Analysis Services SysPrep 功能是隨著 SQL Server 2012 SP1 CU2 啟用。 如需詳細資訊，請參閱[使用 SysPrep 安裝 SQL Server 的考量](https://msdn.microsoft.com/library/ee210754.aspx)和 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall Analysis Services 表格式模式
本章節步驟 hello**摘要**hello 的 Analysis Services 表格式模式安裝。 如需詳細資訊，請參閱 hello 下列：

* [以表格式模式安裝 Analysis Services](https://msdn.microsoft.com/library/hh231722.aspx)
* [表格式模型化 (Adventure Works 教學課程)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall Analysis Services 表格式模式：**

1. 在 hello SQL Server 安裝精靈中，按一下 **安裝**在 hello 左的窗格，然後按一下**新的 SQL server 獨立安裝或加入現有安裝的功能 tooan**。
   
   * 如果您看到 hello**瀏覽資料夾**，瀏覽 tooc:\SQLServer_13.0_full、 c:\SQLServer_12.0_full 或 c:\SQLServer_11.0_full，然後按一下**確定**。
2. 按一下**下一步**在 hello 產品更新 頁面。
3. 在 [hello**安裝類型**頁面上，選取**執行新安裝的 SQL Server**按一下**下一步]**。
4. 在 hello**安裝程式角色**頁面上，按一下**SQL Server 功能安裝**。
5. 在 hello**特徵選取**頁面上，按一下**Analysis Services**。
6. 在 hello**執行個體組態**頁面上，輸入描述性名稱，例如**表格式**到**具名執行個體**和**執行個體識別碼**文字方塊。
7. 在 hello **Analysis Services 組態**頁面上，選取**表格式模式**。 加入 hello 目前使用者 toohello 系統管理員權限清單。
8. 完成並關閉 hello SQL Server 安裝精靈。

## <a name="analysis-services-configuration"></a>Analysis Services 組態
### <a name="remote-access-tooanalysis-services-server"></a>遠端存取 tooAnalysis 服務伺服器
Analysis Services 伺服器僅支援 Windows 驗證。 從用戶端應用程式，例如 SQL Server Management Studio 或 SQL Server Data Tools 遠端 tooaccess Analysis Services hello 虛擬機器需要 toobe tooyour 聯結本機網域，使用 Azure 虛擬網路。 如需詳細資訊，請參閱 [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)。

Analysis Services 的**預設執行個體**會接聽 TCP 連接埠 **2383**。 Hello 虛擬機器防火牆中開啟 hello 連接埠。 Analysis Services 的叢集具名執行個體也會接聽連接埠 **2383**。

如**具名執行個體**Analysis Services 的 SQL Server Browser 服務的 hello 無須 toomanage 連接埠存取。 hello SQL Server Browser 預設組態為通訊埠**2382年**。

在 hello 虛擬機器防火牆中，開啟 連接埠**2382年**並建立靜態 Analysis Services 具名執行個體的連接埠。

1. tooverify 連接埠已經在 hello VM 和哪些處理序正在使用 hello 連接埠上使用，請執行下列命令，以系統管理權限的 hello:
   
        netstat /ao
2. 使用 SQL Server Management Studio toocreate 靜態的 Analysis Services 已命名執行個體的連接埠藉由更新 'Port' 值中表格式 AS 執行個體一般屬性。 如需詳細資訊，請參閱 hello 中的 「 使用固定通訊埠是預設或具名執行個體 」[設定 hello Analysis Services 存取的 Windows 防火牆 tooAllow](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed)。
3. 重新啟動 Analysis Services 服務的 hello hello 表格式執行個體。

如需詳細資訊，請參閱 hello**虛擬機器端點和防火牆連接埠**這份文件中的一節。

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>虛擬機器端點和防火牆連接埠
本節摘要說明 Microsoft Azure 虛擬機器端點 toocreate 和連接埠 tooopen hello 虛擬機器防火牆中。 hello 下表摘要說明 hello **TCP** toocreate 端點以及 hello 連接埠 tooopen hello 虛擬機器防火牆中的連接埠。

* 如果您要使用單一 VM hello 下列兩個項目時，您不需要 toocreate VM 端點，而且您不需要 tooopen hello hello hello VM 上的防火牆連接埠。
  
  * 您要從遠端連線 toohello hello VM 上的 SQL Server 功能。 建立遠端桌面連線 toohello VM，以及存取 hello hello VM 在本機的 SQL Server 功能並不是遠端連線 toohello SQL Server 功能。
  * 不要將透過 Azure 虛擬網路或其他 VPN 通道方案 hello VM tooan 在內部部署網域。
* 如果 hello 虛擬機器不是聯結的 tooa 網域，但是您想 tooremotely 連接 toohello VM 上的 SQL Server 功能：
  
  * Hello hello VM 防火牆中開啟 hello 連接埠。
  * 建立虛擬機器端點 hello 記下連接埠 （*）。
* 如果使用 VPN 通道，例如 Azure 虛擬網路的聯結的 tooa 網域 hello 虛擬機器，然後 hello 端點不需要。 不過 hello hello VM 防火牆中開啟 hello 連接埠。
  
  | Port | 類型 | 說明 |
  | --- | --- | --- |
  | **80** |TCP |報表伺服器遠端存取 (\*)。 |
  | **1433** |TCP |SQL Server Management Studio (\*)。 |
  | **1434** |UDP |SQL Server Browser。 這被必要時 hello 聯結的 tooa 網域中的 VM。 |
  | **2382** |TCP |SQL Server Browser。 |
  | **2383** |TCP |SQL Server Analysis Services 預設執行個體和叢集具名執行個體。 |
  | **使用者定義** |TCP |建立靜態 Analysis Services 具名執行個體的連接埠的通訊埠編號，您選擇，，然後解除封鎖 hello hello 防火牆連接埠號碼。 |

如需有關建立端點的詳細資訊，請參閱 hello 下列：

* 建立端點：[如何 tooSet 端點 tooa 虛擬機器](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。
* SQL Server： 請參閱 hello 「 完成組態步驟 tooconnect toohello 虛擬機器使用 SQL Server Management Studio 」 一節[佈建在 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)。

hello 下列圖表說明在 hello VM 防火牆 tooallow 遠端存取 toofeatures hello 連接埠 tooopen 和 hello VM 上的元件。

![Azure Vm 中 bi 應用程式的連接埠 tooopen](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>資源
* 檢閱 hello hello Azure 虛擬機器環境中使用的 Microsoft 伺服器軟體的支援原則。 hello 遵循主題摘要說明支援 BitLocker、 容錯移轉叢集和網路負載平衡等功能。 [Azure 虛擬機器的 Microsoft 伺服器軟體支援](http://support.microsoft.com/kb/2721672)。
* [Azure 虛擬機器上的 SQL Server 概觀](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [在 Azure 上佈建 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [如何 tooAttach 資料磁碟 tooa 虛擬機器](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [移轉資料庫 tooSQL Azure VM 上的伺服器](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [判斷 hello Analysis Services 執行個體的伺服器模式](https://msdn.microsoft.com/library/gg471594.aspx)
* [多維度模型化 (Adventure Works 教學課程)](https://technet.microsoft.com/library/ms170208.aspx)
* [Azure 文件中心](https://azure.microsoft.com/documentation/)
* [在混合式環境中使用 Power BI](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [透過 Microsoft SQL Server Connect 提交意見和連絡資訊](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>社群內容
* [使用 PowerShell 管理 Azure SQL Database](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

