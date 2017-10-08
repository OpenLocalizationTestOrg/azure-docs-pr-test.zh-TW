---
title: "Azure backup aaaConfigure 報表"
description: "本文說明如何使用復原服務保存庫針對 Azure 備份設定 Power BI 報告。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>設定 Azure 備份報告
這篇文章參步驟 tooconfigure 報表使用 復原服務保存庫和 tooaccess Azure backup 使用 Power BI 報表。 執行這些步驟之後，您可以直接前往 tooPower BI tooview hello 的所有報表、 自訂及建立報表。 

## <a name="supported-scenarios"></a>支援的案例
1. Azure 虛擬機器備份和檔案/資料夾備份 toocloud 使用 Azure 復原服務代理程式支援 azure Backup 的報表。
2. 目前不支援針對 Azure SQL、DPM 和 Azure 備份伺服器的報告功能。
3. 您可以檢視報告跨保存庫，以及跨訂用帳戶，如果相同的儲存體帳戶設定為每個 hello 保存庫。 選取的儲存體帳戶應在 hello 相同區域復原服務保存庫。
4. hello 的 hello 報表排程重新整理頻率是 Power BI 中的 24 小時。 您也可以執行特定的重新整理 hello 報表在 Power BI 中案例的最新資料，客戶儲存體帳戶中用於轉譯報表。 

