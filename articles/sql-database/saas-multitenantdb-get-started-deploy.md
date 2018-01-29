---
title: "部署使用 Azure SQL Database 的分區化多租用戶 SaaS 應用程式 | Microsoft Docs"
description: "部署及探索分區化 Wingtip SaaS 多租用戶資料庫應用程式，其使用 Azure SQL Database 示範 SaaS 模式。"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg
editor: billgib;anjangsh
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/18/2017
ms.author: genemi
ms.openlocfilehash: a7e6e319fb2fa8fee762055b625427403d14d679
ms.sourcegitcommit: b7adce69c06b6e70493d13bc02bd31e06f291a91
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2017
---
# <a name="deploy-and-explore-a-sharded-multi-tenant-application-that-uses-azure-sql-database"></a>部署及探索使用 Azure SQL Database 的分區化多租用戶應用程式

在本教學課程中，您可以部署及探索稱為 Wingtip Tickets 的範例 SaaS 多租用戶資料庫應用程式。 Wingtip 應用程式是設計成用來展示簡化實作 SaaS 案例的 Azure SQL Database 功能。

這個 Wingtips 實作會使用分區化多租用戶資料庫模式。 分區化是依據租用戶識別碼。 租用戶資料會發佈到特定的資料庫，根據租用戶識別碼值。 不論指定資料庫包含多少租用戶，所有資料庫意義上都是多租用戶，因為資料表結構描述包括租用戶識別碼。 

此資料庫模式可讓您在每個分區化或資料庫中儲存一或多個租用戶。 您可以讓每個資料庫由多個租用戶分區化，以針對最低成本最佳化。 或者您可以讓每個資料庫僅儲存一個租用戶，以針對隔離最佳化。 您可以為每個特定租用戶獨立進行最佳化選擇。 第一次儲存租用戶時可以進行選擇，稍後您改變主意時也可以進行選擇。 應用程式的設計是這兩種方式都可以正常運作。

#### <a name="app-deploys-quickly"></a>應用程式部署快速

部署一節提供藍色**部署至 Azure**  按鈕。 按下按鈕時，Wingtip 應用程式會在 5 分鐘後完整部署。 Wingtip 應用程式會在 Azure 雲端中執行，並且使用 Azure SQL Database。 Wingtip 會部署到您的 Azure 訂用帳戶。 您具有完整存取權以使用個別應用程式元件。

應用程式是以三個範例租用戶的資料進行部署。 租用戶會一起儲存在一個多租用戶資料庫。

任何人都可以下載 C# 和 PowerShell 的原始程式碼從 Wingtip 票證[其 GitHub 儲存機制][link-github-wingtip-multitenantdb-55g]。

#### <a name="learn-in-this-tutorial"></a>在本教學課程中學到

> [!div class="checklist"]
> - 如何部署 Wingtip SaaS 應用程式。
> - 在何處取得應用程式原始程式碼和管理指令碼。
> - 關於組成應用程式的伺服器和資料庫。
> - 如何使用「目錄」將租用戶對應到其資料。
> - 如何佈建新租用戶。
> - 如何監視應用程式中的租用戶活動。

建置此初始部署時可以取得一系列相關的教學課程。 教學課程會探索 SaaS 設計和管理模式的範圍。 當您進行教學課程時，我們鼓勵您逐步執行提供的指令碼，以查看如何實作不同的 SaaS 模式。

## <a name="prerequisites"></a>必要條件

若要完成本教學課程，請確定已完成下列必要條件：

- 安裝最新版的 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell][link-azure-get-started-powershell-41q]。

## <a name="deploy-the-wingtip-tickets-app"></a>部署 Wingtip Tickets 應用程式

#### <a name="plan-the-names"></a>計劃名稱

在這一節的步驟中，有兩個位置，您必須在此輸入名稱，讓您為*使用者*和新*資源群組*。 名為個人的*王 Finley*，我們建議下列名稱：
- *使用者：* &nbsp; **af1** &nbsp; *（她首字母加上數字。）*
- *資源群組：* &nbsp; **wingtip af1** &nbsp; *（建議使用全部小寫。附加連字號，則使用者名稱。）*

