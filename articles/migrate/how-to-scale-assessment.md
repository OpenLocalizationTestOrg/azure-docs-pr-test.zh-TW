---
title: "使用 Azure Migrate 進行規模探索和評定 | Microsoft Docs"
description: "說明如何使用 Azure Migrate 服務評定大量的內部部署機器。"
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 01/08/2018
ms.author: raynew
ms.openlocfilehash: 67661e03e65cde3ec2f1aafd5ef755899cf0c77b
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="discover-and-assess-a-large-vmware-environment"></a>探索及評定大型 VMware 環境

本文說明如何使用 [Azure Migrate](migrate-overview.md) 來評定大量內部部署虛擬機器 (VM)。 Azure Migrate 會評定機器，以確認機器是否適合移轉至 Azure。 此服務會提供在 Azure 中執行機器的大小調整建議和成本估計。

## <a name="prerequisites"></a>必要條件

- **VMware**：您計劃移轉的虛擬機器必須透過 vCenter Server 5.5、6.0 或 6.5 版來管理。 此外，您還需要一部執行 5.0 版或更新版本的 ESXi 主機來部署收集器虛擬機器。
- **vCenter 帳戶**：您需要一個唯讀帳戶來存取 vCenter Server。 Azure Migrate 會使用此帳戶來探索內部部署 VM。
- **權限**：在 vCenter Server 中，您需要權限，方可藉由匯入 .OVA 格式的檔案來建立虛擬機器。
- **統計資料設定**：vCenter Server 的統計資料設定應該先設為層級 3，再開始部署。 如果低於層級 3，還是能進行評定，但不會收集儲存體和網路的效能資料。 在此情況下，將根據 CPU 和記憶體的效能資料，以及磁碟和網路介面卡的組態資料來提出大小建議。

## <a name="plan-azure-migrate-projects"></a>規劃 Azure Migrate 專案

根據下列限制來規劃探索和評定：

| **實體** | **機器限制** |
| ---------- | ----------------- |
| 隨附此逐步解說的專案    | 1,500              | 
| 探索  | 1,000              |
| 評量 | 400               |

- 如果要探索及評定的機器少於 400 部，您需要一個專案和一次探索。 根據您的需求，您可以在單一評定中評定所有機器，或將機器分割成多次評定。 
- 如果您要探索的機器介於 400 到 1000 部，您需要一個執行一次探索的專案。 但是，您需要多次評定來評定這些機器，因為單一評定最多可支援 400 部機器。
- 如果您有 1001 到 1500 部機器，您需要一個執行兩次探索的專案。
- 如果您的機器數量超過 1500 部，您需要根據需求建立多個專案及執行多次探索。 例如︰
    - 如果您有 3000 部機器，可以設定兩個執行兩次探索的專案，或三個執行一次探索的專案。
    - 如果您有 5000 部機器，可以設定四個專案：兩個探索 1500 部機器的專案，再加上一個探索 500 部機器的專案。 您也可以設定五個分別執行一次探索的專案。 

## <a name="plan-multiple-discoveries"></a>規劃多次探索

您可以使用相同的 Azure Migrate 收集器，對一或多個專案進行多次探索。 請記住下列規劃考量：
 
- 當您使用 Azure Migrate 收集器進行探索時，可以將探索範圍設定為 vCenter Server 資料夾、資料中心、叢集或主機。
- 若要執行一次以上的探索，請在 vCenter Server 中確認您要探索的虛擬機器是位於支援 1000 部機器限制的資料夾、資料中心、叢集或主機內。
- 基於評定目的，我們建議您將相依的機器保留在同個專案和同次評定內。 在 vCenter Server 中，確認相依的機器位在同一個資料夾、資料中心或叢集內，以供評定。


## <a name="create-a-project"></a>建立專案

根據需求建立 Azure Migrate 專案：

1. 在 Azure 入口網站中，選取 [建立資源]。
2. 搜尋 **Azure Migrate**，然後在搜尋結果中選取 [Azure Migrate (預覽)] 服務。 然後選取 [建立]。
3. 指定專案名稱，以及專案的 Azure 訂用帳戶。
4. 建立新的資源群組。
5. 指定您要建立專案的位置，然後選取 [建立]。 請注意，您仍可針對不同目標位置評定虛擬機器。 為專案指定的位置用於儲存從內部部署虛擬機器收集的中繼資料。

