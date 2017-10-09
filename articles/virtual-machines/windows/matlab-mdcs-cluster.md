---
title: "在虛擬機器上的叢集 aaaMATLAB |Microsoft 文件"
description: "使用 Microsoft Azure 虛擬機器 toocreate MATLAB Distributed Computing Server 叢集 toorun 您需要大量計算的平行 MATLAB 工作負載"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>在 Azure VM 上建立 MATLAB Distributed Computing Server 叢集
使用 Microsoft Azure 虛擬機器 toocreate 其中一個或多個 MATLAB Distributed Computing Server 叢集 toorun 您需要大量計算的平行 MATLAB 工作負載。 安裝在做為基底映像 VM toouse MATLAB Distributed Computing Server 軟體，並使用 Azure 快速入門的範本或 Azure PowerShell 指令碼 (用於[GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy 和管理 hello 叢集。 部署之後，連線 toohello 叢集 toorun 您的工作負載。

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>關於 MATLAB 和 MATLAB Distributed Computing Server
hello [MATLAB](http://www.mathworks.com/products/matlab/)平台最適合用於解決工程及科學問題。 大規模的模擬和資料處理工作的 MATLAB 使用者可以使用 MathWorks 平行計算其運算密集工作負載備份產品 toospeed 利用計算叢集和格線的服務。 [Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) 可讓 MATLAB 使用者平行處理應用程式，並利用多核心處理器、GPU 和計算叢集。 [MATLAB Distributed Computing Server](http://www.mathworks.com/products/distriben/) MATLAB 使用者 tooutilize 運算叢集中的許多電腦會啟用。

藉由使用 Azure 虛擬機器，您可以建立具有所有的 MATLAB Distributed Computing Server 叢集 hello 相同機制可用 toosubmit 平行工作在內部部署叢集，例如互動式作業、 批次作業、 獨立的工作，並通訊的工作。 Hello MATLAB 平台搭配使用 Azure 有許多優點比較 tooprovisioning 和使用傳統內部部署硬體： 虛擬機器的範圍大小，請建立叢集視您只針對付費 hello 計算資源，您使用，因此和大規模的 hello 能力 tootest 模型。  

## <a name="prerequisites"></a>必要條件
* **用戶端電腦**-您必須使用 Azure 和 hello MATLAB Distributed Computing Server 叢集的 Windows 架構的用戶端電腦 toocommunicate 部署之後。
* **Azure PowerShell** -請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall 它在用戶端電腦上。
* **Azure 訂用帳戶** - 如果您沒有訂用帳戶，只需要幾分鐘就可以建立 [免費帳戶](https://azure.microsoft.com/free/) 。 針對較大的叢集，請考慮隨用隨付訂用帳戶或其他購買選項。
* **核心配額**-大型叢集或多個 MATLAB Distributed Computing Server 叢集，您可能需要 tooincrease hello 核心配額 toodeploy。 tooincrease 配額限制時，[開啟線上客戶支援要求](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)不收費。
* **MATLAB、 平行運算工具箱和 MATLAB Distributed Computing Server 授權**-hello 指令碼會假設該 hello [MathWorks 裝載授權管理員](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/)用於所有的授權。  
* **MATLAB Distributed Computing Server 軟體**-將會安裝在將用於做為基底 VM 映像 hello hello 叢集 Vm 的 VM 上。

## <a name="high-level-steps"></a>高階步驟
toouse Azure 虛擬機器的 MATLAB Distributed Computing Server 叢集，hello 下列高階步驟所需。 Hello 文件上隨附的 hello 快速入門範本和指令碼中會有詳細的指示[GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)。

1. **建立基礎 VM 映像**  

   * 在此 VM 上下載並安裝 MATLAB Distributed Computing Server 軟體。

     > [!NOTE]
     > 此程序可能需要幾個小時，但是您只需要 toodo 它，一旦使用 MATLAB 中的每個版本。   
     >
     >
2. **建立一或多個叢集**  

   * 使用提供的 hello PowerShell 指令碼或使用 hello 快速入門範本 toocreate hello 基底 VM 映像從叢集中。   
   * 管理 hello 叢集使用提供的 hello PowerShell 指令碼可讓您 toolist、 暫停、 繼續及刪除叢集。

## <a name="cluster-configurations"></a>叢集組態
目前，hello 叢集建立指令碼和範本可讓您 toocreate 單一的 MATLAB Distributed Computing Server 拓樸。 如果您想要的話，請另外建立一或多個叢集，讓每個叢集擁有不同數量的背景工作 VM、使用不同的 VM 大小等等。

### <a name="matlab-client-and-cluster-in-azure"></a>Azure 中的 MATLAB 用戶端和叢集
hello MATLAB 用戶端節點、 MATLAB 工作排程器節點，以及 MATLAB Distributed Computing Server 「 背景工作 」 節點所有已設定為 Azure Vm 在虛擬網路中，為 hello 下列所示圖。


* toouse hello 叢集時，遠端桌面 toohello 用戶端節點連接。 hello 用戶端節點執行 hello MATLAB 用戶端。
* hello 用戶端節點的所有背景工作可以存取檔案共用。
* MathWorks 裝載授權管理員用於 hello MATLAB 的所有軟體的授權檢查。
* 根據預設，每個核心一個 MATLAB Distributed Computing Server 背景工作會建立 hello 背景工作的 Vm，但您可以指定任意數目。

## <a name="use-an-azure-based-cluster"></a>使用以 Azure 為基礎的叢集
如同其他類型的 MATLAB Distributed Computing Server 叢集，您需要 toouse hello 叢集設定檔管理員 hello MATLAB （hello 用戶端 VM） 上的用戶端 toocreate MATLAB 工作排程器群集設定檔中。

![Cluster Profile Manager](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>後續步驟
* 如需詳細的指示 toodeploy 和管理 Azure 中的 MATLAB Distributed Computing Server 叢集，請參閱 hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)包含 hello 範本和指令碼儲存機制。
* 移 toohello [MathWorks 網站](http://www.mathworks.com/)MATLAB 和 MATLAB Distributed Computing Server 的詳細文件。