現在，選擇您的名稱，並寫下它們。

#### <a name="steps"></a>步驟

1. 按一下下列的藍色**部署至 Azure**  按鈕。
    - 它會開啟 Azure 入口網站以及 Wingtip Tickets SaaS 部署範本。

    [![按鈕會部署至 Azure。][image-deploy-to-azure-blue-48d]][link-aka-ms-deploywtp-mtapp-52k]

2. 輸入部署必要的參數值。

    > [!IMPORTANT]
    > 此示範中，請勿使用任何預先存在的資源群組、 伺服器或集區。 相反地，選擇**建立新的資源群組**。 不使用應用程式之後請刪除此資源群組，以停止相關計費。
    > 請不要將此應用程式或任何它所建立的資源用於生產環境。 驗證和伺服器的防火牆設定，某些方面會刻意不安全，以協助示範在應用程式中。

    - 針對**資源群組** - 選取 [新建] 並提供資源群組的 [名稱] (區分大小寫)。
        - 從下拉式清單中選取 [位置]。
    - 如**使用者**-我們建議您選擇簡短**使用者**值。

3. **部署應用程式**。

    - 按一下以同意條款和條件。
    - 按一下 [購買]。

4. 按一下 [通知] (搜尋方塊右邊的鈴鐺圖示) 來監視部署狀態。 部署 Wingtip 應用程式大約需要五分鐘。

   ![部署成功](media/saas-multitenantdb-get-started-deploy/succeeded.png)

## <a name="download-and-unblock-the-management-scripts"></a>下載並解除封鎖管理指令碼

部署應用程式時，請下載應用程式原始程式碼和管理指令碼。

> [!NOTE]
> 從外部來源下載且解壓縮 zip 檔案時，可能由 Windows 封鎖可執行檔的內容 （指令碼、 Dll）。 從 zip 檔案解壓縮指令碼時，請遵循下列步驟先解除封鎖 .zip 檔案，再進行解壓縮。 解除封鎖.zip 檔案，您可以確保，允許執行指令碼。

1. 瀏覽至 [WingtipTicketsSaaS MultiTenantDb GitHub 存放庫](https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDb)。
2. 按一下 [複製或下載]。
3. 按一下 [下載 ZIP]，並儲存檔案。
4. 以滑鼠右鍵按一下 **WingtipTicketsSaaS-MultiTenantDb-master.zip** 檔案，然後選取 [屬性]。
5. 在 [一般] 索引標籤上，選取 [解除封鎖]，然後按一下 [套用]。
6. 按一下 [SERVICEPRINCIPAL] 。
7. 將檔案解壓縮。

指令碼位於 *..\\WingtipTicketsSaaS-MultiTenantDb-master\\Learning Modules\\* 資料夾中。

## <a name="update-the-configuration-file-for-this-deployment"></a>更新此部署的設定檔

執行任何指令碼之前，請在 **UserConfig.psm1** 中設定「資源群組」和「使用者」值。 將這些變數設定為您在部署期間所設定的相同值。

1. 開啟...\\學習模組\\*UserConfig.psm1*中*PowerShell ISE*。
2. 將 ResourceGroupName 和 Name 更新為您部署的特定值 (只在第 10 行和第 11 行)。
3. 儲存變更。

因此是很重要，它們是正確的指令碼，會使用此檔案中設定的值。 如果您重新部署應用程式，您必須選擇不同的值為使用者與資源群組。 然後再以新值更新 UserConfig.psm1 檔案。

## <a name="run-the-application"></a>執行應用程式

Wingtip 應用程式中的租用戶是管道。 法院可以搭配 hall、 運動社團或裝載事件的任何其他位置。 管道 Wingtip 中註冊為客戶，並為每個地點產生租用戶識別碼。 每個地點公用可以購買票證的事件會列出 Wingtip 中, 其即將發生的事件。

