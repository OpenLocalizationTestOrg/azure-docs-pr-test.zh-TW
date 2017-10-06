---
title: "aaaService 對應整合 System Center Operations Manager |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 這篇文章討論如何使用服務對應 tooautomatically Operations Manager 中建立分散式應用程式圖表。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>服務對應與 System Center Operations Manager 的整合
  > [!NOTE]
  > 這項功能處於公開預覽狀態。
  > 
  
Operations Management Suite 服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件，並將對應 hello 服務之間的通訊。 服務對應可讓您 tooview 伺服器 hello 好您將項目，視為互連提供重要服務的系統。 服務對應可顯示在任何 TCP 連接的架構，而不需要除了 hello 代理程式安裝設定伺服器、 處理程序與連接埠之間的連線。 如需詳細資訊，請參閱 hello[服務對應文件](operations-management-suite-service-map.md)。

與此服務對應和 System Center Operations Manager 之間的整合，您可以在 Operations Manager 服務對應中的 hello 動態相依性地圖為基礎的自動建立分散式應用程式圖表。

## <a name="prerequisites"></a>必要條件
* 管理一組伺服器的 Operations Manager 管理群組。
* Hello 服務對應方案啟用與 Operations Management Suite 工作區。
* 一組伺服器 （至少一個） 是受管理的 Operations Manager 和傳送資料 tooService 對應。 支援 Windows 和 Linux 伺服器。
* 可存取 toohello hello Operations Management Suite 工作區相關聯的 Azure 訂用帳戶的服務主體。 如需詳細資訊，請移至太[建立服務主體](#creating-a-service-principal)。

## <a name="install-hello-service-map-management-pack"></a>安裝 hello 服務對應管理組件
您可以匯入 hello Microsoft.SystemCenter.ServiceMap 管理組件配套 (Microsoft.SystemCenter.ServiceMap.mpb) 啟用 hello 和之間的整合 Operations Manager 服務對應。 hello 配套包含下列管理組件的 hello:
* Microsoft Service Map Application Views
* Microsoft System Center Service Map Internal
* Microsoft System Center Service Map Overrides
* Microsoft System Center Service Map

## <a name="configure-hello-service-map-integration"></a>設定 hello 服務對應整合
安裝 hello 服務對應管理組件，新的節點之後**服務對應**，會顯示下**Operations Management Suite**在 hello**管理**窗格。 

tooconfigure 服務對應整合，請勿 hello 遵循：

1. tooopen hello 組態精靈 的 hello**服務對應概觀** 窗格中，按一下 **加入工作區**。  

    ![[服務對應概觀] 窗格](media/oms-service-map/scom-configuration.png)

2. 在 hello**連接組態**視窗中，輸入 hello 租用戶名稱或識別碼、 應用程式識別碼 （也稱為 hello 使用者名稱或 clientID） 及 hello 服務主體的密碼，然後按一下**下一步**。 如需詳細資訊，請移至太[建立服務主體](#creating-a-service-principal)。

    ![hello 連線組態視窗](media/oms-service-map/scom-config-spn.png)

3. 在 hello**訂閱選取項目**視窗中，選取 hello Azure 訂用帳戶、 Azure 資源群組 (hello 另一個則包含 hello Operations Management Suite 工作區) 和 Operations Management Suite 工作區中，然後按一下**下一步**。

    ![hello Operations Manager 設定 工作區](media/oms-service-map/scom-config-workspace.png)

4. 在 hello**群組選擇機器**視窗，請選擇哪些服務對應電腦群組想 toosync tooOperations 管理員。 按一下**新增/移除電腦群組**，選擇 hello 清單群組**可用的電腦群組**，然後按一下**新增**。  當您完成選取群組，請按一下**確定**toofinish。
    
    ![hello Operations Manager 設定機器群組](media/oms-service-map/scom-config-machine-groups.png)
    
5. 在 hello**伺服器選取項目**視窗中，您設定 hello 服務對應的伺服器群組與您想要 Operations Manager 與服務對應 toosync hello 伺服器。 按一下 [新增/移除伺服器]。   
    
    Hello 伺服器 hello 整合 toobuild 伺服器的分散式應用程式圖表，必須是：

    * 由 Operations Manager 管理
    * 由服務對應管理
    * 列在 hello 服務對應的伺服器群組

    ![hello Operations Manager 設定群組](media/oms-service-map/scom-config-group.png)

6. 選擇性： 選取 hello 管理伺服器資源集區 toocommunicate 利用 Operations Management Suite，然後再按一下**加入工作區**。

    ![hello Operations Manager 設定資源集區](media/oms-service-map/scom-config-pool.png)

    可能需要分鐘 tooconfigure 並註冊 hello Operations Management Suite 工作區。 設定它後，Operations Manager 會起始從 Operations Management Suite hello 第一個服務對應同步。

    ![hello Operations Manager 設定資源集區](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>監視服務對應
新的資料夾，服務對應 hello Operations Management Suite 工作區已連接之後，會顯示在 hello**監視**hello Operations Manager 主控台窗格。

![hello Operations Manager 監視中 窗格](media/oms-service-map/scom-monitoring.png)

hello 服務對應的資料夾有四個節點：
* **作用中警示**： 列出有關 hello 通訊，Operations Manager 與服務對應的 hello 作用中警示。  請注意，這些警示不是正在同步處理的 tooOperations Manager 的 Operations Management Suite 的資訊警示。 

* **伺服器**： 列出 hello 監視的伺服器設定 toosync 從服務對應。

    ![hello Operations Manager 監視的伺服器 窗格](media/oms-service-map/scom-monitoring-servers.png)

* **機器群組相依性檢視**：列出從服務對應同步處理的所有機器群組。 您可以按一下任何群組 tooview 其分散式應用程式圖表。

    ![hello Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-group-dad.png)

* **伺服器相依性檢視**：列出從服務對應同步處理的所有伺服器。 您可以按一下任何伺服器 tooview 其分散式應用程式圖表。

    ![hello Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>編輯或刪除 hello 工作區
您可以編輯或刪除 hello 設定工作區透過 hello**服務對應概觀**窗格 (**管理**窗格 > **Operations Management Suite**  > **服務對應**)。 目前您僅可設定一個 Operations Management Suite 工作區。

![hello Operations Manager 編輯工作區 窗格](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>設定規則和覆寫
一般而言， _Microsoft.SystemCenter.ServiceMapImport.Rule_，從服務對應建立 tooperiodically 提取資訊。 toochange 同步時間，您可以設定的 hello 規則覆寫 (**製作**窗格 >**規則** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![hello Operations Manager 會覆寫屬性 視窗](media/oms-service-map/scom-overrides.png)

* **Enabled**：啟用或停用自動更新。 
* **IntervalMinutes**： 重設 hello 更新之間的時間。 hello 預設間隔為一小時。 若要更頻繁地 toosync server 對應，您可以變更 hello 值。
* **Timeoutseconds 設定**： 重設 hello hello 要求逾時之前的時間長度。 
* **TimeWindowMinutes**： 重設 hello 時間間隔查詢資料。 預設間隔為 60 分鐘。 hello 服務對應所允許的最大值為 60 分鐘。

## <a name="known-issues-and-limitations"></a>已知問題與限制

hello 目前設計顯示 hello 以下問題和限制：
* 您只能連接單一 tooa Operations Management Suite 工作區。
* 雖然您可以新增伺服器 toohello 服務對應的伺服器群組手動透過 hello**製作** 窗格中，這些伺服器 hello 對應未立即同步處理。  它們將在 hello 下一個同步處理循環期間同步處理從服務對應。
* 如果 toohello 分散式應用程式圖表建立 hello 管理組件進行任何變更，這些變更將可能會覆寫 hello 與服務對應的下一個同步處理。

## <a name="create-a-service-principal"></a>建立服務主體
如需建立服務主體的官方 Azure 文件，請參閱︰
* [使用 PowerShell 建立服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [使用 Azure CLI 建立服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [建立服務主體使用 hello Azure 入口網站](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>意見反應
您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？ 請瀏覽我們的 [User Voice 頁面 (英文)](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)，您可以在此頁面提出功能建議或對現有的建議進行投票。
