---
title: "使用 Azure Data Factory 中的資料管理閘道器的 aaaHigh 可用性 |Microsoft 文件"
description: "本文說明如何藉由新增更多節點來相應放大資料管理閘道，以及藉由增加節點中可以並行執行的作業數來相應增加。"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: abnarain
ms.openlocfilehash: 925f63728e23596bca2655636f6535b509fce0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway---high-availability-and-scalability-preview"></a>資料管理閘道 - 高可用性和延展性 (預覽)
本文可協助您使用資料管理閘道來設定高可用性和延展性解決方案。    

> [!NOTE]
> 本文假設您已熟悉資料管理閘道的基本概念。 如果您並不熟悉，請參閱[資料管理閘道](data-factory-data-management-gateway.md)。

>**資料管理閘道版本 2.12.xxxx.x 和更新版本正式支援此預覽功能**。 請確定您使用版本 2.12.xxxx.x 或更新版本。 下載 hello 最新版本的資料管理閘道器[這裡](https://www.microsoft.com/download/details.aspx?id=39717)。

## <a name="overview"></a>概觀
您可以將從 hello 入口網站的單一邏輯閘道的多部在內部部署電腦上安裝資料管理閘道器產生關聯。 這些機器稱為**節點**。 您最多可以有太**四個節點**邏輯閘道相關聯。 邏輯閘道會有多個節點 （在內部部署機器以安裝閘道器） 的 hello 優點為：  

- 提升內部部署機器和雲端資料存放區之間的資料移動效能。  
- 如果其中一個 hello 節點關閉基於某些原因，其他節點是移動 hello 資料仍然可用。 
- 如果其中一個 hello 節點需要 toobe 離線進行維護時，其他節點是移動 hello 資料仍然可用。

您也可以設定 hello 數目**並行資料移動作業**可以執行於節點 tooscale hello 功能，在內部部署和雲端之間移動資料的資料存放區。 

使用 hello Azure 入口網站，您可以監視 hello 狀態這些節點，可幫助您決定是否 tooadd 或從 hello 邏輯閘道移除節點。 

## <a name="architecture"></a>架構 
hello 下列圖表提供 hello 架構概觀的延展性和可用性功能的 hello 資料管理閘道器： 

![資料管理閘道 - 高可用性和延展性](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-high-availability-and-scalability.png)

A**邏輯閘道**是您加入 tooa 資料 factory hello Azure 入口網站中的 hello 閘道。 以前，您只能將一個內部部署 Windows 機器關聯到安裝了邏輯閘道的資料管理閘道。 這個內部部署閘道機器稱為節點。 現在，您可以將關聯設定太**四個實體節點**與邏輯的閘道。 具有多個節點的邏輯閘道稱為**多節點閘道**。  

而這些節點全都是**作用中**狀態。 它們都可以處理資料移動作業 toomove 資料在內部部署和雲端之間的資料存放區。 其中一個 hello 節點做為發送器和背景工作。 Hello 群組中的其他節點是背景工作節點。 A**發送器**節點提取的資料移動工作/作業從 hello 雲端服務，並將其分派 tooworker 節點 （包括本身）。 A**工作者**節點執行內部部署與雲端之間資料移動作業 toomove 資料資料存放區。 所有節點都是背景工作節點。 只有一個節點可以既是發送器節點，又是背景工作節點。    

您通常可以與一個節點開始，**向外延展**tooadd 為 hello 現有的節點上的多個節點爆 hello 資料移動負載。 您也可以**向上延展**hello 閘道節點的資料移動功能藉由增加 hello 所允許 toorun hello 節點的並行工作數。 這項功能也可與單一節點閘道 （即使未啟用 hello 延展性和可用性功能）。 

閘道具有多個節點會保留 hello 資料存放區認證同步的所有節點。 如果沒有節點的連線問題，hello 認證可能不同步。當您將使用閘道的內部部署資料存放區的認證時，它會將認證儲存在 hello 發送器/背景工作節點上。 與其他背景工作角色節點的 hello 發送器節點同步。 這個程序稱為**認證同步**。 可以是 hello 節點之間的通訊通道**加密**所公開的 SSL/TLS 憑證。 

## <a name="set-up-a-multi-node-gateway"></a>設定多節點閘道
本節假設您已經透過下列兩個發行項或熟悉的概念，這些文章中的 hello: 

- [資料管理閘道器](data-factory-data-management-gateway.md)-提供 hello 閘道的詳細的概觀。
- [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) - 包含如何使用具有單一節點之閘道的逐步指示。  

> [!NOTE]
> 在內部部署 Windows 電腦上安裝資料管理閘道器之前，請參閱中所列必要條件[hello 主要文章](data-factory-data-management-gateway.md#prerequisites)。

1. 在 hello[逐步解說](data-factory-move-data-between-onprem-and-cloud.md#create-gateway)，在建立邏輯閘道時，啟用 hello**高可用性和延展性**功能。 

    ![資料管理閘道 - 啟用高可用性和延展性](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-enable-high-availability-scalability.png)
2. 在 hello**設定**頁面上，使用**Express 安裝程式**或**手動安裝**連結 tooinstall hello 第一個節點 （在內部部署 Windows 電腦） 上的閘道。

    ![資料管理閘道 - 快速設定或手動設定](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-express-manual-setup.png)

    > [!NOTE]
    > 如果您使用 hello 快速安裝選項，而且不會加密完成 hello 節點對節點通訊。 hello 節點名稱為與 hello 電腦名稱相同。 如果 hello 節點通訊需要 toobe 加密，或是您想 toospecify 您選擇的節點名稱，請使用手動安裝。 您之後就無法編輯節點名稱。
3. 如果您選擇 [快速設定]
    1. 您會看到 hello hello 閘道的安裝成功之後，下列訊息：

        ![資料管理閘道 - 快速設定成功](media/data-factory-data-management-gateway-high-availability-scalability/express-setup-success.png)
    2. 啟動資料管理 Configuration Manager hello 閘道，依照[這些指示](data-factory-data-management-gateway.md#configuration-manager)。 您會看到 hello 閘道名稱、 節點名稱、 狀態、 等等。

        ![資料管理閘道 - 安裝成功](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)
4. 如果您選擇 [手動設定]：
    1. 從 hello Microsoft Download Center 下載 hello 安裝封裝，您的電腦上執行 tooinstall 閘道。
    2. 使用 hello**驗證金鑰**從 hello**設定**頁面 tooregister hello 閘道。
    
        ![資料管理閘道 - 安裝成功](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-authentication-key.png)
    3. 在 [hello**新的 gateway 節點**] 頁面上，您可以提供自訂**名稱**toohello 的 gateway 節點。 根據預設，節點名稱為與 hello 電腦名稱相同。    

        ![資料管理閘道 - 指定名稱](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-name.png)
    4. 在 hello 下一個頁面上，您可以選擇是否太**啟用節點對節點通訊的加密**。 按一下**略過**toodisable 加密 （預設值）。

        ![資料管理閘道 - 啟用加密](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-node-encryption.png)  
    
        > [!NOTE]
        > 才支援變更的加密模式，當您將單一閘道節點在 hello 邏輯閘道。 toochange hello 加密模式時，閘道有多個節點，執行下列步驟 hello： 刪除所有除了一個節點的 hello 節點、 變更 hello 加密模式中，然後再將 hello 節點一次。
        > 
        > 如需 TLS/SSL 憑證的使用需求清單，請參閱 [TLS/SSL 憑證需求](#tlsssl-certificate-requirements)一節。 
    5. 已成功安裝 hello 閘道之後，請按一下 啟動 Configuration Manager:
    
        ![手動設定 - 啟動組態管理員](media/data-factory-data-management-gateway-high-availability-scalability/manual-setup-launch-configuration-manager.png)   
    6. 您在 hello 節點 （在內部部署 Windows 電腦），會顯示連線狀態，請參閱資料管理閘道組態管理員**閘道名稱**，和**節點名稱**。  

        ![資料管理閘道 - 安裝成功](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-installation-success.png)

        > [!NOTE]
        > 如果您要佈建 Azure VM 上的 hello 閘道，您可以使用[GitHub 上的此 Azure Resource Manager 範本](https://github.com/xiaoyingLJ/vms-with-multiple-data-management-gateway)。 此指令碼會建立邏輯閘道、 資料管理閘道已安裝軟體，以設定 Vm 並與 hello 邏輯閘道註冊它們。 
6. 在 Azure 入口網站啟動 hello**閘道**頁面： 
    1. Hello 資料 factory 首頁 hello 入口網站中，按一下**連結的服務**。
    
        ![Data Factory 首頁](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-home-page.png)
    2. 選取 hello**閘道**toosee hello**閘道**頁面：
    
        ![Data Factory 首頁](media/data-factory-data-management-gateway-high-availability-scalability/linked-services-gateway.png)
    4. 您會看到 hello**閘道**頁面：   

        ![具有單一節點之閘道的檢視](media/data-factory-data-management-gateway-high-availability-scalability/gateway-first-node-portal-view.png) 
7. 按一下**加入節點**hello 工具列 tooadd 節點 toohello 邏輯閘道上。 如果您計劃 toouse 快速安裝，請從 hello 將會新增為節點 toohello 閘道的內部部署機器執行此步驟。 

    ![資料管理閘道 - 新增節點功能表](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)
8. 步驟都類似 toosetting hello 第一個節點。 Configuration Manager UI hello 可讓您設定 hello 節點名稱，如果您選擇 hello 手動安裝選項： 

    ![組態管理員 - 安裝第二個閘道](media/data-factory-data-management-gateway-high-availability-scalability/install-second-gateway.png)
9. Hello 閘道 hello 節點上安裝成功之後，hello Configuration Manager 工具會顯示下列畫面 hello:  

    ![組態管理員 - 安裝第二個閘道成功](media/data-factory-data-management-gateway-high-availability-scalability/second-gateway-installation-successful.png)
10. 如果您開啟 hello**閘道**頁面在 hello 入口網站中，您會看到兩個閘道節點現在： 

    ![閘道與 hello 入口網站中的兩個節點](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)
11. toodelete 閘道] 節點中，按一下**刪除節點**hello 在工具列上，選取 [hello 節點 toodelete，然後再按一下**刪除**從 hello 工具列。 這個動作會刪除從 hello 群組 hello 選取的節點。 請注意，此動作不會解除安裝 hello 資料管理閘道軟體從 hello 節點 （在內部部署 Windows 電腦）。 使用**新增或移除程式**hello 內部 toouninstall hello 閘道上的控制台 中。 當您從 hello 節點解除安裝閘道時，便會自動刪除 hello 入口網站中。   

## <a name="upgrade-an-existing-gateway"></a>升級現有閘道
您可以升級現有閘道 toouse hello 高可用性和延展性功能。 這項功能僅適用於具有 hello 資料管理閘道器版本的節點 > = 2.12.xxxx。 您可以看到資料管理閘道器安裝在電腦中 hello hello 版本**協助**hello 資料管理閘道組態管理員 索引標籤。 

1. 更新 hello 閘道 hello 在內部部署機器 toohello 最新版本上遵循下載並執行的 MSI 安裝程式套件從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717)。 如需詳細資料，請參閱[安裝](data-factory-data-management-gateway.md#installation)一節。  
2. 瀏覽 toohello Azure 入口網站。 啟動 hello **Data Factory 頁面**data factory。 按一下連結服務磚 toolaunch hello**連結的服務頁面**。 選取 hello 閘道 toolaunch hello**閘道頁面**。 按一下並啟用**預覽功能**hello 下列影像所示： 

    ![資料管理閘道 - 啟用預覽功能](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-existing-gateway-enable-high-availability.png)   
2. 一旦 hello 入口網站啟用 hello 預覽功能，請關閉所有頁面。 重新開啟 hello**閘道頁面**toosee hello 新 preview 使用者介面 (UI)。
 
    ![資料管理閘道 - 啟用預覽功能成功](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview-success.png)

    ![資料管理閘道 - 預覽 UI](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-preview.png)

    > [!NOTE]
    > Hello 在升級期間，hello 第一個節點的名稱會是 hello hello 機器名稱。 
3. 現在，新增節點。 在 hello**閘道**頁面上，按一下**加入節點**。  

    ![資料管理閘道 - 新增節點功能表](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-add-node-menu.png)

    請遵循指示 hello 前一個區段 tooset hello 節點。 

### <a name="installation-best-practices"></a>安裝最佳做法

- Hello hello 閘道的主機電腦上設定的電源計劃 hello 機器不休眠。 如果 hello 主機電腦休眠，hello 閘道沒有回應 toodata 要求。
- 備份 hello 與 hello 閘道相關聯的憑證。
- 確定所有節點都有類似的設定 (建議選項) 以獲得理想的效能。 
- 加入兩個以上的節點 tooensure 高可用性。  

### <a name="tlsssl-certificate-requirements"></a>TLS/SSL 憑證需求
以下是 hello TLS/SSL 憑證，用來保護通訊，閘道節點之間的 hello 需求：

- hello 憑證必須是公用信任的 X509 v3 憑證。
- 所有閘道節點都必須信任此憑證。 
- 建議您使用公開 (第三方) 憑證授權單位 (CA) 所發出的憑證。
- 支援 Windows Server 2012 R2 所支援的任何 SSL 憑證金鑰大小。
- 不支援使用 CNG 金鑰的憑證。
- 支援萬用字元憑證。 


## <a name="monitor-a-multi-node-gateway"></a>監視多節點閘道
### <a name="multi-node-gateway-monitoring"></a>多節點閘道監視
在 hello Azure 入口網站，您可以檢視幾乎是即時的資源使用情況 （CPU、 記憶體、 network(in/out) 等） 的快照集，閘道節點的狀態以及每個節點上。 

![資料管理閘道 - 多節點監視](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring.png)

您可以啟用**進階設定**在 hello**閘道**頁面 toosee 進階計量，例如**網路**（in/out）**角色 （& s) 認證狀態**，這是在偵錯閘道問題很有幫助和**並行作業**（執行 / Limit） 這可以已修改 / 據以變更期間的效能微調。 hello 下表提供 hello 中的資料行的描述**閘道節點**清單：  

監視屬性 | 說明
:------------------ | :---------- 
名稱 | Hello 邏輯閘道和節點與 hello 閘道相關聯的名稱。  
狀態 | Hello 邏輯閘道和 hello 閘道節點的狀態。 範例：線上/離線/受限制/等等。如需這些狀態的相關資訊，請參閱[閘道狀態](#gateway-status)一節。 
版本 | 顯示 hello hello 邏輯閘道版本和每個閘道節點。 hello hello 邏輯閘道版本取決於大部分的 hello 群組中的節點的版本。 如果沒有節點具有 hello 邏輯閘道安裝程式中的不同版本，只有 hello 節點與 hello 正確為 hello 邏輯閘道函式相同的版本號碼。 其他在 hello limited 模式下，需要 toobe 手動更新 （只有大小寫自動更新就會失敗）。 
可用的記憶體 | 閘道節點上可用的記憶體。 這個值是近乎即時的快照集。 
CPU 使用率 | 閘道節點的 CPU 使用率。 這個值是近乎即時的快照集。 
網路功能 (輸入/輸出) | 閘道節點的網路使用率。 這個值是近乎即時的快照集。 
並行作業 (執行中/限制) | 每個節點上執行的作業或工作數目。 這個值是近乎即時的快照集。 限制表示 hello 最大並行的工作的每個節點。 這個值是根據 hello 機器大小所定義。 您可以增加並行工作執行，在進階案例中，向上的 hello 限制 tooscale 其中 CPU / 記憶體 / 網路使用率過低，但活動會逾時。這項功能也可與單一節點閘道 （即使未啟用 hello 延展性和可用性功能）。 如需詳細資訊，請參閱[調整考量](#scale-considerations)一節。 
角色 | 有兩種角色 – 發送器和背景工作角色。 所有節點都都會背景工作，這表示它們都可以使用的 tooexecute 作業。 沒有只有一個發送器節點，其使用的 toopull 工作/作業從雲端服務，並分派 toodifferent 背景工作節點 （包括本身）。 

![資料管理閘道 - 進階的多節點監視](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-advanced.png)

### <a name="gateway-status"></a>閘道狀態

hello 下表提供可能的狀態的**閘道節點**: 

狀態  | 註解/案例
:------- | :------------------
線上 | TooData Factory 服務連接的節點。
離線 | 節點已離線。
升級中 | hello 節點正在自動更新。
限制 | 由於 tooConnectivity 問題。 可能是由於在 tooHTTP 連接埠 8050 問題、 服務匯流排連線問題或認證同步處理問題。 
非使用中 | 節點位在不同於其他大多數節點 hello 組態設定。<br/><br/> 它無法連線 tooother 節點時，節點可以是作用中。 


hello 下表提供可能的狀態的**邏輯閘道**。 hello 閘道狀態取決於 hello 閘道節點的狀態。 

狀態 | 註解
:----- | :-------
需要註冊 | 沒有節點尚未註冊的 toothis 邏輯閘道
線上 | 閘道節點已連線
離線 | 沒有處於線上狀態的節點。
限制 | 此閘道中的節點並非全都處於健康情況良好的狀態。 這個狀態是某些節點可能會關閉的警告！ <br/><br/>可能是由於 toocredential 發送器/背景工作節點上的同步處理問題。 

### <a name="pipeline-activities-monitoring"></a>管線/活動監視
hello Azure 入口網站提供的監視體驗與更細微的節點層級詳細資料的管線。 例如，它會顯示哪些活動在哪個節點上執行。 此資訊可能有助於了解特定節點上，假設因為 toonetwork 節流的效能問題。 

![資料管理閘道 - 管線的多節點監視](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-monitoring-pipelines.png)

![資料管理閘道 - 管線詳細資料](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-multi-node-pipeline-details.png)

## <a name="scale-considerations"></a>調整考量

### <a name="scale-out"></a>相應放大
當 hello**可用記憶體偏低**和 hello **CPU 使用率偏高**，加入新節點可幫助跨機器的向外延展 hello 負載。 如果活動到期 tootime 外或閘道已離線的節點失敗，它加入節點 toohello 閘道可幫助。
 
### <a name="scale-up"></a>相應增加
當 hello 可用記憶體和 CPU 使用率不好，但 hello 閒置容量為 0 時，您應該調整藉由增加 hello 可以在節點執行的並行處理作業數目。 您也可以 tooscale 向上活動因為 hello 閘道多載會逾時。 Hello 下列影像所示，您可以增加 hello 節點的最大容量。 我們建議使用 toostart 加倍。  

![資料管理閘道 - 調整考量](media/data-factory-data-management-gateway-high-availability-scalability/data-factory-gateway-scale-considerations.png)


## <a name="known-issuesbreaking-changes"></a>已知問題/重大變更

- 目前，您可以向上 toofour 實體閘道節點的單一邏輯閘道。 如果您需要四個以上的節點，基於效能考量，傳送電子郵件太[DMGHelp@microsoft.com](mailto:DMGHelp@microsoft.com)。
- 您無法重新將 hello 驗證金鑰，從另一個邏輯閘道 tooswitch 從 hello 目前邏輯閘道閘道節點向。 toore 暫存器從 hello 節點解除安裝 hello 閘道、 重新安裝 hello 閘道和註冊的 hello hello 驗證金鑰，與其他邏輯的閘道。 
- 如果您的所有閘道節點需要 HTTP proxy，diahost.exe.config 和 diawp.exe.config，設定 hello proxy，並使用 hello 伺服器管理員 toomake 確定所有節點擁有都 hello 相同 diahost.exe.config 和 diawip.exe.config。如需詳細資訊，請參閱[設定 Proxy 設定](data-factory-data-management-gateway.md#configure-proxy-server-settings)一節。 
- toochange 加密模式的節點對節點通訊在閘道組態管理員中，刪除所有的 hello 節點，只保留一個 hello 入口網站中。 然後，將節點加入之後變更 hello 加密模式。
- 如果您選擇 tooencrypt hello 節點對節點通訊通道，請使用正式的 SSL 憑證。 自我簽署的憑證，可能會為相同的憑證不會受到信任在其他電腦上的憑證授權單位清單中的 hello 造成連線問題。 
- Hello 節點版本低於 hello 邏輯的閘道器版本時，無法註冊閘道節點 tooa 邏輯閘道。 從入口網站刪除 hello 邏輯閘道的所有節點，以便您可以使用較低的版本 node(downgrade) 註冊它。 如果您刪除邏輯閘道的所有節點，手動安裝並註冊新節點 toothat 邏輯閘道。 在此情況下不支援快速設定。
- 您無法使用快速安裝 tooinstall 節點 tooan 現有邏輯閘道，仍在使用雲端認證。 您可以檢查 hello 認證從 hello 閘道器組態管理員 hello 設定 索引標籤上的儲存位置。
- 您無法使用快速安裝 tooinstall 節點 tooan 現有邏輯閘道，其具有節點對節點加密已啟用。 設定 hello 加密模式牽涉到手動新增憑證，因為快速安裝為沒有其他選項。 
- 若要從內部部署環境複製檔案，請勿再使用 \\localhost 或 C:\files，因為您可能無法透過所有節點存取 localhost 或本機磁碟機。 請改用\\ServerName\files toospecify 檔案的位置。


## <a name="rolling-back-from-hello-preview"></a>回復從 hello 預覽 
從 hello 預覽 tooroll 刪除一個節點以外的所有節點。 無論您刪除，但請確定您在 hello 邏輯閘道有至少一個節點的節點。 解除安裝 hello 機器上的閘道或使用 hello Azure 入口網站，您可以刪除節點。 在 Azure 入口網站中 hello hello **Data Factory**頁面上，按一下連結服務 toolaunch hello**連結的服務**頁面。 選取 hello 閘道 toolaunch hello**閘道**頁面。 在 hello 閘道頁面上，您可以看到 hello 與 hello 閘道相關聯的節點。 hello 頁面可讓您從 hello 閘道刪除節點。
 
在刪除之後，按一下 **預覽功能**在 hello 相同的 Azure 入口網站頁面，並停用 hello 預覽功能。 您已經重設閘道 tooone 節點 GA （正式上市） 閘道。


## <a name="next-steps"></a>後續步驟
檢閱下列文章 hello:
- [資料管理閘道器](data-factory-data-management-gateway.md)-提供 hello 閘道的詳細的概觀。
- [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) - 包含如何使用具有單一節點之閘道的逐步指示。 