每個地點取得個人化的 web 應用程式來列出其事件，並銷售票券。 每個 web 應用程式是獨立且從其他租用戶隔離。 在 Azure SQL Database，每個租用戶資料預設儲存在分區化多租用戶資料庫中，每內部。 所有資料會都標記為租用戶識別碼。

中央**事件中樞**網頁提供給租用戶特定部署中的連結清單。 使用下列步驟，以體驗**事件中樞**網頁和個別 web 應用程式：

1. 在網頁瀏覽器中開啟 [事件中樞]：
    - http://events.wingtip。&lt;使用者&gt;。 trafficmanager.net &nbsp; *(取代&lt;使用者&gt;與您部署的使用者值。)*

    ![事件中樞](media/saas-multitenantdb-get-started-deploy/events-hub.png)

2. 按一下 [Events Hub (活動中心)] 中的 [Fabrikam Jazz Club (Fabrikam 爵士俱樂部)]。

   ![活動](./media/saas-multitenantdb-get-started-deploy/fabrikam.png)

#### <a name="azure-traffic-manager"></a>Azure 流量管理員

若要控制的連入要求發佈，Wingtip 應用程式會使用[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)。 每個租用戶的 [事件] 頁面包含它的 URL 中的租用戶名稱。 每個 URL 也包含特定的使用者值。 每個 URL 遵守所顯示的格式，請依照下列步驟：

- http://events.wingtip.&lt;USER&gt;.trafficmanager.net/fabrikamjazzclub

1. 事件的應用程式剖析 URL 從租用戶名稱。 租用戶名稱*fabrikamjazzclub*前面的範例 URL 中。
2. 應用程式然後雜湊來建立索引鍵來存取目錄使用租用戶名稱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。
3. 應用程式類別目錄中找到的索引鍵，並取得租用戶的資料庫的相對位置。
4. 應用程式使用的位置資訊來尋找及存取租用戶中包含的所有資料的資料庫。

#### <a name="events-hub"></a>事件中樞

1. **事件中樞**列出類別目錄和其名所註冊的所有租用戶。
2. [事件中樞] 會使用目錄中的延伸中繼資料來擷取與每個對應相關聯的租用戶名稱，以建構 URL。

在實際執行環境中，您通常會建立一筆 CNAME DNS 記錄[點將公司網際網路網域](../traffic-manager/traffic-manager-point-internet-domain.md)到流量管理員設定檔。

## <a name="start-generating-load-on-the-tenant-databases"></a>開始在租用戶資料庫上產生負載

應用程式已部署完成，請立即使用！ *Demo-LoadGenerator* PowerShell 指令碼會啟動對每個租用戶執行的工作負載。 許多 SaaS 應用程式的實際負載通常是偶發且無法預期的。 為了模擬這種類型的負載，產生器會產生跨所有租用戶散發的負載。 負載包含每個租用戶在隨機間隔發生的隨機暴增。 由於需要數分鐘的時間才會出現負載模式，因此，最好讓產生器先執行至少三或四分鐘，再監視負載。

1. 在 [PowerShell ISE] 中，開啟 ...\\Learning Modules\\Utilities\\*Demo-LoadGenerator.ps1* 指令碼。
2. 按 **F5** 來執行指令碼並啟動負載產生器 (目前先保留預設參數值)。

*Demo-LoadGenerator.ps1* 指令碼會在負載產生器執行所在位置開啟另一個 PowerShell 工作階段。 負載產生器會在此工作階段執行為前景工作，該工作會叫用背景負載產生作業，每個租用戶一個作業。

前景工作啟動之後，它會維持在作業叫用狀態。 工作會為後續佈建的任何新租用戶啟動額外背景作業。

關閉 PowerShell 工作階段會停止所有作業。

您可能想要重新啟動負載產生器工作階段，以使用不同的參數值。 如果是的話，請關閉 PowerShell 產生工作階段，然後重新執行 *Demo-LoadGenerator.ps1*。

## <a name="provision-a-new-tenant-into-the-sharded-database"></a>將新的租用戶佈建到分區化資料庫