## <a name="set-up-the-collector-appliance"></a>設定收集器設備

Azure Migrate 會建立稱為「收集器設備」的內部部署 VM。 此虛擬機器會探索內部部署 VMware 虛擬機器，並將其相關中繼資料傳送至 Azure Migrate 服務。 若要設定收集器設備，您可以下載 .OVA 檔案，並將其匯入內部部署 vCenter Server 執行個體。

### <a name="download-the-collector-appliance"></a>下載收集器設備

如果您有多個專案，只需要將收集器設備下載到 vCenter Server 一次。 下載和設定設備之後，您可以針對每個專案執行設備，並指定唯一的專案識別碼和索引鍵。

1. 在 Azure Migrate 專案中，選取 [開始使用] > [探索及評定] > [探索機器]。
2. 在 [探索機器] 中，選取 [下載] 以下載 OVA 檔案。
3. 在 [複製專案認證] 中，複製專案識別碼和索引鍵。 在設定收集器時，您會需要這些資料。

   
### <a name="verify-the-collector-appliance"></a>確認收集器設備

請先確認 OVA 檔案是安全的，再進行部署：

1. 在存放下載檔案的目標電腦上，開啟系統管理員命令視窗。
2. 執行下列命令以產生 OVA 的雜湊：

   ```C:\>CertUtil -HashFile <file_location> [Hashing Algorithm]```

   使用方式範例：```C:\>CertUtil -HashFile C:\AzureMigrate\AzureMigrate.ova SHA256```
3. 確定所產生的雜湊符合下列設定。
 
    若為 OVA 1.0.8.49 版

    **演算法** | **雜湊值**
    --- | ---
    MD5 | 8779eea842a1ac465942295c988ac0c7
    SHA1 | c136c52a0f785e1fd98865e16479dd103704887d
    SHA256 | 5143b1144836f01dd4eaf84ff94bc1d2c53f51ad04b1ca43ade0d14a527ac3f9

    若為 OVA 1.0.8.40 版：

    **演算法** | **雜湊值**
    --- | ---
    MD5 |afbae5a2e7142829659c21fd8a9def3f
    SHA1 | 1751849c1d709cdaef0b02a7350834a754b0e71d
    SHA256 | d093a940aebf6afdc6f616626049e97b1f9f70742a094511277c5f59eacc41ad

## <a name="create-the-collector-vm"></a>建立收集器 VM

將下載的檔案匯入 vCenter Server：

1. 在 vSphere 用戶端主控台中，選取 [檔案] > [部署 OVF 範本]。

    ![部署 OVF](./media/how-to-scale-assessment/vcenter-wizard.png)

2. 在 [部署 OVF 範本精靈] > [來源] 中，指定 OVA 檔案的位置。
3. 在 [名稱] 和 [位置] 中，指定收集器 VM 的易記名稱，以及要裝載 VM 的所在清查物件。
5. 在 [主機/叢集] 中，指定收集器 VM 的執行所在主機或叢集。
7. 在儲存體中，指定收集器 VM 的儲存目的地。
8. 在 [磁碟格式] 中，指定磁碟類型和大小。
9. 在 [網路對應] 中，指定收集器 VM 所要連線的網路。 此網路必須能夠連線到網際網路，以將中繼資料傳送至 Azure。 
10. 檢閱並確認設定，然後選取 [完成]。

## <a name="identify-the-id-and-key-for-each-project"></a>找出每個專案的識別碼和索引鍵

如果您有多個專案，請務必找出每個專案的識別碼和索引鍵。 當您執行收集器來探索 VM 時，將會需要索引鍵。

1. 在專案中，選取 [開始使用] > [探索及評定] > [探索機器]。
2. 在 [複製專案認證] 中，複製專案識別碼和索引鍵。 
    ![複製專案認證](./media/how-to-scale-assessment/copy-project-credentials.png)

## <a name="set-the-vcenter-statistics-level"></a>設定 vCenter 統計資料層級
以下是在探索期間收集的效能計數器清單。 這些計數器預設可在 vCenter Server 的各個層級取用。 

