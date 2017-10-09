---
title: "aaaInstalling 彈性資料庫工作 |Microsoft 文件"
description: "逐步解說 hello 彈性的工作功能的安裝。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a>安裝彈性資料庫工作概觀
[**彈性資料庫工作**](sql-database-elastic-jobs-overview.md)可以透過 PowerShell 來安裝或透過 hello Azure 傳統 Portal.You 可以獲得存取 toocreate 和安裝 hello PowerShell 封裝時才使用 hello PowerShell API 來管理工作。 此外，hello PowerShell Api 提供更多的功能比 hello 入口網站在此時間點。

如果您已安裝**彈性資料庫工作**透過 hello 入口網站，從現有**彈性集區**，hello 最新的 Powershell preview 包含指令碼 tooupgrade 現有的安裝。 它強烈建議的最新 tooupgrade 安裝 toohello**彈性資料庫工作**順序 tootake 利用透過公開的新功能中的元件 hello PowerShell Api。

## <a name="prerequisites"></a>必要條件
* Azure 訂用帳戶。 如需免費試用版，請參閱 [免費試用版](https://azure.microsoft.com/pricing/free-trial/)。
* Azure PowerShell。 安裝使用 hello hello 最新版本[Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376)。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* [NuGet 命令列公用程式](https://nuget.org/nuget.exe)是使用的 tooinstall hello 彈性資料庫工作的封裝。 如需詳細資訊，請參閱 http://docs.nuget.org/docs/start-here/installing-nuget。

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a>下載並匯入 hello 彈性資料庫工作 PowerShell 封裝
1. 啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello 下載的目錄，NuGet 命令列公用程式 (nuget.exe)。
2. 下載並匯入**彈性資料庫工作**封裝到 hello 目前目錄中以 hello 下列命令：
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    hello**彈性資料庫工作**檔案會放在資料夾中的 hello 本機目錄**Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**其中*x.x.xxxx.x*反映 hello 版本號碼。 hello PowerShell cmdlet （包括必要的用戶端.dll 檔） 位於 hello **tools\ElasticDatabaseJobs**子目錄 hello PowerShell 指令碼 tooinstall，升級和解除安裝也位於 hello **工具**子目錄。
3. 輸入 cd 工具，例如瀏覽 toohello 工具子目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 資料夾底下：
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. 執行的 hello.\InstallElasticDatabaseJobsCmdlets.ps1 指令碼 toocopy hello ElasticDatabaseJobs 目錄於 $home\Documents\WindowsPowerShell\Modules。 這將例如也會自動匯入供使用，hello 模組：
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a>使用 PowerShell 的 hello 彈性資料庫工作元件安裝
1. 啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello \tools 子資料夾下的目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x： 輸入 cd \tools
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. 執行 hello.\InstallElasticDatabaseJobs.ps1 PowerShell 指令碼，並且提供其要求的變數值。 此指令碼會建立描述 hello 元件[彈性資料庫工作的元件和定價](sql-database-elastic-jobs-overview.md#components-and-pricing)以及設定 Azure 雲端服務的 hello tooappropriately 使用 hello 相依元件。

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

當您執行此命令時，會開啟一個向您詢問「使用者名稱」和「密碼」的視窗。 這不是您的 Azure 認證，請輸入 hello 使用者名稱和密碼，將會是您想要新的伺服器 hello toocreate hello 系統管理員認證。

這個範例引動過程上提供的 hello 參數都可以修改您所需的設定。 hello 下列會提供有關每個參數的 hello 行為的詳細資訊：

<table style="width:100%">
  <tr>
    <th>參數</th>
    <th>說明</th>
  </tr>

<tr>
    <td>resourceGroupName</td>
    <td>提供建立新建立的 Azure 元件的 toocontain hello hello Azure 資源群組名稱。 此參數的預設值太"__ElasticDatabaseJob"。 不建議 toochange 此值。</td>
    </tr>

</tr>

    <tr>
    <td>ResourceGroupLocation</td>
    <td>提供用於新建立的 Azure 元件的 hello hello Azure 位置 toobe。 此參數的預設值 toohello 美國中部位置。</td>
</tr>

<tr>
    <td>ServiceWorkerCount</td>
    <td>提供服務工作者 tooinstall hello 數的字。 此參數的預設值 too1。 有較多的工作者可以使用的 tooscale 出 hello 服務和 tooprovide 高可用性。 建議您針對需要高可用性的 hello 服務部署 toouse"2"。</td>
    </tr>

</tr>
    <tr>
    <td>ServiceVmSize</td>
    <td>提供 hello 雲端服務內的使用量 hello VM 大小。 此參數的預設值 tooA0。 接受 A0/A1/A2/A3 的參數值會造成 hello 背景工作角色 toouse ExtraSmall/小型/中等/大型大小，分別。 如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</td>
</tr>

</tr>
    <tr>
    <td>SqlServerDatabaseSlo</td>
    <td>Standard edition 提供 hello 服務等級目標。 此參數的預設值 tooS0。 接受的 S0/S1/S2/S3 的參數值會造成 hello Azure SQL Database toouse hello 各自的 SLO。 如需有關 SQL Database SLO 的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorUserName</td>
    <td>提供 hello hello 新建立的 Azure SQL Database 伺服器的系統管理員使用者名稱。 未指定，PowerShell 認證視窗就會開啟 tooprompt hello 認證。</td>
</tr>

</tr>
    <tr>
    <td>SqlServerAdministratorPassword</td>
    <td>提供新建立的 Azure SQL Database 伺服器 hello hello 系統管理員密碼。 未提供時，PowerShell 認證視窗會開啟 tooprompt hello 認證。</td>
</tr>
</table>

對於需要大量的數字，以平行方式大量資料庫對執行中的作業為目標的系統，建議 toospecify 參數例如:-ServiceWorkerCount 2-ServiceVmSize A2-SqlServerDatabaseSlo S2。

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a>使用 PowerShell 更新現有的彈性資料庫工作元件安裝
**彈性資料庫工作** 可以在現有的安裝中更新，以進行擴充和高可用性。 此程序而不需要 toodrop 允許未來升級的服務程式碼，並重新建立 hello 控制資料庫。 此程序也可用於 hello 相同版本 toomodify hello 服務 VM 大小或 hello 伺服器背景工作計數。

tooupdate hello VM 大小的安裝，執行下列指令碼參數的 hello 更新您所選擇的 toohello 值。

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th>參數</th>
  <th>說明</th>
</tr>

  <tr>
    <td>resourceGroupName</td>
    <td>識別一開始安裝 hello 彈性資料庫工作的元件時所使用的 hello Azure 資源群組名稱。 此參數的預設值太"__ElasticDatabaseJob"。 因為它不是建議 toochange 此值，您不應該有 toospecify 這個參數。</td>
    </tr>
</tr>

</tr>

  <tr>
    <td>ServiceWorkerCount</td>
    <td>提供服務工作者 tooinstall hello 數的字。  此參數的預設值 too1。  有較多的工作者可以使用的 tooscale 出 hello 服務和 tooprovide 高可用性。  建議您針對需要高可用性的 hello 服務部署 toouse"2"。</td>
</tr>

</tr>

    <tr>
    <td>ServiceVmSize</td>
    <td>提供 hello 雲端服務內的使用量 hello VM 大小。 此參數的預設值 tooA0。 接受 A0/A1/A2/A3 的參數值會造成 hello 背景工作角色 toouse ExtraSmall/小型/中等/大型大小，分別。 如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a>安裝 hello 彈性資料庫工作元件使用 hello 入口網站
一旦[建立彈性集區](sql-database-elastic-pool-manage-portal.md)，您可以安裝**彈性資料庫工作**元件 tooenable 執行 hello 彈性集區中的每個資料庫的系統管理工作。 不同於當使用 hello**彈性資料庫工作**PowerShell Api hello 入口網站介面是針對現有的集區執行的目前限制的 tooonly。

**估計時間 toocomplete:** 10 分鐘。

1. Hello hello 透過彈性集區的 hello 儀表板檢視從[Azure 入口網站](https://portal.azure.com/#)，按一下 **建立工作**。
2. 如果您第一次建立 hello 的作業，您必須安裝**彈性資料庫工作**按一下**預覽條款**。
3. 接受 hello 條款，依序按一下 hello 核取方塊。
4. 在 hello 「 安裝服務 」 檢視中，按一下 **工作認證**。
   
    ![安裝 hello 服務][1]
5. 輸入資料庫管理員的使用者名稱和密碼。Hello 安裝的一部分，會建立新的 Azure SQL Database 伺服器。 在這個新的伺服器、 新的資料庫，又稱為 hello 控制資料庫，建立和 toocontain hello 中繼資料用於彈性資料庫工作。 這裡建立 hello 使用者名稱和密碼可用來在 toohello 控制資料庫中記錄的 hello 用途。 執行指令碼針對 hello 集區中的 hello 資料庫使用不同的認證。
   
    ![建立使用者名稱和密碼][2]
6. 按一下 [確定] 按鈕，hello。 hello 元件會為您建立新的幾分鐘後[資源群組](../azure-resource-manager/resource-group-overview.md)。 hello 新資源群組已釘選 toohello 開始面板，如下所示。 一旦建立後，彈性資料庫作業 （雲端服務、 SQL Database、 Service Bus 和儲存體） 會在 hello 群組建立。
   
    ![「開始面板」中的資源群組][3]
7. 如果您嘗試 toocreate 或管理工作，但在安裝彈性資料庫工作，提供**認證**您會看到下列訊息的 hello。
   
    ![部署仍在進行中][4]

如果需要解除安裝，請刪除 hello 資源群組。 請參閱[toouninstall hello 彈性資料庫工作元件的方式](sql-database-elastic-jobs-uninstall.md)。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 [hello] 群組中的每個資料庫建立指令碼執行所確保 hello 適當的權限的認證[保護您的 SQL Database](sql-database-manage-logins.md)。
請參閱[建立和管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)tooget 啟動。

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
