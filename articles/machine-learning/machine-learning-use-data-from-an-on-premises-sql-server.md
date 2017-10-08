---
title: "Azure Machine Learning 中的內部部署 SQL Server 執行 aaaUse |Microsoft 文件"
description: "與 Azure Machine Learning 中使用內部部署 SQL Server 資料庫 tooperform 進階分析的資料。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>使用來自內部部署 SQL Server 資料庫的資料，利用 Azure Machine Learning 執行進階分析

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

通常可搭配內部部署資料的企業希望 tootake 的 hello 小數位數與 hello 雲端為其機器學習服務工作負載的靈活度。 但不希望 toodisrupt 其目前的商務程序和工作流程移動其內部部署資料 toohello 雲端。 Azure Machine Learning 現在支援從內部部署 SQL Server 資料庫讀取資料，然後利用此資料，針對某個模型進行訓練與評分。 您不再需要 hello 雲端和內部部署伺服器之間的 toomanually 複本和同步處理 hello 資料。 相反地，hello**匯入資料**Azure Machine Learning Studio 中的模組現在可以直接從您在內部部署 SQL Server 資料庫讀取您定型和計分工作。

本文章提供如何 tooingress 內部部署 SQL server 資料到 Azure Machine Learning 的概觀。 它假設您已熟悉像是工作區、模組、資料集、實驗等 Azure Machine Learning 概念。

> [!NOTE]
> 此功能不適用於免費的工作區。 如需機器學習服務定價和層級的詳細資訊，請參閱 [Azure 機器學習服務定價](https://azure.microsoft.com/pricing/details/machine-learning/)。
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>安裝 Microsoft 資料管理閘道器 hello
tooaccess Azure Machine Learning 中的內部部署 SQL Server 資料庫，您需要 toodownload 和安裝 hello Microsoft 資料管理閘道器。 當您設定 hello 閘道連線 Machine Learning Studio 中，您必須下載並安裝 hello 閘道使用 hello hello 機會**下載和登錄資料閘道**對話方塊如下所述。

您也可以安裝 hello 資料管理閘道器事先下載並執行 hello MSI 安裝程式套件從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717)。
選擇 hello 最新版本，選取 32 位元或 64 位元，視您的電腦。 hello MSI 也可以使用的 tooupgrade 現有資料管理閘道器 toohello 最新版本，以保留的所有設定。

hello 閘道有 hello 下列必要條件：

* hello 支援 Windows 作業系統版本是 Windows 7、 Windows 8/8.1、 Windows 10、 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2。
* hello 建議 hello 閘道機器組態是至少 2 GHz、 4 核心、 8 GB 的 RAM 和 80 GB 的磁碟。
* 如果 hello 主機電腦休眠，hello 閘道將不會回應 toodata 要求。 因此，設定適當的電源計劃 hello 電腦上，再安裝 hello 閘道。 如果已設定的 toohibernate hello 機器，hello 閘道安裝就會顯示訊息。
* 複製活動發生在特定的頻率，因為 hello 資源 （CPU、 記憶體） 電腦上的使用量 hello 也會遵循的 hello 相同模式尖峰和閒置的時間。 資源使用量也仰賴 hello 移動的資料數量。 如果有多個複製作業正在進行，您將可觀察到資源使用量會在尖峰時段增加。 技術上足夠 hello 上面所列的最小組態時，您可能需要根據特定的負載 toohave 具有更多的資源比 hello 最小組態的組態進行資料移動。

Hello 下列設定及使用資料管理閘道器時，請考慮：

* 單一電腦上只能安裝一個資料管理閘道器的執行個體。
* 您可以針對多個內部部署資料來源使用單一閘道器。
* 您可以連接 toohello 不同的電腦上的多個閘道相同的內部部署資料來源。
* 您一次只能針對一個工作區設定一個閘道器。 目前，閘道無法在工作區之間共用。
* 您可以針對單一工作區設定多個閘道器。 比方說，您可能想 toouse 閘道所連線的 tooyour 測試資料來源，在開發期間及生產閘道當你準備好 toooperationalize。
* hello 閘道不需要 toobe hello 做 hello 資料來源相同電腦上。 但仍使用接近 toohello 資料來源可減少 hello hello 閘道 tooconnect toohello 資料來源的時間。 我們建議您在不同的是從一個主機 hello 在內部部署資料來源的 hello 讓 hello 閘道和資料來源不會競用資源的電腦上安裝 hello 閘道。
* 如果您已在電腦上安裝用於 Power BI 或 Azure Data Factory 案例的閘道器，請於另一台電腦上安裝另一個用於 Azure Machine Learning 的閘道器。

  > [!NOTE]
  > 您無法執行資料管理閘道，Power BI Gateway hello 在同一部電腦。
  >
  >