初始部署在 Tenants1 資料庫中包含三個範例租用戶。 讓我們建立另一個租用戶，並觀察其效果上部署的應用程式。 在此步驟中，您可以按一個索引鍵建立新的租用戶：

1. 開啟...\\學習模組\\佈建和類別目錄\\*示範 ProvisionTenants.ps1*中*PowerShell ISE*。
2. 按**F5** (不**F8**) 執行指令碼 （現在為保留的預設值）。

   > [!NOTE]
   > 您必須執行 PowerShell 指令碼，只要按**F5**索引鍵，不是按**F8**執行選取的組件的指令碼。 問題**F8**在於*$PSScriptRoot*變數就不會進行評估。 此變數需要多指令碼來瀏覽的資料夾，或叫用其他指令碼，或匯入模組。

新的 Red Maple Racing 租用戶會新增至 Tenants1 資料庫，並在目錄中註冊。 新租用戶的票證銷售事件網站會在瀏覽器中開啟：

![新租用戶](./media/saas-multitenantdb-get-started-deploy/red-maple-racing.png)

重新整理**事件中樞**，且新的租用戶現在會顯示在清單中。

## <a name="provision-a-new-tenant-in-its-own-database"></a>在它自己的資料庫中佈建新租用戶

分區化的多租用戶模型可讓您選擇是否要佈建新的租用戶，到包含其他租用戶的資料庫或其本身的資料庫。 租用戶隔離在自己的資料庫以外的下列優點：
- 可以管理租用戶的資料庫的效能，而不需要與其他租用戶需求危害。
- 如有必要，資料庫會還原至之前的時間，因為會影響其他租用戶。

您可以選擇免費試用的客戶或經濟的客戶，放在多租用戶資料庫。 您可以將每個 premium 租用戶放入其本身專用的資料庫。 如果您建立許多包含只有一個租用戶的資料庫時，可以最佳化資源成本彈性集區中所有共同管理它們。

接下來，我們提供另一個租用戶，此時間以其本身的資料庫：

1. 中...\\學習模組\\佈建和類別目錄\\*示範 ProvisionTenants.ps1*，修改*$TenantName*至**Salix Salsa**， *$VenueType*至**舞**和*$Scenario*至**2**。

2. 按下 **F5** 以再次執行指令碼。
    - 這**F5**按佈建新的個別資料庫中新的租用戶。 資料庫和租用戶會在目錄中註冊。 然後瀏覽器會開啟至租用戶的 [事件] 分頁。

   ![Salix Salsa 事件分頁](./media/saas-multitenantdb-get-started-deploy/salix-salsa.png)

   - 向下捲動到分頁底部。 您會在那裡看到資料庫名稱的橫幅，這是租用戶資料的儲存位置。

3. 重新整理**事件中樞**和兩個新的租用戶現在會出現在清單中。

## <a name="explore-the-servers-and-tenant-databases"></a>探索伺服器和租用戶資料庫

現在我們看看一些已部署的資源：