## <a name="prerequisites"></a>必要條件
1. 建立[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)tooconfigure 它的報告。 這個儲存體帳戶是用來儲存與報告相關的資料。
2. [建立 Power BI 帳戶](https://powerbi.microsoft.com/landing/signin/)tooview，自訂和建立您自己的報表使用 Power BI 入口網站。
3. 註冊 hello 資源提供者**Microsoft.insights**如果沒有已登錄，與 hello 訂用帳戶的儲存體帳戶和與 hello 訂用帳戶的 復原服務保存庫 tooenable 報告資料 tooflow toohello儲存體帳戶。 toodo hello 相同，您必須移 tooAzure 入口網站 > 訂用帳戶 > 資源提供者並檢查此提供者 tooregister 它。 

## <a name="configure-storage-account-for-reports"></a>針對報告設定儲存體帳戶
使用下列步驟 tooconfigure hello 儲存體帳戶使用 Azure 入口網站的復原服務保存庫的 hello。 這是一次性的組態和儲存體帳戶設定之後，您可以移 tooPower BI 直接 tooview 內容套件，並利用報告。
1. 如果您已經開啟的復原服務保存庫，請繼續執行 toonext 步驟。 如果您不需要復原服務保存庫開啟之後，但在 hello hello 中樞功能表中，在 Azure 入口網站中按一下**瀏覽**。

   * 在 [hello] 清單中的資源，輸入**復原服務**。
   * 當您開始輸入 hello 清單會篩選根據您的輸入。 當您看到 [復原服務保存庫] 時，請按一下它。

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     復原服務保存庫 hello 清單隨即出現。 從 hello 清單的 復原服務保存庫中，選取保存庫。

     hello 選取保存庫儀表板隨即開啟。
2. 從 hello 的項目清單會出現在保存庫下，按一下 **備份報告**監視與報表區段 tooconfigure hello 儲存體帳戶的報表。

      ![選取備份報告功能表項目步驟 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. 在 hello 備份報告刀鋒視窗中，按一下 **設定** 按鈕。 這會開啟 hello Azure Application Insights 刀鋒視窗中，可用來將推送資料 toocustomer 儲存體帳戶。

      ![設定儲存體帳戶步驟 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. 設定得 hello 狀態切換按鈕**上**選取**封存儲存體帳戶 tooa**核取方塊，以便資料可以開始送 toohello 儲存體帳戶中的報告。

      ![啟用診斷步驟 4](./media/backup-azure-configure-reports/set-status-on.png)
5. 按一下 儲存體帳戶選擇器和選取 hello 儲存體帳戶，從 hello 清單，以儲存報告的資料以及按一下**確定**。

      ![選取儲存體帳戶步驟 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. 選取**AzureBackupReport**核取方塊，也會移動這個 hello 滑桿 tooselect 保留期限報告資料。 報告 hello 儲存體帳戶中的資料會保留選取 使用此滑桿 hello 週期。

      ![選取儲存體帳戶步驟 6](./media/backup-azure-configure-reports/save-configuration.png)
7. 檢閱所有 hello 變更，然後按一下**儲存**按鈕上方，hello 上圖所示。 此動作可確保所有變更都會儲存，且儲存體帳戶已針對儲存報告資料進行設定。

> [!NOTE]
> 一旦您藉由儲存儲存體帳戶設定的報表，您應該**等待 24 小時**的初始資料推入 toocomplete。 只有在該時間之後，您才需要將 Power BI 中的 Azure 備份內容套件匯入。 如需進一步的詳細資料，請參閱[常見問題集一節](#frequently-asked-questions)。 
>
>

## <a name="view-reports-in-power-bi"></a>在 Power BI 中檢視報告 
使用 復原服務保存庫設定儲存體帳戶的報告之後，它會報告中傳送的資料 toostart 大約 24 小時。 24 小時之後設定儲存體帳戶，使用 hello 下列步驟會在 Power BI 中的 tooview 報表：
1. [登入](https://powerbi.microsoft.com/landing/signin/)tooPower BI。
2. 按一下 [取得資料]，然後在內容套件庫中的 [服務] 底下，按一下 [取得]。 使用中所述的步驟[Power BI 文件 tooaccess 內容套件](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)。

     ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-import.png)
3. 在搜尋列中輸入 **Azure Backup**，並按一下 [立即取得]。

      ![取得內容套件](./media/backup-azure-configure-reports/content-pack-get.png)
4. 輸入 hello 上述步驟 5 中設定的儲存體帳戶名稱，然後按一下**下一步** 按鈕。

    ![輸入儲存體帳戶名稱](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. 輸入 hello 這個儲存體帳戶的儲存體帳戶金鑰。 您可以[檢視和複製儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)瀏覽 tooyour Azure 入口網站中的儲存體帳戶。 

     ![輸入儲存體帳戶](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. 按一下 [登入] 按鈕。 登入成功後，您會收到「匯入資料」的通知。

    ![匯入內容套件](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    取得一段時間後**成功**hello 匯入完成後的通知。 如果有大量的 hello 儲存體帳戶中的資料可能需要很少長 tooimport hello 內容套件。
    
    ![成功匯入內容套件](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. 成功時，匯入資料之後**Azure Backup**內容套件會顯示在**應用程式**hello 瀏覽窗格中。 hello 清單現在會顯示 Azure Backup 儀表板、 報表和資料集以黃色星號表示新匯入的報表。 

     ![Azure 備份內容套件](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. 按一下 [儀表板] 底下的 [Azure 備份]，這會顯示一組已釘選的重要資訊報告。

      ![Azure 備份儀表板](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. tooview hello 整組報表，按一下 hello 儀表板中的任何報表。

      ![Azure 備份作業健康情況](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. 按一下該區域中的 hello 報表 tooview 報表中的每個索引標籤。

      ![Azure 備份報告索引標籤](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>常見問題集
1. **如何檢查如果報告資料後啟動流動 toostorage 帳戶中？**
    
    您可以移 toohello 儲存體帳戶設定和選取的容器。 如果 hello 容器擁有 insights-記錄檔-azurebackupreport 的項目，就表示，報告資料以啟動的流動。

2. **什麼是資料推入 toostorage 帳戶和 Azure 備份的內容套件在 Power BI 中的 hello 頻率？**

   對於第 0 天的使用者，將花費大約 24 小時 toopush 資料 toostorage 帳戶。 一旦此初始推送 compelete，hello 遵循 hello 圖所示的頻率重新整理資料。 
      * 資料太相關**作業、 警示、 備份的項目、 保存庫、 受保護的伺服器和原則**推 toocustomer 儲存體帳戶，並在登入。
      * 資料太相關**儲存體**會每隔 24 小時推送 toocustomer 儲存體帳戶。
   
    ![Azure 備份報表資料推送頻率](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI 具有[一天一次的排程重新整理](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)。 您可以執行在 Power BI 中的手動資料重新整理的 hello hello 內容套件。

3. **時間長度可以保留 hello 報表？** 

   在設定儲存體帳戶時，您可以選取報告資料的保留的期限 hello 儲存體帳戶 （使用上述的報表區段的設定儲存體帳戶中的步驟 6） 中。 除此之外，您可以根據需求[在 Excel 中分析報告](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)並儲存它們，以延長保留期間。 

4. **會看到我的所有資料在報表中之後設定 hello 儲存體帳戶？**

   所有 hello 之後產生的資料**」 設定儲存體帳戶"**推入 toohello 儲存體帳戶，而且會出現在報表中。 不過，「進行中的作業」將不會針對報告進行推送。 一旦 hello 工作完成或失敗，它會傳送 tooreports。

5. **如果我已經設定 hello 存放裝置帳戶 tooview 報告，可以變更 hello 組態 toouse 另一個儲存體帳戶？** 

   是，您可以變更 hello 組態 toopoint tooa 不同儲存體帳戶。 連線 tooAzure 備份內容套件時，您應該使用新設定的 hello 儲存體帳戶。 此外，在設定不同的儲存體帳戶之後，新的資料將會流入這個儲存體帳戶。 但是較舊的資料 （然後再變更 hello 組態） 仍會保留在 hello 較舊的儲存體帳戶。

6. **我是否可以檢視跨保存庫及跨訂用帳戶的報告？** 

   是，您可以設定 hello 跨不同的相同儲存體帳戶的保存庫 tooview 跨保存庫的報表。 此外，您可以設定 hello 跨訂用帳戶的保存庫相同的儲存體帳戶。 您接著可以使用這個儲存體帳戶連線 tooAzure 備份內容套件在 Power BI tooview hello 報表中的時。 不過，在 hello 應該選取 hello 儲存體帳戶相同的區域復原服務保存庫。
   
## <a name="next-steps"></a>後續步驟
既然您已經設定 hello 儲存體帳戶和匯入的 Azure 備份內容套件、 hello 下一個步驟是 toocustomize，這些報表和使用報告資料模型 toocreate 報表。 Hello 下列發行項，如需詳細資訊，請參閱。

* [使用 Azure 備份報告資料模型](backup-azure-reports-data-model.md)
* [在 Power BI 中篩選報告](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [在 Power BI 中建立報告](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