* 即使您使用 Azure ExpressRoute 的其他資料，您需要 Azure 機器學習 toouse hello 資料管理閘道器。 即使使用 ExpressRoute，您也應該將資料來源視為內部部署資料來源 (亦即在防火牆後面)。 使用機器學習服務與 hello 資料來源之間的 hello 資料管理閘道器 tooestablish 連線。

您可以在 hello 文件中找到的安裝必要條件、 安裝步驟和疑難排解提示的詳細的資訊[資料管理閘道器](../data-factory/data-factory-data-management-gateway.md)。

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>將內部部署 SQL Server 資料庫的資料輸入至 Azure Machine Learning
在本逐步解說中，您將會在 Azure Machine Learning 工作區中設定資料管理閘道器、設定該閘道器，然後讀取來自內部部署 SQL Server 資料庫的資料。

> [!TIP]
> 開始之前，請先針對 `studio.azureml.net` 停用瀏覽器的快顯封鎖程式。 如果您使用 Google Chrome 瀏覽器 hello，下載並安裝其中一個 hello 數個外掛程式可在 Google Chrome WebStore[按一次應用程式擴充功能](https://chrome.google.com/webstore/search/clickonce?_category=extensions)。
>
>

### <a name="step-1-create-a-gateway"></a>步驟 1：建立閘道器
hello 第一個步驟是 toocreate，設定 hello 閘道 tooaccess 您在內部部署的 SQL 資料庫。

1. 登入太[Azure Machine Learning Studio](https://studio.azureml.net/Home/)和選取 hello 工作區中所要 toowork。
2. 按一下 hello**設定**上 hello 刀鋒視窗左、，然後按一下hello**資料閘道**hello 頂端的索引標籤。
3. 按一下**新的資料閘道**在 hello 囉 」 畫面底部。

    ![新增資料閘道](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. 在 [hello**新的資料閘道**] 對話方塊中，輸入 hello**閘道名稱**並選擇性地加入**描述**。 按一下 hello 底端右下角 toogo toohello 下一個步驟的 hello 組態 hello 箭號。

    ![輸入閘道名稱和描述](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. 在 hello 下載並登錄資料閘道 對話方塊，複製 hello 閘道註冊金鑰 toohello 剪貼簿。

    ![下載並註冊資料閘道](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>如果尚未下載及安裝 hello Microsoft 資料管理閘道器，然後按一下 **下載資料管理閘道器**。 Toothe Microsoft 下載中心您可以在其中選取 hello 閘道器版本您如此會讓需要請下載，並安裝它。 您可以在 hello 發行項的 hello 開頭區段找到安裝必要條件，安裝步驟和疑難排解提示的詳細的資訊[在內部部署來源和資料管理閘道器與雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. 資料管理閘道組態管理員 hello hello 閘道安裝之後，會開啟，並在 hello**註冊閘道** 對話方塊隨即出現。 貼上 hello**閘道註冊金鑰**toohello 剪貼簿，然後按一下您複製**註冊**。
8. 如果您已經安裝了閘道，請執行 hello 資料管理閘道組態管理員。 按一下**變更金鑰**，貼上**閘道註冊金鑰**toohello 剪貼簿複製中的 hello 先前步驟中，按一下 **確定**。
9. Hello 安裝完成時，hello**註冊閘道**的 Microsoft 資料管理閘道組態管理員 對話方塊隨即出現。 Hello 閘道註冊金鑰複製到上一個步驟中的 hello 剪貼簿貼上，按一下 **註冊**。

    ![註冊閘道](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. hello 閘道組態都完成時，設定下列值的 hello hello**首頁**在 Microsoft 資料管理閘道組態管理員 索引標籤：

    * **閘道名稱**和**執行個體名稱**設定 toohello hello 閘道名稱。
    * **註冊**設定得**註冊**。
    * **狀態**設定得**已啟動**。
    * 在 hello 底部顯示 hello 狀態列**連接 tooData 管理閘道雲端服務**以及綠色的核取記號。

      ![資料管理閘道管理員](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      也 hello 註冊成功時，取得更新 azure Machine Learning Studio。

    ![閘道註冊成功](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. 在 [hello**下載並登錄資料閘道**] 對話方塊中，按一下核取記號 toocomplete hello 安裝程式。 hello**設定**頁面會顯示為 「 上線 」 閘道狀態。 您可以在 hello 右手邊窗格中，找到狀態和其他有用的資訊。

    ![閘道設定](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. 在 hello Microsoft 資料管理閘道組態管理員切換 toohello**憑證**此索引標籤上指定的索引 hello 憑證是 hello 在內部部署資料存放區，您指定的使用的 tooencrypt/解密憑證在 hello 入口網站。 此憑證是 hello 預設憑證。 Microsoft 建議變更這個 tooyour 自己的憑證，您先備份您的憑證管理系統中。 按一下**變更**toouse 您自己的憑證而。

    ![變更閘道憑證](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. （選擇性）如果您想 tooenable 詳細資訊記錄，才能與 hello 閘道的問題進行疑難排解，請在 hello Microsoft 資料管理閘道組態管理員切換 toothe**診斷**索引標籤上，並檢查 hello**啟用詳細資訊記錄來進行疑難排解**選項。 hello 記錄資訊可以在 hello Windows 事件檢視器在 hello **Applications and Services Logs**  - &gt; **資料管理閘道器**節點。 您也可以使用 hello**診斷** 索引標籤 tootest hello 連線 tooan 在內部部署資料來源使用 hello 閘道。

    ![啟用詳細資訊記錄](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

如此便完成 Azure Machine Learning 中的 hello 閘道安裝程序。
您要現在準備好 toouse 在內部部署資料。

您可以在 Studio 中針對每個工作區建立和設定多個閘道器。 例如，您可能在開發和其他閘道期間想 tooconnect tooyour 測試資料來源，為您的實際執行資料來源的閘道。 Azure 機器學習可讓您彈性 tooset，視您的公司環境的多個閘道組成。 目前您無法在工作區之間共用一個閘道器，而且單一電腦上只能安裝一個閘道器。 如需詳細資訊，請參閱[利用資料管理閘道在內部部署來源和雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)。

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>步驟 2： 使用 hello 閘道 tooread 資料從內部部署資料來源
您設定 hello 閘道之後，您可以加入**匯入資料**實驗輸入 hello 在內部部署 SQL Server 資料庫中的 hello 資料的模組。

1. 在機器學習 Studio 中，選取 hello**實驗**索引標籤上，按一下  **+ 新增**在 hello 左下角，然後選取**空白實驗**（或選取數個範例的其中一個實驗可用）。
2. 尋找並拖曳 hello**匯入資料**模組 toohello 實驗畫布。
3. 按一下**存**hello 畫布下方。 Hello 實驗名稱中輸入 「 Azure 機器學習內部部署 SQL Server 教學課程 」，選取工作區中，然後按一下 hello**確定**核取記號。

   ![以新名稱儲存實驗](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. 按一下 hello**匯入資料**模組 tooselect 它，然後在**屬性**窗格 toohello 方 hello 畫布上，選取 「 內部部署 SQL 資料庫 」 中 hello**資料來源**下拉式清單。
5. 選取 hello**資料閘道**您安裝並註冊。 您可以藉由選取 [(新增資料閘道...)] 來設定其他閘道。

   ![從匯入資料模組選取資料閘道](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. 輸入 hello SQL**資料庫伺服器名稱**和**資料庫名稱**，連同 hello SQL**資料庫查詢**想 tooexecute。
7. 按一下 [使用者名稱和密碼] 下方的 [輸入值]，然後輸入資料庫認證。 根據您內部部署 SQL Server 的設定方式而定，您可以使用 Windows 整合式驗證或 SQL Server 驗證。

   ![輸入資料庫認證](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   hello 訊息所需的 「 值 」 變更太"值集 」 的綠色的核取記號。 您只需要 tooenter hello 認證一次除非 hello 資料庫資訊或密碼變更。 Azure Machine Learning 會使用您提供當您安裝 hello 閘道 tooencrypt hello 認證 hello 雲端中的 hello 憑證。 Azure 永遠不會在沒有加密的情況下儲存內部部署認證。

   ![匯入資料模組屬性](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. 按一下**執行**toorun hello 實驗。

一旦 hello 實驗完成執行時，您可以視覺化 hello 資料 hello hello 輸出連接埠，即可匯入從 hello 資料庫**匯入資料**模組並選取**視覺化**。

當實驗完成開發之後，您就能部署和操作您的模型。 使用 hello 批次執行服務，設定在 hello hello 在內部部署 SQL Server 資料庫中的資料**匯入資料**模組會讀取並用於計分。 計分內部資料，您可以使用 hello 要求回應服務，因此 Microsoft 建議使用[Excel 增益集](machine-learning-excel-add-in-for-web-services.md)改為。 目前，撰寫 tooan 內部部署 SQL Server 資料庫，透過**匯出資料**不支援，請在您實驗中或已發行的 web 服務。