1. 在 [Azure 入口網站](http://portal.azure.com)中，瀏覽至資源群組的清單。 開啟當您部署應用程式時建立的資源群組。

   ![資源群組](./media/saas-multitenantdb-get-started-deploy/resource-group.png)

2. 按一下 **catalog-mt&lt;USER&gt;** 伺服器。 目錄伺服器包含名為 tenantcatalog和 basetenantdb 的兩個資料庫。 basetenantdb 資料庫是空白的範本資料庫。 它會複製以建立新的租用戶資料庫，無論是用於許多租用戶或僅一個租用戶。

   ![目錄伺服器](./media/saas-multitenantdb-get-started-deploy/catalog-server.png)

3. 返回資源群組，然後選取保留租用戶資料庫的 tenants1-mt 伺服器。
    - tenants1 資料庫是多租用戶資料庫，其中會儲存原始的三個租用戶，加上您新增的第一個租用戶。 它會設定為 50 DTU 標準資料庫。
    - **Salixsalsa** 資料庫會保留 Salix Salsa 舞蹈場地，作為其唯一的租用戶。 根據預設，它會設定為 50 DTU 的標準版本資料庫。

   ![租用戶伺服器](./media/saas-multitenantdb-get-started-deploy/tenants-server.png)


## <a name="monitor-the-performance-of-the-database"></a>監視資料庫的效能

如果載入器已執行幾分鐘的時間，遙測資料不足可查看監視 Azure 入口網站內建功能的資料庫。

1. 瀏覽至 **tenants1-mt&lt;USER&gt;** 伺服器，然後按一下 [tenants1] 以檢視其中有四個租用戶之資料庫的資源使用率。 每個租用戶受限於負載產生器的偶發性過重負載：

   ![監視 tenants1](./media/saas-multitenantdb-get-started-deploy/monitor-tenants1.png)

   DTU 使用率圖表妥善說明多租用戶資料庫如何跨多個租用戶支援無法預測的工作負載。 在此情況下，負載產生器會將大約 30 DTU 的偶發性負載套用至每個租用戶。 此負載等於 50 DTU 資料庫的 60% 使用率。 超過 60% 的尖峰是同時將負載套用至多個租用戶的結果。

2. 瀏覽至**tenants1 mt&lt;使用者&gt;**伺服器，然後按一下**salixsalsa**資料庫。 在此資料庫包含只有一個租用戶，您可以看到的資源使用率。

   ![salixsalsa 資料庫](./media/saas-multitenantdb-get-started-deploy/monitor-salix.png)

負載產生器將類似負載套用至每個租用戶，不論每個租用戶位於哪個資料庫。 在 **salixsalsa** 資料庫中只有一個租用戶時，您可以看到相較於具有數個租用戶的資料庫，此資料庫可以承受較高的負載。 

#### <a name="resource-allocations-vary-by-workload"></a>資源配置會因工作負載

有時多租用戶資料庫需要更多資源的良好的效能比單一租用戶資料庫，但不是一定。 最佳的資源配置取決於特定工作負載特性為租用戶系統中。

負載產生器指令碼所產生的工作負載是僅供說明用途。

## <a name="additional-resources"></a>其他資源

- 若要了解多租用戶 SaaS 應用程式，請參閱[多租用戶 SaaS 應用程式的設計模式](saas-tenancy-app-design-patterns.md)。

- 若要深入了解彈性集區，請參閱：
    - [彈性集區可協助您管理及調整多個 Azure SQL database](sql-database-elastic-pool.md)
    - [使用 Azure SQL Database 相應放大](sql-database-elastic-scale-introduction.md)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解：

> [!div class="checklist"]
> - 如何部署 Wingtip 票證 SaaS 多租用戶資料庫應用程式。
> - 關於伺服器和資料庫，便會產生應用程式。
> - 租用戶會對應至其資料*目錄*。
> - 如何將新租用戶佈建到多租用戶資料庫與單一租用戶資料庫。
> - 如何檢視集區的使用率，以監視租用戶活動。
> - 如何刪除範例資源以停止相關計費。

現在，請嘗試[佈建和類別目錄教學課程](sql-database-saas-tutorial-provision-and-catalog.md)。


<!--  Link references.

A [series of related tutorials] is available that build upon this initial deployment.
[link-wtp-overivew-jumpto-saas-tutorials-97j]: saas-multitenantdb-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials

-->

[link-aka-ms-deploywtp-mtapp-52k]: http://aka.ms/deploywtp-mtapp


[link-azure-get-started-powershell-41q]: https://docs.microsoft.com/powershell/azure/get-started-azureps

[link-github-wingtip-multitenantdb-55g]: https://github.com/Microsoft/WingtipTicketsSaaS-MultiTenantDB/



<!--  Image references.

[image-deploy-to-azure-blue-48d]: http://aka.ms/deploywtp-mtapp "Button for Deploy to Azure."
-->

[image-deploy-to-azure-blue-48d]: media/saas-multitenantdb-get-started-deploy/deploy.png "部署至 Azure 的按鈕。"

