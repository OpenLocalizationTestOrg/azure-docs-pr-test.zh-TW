---
title: "適用於開發人員的 Azure 批次 aaaOverview |Microsoft 文件"
description: "了解 hello 批次服務和其 Api 開發的觀點而言 hello 功能。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>使用 Batch 開發大規模的平行運算解決方案

本概觀 hello 的 hello Azure 批次服務的核心元件，我們將討論 hello 主要服務功能和資源，批次的開發人員可以使用 toobuild 大規模的平行運算解決方案。

您正在開發分散式計算應用程式，或服務，會發出直接[REST API] [ batch_rest_api]呼叫，或您要使用其中一種 hello[批次 Sdk](batch-apis-tools.md#azure-accounts-for-batch-development)，您將使用許多 hello 資源和本文所討論的功能。

> [!TIP]
> 較高層級簡介 toohello 批次服務，請參閱[Azure Batch 基本概念](batch-technical-overview.md)。
>
>

## <a name="batch-service-workflow"></a>Batch 服務工作流程
hello 下列高階工作流程是典型的幾乎所有應用程式和使用 hello 處理平行的工作負載的批次服務的服務：

1. 上傳 hello**資料檔案**想 tooprocess tooan [Azure 儲存體][ azure_storage]帳戶。 批次包含內建支援，可以存取 Azure Blob 儲存體，和您的工作可以下載這些檔案太[計算節點](#compute-node)hello 工作執行時。
2. 上傳 hello**應用程式檔案**將執行您的工作。 這些檔案可以是二進位檔或指令碼和它們的相依性，並且會執行作業中的 hello 工作。 您的工作可以下載這些檔案從您的儲存體帳戶，或者您可以使用 hello[應用程式封裝](#application-packages)批次的應用程式管理和部署的功能。
3. 建立計算節點的 [集區](#pool) 。 當您建立一個集區時，您會指定 hello 的 hello 集區、 大小和 hello 作業系統的運算節點數目。 當工作中的每個工作執行時，它會指派 tooexecute 其中一個集區中的 hello 節點上。
4. 建立 [作業](#job)。 作業可管理一群工作。 您會將每個作業 tooa 特定集區將在其中執行該作業的工作產生關聯。
5. 新增[工作](#task)toohello 作業。 Hello 應用程式或指令碼，您上傳 tooprocess hello 資料檔案，它會從儲存體帳戶下載，則會執行每項工作。 每項工作完成時，它可以上傳其輸出 tooAzure 儲存體。
6. 監控工作進度，並從 Azure 儲存體擷取 hello 工作輸出。

hello 下列各節討論這些與 hello 批次的啟用分散式計算案例的其他資源。

> [!NOTE]
> 您需要[批次帳戶](#account)toouse hello 批次服務。 大部分 Batch 解決方案也會使用 [Azure 儲存體][azure_storage] 帳戶來儲存和擷取檔案。 批次目前支援的只有 hello**一般用途**儲存體帳戶類型，如步驟 5 中所述[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)中[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。
>
>

## <a name="batch-service-resources"></a>Batch 服務資源
部分的下列資源--帳戶 hello 計算節點、 集區、 工作和工作，即所需使用 hello 批次服務的所有方案。 其他資源 (如作業排程和應用程式套件) 都很實用，但為選用功能。

* [帳戶](#account)
* [計算節點](#compute-node)
* [集區](#pool)
* [作業](#job)

  * [作業排程](#scheduled-jobs)
* [Task](#task)

  * [啟動工作](#start-task)
  * [作業管理員工作](#job-manager-task)
  * [作業準備和作業釋放工作](#job-preparation-and-release-tasks)
  * [多重執行個體工作 (MPI)](#multi-instance-tasks)
  * [作業相依性](#task-dependencies)
* [應用程式封裝](#application-packages)

## <a name="account"></a>帳戶
批次帳戶是 hello 批次服務中的唯一識別的實體。 所有處理都與 Batch 帳戶相關聯。

您可以建立使用 hello Azure Batch 帳戶[Azure 入口網站](batch-account-create-portal.md)或以程式設計的方式，例如以 hello [Batch Management.NET 程式庫](batch-management-dotnet.md)。 建立 hello 帳戶時，您可以將 Azure 儲存體帳戶產生關聯。

### <a name="pool-allocation-mode"></a>集區配置模式

當您建立 Batch 帳戶時，可以指定如何配置計算節點的[集區](#pool)。 您可以選擇 tooallocate 集區的運算節點中的訂用帳戶管理的 Azure 批次，或您可以將他們配置您的訂用帳戶中。 hello*集區配置模式*hello 帳戶的屬性會決定集區配置的位置。 

toodecide 的集區配置模式 toouse，請考慮這最適合您的案例：

* **批次服務**： 批次服務是 hello 預設集區配置模式，集區中配置管理 Azure 訂用帳戶中的 hello 背景。 請記住下列重點 hello 批次服務集區配置模式的相關：

    - hello 批次服務集區配置模式下支援雲端服務和虛擬機器的集區。
    - hello 批次服務集區配置模式支援兩個共用金鑰驗證或[Azure Active Directory 驗證](batch-aad-auth.md)(Azure AD)。 
    - 您可以使用任一專用或低優先順序的計算節點以 hello 批次服務集區配置模式下所配置的集區中。
    - 如果您計劃 toocreate Azure 虛擬機器的集區從自訂 VM 映像，或者如果您計劃 toouse 虛擬網路，請勿使用 hello 批次服務集區配置模式。 改為建立您的帳戶與 hello 使用者訂用帳戶集區配置模式。
    - 建立與 hello 批次服務集區配置模式下，帳戶佈建的虛擬機器集區必須從建立[Azure 虛擬機器 Marketplace] [ vm_marketplace]映像。

* **使用者訂用帳戶**: hello 使用者訂用帳戶集區配置模式中，批次集區會在 hello hello 帳戶建立所在的 Azure 訂用帳戶中配置。 請記住下列重點 hello 使用者訂用帳戶集區配置模式的相關：
     
    - hello 使用者訂用帳戶集區配置模式下支援只有虛擬機器的集區。 並不支援雲端服務集區。
    - toocreate 虛擬機器的集區的自訂 VM 映像或 toouse 虛擬網路與虛擬機器集區，您必須使用 hello 使用者訂用帳戶集區配置模式。  
    - 您必須使用[Azure Active Directory 驗證](batch-aad-auth.md)與 hello 使用者訂用帳戶中配置的集區。 
    - 您必須設定 Azure 金鑰保存庫為您的 Batch 帳戶如果 hello 集區配置模式下設定 tooUser 訂用帳戶。 
    - 您可以使用只有專用的運算節點中建立與 hello 使用者訂用帳戶集區配置模式下的帳戶的集區中。 不支援低優先順序的節點。
    - 在具有 hello 使用者訂用帳戶集區配置模式下的帳戶中佈建的虛擬機器集區可以建立從[Azure 虛擬機器 Marketplace] [ vm_marketplace]映像，或從自訂映像，您提供。

下表中的 hello 比較 hello 批次服務和使用者訂用帳戶集區配置模式。

| **集區配置模式**                 | **Batch 服務**                                                                                       | **使用者訂用帳戶**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **集區配置位置**               | Azure 管理的訂用帳戶                                                                           | hello 使用者訂用帳戶中的 hello 批次建立帳戶                        |
| **支援的組態**             | <ul><li>雲端服務設定</li><li>虛擬機器設定 (Linux 和 Windows)</li></ul> | <ul><li>虛擬機器設定 (Linux 和 Windows)</li></ul>                |
| **支援的 VM 映像**                  | <ul><li>Azure Marketplace 影像</li></ul>                                                              | <ul><li>Azure Marketplace 影像</li><li>自訂映像</li></ul>                   |
| **支援的計算節點類型**         | <ul><li>專用節點</li><li>低優先順序節點</li></ul>                                            | <ul><li>專用節點</li></ul>                                                  |
| **支援的驗證**             | <ul><li>共用金鑰</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **需要 Azure Key Vault**             | 否                                                                                                      | 是                                                                                |
| **核心配額**                           | 取決於 Batch 核心配額                                                                          | 取決於訂用帳戶核心配額                                              |
| **Azure 虛擬網路 (Vnet) 支援** | 建立以 hello 雲端服務組態集區                                                      | 建立以 hello 虛擬機器組態的集區                               |
| **支援的 Vnet 部署模型**      | 使用傳統部署模型建立的 Vnet                                                             | Vnet 建立 hello 傳統部署模型或 Azure 資源管理員 |

## <a name="azure-storage-account"></a>Azure 儲存體帳戶

大部分 Batch 解決方案都使用 Azure 儲存體來儲存資源檔和輸出檔。  

批次目前僅支援 hello 一般用途儲存體帳戶類型，如所述的步驟 5 中[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)中[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 您的 Batch 工作 (包括標準工作、啟動工作、作業準備工作和作業發行工作) 必須指定位於一般用途的儲存體帳戶中的資源檔。


## <a name="compute-node"></a>計算節點
Azure 虛擬機器 (VM) 或雲端服務是專用的 tooprocessing 部分應用程式的工作負載的 VM 運算節點。 節點的 hello 大小會決定 hello CPU 核心數目、 記憶體容量和配置 toohello 節點的本機檔案系統大小。 您可以使用 Azure 雲端服務，從 hello 的映像，以建立集區的 Windows 或 Linux 節點[Azure 虛擬機器 Marketplace][vm_marketplace]，或您準備自訂映像。 請參閱下列資訊 hello[集區](#pool)> 一節，如需有關這些選項。

節點可以執行任何可執行檔或指令碼支援的 hello 作業系統環境的 hello 節點。 這包括適用於 Windows 的 \*.exe、\*.cmd、\*.bat 和 PowerShell 指令碼，以及適用於 Linux 的二進位檔、Shell 和 Python 指令碼。

Batch 中的所有計算節點也包括︰

* 工作可參考的標準[資料夾結構](#files-and-directories)與相關聯的[環境變數](#environment-settings-for-tasks)。
* **防火牆**之設定的設定 toocontrol 存取。
* [遠端存取](#connecting-to-compute-nodes)tooboth (遠端桌面通訊協定 (RDP)) Windows 和 Linux (安全殼層 (SSH)) 節點。

## <a name="pool"></a>集區
集區是應用程式執行所在的一群節點。 hello 集區可以手動建立，或自動 hello 批次服務時指定 hello 工作 toobe 完成。 您可以建立和管理的集區，以符合您的應用程式的 hello 資源需求。 集區僅供在其中建立 hello Batch 帳戶。 批次帳戶可以有多個集區。

在 hello 核心 Azure 運算平台上，建置 azure 批次集區。 它們提供大規模的配置、 應用程式安裝、 資料分佈、 健康狀態監控，以及彈性調整的運算節點區內 hello 數字 ([調整](#scaling-compute-resources))。

加入 tooa 集區的每個節點會指派唯一的名稱和 IP 位址。 當從集區移除節點時，toohello 作業系統或檔案所做的任何變更都會遺失，且其名稱和 IP 位址釋出供未來使用。 當節點離開集區時，其存留期就結束。

當您建立一個集區時，您可以指定下列屬性的 hello。 某些設定而有所不同，hello hello 批次的集區配置模式下[帳戶](#account):

- 計算節點作業系統和版本
- 計算節點類型和目標節點數目
- Hello 計算節點的大小
- 調整原則
- 工作排程原則
- 計算節點的通訊狀態
- 計算節點的啟動工作
- 應用程式封裝
- 網路組態

這些設定在 hello 下列各節中詳細說明。

> [!IMPORTANT]
> 以 hello 批次服務集區配置模式下建立的批次帳戶有限制 hello 批次帳戶的核心數目的預設配額。 hello 核心數目對應 toohello 的運算節點數目。 您可以找到 hello 預設配額和指示如何太[增加配額](batch-quota-limit.md#increase-a-quota)中[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。 如果您的集區不達成其目標節點數目，hello 核心配額可能 hello 原因。
>
>以 hello 使用者訂用帳戶集區配置模式下建立的批次帳戶未觀察到的 hello 批次服務配額。 相反地，它們共用在 hello hello 的核心配額指定訂用帳戶。 如需詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)中的 [虛擬機器限制](../azure-subscription-service-limits.md#virtual-machines-limits)。
>
>

### <a name="compute-node-operating-system-and-version"></a>計算節點作業系統和版本

當您建立的批次集區時，您可以指定 hello Azure 虛擬機器組態和 hello 類型的作業系統想 toorun hello 集區中每個計算節點上的系統。 hello 共有兩種設定可在批次中可：

- hello**虛擬機器組態**，以指定該 hello 集區 Azure 虛擬機器所組成。 這些 VM 可能會從 Linux 或 Windows 映像加以建立。 

    當您建立 hello 虛擬機器組態為基礎的集區時，您必須指定不僅 hello 的 hello 節點的大小和 hello 映像使用 toocreate hello 來源，但也 hello**虛擬機器映像參考**和 hello批次**節點代理程式 SKU** toobe hello 節點上安裝。 如需指定這些集區屬性的詳細資訊，請參閱 [在 Azure Batch 集區中佈建 Linux 計算節點](batch-linux-nodes.md)。

- hello**雲端服務設定**，以指定該 hello 集區 Azure 雲端服務節點所組成。 雲端服務組態「只」提供 Windows 計算節點。

    雲端服務設定集區的可用的作業系統會列在 hello [Azure 客體作業系統版本與 SDK 相容性比較表](../cloud-services/cloud-services-guestos-update-matrix.md)。 當您建立包含雲端服務節點的集區時，您需要 toospecify hello 節點大小及其*OS 系列*。 雲端服務是部署的 tooAzure 的速度會比執行 Windows 的虛擬機器。 如果您需要 Windows 計算節點的集區，可能會發現雲端服務提供了部署時間方面的效能優勢。

    * hello *OS 系列*也會決定哪一個版本的.NET 安裝以 hello OS。
    * 與雲端服務中的背景工作角色，您可以指定*OS 版本*(如需背景工作角色的詳細資訊，請參閱 hello[告訴我雲端服務](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services)> 一節中 hello[雲端服務概觀](../cloud-services/cloud-services-choose-me.md))。
    * 因為背景工作角色，我們建議您指定`*`hello *OS 版本*以便 hello 節點會自動升級，而且沒有任何所需 toocater toonewly 發行版本。 選取特定的作業系統版本的 hello 主要使用案例是 tooensure 應用程式相容性，可讓測試 toobe 允許 hello 版本 toobe 更新之前所執行的回溯相容性。 在驗證之後 hello *OS 版本*可以更新 hello 集區可以安裝新作業系統映像 hello-針對任何正在執行的工作會被打斷並且排入佇列。

當您建立一個集區時，您必須 tooselect hello 適當**nodeAgentSkuId**，端視 hello OS hello 基底映像的 VHD。 您可以取得可用的節點代理程式 SKU 識別碼傳回 tootheir 對應 OS 映像參考呼叫 hello[清單支援節點代理程式 Sku](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus)作業。

請參閱 hello[帳戶](#account)> 一節，如需設定 hello 集區配置模式下，當您建立批次帳戶資訊。

#### <a name="custom-images-for-virtual-machine-pools"></a>適用於虛擬機器集區的自訂映像

toouse 自訂映像 tooprovision 虛擬機器集區，建立您的 Batch 帳戶與 hello 使用者訂用帳戶集區配置模式。 在此模式中，批次集區配置到 hello hello 帳戶所在的訂用帳戶。 請參閱 hello[帳戶](#account)> 一節，如需設定 hello 集區配置模式下，當您建立批次帳戶資訊。

toouse 自訂映像，您將需要 tooprepare hello 映像，將它一般化。 準備 Azure 的 Vm 所傳來的自訂 Linux 映像的相關資訊，請參閱[擷取做為範本 Azure Linux VM toouse](../virtual-machines/linux/capture-image-nodejs.md)。 如需有關從 Azure VM 準備自訂 Windows 映像的資訊，請參閱[使用 Azure PowerShell 建立自訂 VM 映像](../virtual-machines/windows/tutorial-custom-images.md)。 

> [!IMPORTANT]
> 當您準備自訂映像，請記得 hello 下列：
> - 請確定該 hello 基本 OS 映像使用的 tooprovision 您批次集區並沒有任何預先安裝 Azure 擴充功能，例如 hello 自訂指令碼延伸模組。 如果 hello 映像包含預先安裝的擴充功能，則 Azure 可能會遇到部署 hello VM 的問題。
> - 請確定該 hello 基本 OS 映像您提供使用 hello 預設暫存磁碟機，如 hello 批次節點代理程式目前必須要有 hello 預設暫存磁碟機。
>
>

toocreate 使用自訂映像的虛擬機器組態集區，您將需要一個或更一般的 Azure 儲存體帳戶 toostore 自訂的 VHD 映像。 自訂映像會儲存為 blob。 您的自訂映像時建立集區，tooreference 指定 hello hello hello 自訂映像 VHD blob 的 Uri [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk)屬性 hello [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf)屬性。

請確定您的儲存體帳戶符合下列準則的 hello:   

- hello 儲存體帳戶包含 hello 自訂映像的 VHD blob 需要在 toobe hello 相同訂用帳戶，因為 hello 批次帳戶 （hello 使用者訂用帳戶）。
- hello 指定儲存體帳戶需要在 hello toobe hello Batch 帳戶與相同的區域。
- 目前僅支援標準一般用途的儲存體帳戶。 Hello 未來會支援 azure 高階儲存體。
- 您可以指定一個具有多個自訂 VHD blob 的儲存體帳戶，或是多個儲存體帳戶，每個皆具有單一的 blob。 我們建議您 toouse 多個儲存體帳戶 tooget 更佳的效能。
- Too40 Linux VM 執行個體或 20 Windows VM 執行個體，可支援一個唯一的自訂映像的 VHD blob。 您將需要 toocreate hello VHD blob toocreate 集區與多個 Vm 的副本。 例如，具有 200 Windows Vm 之集區需要 10 個唯一的 VHD blob 指定 hello **osDisk**屬性。

toocreate 使用 hello Azure 入口網站的自訂映像從集區：

1. 瀏覽 tooyour hello Azure 入口網站中的批次帳戶。
2. 在 hello**設定**刀鋒視窗中，選取 hello**集區**功能表項目。
3. 在 hello**集區**刀鋒視窗中，選取 hello**新增**hello; 命令**新增集區**刀鋒視窗會顯示。
4. 選取**自訂映像 (Linux/Windows)**從 hello**映像類型**下拉式清單。 hello 入口網站會顯示 hello**自訂映像**選擇器。 從 hello 選擇一或多個 Vhd 相同的容器，按一下 hello**選取** 按鈕。 
    將加入支援多個 Vhd，從不同的儲存體帳戶和不同的容器，在未來的 hello。
5. 選取正確的 hello **Sku/方案發行者/**您自訂的 Vhd，請選取所需的 hello**快取**模式中，然後在所有的填滿 hello hello 集區的其他參數。
6. toocheck 如果集區為基礎的自訂映像，請參閱 hello**作業系統**屬性中的 hello hello 資源摘要區段**集區**刀鋒視窗。 hello 這個屬性的值應該是**自訂 VM 映像**。
7. 集區相關聯的所有自訂 Vhd 會顯示在集區 hello**屬性**刀鋒視窗。

### <a name="compute-node-type-and-target-number-of-nodes"></a>計算節點類型和目標節點數目

當您建立一個集區時，您可以指定哪些類型的計算節點，並針對每個 hello 目標數目。 計算節點的 hello 兩個類型為：

- **專用計算節點。** 專用計算節點會保留給您的工作負載使用。 它們會比低優先權的節點更為昂貴，但保證 toonever 清空。

- **低優先順序的計算節點。** 低優先權的節點多餘的容量在中充分利用 Azure toorun 批次的工作負載。 低優先順序的節點每小時比專用節點更便宜，並可啟用需要大量計算能力的工作負載。 如需詳細資訊，請參閱[使用低優先順序的 VM 搭配 Batch](batch-low-pri-vms.md)。

    Azure 多餘的容量不足時，可能會佔用低優先順序的計算節點。 如果節點先佔時執行工作時，hello 工作會排入佇列，然後再次執行，一旦計算節點再次變為無法使用。 低優先權的節點會是很適合用於工作負載 hello 作業完成時間是彈性以及 hello 工作分散到多的節點。 在您的案例決定 toouse 低優先權的節點之前，請確定任何工作，會遺失，因為 toopreemption 會最少且容易 toorecreate。

    只會針對批次帳戶建立 hello 集區配置模式下設定太低優先順序的計算節點可用**批次服務**。

您可以在 hello 這兩個低優先權置和專用的運算節點相同的集區。 每個節點類型&mdash;低優先權置和專用&mdash;有它自己的目標設定，可以指定預期的 hello 節點數目。 
    
hello 的運算節點數目是參照的 tooas*目標*因為在某些情況下，您的集區可能無法送達預期的 hello 節點數目。 例如，集區可能無法達成 hello 目標若達到 hello[核心配額](batch-quota-limit.md)您批次帳戶第一次。 或 hello 集區可能無法達成 hello 目標，如果您已套用的自動調整公式 toohello 集區，以限制 hello 的節點數目上限。

如需低優先順序和專用計算節點的價格資訊，請參閱 [Batch 價格](https://azure.microsoft.com/pricing/details/batch/)。

### <a name="size-of-hello-compute-nodes"></a>Hello 計算節點的大小

**雲端服務組態** 計算節點大小會列於 [雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md)。 Batch 支援 `ExtraSmall`、`STANDARD_A1_V2` 和 `STANDARD_A2_V2` 以外的所有雲端服務大小。

[虛擬機器組態] 計算節點大小列於 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md) (Linux) 和 [Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md) (Windows)。 除了 `STANDARD_A0` 和進階儲存體的大小 (`STANDARD_GS`、`STANDARD_DS` 和 `STANDARD_DSV2` 系列) 以外，Batch 支援所有的 Azure VM 大小。

選取時計算節點大小，請考慮 hello 特性和 hello hello 節點，您將執行的應用程式的需求。 層面，例如是否 hello 應用程式是多執行緒和會耗用多少記憶體可協助判斷 hello 最適當且符合成本效益節點大小。 它是一般 tooselect 假設一項工作的節點大小將會在節點執行一次。 不過，很可能 toohave 多個工作 （並因此多個應用程式執行個體）[平行執行](batch-parallel-node-tasks.md)在作業執行期間計算節點。 在此案例中很常見 toochoose 較大節點大小 tooaccommodate hello 增加的要求平行工作執行。 如需詳細資訊，請參閱[工作排程原則](#task-scheduling-policy)。

所有集區中的 hello 節點都 hello 相同大小。 如果您想 toorun 應用程式使用不同的系統需求和 （或） 載入層級，我們建議您使用不同的集區。

### <a name="scaling-policy"></a>調整原則

針對動態的工作負載，您可以撰寫，並套用[的自動調整公式](#scaling-compute-resources)tooa 集區。 hello 批次服務會定期評估您的公式，並調整 hello 節點區內 hello 根據不同的集區、 作業，以及您可以指定的工作參數的數目。

### <a name="task-scheduling-policy"></a>工作排程原則

hello[工作，每個節點的最大](batch-parallel-node-tasks.md)組態選項會決定 hello 可以平行執行 hello 集區中每個計算節點上的工作數目上限。

hello 預設組態會指定節點上，執行一次一項工作，但是有很有幫助 toohave 案例的節點上同時執行兩個或多個工作。 請參閱 hello[範例案例](batch-parallel-node-tasks.md#example-scenario)在 hello[並行節點工作](batch-parallel-node-tasks.md)文章 toosee 如何從每個節點的多個工作可以受益。

您也可以指定*填滿類型*可判斷是否位於集區中的所有節點間平均散佈 hello 工作批次，或指派工作 tooanother 節點之前組件以 hello 工作最大數目的每個節點。

### <a name="communication-status-for-compute-nodes"></a>計算節點的通訊狀態

在大部分情況下，工作會獨立運作，而且不需要 toocommunicate 彼此。 不過，有一些工作必須進行通訊的應用程式，例如 [MPI 案例](batch-mpi.md)。

您可以設定集區 tooallow**節點間通訊**，如此一來，集區中的節點可以在執行階段通訊。 啟用節點間通訊時，[雲端服務組態] 集區中的節點可以在超過 1100 個連接埠上彼此通訊，而且 [虛擬機器組態] 集區並不會限制任何連接埠的流量。

請注意，啟用節點間通訊也會影響叢集內的 hello 節點 hello 放置可能會由於部署的限制限制 hello 的集區中的節點數目上限。 如果您的應用程式不需要節點之間的通訊，hello 批次服務可以配置可能有大量節點 toohello 集區從許多不同的叢集和資料中心 tooenable 增加平行處理能力。

### <a name="start-tasks-for-compute-nodes"></a>計算節點的啟動工作

選擇性的 hello*啟動工作*該節點會加入 hello 集區，而且每次節點重新啟動或重新安裝映像的每個節點上執行。 hello 啟動工作是特別適用於運算節點準備 hello 執行的工作，例如安裝 hello 計算節點執行您的工作的 hello 應用程式。

### <a name="application-packages"></a>應用程式封裝

您可以指定[應用程式封裝](#application-packages)toodeploy toohello 計算 hello 集區中的節點。 應用程式套件提供簡化的部署和版本管理您的工作執行的 hello 應用程式。 您針對集區指定的應用程式封裝會安裝於加入該集區的每個節點，以及在節點重新啟動或重新安裝映像時安裝。

> [!NOTE]
> 在 2017 年 7 月 5 日之後建立的所有 Batch 集區都支援應用程式套件。 只有建立 hello 集區時使用的雲端服務組態，10 年 3 月 2016年和 5 年 7 月 2017年之間建立的批次集區中支援它們。 建立先前 too10 2016 年 3 月的批次集區不支援應用程式封裝。 如需有關使用應用程式套件 toodeploy 您應用程式 tooyour 批次的節點，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。
>
>

### <a name="network-configuration"></a>網路組態

您可以指定 hello Azure 子網路[虛擬網路 (VNet)](../virtual-network/virtual-networks-overview.md)應在哪個 hello 集區計算建立節點。 請參閱 hello[集區的網路設定](#pool-network-configuration)節的詳細資訊。


## <a name="job"></a>作業
作業是工作的集合。 它會管理其工作集區中的 hello 計算節點上執行計算的方式。

* 指定 hello hello 工作**集區**在哪一個 hello 工作是 toobe 執行。 您可以為每個作業建立新的集區，或將集區使用於許多工作。 您可以針對與作業排程相關聯的每項作業建立集區，或針對與作業排程相關聯的所有作業建立集區。
* 您可以指定選擇性的 **作業優先順序**。 工作提交具有較高的優先順序比目前正在進行中的工作之後，hello hello 較高優先順序作業的工作會插入到 hello 佇列前面 hello 較低優先順序的工作的工作。 已在執行中的較低優先順序作業中的工作不會被優先佔用。
* 您可以使用作業**條件約束**toospecify 某些限制為您的工作：

    您可以設定**最大 wallclock 時間**，如此一來，如果工作執行的時間超過指定的 hello wallclock 最大時間，hello 工作和所有的工作都會終止。

    Batch 可以偵測並重試失敗的工作。 您可以指定 hello**工作重試次數上限**做為條件約束，包括工作是否*一律*或*從未*重試。 重試工作表示該 hello 工作排入佇列的 toobe 再執行一次。
* 用戶端應用程式可以加入工作 tooa 作業，或者您可以指定[作業管理員工作](#job-manager-task)。 作業管理員工作包含作業的必要 toocreate hello 所需工作的 hello 資訊、 與 hello 作業管理員工作在其中一個 hello 上正在執行中的計算節點 hello 集區。 hello 作業管理員工作會處理批次-由具體它已排入佇列只要 hello 工作建立時，並重新啟動失敗。 作業管理員工作是*必要*工作所建立的[作業排程](#scheduled-jobs)，所以 hello 唯一方式 toodefine hello 工作 hello 工作具現化之前。
* 根據預設，工作 hello 作用中狀態時維持 hello 作業內的所有工作都都已完成。 使 hello 作業會自動終止 hello 作業中的所有工作完成時，您可以變更此行為。 集 hello 作業的**onAllTasksComplete**屬性 ([OnAllTasksComplete] [ net_onalltaskscomplete]在批次.NET) 太*terminatejob* tooautomatically所有的工作會處於 hello 完成狀態，請終止 hello 工作。

    請注意 hello 批次服務會考量與工作*沒有*工作 toohave 所有的工作完成。 因此，這個選項最常搭配 [作業管理員工作](#job-manager-task)使用。 如果您想 toouse 自動作業終止，而不是工作管理員，您應該一開始會設定新的工作**onAllTasksComplete**屬性太*noaction*，然後將它設定太*terminatejob*只完成新增工作 toohello 工作之後。

### <a name="job-priority"></a>作業優先順序
您可以指派優先權 toojobs 在批次中所建立。 hello 批次服務將使用 hello hello 作業 toodetermine hello 順序的工作排程帳戶內的優先順序值 (這不是與混淆的 toobe[排程的工作](#scheduled-jobs))。 hello 優先順序值的範圍從-1000 too1000，與-1000 hello 最低優先順序，1000年正在 hello 最高。 tooupdate hello 優先順序的作業時，呼叫 hello[更新作業的 hello 屬性][ rest_update_job]作業 (批次 REST)，或修改 hello [CloudJob.Priority] [ net_cloudjob_priority]屬性 (批次.NET)。

Hello 內使用相同帳戶，較高優先順序的作業會排程優先於優先順序較低的工作。 一個帳戶中具有較高優先順序值的作業，其排程優先順序並不高於不同帳戶中較低優先順序值的另一項作業。

不同集區的作業排程是獨立的。 在不同的集區之間，即使作業的優先順序較高，如果其相關聯的集區缺少閒置的節點，並不保證此作業會優先排程。 在 hello 相同的集區作業以 hello 相同優先權層級機會都相同的排程。

### <a name="scheduled-jobs"></a>Scheduled jobs
[工作排程][ rest_job_schedules] toocreate hello 批次服務內的週期性工作可讓您。 作業排程指定 toorun 作業，並且包含執行 hello 作業 toobe hello 規格。 您可以指定 hello hello 排程-持續時間的時間上限時 hello 排程作用中-且 hello 期間建立工作的頻率排程期。

## <a name="task"></a>Task
工作是與作業相關聯的計算單位。 工作是在節點上執行。 工作會指派 tooa 節點執行，或佇列中直到節點變成可用為止。 簡而言之，工作會執行一個或多個程式或指令碼在計算節點 tooperform hello 您需要完成的工作。

建立工作時，您可以指定︰

* hello**命令列**hello 工作。 這是 hello hello 計算節點執行應用程式或指令碼的命令列。

    請務必 hello 命令列的 toonote 實際上不會執行下一個殼層。 因此，它原本就不會使用的殼層功能，例如[環境變數](#environment-settings-for-tasks)擴充 (這包括 hello `PATH`)。 tootake 利用這類功能，您必須叫用 hello 殼層 hello 命令列-例如，透過啟動`cmd.exe`Windows 節點上或`/bin/sh`on Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    應用程式或指令碼不是，如果您的工作需要 toorun hello 節點的`PATH`或參考環境變數，叫用明確在 hello 工作命令列中的 hello shell。
* **資源檔**包含 hello 資料 toobe 處理。 Hello 工作的命令列執行之前，這些檔案會自動複製的 toohello 節點，從 Blob 儲存體中的一般用途的 Azure 儲存體帳戶。 如需詳細資訊，請參閱 hello 章節[啟動工作](#start-task)和[檔案和目錄](#files-and-directories)。
* hello**環境變數**您的應用程式所需。 如需詳細資訊，請參閱 hello[工作的環境設定](#environment-settings-for-tasks)> 一節。
* hello**條件約束**下哪些 hello 應該執行的工作。 例如，條件約束包括 hello 最大時間 hello 工作允許 toorun，hello 最大次數應該重試失敗的工作，且 hello 最大時間 hello 工作的工作目錄中的檔案會保留。
* **應用程式封裝**toodeploy toohello 計算的節點的 hello 工作是排定的 toorun。 [應用程式封裝](#application-packages)提供簡化的部署和版本管理您的工作執行的 hello 應用程式。 工作層級應用程式封裝是特別有用的共用集區，其中一個集區中，執行不同的工作，且環境中的工作完成時，不會刪除 hello 集區。 如果作業有 hello 集區中的節點比有較少的工作，工作應用程式封裝可以減少資料傳輸因為您的應用程式是執行工作的已部署的唯一 toohello 節點。

此外您定義 tooperform 計算節點上的 tootasks，hello 下列特殊的工作也會提供 hello 批次服務：

* [啟動工作](#start-task)
* [作業管理員工作](#job-manager-task)
* [作業準備和作業釋放工作](#job-preparation-and-release-tasks)
* [多重執行個體工作 (MPI)](#multi-instance-tasks)
* [作業相依性](#task-dependencies)

### <a name="start-task"></a>啟動工作
透過建立關聯**啟動工作**與集區，您就可以準備 hello 作業環境的節點。 例如，您可以執行動作，如安裝您的工作執行的 hello 應用程式或啟動的背景處理序。 hello 執行啟動工作每次節點開始，只要它會保留在 hello 集區-包括 hello 節點時第一次加入 toohello 集區和何時重新啟動或重新安裝映像。

Hello 啟動工作的主要優點是它可以包含所有必要 tooconfigure hello 資訊的計算節點，並安裝所需的工作執行的 hello 應用程式。 因此，增加 hello 集區中的節點數目很簡單，只指定 hello 新目標節點計數。 hello 啟動工作提供 hello 批次服務 hello 資訊所需的 tooconfigure hello 新節點並取得這些做好接受的工作。

做為任何 Azure 批次工作，您可以指定一份**資源檔**中[Azure 儲存體][azure_storage]，此外 tooa**命令列**toobe執行。 hello 批次服務會首先會從 Azure 儲存體，複製 hello 資源檔案 toohello 節點，然後執行 hello 命令列。 集區啟動工作，hello 檔案清單通常包含 hello 工作應用程式和其相依性。

不過，hello 啟動工作也可能包括參考資料 toobe hello 計算節點執行的所有工作所都使用的。 例如，無法執行啟動工作的命令列`robocopy`作業 toocopy 應用程式檔案 （其指定的資源檔，下載 toohello 節點） 從 hello 啟動工作的[工作目錄](#files-and-directories)toohello[共用的資料夾](#files-and-directories)，然後執行 MSI 或`setup.exe`。

最好通常為 hello 開始工作 toocomplete hello 批次服務 toowait 之前考慮 hello 節點準備 toobe 指派工作，但您可以設定此。

如果計算節點上，啟動工作失敗，則 hello hello 節點狀態是更新的 tooreflect hello 失敗，且 hello 節點未指派任何工作。 如果發生問題的資源檔案複製從儲存體，或如果 hello 由其命令列執行的處理程序傳回非零結束代碼，啟動工作可能會失敗。

如果您加入或更新現有的集區的 hello 啟動工作，您必須重新啟動 hello 啟動工作 toobe 套用 toohello 節點及其的計算節點。

>[!NOTE]
> hello 啟動工作的總大小必須小於或等於 too32768 字元，包括資源檔和環境變數。 tooensure 啟動工作符合此需求，您可以使用兩種方法的其中一個：
>
> 1. 您可以使用應用程式封裝 toodistribute 應用程式或資料批次集區中的每個節點之間。 如需應用程式套件的詳細資訊，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。
> 2. 您可以手動建立已壓縮的封存檔，其中包含您的應用程式檔案。 將您的 zip 的封存 tooAzure 儲存體上傳為 blob。 指定封存壓縮的 hello 做為啟動工作的資源檔。 Hello 命令列執行開始工作之前，請解壓縮 hello 封存從 hello 命令列。 
>
>    toounzip hello 封存檔中，您可以使用 hello 封存您選擇的工具。 您將需要 tooinclude hello 工具 toounzip hello 封存做 hello 啟動工作的資源檔。
>
>

### <a name="job-manager-task"></a>作業管理員工作
您通常會使用**作業管理員工作**toocontrol 及/或監視工作執行，例如 toocreate 和送出 hello 工作作業，判斷其他工作 toorun，判斷當工作完成時。 不過，作業管理員工作不受限制的 toothese 活動。 它是可以執行任何動作所需的 hello 作業完全完備的工作。 比方說，作業管理員工作可能會下載指定為參數的檔案、 分析 hello 內容，該檔案，以及提交這些內容為基礎的其他工作。

作業管理員工作會在所有其他工作之前啟動。 它提供下列功能的 hello:

* 它會自動做為工作所提交 hello 批次服務建立 hello 作業時。
* 它會排程的 tooexecute hello 之前作業的其他工作。
* 其相關聯的節點是 hello 最後 toobe 正在 downsized hello 集區時，從集區移除。
* 其終止可以繫結的 toohello 終止 hello 作業中的所有工作。
* 作業管理員工作需要重新啟動 toobe 時指定 hello 最高優先權。 如果找不到閒置的節點，hello 批次服務可能會終止其中一個 hello hello 作業管理員工作 toorun hello 集區 toomake 空間中的其他執行中工作。
* 一項作業中的作業管理員工作沒有透過 hello 工作的其他工作的優先順序。 不同作業之間，只注重作業層級優先順序。

### <a name="job-preparation-and-release-tasks"></a>作業準備和作業釋放工作
Batch 會提供作業前執行設定的作業準備工作。 作業釋放工作則用於作業後維護或清理。

* **作業準備工作**: toorun 排程工作的所有計算節點上執行作業準備工作，而任何 hello 之前，先執行其他作業 」 工作。 您可以使用作業準備工作 toocopy 共用的所有工作，但資料唯一 toohello 工作，例如。
* **作業解除工作**: hello 執行至少一個工作的集區中的每個節點上完成作業後，執行作業解除工作。 您可以使用作業發行工作 toodelete 資料複製的 hello 作業準備工作或 toocompress 和上傳診斷記錄資料，例如。

同時作業準備，與發行工作時，允許您 toospecify 命令列 toorun hello 工作會叫用。 它們會提供許多功能，例如檔案下載、提升權限的執行、自訂環境變數、最大執行持續時間、重試計數、檔案保留時間。

如需關於作業準備和釋放工作的詳細資訊，請參閱 [在 Azure Batch 計算節點上執行準備和完成的工作](batch-job-prep-release.md)。

### <a name="multi-instance-task"></a>多重執行個體工作
A[多重執行個體工作](batch-mpi.md)是同時為多個計算節點上的設定的 toorun 的工作。 多個執行個體的工作，您可以啟用高效能運算的案例需要的運算節點的群組一起配置 tooprocess 單一的工作負載 (例如訊息傳遞介面 (MPI))。

如需執行批次中的 MPI 工作使用 hello 批次.NET 程式庫的詳細討論，請參閱[使用多個執行個體工作 toorun Azure 批次中的訊息傳遞介面 (MPI) 應用程式](batch-mpi.md)。

### <a name="task-dependencies"></a>作業相依性
[工作的相依性](batch-task-dependencies.md)名稱所示為 hello、 讓您 toospecify 工作相依於 hello 完成之前執行其他工作。 這項功能提供支援的情況下，「 下游 」 工作會消耗 hello 輸出的 「 上游 」 的工作--或上游的工作執行某些初始化所需的下游工作。 toouse 這項功能，您必須第一個啟用工作相依性批次作業。 然後，針對每項工作相依於另一個 （或其他許多），指定 hello 取決於該工作的工作。

與工作相依性，您可以設定類似 hello 下列案例：

* taskB 相依於 taskA (直到 taskA 完成，才會開始執行 taskB)。
* taskC 同時相依於 taskA 和 taskB。
* taskD 在執行前相依於某個範圍的工作，例如工作 1 至 10。

簽出[工作 Azure 批次中的相依性](batch-task-dependencies.md)和 hello [TaskDependencies] [ github_sample_taskdeps] hello 中的程式碼範例[azure 批次範例][github_samples] GitHub 儲存機制，如需深入了解有關這項功能。

## <a name="environment-settings-for-tasks"></a>工作的環境設定
Hello 批次服務所執行的每一項工作中有存取 tooenvironment 變數，它會計算節點上設定。 這包括 hello 批次服務所定義的環境變數 ([服務定義][msdn_env_vars]) 以及您可以為您的工作定義的自訂環境變數。 hello 應用程式和您的工作執行的指令碼沒有存取 toothese 環境變數在執行期間。

您也可以填入 hello hello 工作或作業層級設定自訂的環境變數*環境設定*這些實體的屬性。 例如，請參閱 hello[加入工作 tooa 作業][ rest_add_task]作業 (批次 REST API) 或 hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env]和[CloudJob.CommonEnvironmentSettings] [ net_job_env]批次.NET 中的屬性。

用戶端應用程式或服務可以使用來取得工作的環境變數，服務定義和自訂，hello[取得工作的相關資訊][ rest_get_task_info]作業 (批次 REST) 或存取hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env]屬性 (批次.NET)。 計算節點上執行的處理序可以存取這些和其他環境變數，在 [hello] 節點，例如，使用 hello 熟悉`%VARIABLE_NAME%`(Windows) 或`$VARIABLE_NAME`(Linux) 語法。

您可以在[計算節點環境變數][msdn_env_vars]中找到所有服務定義的環境變數完整清單。

## <a name="files-and-directories"></a>檔案和目錄
每個工作會在其「工作目錄」  下建立零個或多個檔案和目錄。 這個工作目錄可以用來儲存 hello 工作，它處理、 hello 資料所執行的 hello 程式和 hello 輸出的 hello 處理，它會執行。 Hello 工作使用者所擁有的所有檔案和目錄的工作。

hello 批次服務會公開 hello hello 節點上的檔案系統的一部分*根目錄*。 工作可以藉由參考 hello 存取 hello 根目錄`AZ_BATCH_NODE_ROOT_DIR`環境變數。 如需有關如何使用環境變數的詳細資訊，請參閱 [工作的環境設定](#environment-settings-for-tasks)。

hello 的根目錄包含下列目錄結構的 hello:

![計算節點目錄結構][1]

* **共用**： 這個目錄太提供讀取/寫入存取*所有*節點上執行的工作。 Hello 節點執行任何工作，都可以建立、 讀取、 更新和刪除這個目錄中的檔案。 工作可以存取這個目錄藉由參考 hello`AZ_BATCH_NODE_SHARED_DIR`環境變數。
* **啟動**：啟動工作使用這個目錄做為它的工作目錄。 所有的 hello 檔案，則下載的 toohello hello 啟動工作的節點會儲存在這裡。 hello 啟動工作，都可以建立、 讀取、 更新和刪除此目錄下的檔案。 工作可以存取這個目錄藉由參考 hello`AZ_BATCH_NODE_STARTUP_DIR`環境變數。
* **工作**: hello 節點上執行的每項工作會建立目錄。 它參考 hello 存取`AZ_BATCH_TASK_DIR`環境變數。

    在每個工作目錄，hello 批次服務會建立工作目錄 (`wd`) 會指定其唯一的路徑所 hello`AZ_BATCH_TASK_WORKING_DIR`環境變數。 此目錄提供讀取/寫入存取 toohello 工作。 hello 工作可以建立、 讀取、 更新和刪除這個目錄下的檔案。 這個目錄會保留根據 hello *RetentionTime* hello 工作指定的條件約束。

    `stdout.txt`和`stderr.txt`： 這些檔案會寫入 hello hello 工作執行期間的 toohello 工作資料夾。

> [!IMPORTANT]
> 當從 hello 集區中移除某個節點*所有*的 hello 儲存在 hello 節點的檔案會遭到移除。
>
>

## <a name="application-packages"></a>應用程式封裝
hello[應用程式封裝](batch-application-packages.md)便於管理的應用程式部署功能提供 toohello 計算節點的 程式集區。 您可以上傳和管理您的工作，包括其二進位檔 hello 應用程式執行的多個版本，並支援檔案。 然後您可自動部署一或多個這些應用程式 toohello 計算集區中的節點。

您可以指定在 hello 集區和工作層級的應用程式封裝。 當您指定集區的應用程式封裝時，hello 應用程式是部署的 tooevery hello 集區中的節點。 當您指定的工作應用程式封裝時，hello 應用程式已部署的唯一 toonodes 的 hello 作業 」 工作的至少一個已排程的 toorun，hello 之前執行工作的命令列。

批次的控制代碼 hello 使用 Azure 儲存體 toostore 應用程式封裝的詳細資料，並將其部署 toocompute 節點，因此可以簡化您的程式碼和管理額外負荷。

toofind 深入了解 hello 應用程式封裝功能，請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)。

> [!NOTE]
> 如果您將加入集區的應用程式封裝 tooan*現有*集區，如 hello 應用程式套件部署 toobe toohello 節點，您必須重新啟動其計算節點。
>
>

## <a name="pool-and-compute-node-lifetime"></a>集區和計算節點存留期
當您設計您的 Azure 批次方案時，您可以 toomake 設計決策與相關當集區建立，並將時間計算這些集區中的節點會保持可用。

在某一端 hello 廣泛的詳細資訊，您可以建立您送出，每個工作的集區及執行其工作完成時立即刪除 hello 集區。 這最大化使用量，因為有需要與在閒置時，立即關閉時，只會配置 hello 節點。 這表示 hello 工作必須等候 hello 節點 toobe 配置，很重要的工作都會排定執行節點，可個別、 已配置，因為與 hello 的 toonote 時啟動工作已完成。 批次未*不*等候直到所有節點區內都可用指派工作 toohello 節點之前。 這可確保所有可用節點的最大使用率。

在 hello 另一端的 hello 另一方面，如果需要立即啟動工作是 hello 最高的優先順序，您可以建立事先的集區並讓它的節點可供才能提交工作。 在此案例中，工作可以立即啟動，但節點可能閒置時等候它們 toobe 指派。

有一個通常用來處理可變但持續負載的組合方法。 您可以有多個工作提交給，但可以調整 hello 節點數目，向上或向下，根據 toohello 工作負載集區 (請參閱[調整計算資源](#scaling-compute-resources)hello 下列區段中)。 您可以根據目前的負載被動完成，或在負載可預測時主動完成。

## <a name="virtual-network-vnet-and-firewall-configuration"></a>虛擬網路 (VNet) 和防火牆設定 

當您佈建的 Azure 批次中的運算節點的集區時，您可以將 hello 集區與子網路的 Azure[虛擬網路 (VNet)](../virtual-network/virtual-networks-overview.md)。 toolearn 進一步了解建立 VNet 與子網路，請參閱[建立 Azure 虛擬網路子網路與](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。 

 * hello 與集區相關聯的 VNet 必須是：

   * 在 hello 相同 Azure**區域**為 hello Azure Batch 帳戶。
   * 在 hello 相同**訂用帳戶**為 hello Azure Batch 帳戶。

* hello 的 VNet 支援的型別取決於集區配置的方式在 hello Batch 帳戶：

    - 如果 hello 批次帳戶集區配置模式下設定 tooBatch 服務，則您可以指派以 hello 建立 VNet 只有 toopools**雲端服務設定**。 此外，VNet 必須建立與 hello 傳統部署模型 hello 所指定。 不支援與 hello Azure Resource Manager 部署模型所建立的 Vnet。
 
    - 如果 hello 批次帳戶集區配置模式下設定 tooUser 訂用帳戶，則您可以指派以 hello 建立 VNet 只有 toopools**虛擬機器組態**。 建立 hello 與集區**雲端服務組態**不支援。 hello 與 hello Azure Resource Manager 部署模型或 hello 傳統部署模型可能建立相關聯的 VNet。

    表摘要 VNet 支援根據 toopool 配置模式，請參閱 hello[集區配置模式](#pool-allocation-mode)> 一節。

* 如果您的 Batch 帳戶的 hello 集區配置模式下設定 tooBatch 服務，您必須提供權限 hello 批次服務主體 tooaccess hello VNet。 hello VNet 必須指派 hello [Classic Virtual Machine Contributor Role-Based 存取控制 (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor)角色 toohello 批次服務主體。 如果未提供 RBAC 角色指定 hello hello 批次服務會傳回 400 （不正確的要求）。 tooadd hello Azure 入口網站中的 hello 角色：

    1. 選取 hello **VNet**，然後**存取控制 (IAM)** > **角色** > **虛擬機器參與者** > **新增**。
    2. 在 hello**新增權限**刀鋒視窗中，選取 hello**虛擬機器參與者**角色。
    3. 在 hello**新增權限**刀鋒視窗中，搜尋 hello 批次 API。 搜尋每個這些字串接著直到您找到 hello API:
        1. **MicrosoftAzureBatch**。
        2. **Microsoft Azure Batch**。 較新的 Azure AD 租用戶可以使用這個名稱。
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864**是 hello 識別碼 hello 批次 API。 
    3. 選取 hello 批次 API 服務主體。 
    4. 按一下 [儲存] 。

        ![指定 VM 參與者角色 tooBatch 服務主體](./media/batch-api-basics/iam-add-role.png)


* hello 指定子網路必須擁有足夠的可用**IP 位址**tooaccommodate hello 的目標節點總數，也就是 hello 的 hello 總和`targetDedicatedNodes`和`targetLowPriorityNodes`hello 集區的內容。 如果 hello 子網路沒有足夠的可用 IP 位址，hello 批次服務部分配置 hello 集區中的 hello 計算節點，並傳回調整大小錯誤。

* hello 指定子網路必須允許來自 hello 批次服務 toobe 通訊能 tooschedule 工作 hello 計算節點上。 如果通訊 toohello 計算節點拒絕**網路安全性群組 (NSG)** hello 批次服務會將太 hello 的 hello 運算節點的狀態相關聯 VNet，hello**無法使用**。

* 如果 hello 可讓您指定具有相關聯的 VNet**網路安全性群組 (Nsg)**及/或**防火牆**，則必須啟用幾個保留的系統連接埠，以輸入通訊：

- 若為使用虛擬機器組態所建立的集區，請啟用連接埠 29876 和 29877，另外，請針對 Linux 啟用連接埠 22，至於 Windows 則啟用連接埠 3389。 
- 若為使用雲端服務組態所建立的集區，請啟用連接埠 10100、20100 和 30100。 
- 啟用輸出連線 tooAzure 連接埠 443 上的儲存體。 此外，請確定為 VNET 提供服務的任何自訂 DNS 伺服器，都能解析您的 Azure 儲存體端點。 具體來說，hello 表單的 URL`<account>.table.core.windows.net`應該是可解析。

    hello 以下表格說明 hello 輸入 tooenable 需要您建立與 hello 虛擬機器組態的集區的連接埠：

    |    目的地連接埠    |    來源 IP 位址      |    Batch 會新增 NSG 嗎？    |    所需的 VM toobe 可用？    |    使用者的動作   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>使用 hello 虛擬機器組態建立的集區： 29876、 29877</li><li>建立與 hello 雲端服務組態的集區： 10100、 20100、 30100</li></ul>         |    僅限 Batch 服務角色 IP 位址 |    是。 批次會新增在 hello 層級的網路介面 (NIC) 附加 tooVMs Nsg。 這些 NSG 只允許來自 Batch 服務角色 IP 位址的流量。 即使您 abra estos puertos para hello 整個網站，取得在 hello NIC 封鎖 hello 流量 |    是  |  您不需要 toospecify NSG，因為批次允許只有批次的 IP 位址。 <br /><br /> 不過，如果您指定 NSG，請確定這些連接埠已對輸入流量開啟。 <br /><br /> 如果您指定 * 當 hello 您 NSG 中的來源 IP，批次仍將 Nsg 加入的附加 NIC tooVMs hello 層級。 |
    |    3389、22               |    使用者電腦，作為偵錯用途，好讓您可以從遠端存取 hello VM。    |    否                                    |    否                     |    如果您想 toopermit 遠端存取 (RDP/SSH) toohello VM，請加入 Nsg。   |                 

    hello 下表描述您需要儲存體 tooenable toopermit 存取 tooAzure hello 輸出連接埠：

    |    輸出連接埠    |    目的地    |    Batch 會新增 NSG 嗎？    |    所需的 VM toobe 可用？    |    使用者的動作    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure 儲存體    |    否    |    是    |    如果您新增任何 Nsg，請確定此連接埠是開啟 toooutbound 流量。    |


## <a name="scaling-compute-resources"></a>調整計算資源
與[自動縮放比例](batch-automatic-scaling.md)，您可以讓 hello 批次服務動態調整 hello 根據 toohello 目前工作負載和資源使用狀況計算案例的集區中的運算節點數目。 這可讓您 toolower hello 您需要使用只有 hello 資源以執行您的應用程式的整體成本，並釋出那些您不需要。

撰寫 [自動調整公式](batch-automatic-scaling.md#automatic-scaling-formulas) 並將該公式與集區建立關聯，以啟用自動調整。 hello 批次服務會使用 hello 公式 toodetermine hello 目標數目節點區內 hello hello 下一步調整間隔 （您可以設定間隔）。 當您建立它，或啟用稍後調整集區上，您可以指定 hello 自動調整集區設定。 您也可以更新 hello 調整啟用調整集區上的設定。

例如，可能是作業會需要您送出非常大量的工作 toobe 執行。 您可以指派的縮放比例的公式 toohello 集區，調整 hello hello hello 目前的佇列工作數目和 hello 完成率 hello 作業中的 hello 工作為基礎的集區中的節點數目。 hello 批次服務會定期評估 hello 公式，並調整大小 hello 集區，根據工作負載和其他公式的設定。 hello 服務節點將視需要增加時有大量的佇列工作，並移除的節點時沒有排入佇列或執行工作。

調整的公式可以根據 hello 下列度量：

* **時間度量**收集中指定的 hello 每隔五分鐘的統計資料為根據的小時數。
* **資源度量** 是以 CPU 使用量、頻寬使用量、記憶體使用量和節點的數目為基礎。
* **工作計量**是以工作狀態為基礎，例如 [作用中] \(已排入佇列)、[執行中] 或 [已完成]。

當自動縮放比例減少的集區中的運算節點的 hello 數目時，您必須考慮如何 toohandle 工作執行時的 hello hello 減少作業。 tooaccommodate，批次提供*節點解除配置選項*併入您的公式。 例如，您可以指定，正在執行的工作會立即停止，立即停止然後另一個節點上，執行排入佇列或 hello 節點會從 hello 集區移除之前，允許 toofinish。

如需關於自動調整應用程式的詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](batch-automatic-scaling.md)。

> [!TIP]
> toomaximize 運算資源使用量、 設定 hello 目標數目節點 toozero hello 結束工作，但不允許執行的工作 toofinish。
>
>

## <a name="security-with-certificates"></a>憑證的安全性
時，您通常需要 toouse 憑證加密或解密機密資訊的工作，例如 hello 金鑰[Azure 儲存體帳戶][azure_storage]。 toosupport，您可以在節點上安裝憑證。 加密的密碼會透過命令列參數傳遞 tootasks 或內嵌在其中一個 hello 工作的資源，並可使用的 toodecrypt hello 安裝憑證。 它們。

使用 hello[加入憑證][ rest_add_cert]作業 (批次 REST) 或[CertificateOperations.CreateCertificate] [ net_create_cert]方法 (批次.NET)tooadd 憑證 tooa Batch 帳戶。 您接著可以將 hello 憑證與新的或現有的集區。 憑證與集區相關聯時，hello 批次服務會在 hello 集區中的每個節點上安裝 hello 憑證。 hello 節點啟動時，啟動 （包括 hello 啟動工作和作業管理員工作） 的任何工作之前，hello 批次服務會安裝 hello 適當的憑證。

如果您新增憑證 tooan*現有*集區，您必須重新啟動其計算節點 hello 憑證 toobe 套用 toohello 節點。

## <a name="error-handling"></a>錯誤處理
您可能會發現需要 toohandle 批次方案中的工作和應用程式失敗。

### <a name="task-failure-handling"></a>工作失敗處理
工作失敗可分成下列幾類：

* **前置處理失敗**

    如果工作失敗 toostart，前置處理的錯誤設定 hello 工作。  

    前置處理錯誤的發生原因 hello 工作的資源檔案已移動、 hello 儲存體帳戶已無法再使用，或遇到其他問題，予以防止的 hello 成功複製的檔案 toohello 節點。

* **檔案上傳失敗**

    如果工作指定的檔案上傳因任何原因失敗，將檔案上傳錯誤設定 hello 工作。

    檔案可能會發生錯誤如果 hello SAS 提供存取 Azure 儲存體無效或不提供寫入權限、 如果 hello 儲存體帳戶不再可用，或者如果另一個問題是發生導致 hello 成功複製的檔案上傳hello 節點。    

* **應用程式失敗**

    hello 工作的命令列所指定的 hello 程序也會失敗。 hello 程序會被視為 toohave 失敗時則為非零結束代碼由 hello hello 工作所執行的處理序 (請參閱*工作的結束代碼*hello 下一節)。

    應用程式失敗，您可以設定批次向上 tooa tooautomatically 重試 hello 工作指定的次數。

* **條件約束失敗**

    您可以設定的條件約束會指定作業或工作，hello 最大的執行持續期間 hello *maxWallClockTime*。 這可用於結束失敗 tooprogress 的工作。

    當超過 hello 最大時間量時，hello 工作會標示為*完成*，但 hello 結束程式碼會設定太`0xC000013A`和 hello *schedulingError*欄位標示為`{ category:"ServerError", code="TaskEnded"}`。

### <a name="debugging-application-failures"></a>應用程式失敗偵錯
* `stderr`和`stdout`

    在執行期間，應用程式可能會產生您可以使用 tootroubleshoot 問題的診斷輸出。 Hello 中所述前一節的[檔案和目錄](#files-and-directories)，hello 批次服務寫入標準輸出和標準錯誤輸出太`stdout.txt`和`stderr.txt`hello hello 工作目錄中的檔案計算節點。 您可以使用 hello Azure 入口網站，或其中一個 hello 批次 Sdk toodownload 這些檔案。 例如，您可以擷取這些和其他檔案，供疑難排解之用，使用[ComputeNode.GetNodeFile] [ net_getfile_node]和[CloudTask.GetNodeFile] [ net_getfile_task] hello 批次.NET 程式庫中。

* **工作結束代碼**

    如先前所述，則工作會標示為失敗 hello 批次服務，如果 hello hello 工作所執行的處理序傳回非零結束代碼。 批次時工作執行的處理序，填入 hello 工作結束程式碼內容，以 hello*傳回 hello 程序的程式碼*。 它是工作的結束碼的重要 toonote**不**取決於 hello 批次服務。 取決於工作的結束代碼 hello 程序本身或 hello 作業系統上執行哪些 hello 程序。

### <a name="accounting-for-task-failures-or-interruptions"></a>處理工作失敗或中斷
工作可能偶爾會失敗或中斷。 hello 工作應用程式本身可能會失敗，hello 節點正在執行哪些 hello 工作可能會重新開機，或 hello 節點可能會移除從 hello 集區調整大小作業期間如果 hello 集區的解除配置原則是設定 tooremove 立即而不需等待的節點工作 toofinish。 在所有情況下，hello 工作可以自動排入佇列的批次以便在另一個節點上執行。

它也可能會有間歇性問題 toocause 工作 toohang 或花太長 tooexecute。 您可以設定工作的 hello 最大執行時間間隔。 如果超過 hello 最大執行時間間隔，hello 批次服務會中斷 hello 工作應用程式。

### <a name="connecting-toocompute-nodes"></a>連接 toocompute 節點
您可以執行其他偵錯和疑難排解遠端登入 tooa 計算節點。 您可以使用 Windows 節點 hello Azure 入口網站 toodownload 遠端桌面通訊協定 (RDP) 檔案，並取得 Linux 節點的安全殼層 (SSH) 連接資訊。 您同樣可以這樣使用 hello 批次 Api-例如，[批次.NET] [ net_rdpfile]或[批次 Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh)。

> [!IMPORTANT]
> 透過 RDP 或 SSH tooconnect tooa 節點，您必須先建立使用者 hello 節點上。 toodo，您可以使用 Azure 入口網站，hello[新增使用者帳戶 tooa 節點][ rest_create_user]使用 hello 批次 REST API，呼叫 hello [ComputeNode.CreateComputeNodeUser] [net_create_user]方法在批次.NET 或呼叫 hello [add_user] [ py_add_user] hello 批次 Python 模組中的方法。
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>疑難排解有問題的計算節點
在某些工作失敗的情況下，批次的用戶端應用程式或服務可以檢查失敗的 hello 工作 tooidentify 異常節點 hello 中繼資料。 集區中的每個節點指定唯一的識別碼，以及工作執行所在的 hello 節點包含在 hello 工作中繼資料。 在找出問題節點之後，您即可對其採取數個行動︰

* **重新啟動 hello 節點**([REST][rest_reboot] | [.NET][net_reboot])

    重新啟動的 hello 節點有時可以清除等陷入不斷或損毀處理序的潛在問題。 請注意，是否您的集區會使用啟動工作，或您的工作會使用作業準備工作，它們會執行 hello 節點重新啟動時。
* **重新安裝映像 hello 節點**([REST][rest_reimage] | [.NET][net_reimage])

    這會重新安裝 hello 作業系統 hello 節點上。 與重新啟動節點，啟動工作，並已建立映像 hello 節點之後，會重新執行作業準備工作。
* **移除 hello 集區中的 hello 節點**([REST][rest_remove] | [.NET][net_remove])

    有時候很有必要 toocompletely 移除 hello 節點從 hello 集區。
* **停用工作排程在 hello 節點**([REST][rest_offline] | [.NET][net_offline])

    這實際上會讓 hello 節點離線，好讓沒有進一步的工作會指派 tooit，但是允許 hello 節點 tooremain 執行以及 hello 集區中。 這可讓您 tooperform 進一步調查 hello 原因的 hello 失敗遺失 hello 失敗的工作的資料，而不造成額外的工作失敗的 hello 節點。 例如，您可以停用工作排程 hello 節點上然後[遠端登入](#connecting-to-compute-nodes)tooexamine hello 節點的事件記錄檔，或執行其他疑難排解。 完成您的調查之後，您可以藉由啟用工作排程，然後讓 hello 節點上線 ([REST][rest_online] | [.NET] [net_online])，或執行 hello 的其中一個先前所討論的其他動作。

> [!IMPORTANT]
> 描述這一節-每個動作以重新開機，重新安裝映像、 remove 和停用排程工作-您可以 toospecify 執行 hello 動作時，如何處理目前在 hello 節點上執行的工作。 例如，當您停用工作排程在節點上使用 hello 批次.NET 用戶端程式庫，您可以指定[DisableComputeNodeSchedulingOption] [ net_offline_option]列舉值 toospecify，是否太**Terminate**執行工作、**重新排入佇列**以供在其他節點上排程或執行 hello 動作之前允許執行的工作 toocomplete (**TaskCompletion**)。
>
>

## <a name="next-steps"></a>後續步驟
* 深入了解 hello[批次應用程式開發介面和工具](batch-apis-tools.md)可用來建置批次的解決方案。
* 逐步解說範例批次應用程式中逐步[開始使用 hello Azure Batch Library for.NET](batch-dotnet-get-started.md)。 另外還有[Python 版本](batch-python-tutorial.md)在 Linux 執行工作負載的 hello 教學課程的計算節點。
* 下載並建置 hello[批次總管][ github_batchexplorer]開發批次方案過程中使用的範例專案。 您可以使用 hello 批次檔案總管 執行 hello 下列以及其他更多：

  * 監視和管理 Batch 帳戶內的集區、作業和工作
  * 從節點下載 `stdout.txt`、`stderr.txt` 和其他檔案
  * 在節點上建立使用者，並下載遠端登入的 RDP 檔案
* 了解如何太[建立集區的 Linux 運算節點](batch-linux-nodes.md)。
* 請瀏覽 hello [Azure Batch 論壇][ batch_forum] MSDN 上。 hello 論壇是關於更佳放置 tooask 問題，您只想了，或在批次中使用的是專家。

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