我們建議您為統計資料層級設定最高的一般層級 (3)，以正確收集所有計數器。 如果您的 vCenter 設定為較低層級，只有幾個計數器能完整收集，其他會設定為 0。 因此評定可能會顯示不完整的資料。 

下表也會列出不收集特定計數器時會受到影響的評定結果。

|計數器                                  |Level    |每一裝置層級  |評定影響                               |
|-----------------------------------------|---------|------------------|------------------------------------------------|
|cpu.usage.average                        | 1       |NA                |建議的虛擬機器大小和成本                    |
|mem.usage.average                        | 1       |NA                |建議的虛擬機器大小和成本                    |
|virtualDisk.read.average                 | 2       |2                 |磁碟大小、儲存成本和虛擬機器大小         |
|virtualDisk.write.average                | 2       |2                 |磁碟大小、儲存成本和虛擬機器大小         |
|virtualDisk.numberReadAveraged.average   | 1       |3                 |磁碟大小、儲存成本和虛擬機器大小         |
|virtualDisk.numberReadAveraged.average  | 1       |3                 |磁碟大小、儲存成本和虛擬機器大小         |
|net.received.average                     | 2       |3                 |虛擬機器大小和網路成本                        |
|net.transmitted.average                  | 2       |3                 |虛擬機器大小和網路成本                        |

> [!WARNING]
> 如果您剛剛設定較高的統計資料層級，可能需要一天的時間才能產生效能計數器。 因此，建議您在一天後執行探索。

## <a name="run-the-collector-to-discover-vms"></a>執行收集器來探索 VM

針對每個需要執行的探索，您要執行收集器來探索所需範圍內的虛擬機器。 請逐一執行探索。 系統不支援並行探索，且每個探索的範圍不得相同。

1. 在 vSphere 用戶端主控台中，以滑鼠右鍵按一下 [VM] > [開啟主控台]。
2. 提供設備的語言、時區和密碼喜好設定。
3. 在桌面上，選取 [執行收集器] 捷徑。
4. 在 Azure Migrate 收集器中，開啟 [設定必要條件]，然後：

   a. 接受授權條款，並閱讀第三方資訊。

   收集器會確認 VM 是否能夠存取網際網路。
   
   b. 如果虛擬機器能夠透過 Proxy 存取網際網路，請選取 [Proxy 設定]，然後指定 Proxy 位址和接聽連接埠。 如果 Proxy 需要驗證，請指定認證。

   收集器會檢查收集器服務是否正在執行。 根據預設，收集器 VM 上會安裝此服務。

   c. 下載並安裝 VMware PowerCLI。

5. 在 [指定 vCenter Server 詳細資料] 中，執行下列動作：
    - 指定 vCenter Server 的名稱 (FQDN) 或 IP 位址。
    - 在 [使用者名稱] 和 [密碼] 中，指定收集器要用來探索 vCenter Server 中虛擬機器的唯讀帳戶認證。
    - 在 [選取範圍] 中，選取虛擬機器探索的範圍。 收集器只能探索指定範圍內的虛擬機器。 範圍可以設定為特定資料夾、資料中心或叢集。 其不應包含超過 1000 個虛擬機器。 

6. 在 [指定移轉專案] 中，指定專案的識別碼和索引鍵。 如果您之前未複製，請從收集器虛擬機器開啟 Azure 入口網站。 在專案的 [概觀] 頁面上，選取 [探索機器]，然後複製值。  
7. 在 [檢視收集進度] 中監視探索程序，然後確認從虛擬機器收集到的中繼資料位於範圍內。 收集器會提供概略的探索時間。


### <a name="verify-vms-in-the-portal"></a>在入口網站中確認 VM

探索時間取決於您要探索多少 VM。 一般來說，若是 100 個虛擬機器，探索大約會在收集器完成執行後的一小時完成。 

1. 在 Migration Planner 專案中，選取 [管理] > [機器]。
2. 確認您想要探索的 VM 出現在入口網站內。


## <a name="next-steps"></a>後續步驟

- 了解如何[建立評定群組](how-to-create-a-group.md)。
- [深入了解](concepts-assessment-calculation.md)評定的計算方式。
