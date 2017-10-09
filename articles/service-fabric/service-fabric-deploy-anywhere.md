---
title: "在 Windows Server 和 Linux 上的 aaaCreate Azure Service Fabric 叢集 |Microsoft 文件"
description: "執行 Windows Server 和 Linux，這表示您的 Service Fabric 叢集將無法 toodeploy 和主機 Service Fabric 應用程式是您可以執行 Windows Server 或 Linux 的任何地方。"
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>在 Windows Server 或 Linux 上建立 Service Fabric 叢集
Azure Service Fabric 叢集是一組由網路連線的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。 隸屬於叢集的機器或 VM 稱為叢集模式。 叢集可以調整 toothousands 的節點。 如果您加入新的節點 toohello 叢集，則 Service Fabric 重新平衡 hello 服務磁碟分割複本和執行個體跨 hello 增加的節點數目。 整體應用程式的效能改善，而存取 toomemory 競爭會減少。 如果未有效率地使用 hello hello 叢集中的節點，您可以減少 hello hello 叢集中的節點數目。 Service Fabric 再次重新平衡 hello 磁碟分割複本，每個節點上的 hello 硬體的更有效地使用執行個體的節點 toomake hello 減少數目之間。

Service Fabric 可以 hello 建立的任何 Vm 或執行 Windows Server 或 Linux 電腦上的 Service Fabric 叢集。 這表示您無法 toodeploy 而且具有一組互相連接的 Windows Server 或 Linux 電腦在任何環境中執行 Service Fabric 應用程式，可能是在內部，Microsoft Azure 或任何雲端提供者。

## <a name="create-service-fabric-clusters-on-azure"></a>在 Azure 上建立 Service Fabric 叢集
在 Azure 上建立叢集是為了在透過資源模型範本或 hello Azure 入口網站。 讀取[建立 Service Fabric 叢集所使用的資源管理員範本](service-fabric-cluster-creation-via-arm.md)或[從 hello Azure 入口網站建立 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)如需詳細資訊。

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Azure 上的叢集支援的作業系統
您即可以 toocreate 叢集上執行這些作業系統的 Vm:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (公開預覽中) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>在內部部署或透過任何雲端提供者建立 Service Fabric 獨立叢集
Service Fabric 會提供安裝套件您 toocreate 獨立 Service Fabric 叢集內部部署或在任何雲端提供者

如需在 Windows Server 上設定獨立 Service Fabric 叢集的詳細資訊，請參閱 [建立適用於 Windows Server 的 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>任何雲端部署與內部部署之比較
建立 Service Fabric 叢集在內部部署的 hello 程序是一組的 Vm 與您所選擇的任何雲端上建立叢集類似 toohello 程序。 hello 初始步驟 tooprovision hello Vm 都受到 hello 雲端提供者或您所使用的內部部署環境。 一旦您有一組的 Vm 與啟用它們之間的網路連線然後 hello 向上 hello Service Fabric 封裝步驟 tooset、 編輯 hello 叢集設定，並執行 hello 叢集建立與管理指令碼完全相同。 這可確保您的知識和經驗的操作和管理 Service Fabric 叢集時，是可轉移 tootarget 您選擇新的裝載環境。

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>建立獨立 Service Fabric 叢集的優點
* 是免費 toochoose 任何雲端提供者 toohost 您的叢集。
* Service Fabric 應用程式，一次寫入時，可以執行在多個裝載環境中的最小 toono 變更。
* 建立 Service Fabric 應用程式的知識會夾帶從一個裝載環境 tooanother。
* 執行和管理 Service Fabric 的操作經驗從一個環境 tooanother 移轉叢集執行。
* 不受裝載環境條件約束束縛的廣大客戶群。
* 一層額外的可靠性和廣泛中斷的防護存在是因為您可以將 hello 服務移動到 tooanother 部署環境，如果資料中心或雲端提供者已停止。

## <a name="supported-operating-systems-for-standalone-clusters"></a>獨立叢集支援的作業系統
您即可以 toocreate 叢集 Vm 上執行這些作業系統的電腦：

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (敬請期待)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Azure 上的 Service Fabric 叢集的優點勝於在內部部署建立的獨立 Service Fabric 叢集
在 Azure 上執行 Service Fabric 叢集提供優於 hello 在內部部署選項，因此如果您沒有執行您的叢集的特定需求，則建議您使用它們執行在 Azure 上。 在 Azure 上，我們會提供整合與其他 Azure 功能和服務，讓作業與 hello 叢集的管理更容易且更可靠。

* **Azure 入口網站：** Azure 入口網站可讓您輕鬆 toocreate 和管理叢集。
* **Azure 資源管理員：**使用 Azure 資源管理員可輕鬆管理 hello 叢集做為一個單位使用的所有資源，並簡化成本追蹤及計費。
* **Service Fabric 叢集做為 Azure 資源** Service Fabric 叢集是 ARM 資源，因此可以像其他 Azure 中的 ARM 資源進行模型化。
* **與 Azure 基礎結構整合**Service Fabric 會與基礎作業系統、 網路和其他升級 tooimprove 可用性和可靠性的應用程式的 Azure 基礎結構的 hello 協調。  
* **診斷：** 在 Azure 上，我們提供與 Azure 診斷及 Log Analytics 的整合。
* **自動調整：**在 Azure 上的叢集，我們提供的自動調整的內建功能，因為 tooVirtual 機器規模集。 在內部部署和其他雲端環境中，您會有 toobuild 您自己的自動調整功能或手動調整叢集使用 hello 服務網狀架構會公開的應用程式開發介面的小數位數。

## <a name="next-steps"></a>後續步驟

* 在執行 Windows Server 的 VM 或電腦上建立叢集： [建立適用於 Windows Server 的 Service Fabric 叢集](service-fabric-cluster-creation-for-windows-server.md)
* 在執行 Linux 的 VM 或電腦上建立叢集︰ [Linux 上的 Service Fabric](service-fabric-linux-overview.md)
* 了解 [Service Fabric 支援選項](service-fabric-support.md)

