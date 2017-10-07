---
title: "虛擬機器的高可用性的 SAP NetWeaver aaaAzure |Microsoft 文件"
description: "Azure 虛擬機器上的 SAP NetWeaver 高可用性指南"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>SAP NetWeaver 的 Azure 虛擬機器高可用性

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Azure 虛擬機器是 hello 解決方案需要計算、 儲存和網路資源的最小時間，而不冗長的採購循環的組織。 您可以使用 Azure 虛擬機器 toodeploy 傳統應用程式為基礎的 SAP NetWeaver 的 ABAP、 Java 和 ABAP + Java 堆疊等。 擴充的可靠性與可用性，無須其他內部部署資源。 「Azure 虛擬機器」支援跨單位連線能力，貴公司可將「Azure 虛擬機器」整合到其內部部署網域、私人雲端，以及 SAP 系統環境中。

在本文中，我們將討論 hello，您可以採取的步驟 toodeploy 高可用性的 SAP 系統在 Azure 中使用 hello Azure Resource Manager 部署模型。 我們會引導您完成這些主要工作：

* 尋找 hello 右 SAP 附註和安裝指南，列在 hello[資源][ sap-ha-guide-2] > 一節。 本文補充 SAP 安裝文件集，SAP 附註，也就是 hello 主要資源，幫助您安裝和部署在特定平台上的 SAP 軟體。
* 了解 hello hello Azure Resource Manager 部署模型與 hello Azure 傳統部署模型之間的差異。
* 瞭解 Windows Server 容錯移轉叢集的仲裁模式，因此您可以選取最適合您的 Azure 部署的 hello 模型。
* 了解 Azure 服務中的「Windows Server 容錯移轉叢集」共用儲存體。
* 了解如何 toohelp 保護單一---失敗點元件類似進階商業應用程式開發 (ABAP) SAP 中央服務 (ASCS) / SAP 中央服務 (SCS) 和資料庫管理系統 (DBMS) 及重複元件，例如 SAP應用程式伺服器，在 Azure 中。
* 藉由使用 Azure Resource Manager，遵循在 Windows Server 容錯移轉叢集的叢集中安裝及設定高可用性 SAP 系統的逐步說明範例。
* 深入了解額外的步驟需要的 toouse Windows Server 容錯移轉叢集在 Azure 中，但這不需要在內部部署部署中。

toosimplify 部署和設定，在本文中，我們使用 hello SAP 三層式高可用性資源管理員範本。 hello 範本來自動化部署所需的高可用性的 SAP 系統的 hello 整個基礎結構。 hello 基礎結構也支援 SAP 系統的 SAP 應用程式的效能標準 (SAP) 的大小。

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> 必要條件
開始之前，請確定您符合 hello 必要條件 hello 下列各節中所述。 此外，請確定 toocheck hello 中列出的所有資源[資源][ sap-ha-guide-2] > 一節。

在本文中，我們針對[使用受控磁碟的三層式 SAP NetWeaver](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/) 使用 Azure Resource Manager 範本。 如需範本的實用概觀，請參閱 [SAP Azure Resource Manager 範本](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/)。

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> 資源
這些文章涵蓋 Azure 中的 SAP 部署：

* [SAP NetWeaver 的 Azure 虛擬機器規劃和實作指南][planning-guide]
* [SAP NetWeaver 的 Azure 虛擬機器部署][deployment-guide]
* [SAP NetWeaver 的 Azure 虛擬機器 DBMS 部署][dbms-guide]
* [SAP NetWeaver 的 Azure 虛擬機器高可用性 (本指南)][sap-ha-guide]

> [!NOTE]
> 可能的話，我們提供連結 toohello 參考 SAP 安裝指南 (請參閱 hello [SAP 安裝指南][sap-installation-guides])。 必要條件和 hello 安裝程序，它的建議 tooread hello SAP NetWeaver 安裝指南仔細的相關資訊。 本文僅涵蓋可與 Azure 虛擬機器搭配使用之 SAP NetWeaver 架構系統的特定工作。
>
>

這些 SAP 附註是在 Azure 中 SAP 相關的 toohello 主題：

| 附註編號 | 課程名稱 |
| --- | --- |
| [1928533] |Azure 上的 SAP 應用程式︰支援的產品和大小 |
| [2015553] |Microsoft Azure 上的 SAP：支援的必要條件 |
| [1999351] |適用於 SAP 的增強型 Azure 監視功能 |
| [2178632] |Microsoft Azure 上的 SAP 主要監視度量 |
| [1999351] |Windows 上的虛擬化︰增強型監視功能 |
| [2243692] |針對 SAP DBMS 執行個體使用 Azure 進階 SSD 儲存體 |

深入了解 hello[的 Azure 訂用帳戶限制][azure-subscription-service-limits-subscription]，包括一般的預設限制和最大限制。

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>高可用性的 SAP 的 Azure Resource Manager vs hello Azure 傳統部署模型
會在下列區域的 hello 不同 hello Azure 資源管理員和 Azure 傳統部署模型：

- 資源群組
- Azure 內部負載平衡器上 hello Azure 資源群組的相依性
- 支援 SAP 多 SID 案例

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> 資源群組
Azure 資源管理員 中，您可以使用資源群組 toomanage hello 應用程式的所有資源在您的 Azure 訂用帳戶。 整合式的方法，在資源群組中，所有資源有都 hello 相同生命週期。 例如，所有的資源在建立 hello 相同時間，而且它們已經刪除了 hello 位於相同的時間。 深入了解[資源群組](../../../azure-resource-manager/resource-group-overview.md#resource-groups)。

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure 內部負載平衡器上 hello Azure 資源群組的相依性

在 hello Azure 傳統部署模型中，沒有 hello Azure 內部負載平衡器 （Azure 負載平衡器服務） 與 hello 雲端服務之間的相依性。 每個內部負載平衡器需要一個雲端服務。

Azure 資源管理員 中，每個 Azure 資源必須 toobe 放入 Azure 資源群組，而且這適用於 Azure 負載平衡器以及。 不過，目前沒有任何需要 toohave 一項 Azure 資源群組的每個 Azure 負載平衡器，例如一個 Azure 資源群組可包含多個 Azure 負載平衡器。 hello 環境是比較簡單且更有彈性。 

### <a name="support-for-sap-multi-sid-scenarios"></a>支援 SAP 多 SID 案例

在 Azure Resource Manager 中，您可以在一個叢集中安裝多個 SAP 系統識別碼 (SID) ASCS/SCS 執行個體。 因為每個 Azure 內部負載平衡器的多個 IP 位址支援，可能有多重 SID 執行個體。

toouse hello Azure 傳統部署模型，請遵循 hello 程序中所述[在 Azure 中的 SAP NetWeaver： 使用 Windows Server 容錯移轉叢集與 SIOS DataKeeper Azure 中的叢集 SAP ASCS/SCS 執行個體](http://go.microsoft.com/fwlink/?LinkId=613056)。

> [!IMPORTANT]
> 我們強烈建議您針對 SAP 安裝使用 hello Azure Resource Manager 部署模型。 它提供 hello 傳統部署模型中未提供的許多好處。 進一步了解 Azure [部署模型][virtual-machines-azure-resource-manager-architecture-benefits-arm]。   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server 容錯移轉叢集
Windows Server 容錯移轉叢集是高可用性的 SAP ASCS/SCS 安裝和 DBMS Windows 中的 hello 基礎。

容錯移轉叢集是 1 + n 個獨立的伺服器 （節點），會一起運作的應用程式和服務 tooincrease hello 可用性群組。 如果節點失敗，Windows Server 容錯移轉叢集計算 hello 維護狀況良好時可能發生的失敗數目叢集 tooprovide 應用程式和服務。 您可以選擇從不同的仲裁模式 tooachieve 容錯移轉叢集。

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> 仲裁模式
當您使用 Windows Server 容錯移轉叢集時，可以從四種仲裁模式中選擇：

* **節點多數**。 Hello 叢集的每個節點可以在此投票。 一半以上的 hello 投票，也就是 hello 只能與大部分的投票，叢集函式。 我們建議針對節點數目為奇數的叢集使用此選項。 例如，七個節點叢集中的三個節點可能會失敗，而 hello 叢集靜像達成大多數並繼續 toorun。  
* **節點與磁碟多數**。 每個節點與 hello 叢集存放區中的指定的磁碟 （磁碟見證） 可以在此投票可用且處於通訊狀態。 hello 叢集函式只能搭配 hello 的多數投票，也就是一半以上的 hello 投票。 此模式適用於節點數目為偶數的叢集環境。 如果一半 hello 節點和 hello 磁碟在線上，hello 叢集會維持狀況良好的狀態。
* **節點與檔案共用多數**。 Hello 系統管理員指定的檔案共用 （檔案共用見證） 會建立每個節點加號可以在此投票，不論 hello 節點與檔案共用是否可用且處於通訊。 hello 叢集函式只能搭配 hello 的多數投票，也就是一半以上的 hello 投票。 此模式適用於節點數目為偶數的叢集環境。 它類似 toohello 節點與磁碟多數 模式中，但是它使用見證檔案共用，而不是見證磁碟。 此模式是簡單 tooimplement，但如果 hello 檔案共用本身不是高可用性，它可能會成為單一失敗點。
* **無多數：僅磁碟**。 如果有一個節點可用且 hello 叢集存放區中的特定磁碟通訊，hello 叢集有仲裁。 也會在與該磁碟通訊的唯一 hello 節點可以加入 hello 叢集。 建議您不要使用此模式。
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server 容錯移轉叢集內部部署
圖 1 顯示兩個節點的叢集。 如果 hello hello 節點之間的網路連線失敗與這兩個節點才能保持註冊並執行，仲裁磁碟或檔案共用判斷哪一個節點會繼續 tooprovide hello 叢集的應用程式和服務。 hello 具有存取 toohello 仲裁磁碟或檔案共用為 hello 節點，以確保服務繼續執行。

由於這個範例會使用雙節點叢集，我們使用 hello 節點與檔案共用多數仲裁模式。 hello 節點與磁碟多數也是有效的選項。 在生產環境中，建議您使用仲裁磁碟。 您可以使用網路和儲存體系統技術 toomake 它高度可用。

![圖 1：Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例][sap-ha-guide-figure-1000]

_**圖 1：**Azure 中 SAP ASCS/SCS 之 Windows Server 容錯移轉叢集組態的範例_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> 共用儲存體
圖 1 也顯示兩個節點的共用儲存體叢集。 在內部部署的共用存放裝置叢集中，hello 叢集中所有節點會都偵測共用存放裝置。 鎖定機制會保護 hello 資料損毀。 所有節點也可以偵測到另一個節點是否發生失敗。 如果一個節點失敗，hello 剩餘的節點會取得 hello 存放裝置資源的擁有權，並確保 hello 可用性的服務。

> [!NOTE]
> 您不需要與某些 DBMS 應用程式 (例如 SQL Server) 共用提供高可用性的磁碟。 SQL Server Alwayson 複寫 DBMS 資料和記錄檔從一個叢集節點 toohello 本機磁碟上的另一個叢集節點的 hello 本機磁碟上。 在此情況下，Windows hello 的叢集設定不需要共用的磁碟。
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> 網路與名稱解析
用戶端電腦連線到 hello 叢集透過一個虛擬 IP 位址和虛擬主機名稱的 DNS 伺服器提供該 hello。 hello 內部節點以及 hello DNS 伺服器可以處理多個 IP 位址。

在一般設定中，您會使用兩個或更多個網路連線：

* 專用的連接 toohello 儲存體
* 叢集-內部網路連線的 hello 活動訊號
* 公用網路的用戶端使用 tooconnect toohello 叢集

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Azure 中的 Windows Server 容錯移轉叢集
比較 toobare 金屬或私人雲端部署，Azure 虛擬機器需要額外的步驟 tooconfigure Windows Server 容錯移轉叢集。 當您建置共用的叢集磁碟時，您會需要數個 IP 位址和虛擬主機名稱的 tooset hello SAP ASCS/SCS 執行個體。

在本文中，我們會討論重要概念和 hello 額外的步驟需要的 toobuild 在 Azure 中 SAP 中央服務的高可用性叢集。 我們會示範如何向上 hello 協力廠商工具 SIOS DataKeeper tooset 和如何 tooconfigure hello Azure 內部負載平衡器。 您可以使用這些工具 toocreate Windows 容錯移轉叢集與 Azure 中的檔案共用見證。

![圖 2：Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1001]

_**圖 2：**Azure 中沒有共用磁碟的 Windows Server 容錯移轉叢集組態_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> 使用 SIOS DataKeeper 在 Azure 中共用磁碟
您需要針對高可用性的 SAP ASCS/SCS 執行個體叢集共用儲存體。 2016 年 9 月的 Azure 不提供共用存放裝置，您可以使用 toocreate 共用存放裝置叢集。 您可以使用協力廠商軟體 SIOS DataKeeper 叢集版本 toocreate 鏡像的儲存體，可以模擬叢集共用存放裝置。 hello SIOS 方案提供即時的同步資料複寫。 可以為叢集建立共用磁碟資源的方式為：

1. 在 Windows 叢集組態中附加 hello 虛擬機器 (Vm) 的額外磁碟 tooeach。
2. 在兩個虛擬機器節點上執行 SIOS DataKeeper Cluster Edition。
3. 設定 SIOS DataKeeper 叢集版本，它會反映 hello hello 額外附加的磁碟區，從 hello 來源虛擬機器 toohello 附加額外的磁碟區 hello 目標虛擬機器的內容。 SIOS DataKeeper 抽象化 hello 來源和目標本機磁碟區，並接著呈現 tooWindows Server 容錯移轉叢集與一個共用磁碟。

取得 [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/)的詳細資訊。

![圖 3：Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

_**圖 3：**Azure 中使用 SIOS DataKeeper 的 Windows Server 容錯移轉叢集組態_

> [!NOTE]
> 您不需要與某些 DBMS 產品 (例如 SQL Server) 共用提供高可用性的磁碟。 SQL Server Alwayson 複寫 DBMS 資料和記錄檔從一個叢集節點 toohello 本機磁碟上的另一個叢集節點的 hello 本機磁碟上。 在此情況下，Windows hello 的叢集設定不需要共用的磁碟。
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Azure 中的名稱解析
hello Azure 雲端平台不提供 hello 選項 tooconfigure 虛擬 IP 位址，例如浮點的 IP 位址。 您需要的替代方案 tooset 的虛擬 IP 位址 tooreach hello 叢集資源 hello 雲端中。
Azure hello Azure 負載平衡器服務中有內部負載平衡器。 與 hello 內部負載平衡器，用戶端會透過 hello 叢集虛擬 IP 位址連線 hello 叢集。
您需要包含 hello 叢集節點的 hello 資源群組中的 toodeploy hello 內部負載平衡器。 然後，設定所有必要的通訊埠與 hello 探查 hello 內部負載平衡器的連接埠轉送規則。
hello 用戶端可以透過 hello 虛擬主機名稱連接。 hello DNS 伺服器解析 hello 叢集 IP 位址，與 hello 內部負載平衡器控點連接埠轉送 toohello hello 叢集作用中的節點。

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Azure 基礎結構即服務 (IaaS) 中的 SAP NetWeaver 高可用性
tooachieve SAP 應用程式的高可用性，例如 SAP 軟體元件，您需要下列元件 tooprotect hello:

* SAP 應用程式伺服器執行個體
* SAP ASCS/SCS 執行個體
* DBMS 伺服器

如需在高可用性案例中保護 SAP 元件的詳細資訊，請參閱 [SAP NetWeaverAzure 的虛擬機器規劃和實作][planning-guide-11]。

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> 高可用性的 SAP 應用程式伺服器
您通常不需要特定的高可用性解決方案 hello SAP 應用程式伺服器和對話方塊執行個體。 您可以透過備援來達成高可用性，而且您會在 Azure 虛擬機器之不同的執行個體中，設定多個對話方塊執行個體。 您應該至少要有兩個 SAP 應用程式執行個體安裝在 Azure 虛擬機器的兩個執行個體中。

![圖 4：高可用性的 SAP 應用程式伺服器][sap-ha-guide-figure-2000]

_**圖 4：**高可用性的 SAP 應用程式伺服器_

您必須將所有虛擬機器主機中的 SAP 應用程式伺服器執行個體 hello 相同 Azure 可用性設定組。 Azure 可用性設定組可確保：

* 所有虛擬機器都屬於 hello 相同升級網域。 升級網域，例如，可確保 hello 虛擬機器不在 hello 更新相同計劃性的維護停機期間的時間。
* 所有虛擬機器都屬於 hello 相同容錯網域。 「 故障 」 網域，例如，確保已部署虛擬機器，以便任何單一失敗點會影響 hello 的所有虛擬機器的可用性。

深入了解如何太[管理虛擬機器可用性 hello][virtual-machines-manage-availability]。

Unmanaged 僅限磁碟： hello Azure 儲存體帳戶是潛在的單一失敗點，因為它是重要的 toohave 至少兩個 Azure 儲存體帳戶，分兩個以上的虛擬機器。 在理想的安裝程式中執行 SAP dialog 執行個體的每部虛擬機器的 hello 磁碟將部署於不同的儲存體帳戶。

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> 高可用性的 SAP ASCS/SCS 執行個體
圖 5 是高可用性的 SAP ASCS/SCS 執行個體範例。

![圖 5：高可用性的 SAP ASCS/SCS 執行個體][sap-ha-guide-figure-2001]

_**圖 5：**高可用性的 SAP ASCS/SCS 執行個體_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> 在 Azuer 中使用 Windows Server 容錯移轉叢集的 SAP ASCS/SCS 執行個體高可用性
比較 toobare 金屬或私人雲端部署，Azure 虛擬機器需要額外的步驟 tooconfigure Windows Server 容錯移轉叢集。 toobuild Windows 容錯移轉叢集，您需要共用的叢集磁碟、 幾個 IP 位址，數個虛擬主機名稱，以及 Azure 內部負載平衡器叢集化 SAP ASCS/SCS 執行個體。 我們將在討論 hello 文章稍後的更多詳細資料。

![圖 6：Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態][sap-ha-guide-figure-1002]

_**圖 6：**Azure 中使用 SIOS DataKeeper 之 SAP ASCS/SCS 的 Windows Server 容錯移轉叢集組態_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> 高可用性的 DBMS 執行個體
hello DBMS 也是 SAP 系統中的單一窗口。 您需要 tooprotect 它使用高可用性解決方案。 圖 7 顯示在 Azure 中的 SQL Server Alwayson 高可用性解決方案，Windows Server 容錯移轉叢集和 hello Azure 內部負載平衡器。 SQL Server Always On 會使用自己的 DBMS 複寫來複寫 DBMS 資料和記錄檔。 在此情況下，您不需要叢集共用的磁碟，這可簡化 hello 整個安裝程式。

![圖 7：高可用性的 SAP DBMS，使用 SQL Server Always On 的範例][sap-ha-guide-figure-2003]

_**圖 7：**高可用性的 SAP DBMS，使用 SQL Server Always On 的範例_

如需在 Azure 中的 SQL Server 叢集所使用 hello Azure Resource Manager 部署模型的詳細資訊，請參閱下列文章：

* [用 Resource Manager 在 Azure 虛擬機器中設定 Always On 可用性群組][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [在 Azure 中為 Always On 可用性群組設訂內部負載平衡器][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> 端對端高可用性部署案例

### <a name="deployment-scenario-using-architectural-template-1"></a>使用架構範本 1 的部署案例

圖 8 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。 此案例如下所示設定︰

- Hello SAP ASCS/SCS 執行個體使用一個專用的叢集。
- Hello DBMS 執行個體使用一個專用的叢集。
- SAP 應用程式伺服器執行個體會部署在他們自己專用的 VM。

![圖 8：SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集][sap-ha-guide-figure-2004]

_**圖 8：**SAP 高可用性架構範本 1，包含用於 ASCS/SCS 和用於 DBMS 執行個體的專用叢集_

### <a name="deployment-scenario-using-architectural-template-2"></a>使用架構範本 2 的部署案例

圖 9 顯示**一個** SAP 系統在 Azure 中 SAP NetWeaver 高可用性架構的範例。 此案例如下所示設定︰

- 一個專用的叢集用於**兩者**hello SAP ASCS/SCS 執行個體，並且 hello DBMS。
- SAP 應用程式伺服器執行個體會部署在自己專用的 VM。

![圖 9：SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集][sap-ha-guide-figure-2005]

_**圖 9：**SAP 高可用性架構範本 2，包含用於 ASCS/SCS 的專用叢集和用於 DBMS 的專用叢集_

### <a name="deployment-scenario-using-architectural-template-3"></a>使用架構範本 3 的部署案例

圖 10 顯示**兩個** SAP 系統與 &lt;SID1&gt; 和 &lt;SID2&gt;，在 Azure 中 SAP NetWeaver 高可用性架構的範例。 此案例如下所示設定︰

- 一個專用的叢集用於**兩者**hello SAP ASCS/SCS SID1 執行個體*和*hello SAP ASCS/SCS SID2 執行個體 （一個叢集）。
- 一個專用的叢集用於 DBMS SID1，另一個專用的叢集用於 DBMS SID2 (兩個叢集)。
- Hello SID1 的 SAP 系統的 SAP 應用程式伺服器執行個體都有自己專用的 Vm。
- Hello SID2 的 SAP 系統的 SAP 應用程式伺服器執行個體都有自己專用的 Vm。

![圖 10：SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集][sap-ha-guide-figure-6003]

_**圖 10：**SAP 高可用性架構範本 3，包含用於不同 ASCS/SCS 執行個體的專用叢集_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>準備 hello 基礎結構

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Hello 基礎結構做好架構範本 1
適用於 SAP 的 Azure Resource Manager 範本有助於簡化部署所需的資源。

hello 三層式範本 Azure 資源管理員中也會支援這類高可用性案例架構的範本 1，有兩個叢集。 每個叢集是適用於 SAP ASCS/SCS 和 DBMS 的 SAP 單一失敗點。

以下是您可以在其中取得 hello 範例案例，我們在本文中說明的 Azure 資源管理員範本：

* [Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [使用受控磁碟的 Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md) \(英文\)  
* [自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [使用受控磁碟的自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md) \(英文\)

tooprepare hello 基礎結構架構範本 1:

- 在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **SYSTEMAVAILABILITY**方塊中，選取**HA**。

  ![圖 11：設定 SAP 高可用性 Azure Resource Manager 參數][sap-ha-guide-figure-3000]

_**圖 11：**設定 SAP 高可用性 Azure Resource Manager 參數_


  hello 範本會建立：

  * **虛擬機器**：
    * SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-di-<*Number*>
    * ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-ascs-<*Number*>
    * DBMS 叢集：<*SAPSystemSID*>-db-<*Number*>

  * **所有虛擬機器的網路卡，包含關聯的 IP 位址**：
    * <*SAPSystemSID*>-nic-di-<*Number*>
    * <*SAPSystemSID*>-nic-ascs-<*Number*>
    * <*SAPSystemSID*>-nic-db-<*Number*>

  * **Azure 儲存體帳戶 (僅限非受控磁碟)**

  * 下列項目的**可用性群組**：
    * SAP 應用程式伺服器虛擬機器︰<*SAPSystemSID*>-avset-di
    * SAP ASCS/SCS 叢集虛擬機器︰<*SAPSystemSID*>-avset-ascs
    * DBMS 叢集虛擬機器︰<*SAPSystemSID*>-avset-db

  * **Azure 內部負載平衡器**：
    * 與 hello ASCS/SCS 執行個體和 IP 位址的所有連接埠 <*SAPSystemSID*>-lb 集 ascs
    * 與 hello 的 SQL Server DBMS 和 IP 位址的所有連接埠 <*SAPSystemSID*>-lb 集 db

  * **網路安全性群組**：<*SAPSystemSID*>-nsg-ascs-0  
    * 開啟外部的遠端桌面通訊協定 (RDP) 連接埠 toohello 與 <*SAPSystemSID*>-ascs-0 的虛擬機器

> [!NOTE]
> Hello 網路卡和 Azure 內部負載平衡器的所有 IP 位址都都**動態**預設。 它們也變更**靜態**IP 位址。 我們將描述如何 toodo 這 hello 文件中的更新版本。
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>使用公司網路連線能力 （跨內部部署） toouse 在生產環境中部署虛擬機器
針對生產環境 SAP 系統，使用 Azure 站對站 VPN 或 Azure ExpressRoute，部署具有 [公司網路連線能力 (跨單位)][planning-guide-2.2] 的 Azure 虛擬機器。

> [!NOTE]
> 您可以使用您的 Azure 虛擬網路執行個體。 hello 虛擬網路和子網路已建立並備妥。
>
>

1.  在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **NEWOREXISTINGSUBNET**方塊中，選取**現有**。
2.  在 hello **SUBNETID**方塊中，加入您備妥的 Azure 網路 SubnetID 您計劃 toodeploy Azure 虛擬機器的 hello 完整字串。
3.  tooget 一份所有 Azure 網路子網路中，執行這個 PowerShell 命令：

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  hello**識別碼**欄位會顯示 hello **SUBNETID**。
4. tooget 所有清單**SUBNETID**值，執行這個 PowerShell 命令：

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  hello **SUBNETID**看起來像這樣：

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> 用於測試和示範的 SAP 執行個體僅限部署雲端
您可以在僅限雲端部署模型中部署您的高可用性 SAP 系統。 這種部署主要對於示範和測試的使用案例相當有用。 但不適用於生產環境使用案例。

- 在 Azure 入口網站上 hello hello**參數**刀鋒視窗中的，在 hello **NEWOREXISTINGSUBNET**方塊中，選取**新**。 保留 hello **SUBNETID**欄位空白。

  hello SAP Azure Resource Manager 範本會自動建立 hello Azure 虛擬網路和子網路。

> [!NOTE]
> 您也需要 toodeploy 至少一個專用的虛擬機器的 Active Directory 和 DNS 在 hello 相同 Azure 虛擬網路的執行個體。 hello 範本並不會建立這些虛擬機器。
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Hello 基礎結構做好架構範本 2

針對 SAP toohelp 簡化架構範本 2 SAP 部署必要的基礎結構資源，您可以使用此 Azure Resource Manager 範本。

您可以在這裡取得此部署案例的 Azure Resource Manager 範本：

* [Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [使用受控磁碟的 Azure Marketplace 映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md) \(英文\)  
* [自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [使用受控磁碟的自訂映像](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md) \(英文\)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Hello 基礎結構做好架構範本 3

您可以準備 hello 基礎結構，並設定為 SAP**多重 SID**。 例如，您可以將額外的 SAP ASCS/SCS 執行個體新增至現有的叢集組態以建立 SAP 多 SID 組態。 如需詳細資訊，請參閱[Azure 資源管理員中設定額外的 SAP ASCS/SCS 執行個體到現有的叢集組態 toocreate SAP 多 SID 組態][sap-ha-multi-sid-guide]。

如果您想 toocreate 新的多個 SID 叢集，您可以使用 hello 多重 SID [GitHub 上的快速入門範本](https://github.com/Azure/azure-quickstart-templates)。
toocreate 新的多個 SID 叢集，您需要下列三個範本 toodeploy hello:

* [ASCS/SCS 範本](#ASCS-SCS-template)
* [資料庫範本](#database-template)
* [應用程式伺服器範本](#application-servers-template)

hello 以下幾節有更多詳細 hello 範本和您需要 tooprovide hello 範本中的 hello 參數。

#### <a name="ASCS-SCS-template"></a> ASCS/SCS 範本

hello ASCS/SCS 範本部署，您可以使用 toocreate 裝載多個 ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集的兩部虛擬機器。

hello ASCS/SCS 多重 SID 範本，在 hello tooset [ASCS/SCS 多重 SID 範本][ sap-templates-3-tier-multisid-xscs-marketplace-image]或[ASCS/SCS 多重 SID 範本使用受管理磁碟][ sap-templates-3-tier-multisid-xscs-marketplace-image-md]，輸入 hello 下列參數的值：

  - **資源前置詞**。  設定 hello 資源前置詞，也就是使用的 tooprefix hello 部署期間建立的所有資源。 Hello 資源不屬於 tooonly 一個 SAP 系統，因為 hello 資源 hello 前置詞不是 hello 一個 SAP 系統的 SID。  hello 首碼必須介於**三到六個字元**。
  - **堆疊類型**。 選取 hello SAP 系統的 hello 堆疊型的別。 根據 hello 堆疊型別，Azure 負載平衡器具有一個 （ABAP 或 Java 只） 或兩個 (ABAP + Java) 私用每個 IP 位址的 SAP 系統。
  -  **OS 類型**。 選取 hello 作業系統 hello 虛擬機器。
  -  **SAP 系統計數**。 選取 hello 數目要 tooinstall 此叢集中的 SAP 系統。
  -  **系統可用性**。 選取 **HA**。
  -  **管理員使用者名稱和管理員密碼**。 建立新的使用者可以使用的 toosign toohello 機器中。
  -  **新的或現有的子網路**。 設定應該建立新的虛擬網路和子網路，還是應該使用現有子網路。 如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取**現有**。
  -  **子網路識別碼**。設定虛擬機器應該連接 hello 子網路 toowhich hello hello 識別碼。 選取您的虛擬私人網路 (VPN) 或 ExpressRoute 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。 hello 識別碼通常看起來像這樣：

   /subscriptions/<*訂用帳戶識別碼*>/resourceGroups/<*資源群組名稱*>/providers/Microsoft.Network/virtualNetworks/<*虛擬網路名稱*>/subnets/<*子網路名稱*>

hello 範本部署一個 Azure 負載平衡器執行個體，可支援多個 SAP 系統。

- hello ASCS 執行個體的執行個體號碼 00，10，20 設定...
- hello SCS 執行個體的執行個體號碼 01，11，21 設定...
- hello ASCS Enqueue 複寫伺服器 （端） (僅 Linux) 執行個體的執行個體號碼 02，12，22 設定...
- hello SCS 端 (只有 Linux) 執行個體設定的執行個體號碼 03，13，23...

hello 負載平衡器包含 1 (適用於 Linux 的 2) VIP(s)、 ASCS/SCS 1 x VIP 和 1 x VIP 端 (只有 Linux)。

hello 下列清單包含所有的負載平衡的規則 （其中 x 是 hello 數目 hello SAP 系統，例如 1、 2、 3 …）：
- 每個 SAP 系統的 Windows 特定連接埠︰445、5985
- ASCS 連接埠 (執行個體數目 x0)︰32x0、36x0、39x0、81x0、5x013、5x014、5x016
- SCS 連接埠 (執行個體數目 x1)︰32x1、33x1、39x1、81x1、5x113、5x114、5x116
- Linux 上的 ASCS ERS 連接埠 (執行個體數目 x2)︰33x2、5x213、5x214、5x216
- Linux 上的 SCS ERS 連接埠 (執行個體數目 x3)︰33x3、5x313、5x314、5x316

hello 負載平衡器設定的 toouse hello 遵循 （其中 x 是 hello 數目 hello SAP 系統，例如 1、 2、 3 …） 的探查連接埠：
- ASCS/SCS 內部負載平衡器探查連接埠︰620x0
- ERS 內部負載平衡器探查連接埠 (僅 Linux)︰621x2

#### <a name="database-template"></a> 資料庫範本

hello 資料庫範本部署一或兩部虛擬機器，您可以使用 tooinstall hello 一個 SAP 系統的關聯式資料庫管理系統 (RDBMS)。 例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要 toodeploy 此範本五次。

hello 資料庫多 SID 範本，在 hello tooset[資料庫多 SID 範本][ sap-templates-3-tier-multisid-db-marketplace-image]或[資料庫多 SID 範本使用受管理磁碟][ sap-templates-3-tier-multisid-db-marketplace-image-md]，輸入 hello 下列參數的值：

  -  **SAP 系統識別碼**。輸入您想要 tooinstall 的 SAP 系統 hello hello SAP 系統識別碼。 hello 識別碼將用於做為前置詞已部署的 hello 資源。
  -  **OS 類型**。 選取 hello 作業系統 hello 虛擬機器。
  -  **Dbtype**。 選取 hello 類型要 tooinstall hello 叢集上的 hello 資料庫。 選取**SQL**如果您想 tooinstall Microsoft SQL Server。 選取**HANA**如果您打算 tooinstall SAP HANA hello 虛擬機器。 請確定 tooselect hello 正確運作的系統類型： 選取**Windows** SQL，和 hana 選取 Linux 散發套件。 hello Azure 負載平衡器的虛擬機器必須連接的 toohello 設定 toosupport hello 選取資料庫類型：
    * **SQL**。 hello 負載平衡器將負載平衡連接埠 1433年。 請確定 toouse for SQL Server Alwayson 安裝程式的這個連接埠。
    * **HANA**。 hello 負載平衡器將負載平衡連接埠 35015 和 35017。 請確定 tooinstall SAP HANA 與執行個體號碼**50**。
    hello 負載平衡器會使用探查連接埠 62550。
  -  **SAP 系統大小**。 會提供設定的新系統的 SAPS hello 的 hello 次數。 如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。
  -  **系統可用性**。 選取 **HA**。
  -  **管理員使用者名稱和管理員密碼**。 建立新的使用者可以使用的 toosign toohello 機器中。
  -  **子網路識別碼**。輸入 hello 識別碼 hello hello hello ASCS/SCS 範本，請在部署您使用的子網路或建立 hello 子網路識別碼 hello hello ASCS/SCS 範本部署的一部分。

#### <a name="application-servers-template"></a> 應用程式伺服器範本

hello 應用程式伺服器範本部署可以做一個 SAP 系統的 SAP 應用程式伺服器執行個體的兩個或多個虛擬機器。 例如，如果您部署五個 SAP 系統的 ASCS/SCS 範本，您需要 toodeploy 此範本五次。

hello 應用程式伺服器多 SID 範本中，在 hello tooset[應用程式伺服器多 SID 範本][ sap-templates-3-tier-multisid-apps-marketplace-image]或[使用受管理磁碟應用程式伺服器的多重SID範本][ sap-templates-3-tier-multisid-apps-marketplace-image-md]，輸入 hello 下列參數的值：

  -  **SAP 系統識別碼**。輸入您想要 tooinstall 的 SAP 系統 hello hello SAP 系統識別碼。 hello 識別碼將用於做為前置詞已部署的 hello 資源。
  -  **OS 類型**。 選取 hello 作業系統 hello 虛擬機器。
  -  **SAP 系統大小**。 將提供的 SAPS hello 新系統的 hello 數目。 如果您不確定需要多少的 SAPS hello 系統，請要求您 SAP 技術合作夥伴或系統整合者。
  -  **系統可用性**。 選取 **HA**。
  -  **管理員使用者名稱和管理員密碼**。 建立新的使用者可以使用的 toosign toohello 機器中。
  -  **子網路識別碼**。輸入 hello 識別碼 hello hello hello ASCS/SCS 範本，請在部署您使用的子網路或建立 hello 子網路識別碼 hello hello ASCS/SCS 範本部署的一部分。


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure 虛擬網路
在本例中，hello hello Azure 虛擬網路位址空間會是 10.0.0.0/16。 有一個名為 **Subnet**、網址範圍為 10.0.0.0/24 的子網路。 所有虛擬機器和內部負載平衡器會部署在此虛擬網路中。

> [!IMPORTANT]
> 不進行任何變更 toohello hello 客體作業系統內的網路設定。 包括 IP 位址、DNS 伺服器和子網路。 在 Azure 中設定所有網路設定。 hello 動態主機設定通訊協定 (DHCP) 服務會傳播您的設定。
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> DNS IP 位址

tooset hello 所需的 DNS IP 位址，執行下列步驟 hello。

1.  Hello hello 上的 Azure 入口網站中**DNS 伺服器**刀鋒視窗中，請確定您的虛擬網路**DNS 伺服器**選項設定得**自訂 DNS**。
2.  選取您根據的網路您擁有 hello 類型的設定。 如需詳細資訊，請參閱下列資源的 hello:
    * [公司網路連線 （跨內部部署）][planning-guide-2.2]： 新增 hello hello 在內部部署 DNS 伺服器 IP 位址。  
    您可以擴充在內部部署 DNS 伺服器 toohello 虛擬機器會在 Azure 中執行。 在這種情況下，您可以加入 hello IP 位址的 hello Azure 虛擬機器執行 hello DNS 服務。
    * [僅限雲端部署][planning-guide-2.1]： 部署額外的虛擬機器在 hello 做為 DNS 伺服器的相同虛擬網路執行個體。 新增 hello Azure hello IP 位址設定好 toorun DNS 服務的虛擬機器。

    ![圖 12：設定 Azure 虛擬網路的 DNS 伺服器][sap-ha-guide-figure-3001]

    _**圖 12：**設定 Azure 虛擬網路的 DNS 伺服器_

  > [!NOTE]
  > 如果您變更 hello hello DNS 伺服器 IP 位址，您需要 toorestart hello Azure 虛擬機器 tooapply hello 變更，將傳播 hello 新 DNS 伺服器。
  >
  >

在本例中，hello DNS 服務已安裝，並設定這些 Windows 虛擬機器：

| 虛擬機器角色 | 虛擬機器主機名稱 | 網路卡名稱 | 靜態 IP 位址 |
| --- | --- | --- | --- |
| 第一部 DNS 伺服器 |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| 第二部 DNS 伺服器 |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>主機名稱和 hello SAP ASCS/SCS 叢集執行個體和 DBMS 叢集執行個體的靜態 IP 位址

對於內部部署，您需要下列保留的主機名稱和 IP 位址：

| 虛擬主機名稱角色 | 虛擬主機名稱 | 虛擬靜態 IP 位址 |
| --- | --- | --- |
| SAP ASCS/SCS 第一個叢集虛擬主機名稱 (用於叢集管理) |pr1-ascs-vir |10.0.0.42 |
| SAP ASCS/SCS 執行個體虛擬主機名稱 |pr1-ascs-sap |10.0.0.43 |
| SAP DBMS 第二個叢集虛擬主機名稱 (叢集管理) |pr1-dbms-vir |10.0.0.32 |

當您建立 hello 叢集時，建立 hello 虛擬主機名稱**pr1-ascs-虛擬**和**pr1-dbms 層虛擬**和 hello 相關聯的管理 hello 叢集本身的 IP 位址。 如需有關資訊 toodo，請參閱[收集在叢集組態中的叢集節點][sap-ha-guide-8.12.1]。

您可以手動建立 hello 其他兩個的虛擬主機名稱， **pr1 ascs sap**和**pr1 dbms sap**，以及相關聯的 hello hello DNS 伺服器上的 IP 位址。 hello 叢集的 SAP ASCS/SCS 執行個體和叢集的 hello DBMS 執行個體使用這些資源。 如需有關資訊 toodo，請參閱[建立叢集的 SAP ASCS/SCS 執行個體的虛擬主機名稱][sap-ha-guide-9.1.1]。

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>設定靜態 IP 位址的 hello SAP 虛擬機器
在叢集中部署 hello 虛擬機器 toouse 之後，您需要 tooset 靜態 IP 位址的所有虛擬機器。 Hello Azure 虛擬網路組態中，而不是在 hello 客體作業系統，請執行這項操作。

1.  在 hello Azure 入口網站，選取 **資源群組** > **網路卡** > **設定** > **IP 位址**.
2.  在 hello **IP 位址**刀鋒視窗下**指派**，選取**靜態**。 在 hello **IP 位址**方塊中，輸入您想 toouse hello IP 位址。

  > [!NOTE]
  > 如果您變更 hello hello 網路卡的 IP 位址，您需要 toorestart hello Azure 虛擬機器 tooapply hello 變更。  
  >
  >

  ![圖 13： 設定每個虛擬機器的 hello 網路卡的靜態 IP 位址][sap-ha-guide-figure-3002]

  _**圖 13:**設定 hello 的每個虛擬機器的網路卡的靜態 IP 位址_

  也就是說，重複此步驟中的所有網路介面的所有虛擬機器，包括您想 toouse，為您的 Active Directory/DNS 服務的虛擬機器。

在我們的範例中，有下列虛擬機器和靜態 IP 位址：

| 虛擬機器角色 | 虛擬機器主機名稱 | 網路卡名稱 | 靜態 IP 位址 |
| --- | --- | --- | --- |
| 第一部 SAP 應用程式伺服器執行個體 |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| 第二部 SAP 應用程式伺服器執行個體 |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| 最後一部 SAP 應用程式伺服器執行個體 |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| ASCS/SCS 執行個體的第一個叢集節點 |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| ASCS/SCS 執行個體的第二個叢集節點 |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| DBMS 執行個體的第一個叢集節點 |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| DBMS 執行個體的第二個叢集節點 |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Hello Azure 內部負載平衡器設定的靜態 IP 位址

hello SAP 的 Azure Resource Manager 範本會建立用於 hello SAP ASCS/SCS 執行個體的叢集和 hello DBMS 叢集 Azure 內部負載平衡器。

> [!IMPORTANT]
> hello hello hello SAP ASCS/SCS 是虛擬的主機名稱的 IP 位址 hello 相同作為 hello hello SAP ASCS/SCS 內部負載平衡器 IP 位址： **pr1-lb 集 ascs**。
> hello hello dbms hello 虛擬名稱的 IP 位址 hello 相同作為 hello hello DBMS 內部負載平衡器 IP 位址： **pr1 lb dbms**。
>
>

tooset hello Azure 內部的靜態 IP 位址的負載平衡器：

1.  hello 初始的部署設定 hello 內部負載平衡器 IP 位址太**動態**。 Hello hello 上的 Azure 入口網站中**IP 位址**刀鋒視窗底下**指派**，選取**靜態**。
2.  Hello hello 內部負載平衡器的 IP 位址設定**pr1-lb 集 ascs** hello hello SAP ASCS/SCS 執行個體的虛擬主機名稱 toohello IP 位址。
3.  Hello hello 內部負載平衡器的 IP 位址設定**pr1 lb dbms** hello hello DBMS 執行個體的虛擬主機名稱 toohello IP 位址。

  ![圖 14: Hello hello SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址][sap-ha-guide-figure-3003]

  _**圖 14:** hello hello SAP ASCS/SCS 執行個體的內部負載平衡器設定靜態 IP 位址_

在我們的範例中，有兩個 Azure 內部負載平衡器具備這些靜態 IP 位址：

| Azure 內部負載平衡器角色 | Azure 內部負載平衡器名稱 | 靜態 IP 位址 |
| --- | --- | --- |
| SAP ASCS/SCS 執行個體內部負載平衡器 |pr1-lb-ascs |10.0.0.43 |
| SAP DBMS 內部負載平衡器 |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則

hello SAP 的 Azure Resource Manager 範本會建立您所需要的 hello 連接埠：
* 具有 hello 預設執行個體號碼的 ABAP ASCS 執行個體， **00**
* Java SCS 執行個體，與 hello 預設執行個體號碼**01**

當您安裝 SAP ASCS/SCS 執行個體時，您必須使用 hello 預設執行個體號碼**00**的 ABAP ASCS 執行個體和 hello 預設執行個體號碼**01** Java SCS 執行個體。

接下來，建立必要的內部負載平衡 hello SAP NetWeaver 連接埠的端點。

toocreate 所需內部負載平衡的端點，首先，建立這些負載平衡 hello SAP NetWeaver ABAP ASCS 連接埠的端點：

| 服務/負載平衡規則名稱 | 預設連接埠號碼 | (執行個體號碼為 00 的 ASCS 執行個體) (ERS 為 10) 的具體連接埠 |
| --- | --- | --- |
| 加入佇列伺服器 / *lbrule3200* |32<*InstanceNumber*> |3200 |
| ABAP 訊息伺服器 / *lbrule3600* |36<*InstanceNumber*> |3600 |
| 內部 ABAP 訊息 / *lbrule3900* |39<*InstanceNumber*> |3900 |
| 訊息伺服器 HTTP / *Lbrule8100* |81<*InstanceNumber*> |8100 |
| SAP 啟動服務 ASCS HTTP / *Lbrule50013* |5<*InstanceNumber*>13 |50013 |
| SAP 啟動服務 ASCS HTTPS / *Lbrule50014* |5<*InstanceNumber*>14 |50014 |
| 加入佇列複寫 / *Lbrule50016* |5<*InstanceNumber*>16 |50016 |
| SAP 啟動服務 ERS HTTP *Lbrule51013* |5<*InstanceNumber*>13 |51013 |
| SAP 啟動服務 ERS HTTP *Lbrule51014* |5<*InstanceNumber*>14 |51014 |
| Win RM *Lbrule5985* | |5985 |
| 檔案共用 *Lbrule445* | |445 |

_**表 1:**的連接埠號碼的 hello SAP NetWeaver ABAP ASCS 執行個體_

然後，建立這些負載平衡 hello SAP NetWeaver Java SCS 連接埠的端點：

| 服務/負載平衡規則名稱 | 預設連接埠號碼 | (執行個體號碼為 01 的 SCS 執行個體) (ERS 為 11) 的具體連接埠 |
| --- | --- | --- |
| 加入佇列伺服器 / *lbrule3201* |32<*InstanceNumber*> |3201 |
| 閘道伺服器 / *lbrule3301* |33<*InstanceNumber*> |3301 |
| Java 訊息伺服器 / *lbrule3900* |39<*InstanceNumber*> |3901 |
| 訊息伺服器 HTTP / *Lbrule8101* |81<*InstanceNumber*> |8101 |
| SAP 啟動服務 SCS HTTP / *Lbrule50113* |5<*InstanceNumber*>13 |50113 |
| SAP 啟動服務 SCS HTTPS / *Lbrule50114* |5<*InstanceNumber*>14 |50114 |
| 加入佇列複寫 / *Lbrule50116* |5<*InstanceNumber*>16 |50116 |
| SAP 啟動服務 ERS HTTP *Lbrule51113* |5<*InstanceNumber*>13 |51113 |
| SAP 啟動服務 ERS HTTP *Lbrule51114* |5<*InstanceNumber*>14 |51114 |
| Win RM *Lbrule5985* | |5985 |
| 檔案共用 *Lbrule445* | |445 |

_**表 2:**的連接埠號碼的 hello SAP NetWeaver Java SCS 執行個體_

![圖 15： 預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-figure-3004]

_**圖 15:**預設 ASCS/SCS 負載平衡 hello Azure 內部負載平衡器規則_

Hello hello 負載平衡器的 IP 位址設定**pr1 lb dbms** hello hello DBMS 執行個體的虛擬主機名稱 toohello IP 位址。

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則

如果您想 toouse 不同數字 hello SAP ASCS 或 SCS 執行個體時，您必須變更其連接埠的 hello 名稱和值的預設值。

1.  在 hello Azure 入口網站，選取   **<* SID*>-lb 集 ascs 負載平衡器 * * >**負載平衡規則**。
2.  所有的負載平衡規則屬於 toohello SAP ASCS 或 SCS 執行個體，變更這些值：

  * 名稱
  * 連接埠
  * 後端連接埠

  例如，如果您想 toochange hello 預設 ASCS 執行個體號碼從 00 too31，您需要 toomake hello 變更如表 1 中所列的所有連接埠。

  以下是連接埠 *lbrule3200*的更新範例。

  ![圖 16： 變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-figure-3005]

  _**圖 16:**變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>新增 Windows 虛擬機器 toohello 網域

指派靜態 IP 位址 toohello 虛擬機器之後，新增 hello 虛擬機器 toohello 網域。

![圖 17： 新增虛擬機器 tooa 網域][sap-ha-guide-figure-3006]

_**圖 17:**新增虛擬機器 tooa 網域_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Hello SAP ASCS/SCS 執行個體的兩個叢集節點上新增登錄項目

Azure 負載平衡器已關閉連線時 hello 連線閒置一段時間的時間 （閒置逾時） 的內部負載平衡器。 在對話方塊執行個體的開啟連接 toohello SAP 加入佇列中的 SAP 工作流程處理一旦 hello 第一個加入佇列/清除佇列要求需求 toobe 傳送。 這些連線通常會保持已建立 hello 工作處理程序才能或 hello 佇列處理序重新啟動。 不過，如果 hello 連線已經閒置一段時間，hello Azure 內部負載平衡器關閉 hello 連線。 這不是問題，因為 hello SAP 工作處理序重新建立 hello 連線 toohello 加入佇列的程序，如果不存在。 這些活動會記載於 hello 開發人員追蹤 SAP 程序，但是他們建立大量額外的內容中這些追蹤。 它是個不錯的主意 toochange hello TCP/IP`KeepAliveTime`和`KeepAliveInterval`兩個叢集節點上。 結合這些變更的 hello TCP/IP 參數搭配 hello 本文稍後所述的 SAP 設定檔參數。

tooadd hello SAP ASCS/SCS 執行個體的兩個叢集節點上的登錄項目首先，新增這些 Windows 登錄項目在這兩個 Windows 叢集節點上的 SAP ASCS/SCS 中：

| Path | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| 變數名稱 |`KeepAliveTime` |
| 變數類型 |REG_DWORD (十進位) |
| 值 |120000 |
| 連結 toodocumentation |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**表 3:**變更 hello 第一個 TCP/IP 參數_

然後，在 SAP ASCS/SCS 的兩個 Windows 叢集節點上都新增下列 Windows 登錄項目：

| 路徑 | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| 變數名稱 |`KeepAliveInterval` |
| 變數類型 |REG_DWORD (十進位) |
| 值 |120000 |
| 連結 toodocumentation |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**表 4:**變更 hello 第二個 TCP/IP 參數_

**tooapply hello 變更，重新啟動這兩個叢集節點**。

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> 設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集

設定 SAP ASCS/SCS 執行個體的 Windows Server 容錯移轉叢集包含下列工作︰

- 在叢集組態中的收集 hello 叢集節點
- 設定叢集檔案共用見證

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>收集在叢集組態中的 hello 叢集節點

1.  在 hello 新增角色及功能精靈，加入容錯移轉叢集 tooboth 叢集節點。
2.  使用容錯移轉叢集管理員設定 hello 容錯移轉叢集。 在 [容錯移轉叢集管理員] 中，選取**建立叢集**，然後再加入 hello 第一個叢集，節點 a 只 hello 名稱不要在新增 hello 第二個節點。您可以在稍後步驟中加入 hello 第二個節點。

  ![圖 18： 新增 hello 伺服器或虛擬機器名稱的第一個叢集節點 hello][sap-ha-guide-figure-3007]

  _**圖 18:**新增 hello 伺服器或虛擬機器名稱的第一個叢集節點 hello_

3.  輸入 hello 叢集網路名稱 （虛擬主機名稱） hello。

  ![圖 19： 輸入 hello 叢集名稱][sap-ha-guide-figure-3008]

  _**圖 19:**輸入 hello 叢集名稱_

4.  在您建立 hello 叢集後，執行叢集驗證測試。

  ![圖 20： 執行 hello 叢集驗證檢查][sap-ha-guide-figure-3009]

  _**圖 20:**執行 hello 叢集驗證檢查_

  您可以忽略這個時候 hello 程序中的磁碟的任何警告。 您要加入的檔案共用見證和 hello SIOS 共用磁碟更新版本。 在這個階段，您不需要 tooworry 具有仲裁。

  ![圖 21：找不到仲裁磁碟][sap-ha-guide-figure-3010]

  _**圖 21：**_

  ![圖 22：核心叢集資源需要新的 IP 位址][sap-ha-guide-figure-3011]

  _**圖 22：**核心叢集資源需要新的 IP 位址_

5.  變更 hello hello 核心叢集服務的 IP 位址。 hello 叢集之前，無法啟動變更 hello IP 位址的 hello 核心叢集服務，因為 hello hello 伺服器 IP 位址指向 tooone 的 hello 虛擬機器節點。 這麼做在 hello**屬性**hello 核心叢集服務的 IP 資源頁面。

  例如，我們需要 tooassign IP 位址 (在本例中， **10.0.0.42**) hello 叢集虛擬主機名稱**pr1-ascs-虛擬**。

  ![圖 23: Hello 內容 對話方塊中變更 hello IP 位址][sap-ha-guide-figure-3012]

  _**圖 23:**在 hello**屬性**對話方塊中，變更 hello IP 位址_

  ![圖 24： 已保留供 hello 叢集的 hello IP 位址指派給][sap-ha-guide-figure-3013]

  _**圖 24:** hello hello 叢集保留的 IP 位址指派給_

6.  將 hello 叢集虛擬主機名稱上線。

  ![圖 25： 叢集的核心服務已啟動且正在執行，並以 hello 更正 IP 位址][sap-ha-guide-figure-3014]

  _**圖 25:**叢集的核心服務已啟動且正在執行且與 hello 更正 IP 位址_

7.  新增第二個叢集節點 hello。

  Hello 核心叢集服務已啟動且正在執行，您可以新增 hello 第二個叢集節點。

  ![圖 26： 新增 hello 第二個叢集節點][sap-ha-guide-figure-3015]

  _**圖 26:**新增 hello 第二個叢集節點_

8.  輸入 hello 第二個叢集節點主機的名稱。

  ![圖 27： 輸入 hello 第二個叢集節點主機名稱][sap-ha-guide-figure-3016]

  _**圖 27:**輸入 hello 第二個叢集節點主機名稱_

  > [!IMPORTANT]
  > 務必要是屬於該 hello**新增所有合格的存放裝置 toohello 叢集** 核取方塊**不**選取。  
  >
  >

  ![圖 28： 未選取 hello 核取方塊][sap-ha-guide-figure-3017]

  _**圖 28:**不要**不**選取 hello 核取方塊_

  您可以忽略有關仲裁和磁碟的警告。 您將會在 hello 仲裁和共用 hello 磁碟更新版本中中, 所述[SAP ASCS/SCS 叢集共用磁碟的安裝 SIOS DataKeeper 叢集版本][sap-ha-guide-8.12.3]。

  ![圖 29： 忽略 hello 磁碟仲裁的相關警告][sap-ha-guide-figure-3018]

  _**圖 29:**忽略 hello 磁碟仲裁的相關警告_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> 設定叢集檔案共用見證

設定叢集檔案共用見證包含下列工作︰

- 建立檔案共用
- 設定容錯移轉叢集管理員 中的 hello 檔案共用見證仲裁

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> 建立檔案共用

1.  選取檔案共用見證，而不是仲裁磁碟。 SIOS DataKeeper 支援此選項。

  在本文中的 hello 範例，hello 檔案共用見證是在 Azure 中執行的 hello Active Directory/DNS 伺服器上。 hello 檔案共用見證稱為**domcontr 0**。 您會設定 VPN 連線 tooAzure （透過站對站 VPN 或 Azure ExpressRoute），因為您 Active Directory/DNS 在內部部署和服務並不適合 toorun 檔案共用見證。

  > [!NOTE]
  > 如果只在內部部署 Active Directory/DNS 服務會不 hello Active Directory/DNS 的 Windows 作業系統執行內部部署上設定您的檔案共用見證。 在 Azure 和 Active Directory DNS 內部部署中執行之叢集節點之間的網路延遲可能太大，而且會造成連線問題。 為確定 tooconfigure hello 檔案共用見證正在關閉 toohello 叢集節點的 Azure 虛擬機器上。  
  >
  >

  hello 仲裁磁碟機需要至少 1024 MB 的可用空間。 我們建議的 hello 仲裁磁碟機的可用空間的 2048 MB。

2.  新增 hello 叢集名稱物件。

  ![圖 30： 指派 hello 共用的權限 hello hello 叢集名稱物件][sap-ha-guide-figure-3019]

  _**圖 30:**指派 hello hello hello 叢集名稱物件共用的權限_

  請務必 hello 權限，包含 hello hello 叢集名稱物件的共用資料夾中的 hello 授權 toochange 資料 (在本例中， **pr1-ascs-虛擬 $**)。

3.  tooadd hello 叢集名稱物件 toohello 清單中，選取**新增**。 變更電腦物件、 新增 toothose 圖 31 所示為 hello 篩選 toocheck。

  ![圖 31： 變更 hello 物件類型 tooinclude 電腦][sap-ha-guide-figure-3020]

  _**圖 31:**變更 hello 物件類型 tooinclude 電腦_

  ![選取 [圖 32: Hello 的電腦] 核取方塊][sap-ha-guide-figure-3021]

  _**圖 32:**選取 hello**電腦**核取方塊_

4.  輸入 hello 的叢集名稱物件圖 31 中所示。 因為 hello 記錄已經建立，您可以變更 hello 權限，如圖 30 中所示。

5.  選取 hello**安全性**hello 共用，並將其設定 索引標籤是更詳細的 hello 叢集名稱物件的權限。

  ![圖 33: Hello 檔案共用的仲裁設定 hello hello 叢集名稱物件的安全性屬性][sap-ha-guide-figure-3022]

  _**圖 33:** hello 檔案共用的仲裁設定 hello hello 叢集名稱物件的安全性屬性_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>設定容錯移轉叢集管理員 中的 hello 檔案共用見證仲裁

1.  開啟 hello 設定仲裁設定精靈 」。

  ![圖 34： 啟動 hello 設定叢集仲裁設定精靈][sap-ha-guide-figure-3023]

  _**圖 34:**開始 hello 設定叢集仲裁設定精靈_

2.  在 hello**選取仲裁設定**頁面上，選取**選取 hello 仲裁見證**。

  ![圖 35：您可以選擇的仲裁組態][sap-ha-guide-figure-3024]

  _**圖 35：**您可以選擇的仲裁組態_

3.  在 hello**選取仲裁見證**頁面上，選取**設定檔案共用見證**。

  ![圖 36： 選取 hello 檔案共用見證][sap-ha-guide-figure-3025]

  _**圖 36:**選取 hello 檔案共用見證_

4.  輸入 hello UNC 路徑 toohello 檔案共用 (在本例中， \\domcontr 0\FSW)。 toosee hello 進行的變更，選取一份**下一步**。

  ![圖 37： 定義 hello hello 見證共用的檔案共用位置][sap-ha-guide-figure-3026]

  _**圖 37:**定義 hello hello 見證共用的檔案共用位置_

5.  選取 hello 您要的變更，然後選取**下一步**。 您需要 toosuccessfully 38 圖所示，重新設定 hello 叢集組態。  

  ![圖 38： 確認您已重新設定 hello 叢集][sap-ha-guide-figure-3027]

  _**圖 38:**確認您已重新設定 hello 叢集_

已成功安裝 hello Windows 容錯移轉叢集之後, 在 Azure 中進行 toosome 閾值 tooadapt 容錯移轉偵測 tooconditions toobe 需要的變更。 hello 參數 toobe 變更會記載於這篇部落格： https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/。 假設兩個 Vm，建置 hello ASCS/SCS 的 Windows 叢集設定位於 hello 相同子網路、 hello 下列參數需要變更 toobe toothese 值：
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

這些設定和已測試的客戶提供良好的折衷方案 toobe 足夠彈性 hello 某一端。 Hello 上另一方面這些設定已提供快速不足，無法容錯移轉中 SAP 軟體或節點/VM 失敗真的錯誤條件。 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Hello SAP ASCS/SCS 叢集共用磁碟的安裝 SIOS DataKeeper 叢集版本

您現在在 Azure 中有運作中的 Windows Server 容錯移轉叢集組態。 但是，tooinstall SAP ASCS/SCS 執行個體，您需要共用的磁碟資源。 您無法在 Azure 中建立您所需的 hello 共用磁碟資源。 SIOS DataKeeper 叢集版本是您可以使用 toocreate 共用磁碟資源的協力廠商解決方案。

叢集共用磁碟的 hello SAP ASCS/SCS 安裝 SIOS DataKeeper 叢集版本包含下列工作：

- 加入 hello.NET Framework 3.5
- 安裝 SIOS DataKeeper
- 設定 SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>新增 hello.NET Framework 3.5
hello Microsoft.NET Framework 3.5 不自動啟動，或是安裝在 Windows Server 2012 R2 上。 因為 SIOS DataKeeper 需要 hello.NET Framework toobe DataKeeper 上所安裝的所有節點上，您必須安裝.NET Framework 3.5 hello hello hello 叢集中的所有虛擬機器的來賓作業系統上。

有兩種方式 tooadd hello.NET Framework 3.5:

- 在 Windows 中使用 hello 新增角色及功能精靈 39 圖所示。

  ![圖 39： 使用 hello 新增角色及功能精靈來安裝.NET Framework 3.5 hello][sap-ha-guide-figure-3028]

  _**圖 39:**使用 hello 新增角色及功能精靈安裝 hello.NET Framework 3.5_

  ![圖 40： 安裝進度列，當您安裝.NET Framework 3.5 hello 使用 hello 新增角色及功能精靈][sap-ha-guide-figure-3029]

  _**圖 40:**安裝進度列，當您安裝.NET Framework 3.5 hello 使用 hello 新增角色及功能精靈_

- 使用 hello 命令列工具 dism.exe。 此類型的安裝，您必須在 hello Windows 安裝媒體上的 tooaccess hello SxS 目錄。 在提高權限的命令提示字元上，輸入：

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> 安裝 SIOS DataKeeper

Hello 叢集中的每個節點上安裝 SIOS DataKeeper 叢集版本。 toocreate 虛擬共用存放裝置與 SIOS DataKeeper 建立同步處理的鏡像，然後模擬叢集共用存放裝置。

安裝 hello SIOS 軟體之前，請建立 hello 網域使用者**DataKeeperSvc**。

> [!NOTE]
> 新增 hello **DataKeeperSvc**使用者 toohello**本機系統管理員**群組兩個叢集節點上。
>
>

tooinstall SIOS DataKeeper:

1.  這兩個叢集節點上安裝 hello SIOS 軟體。

  ![SIOS 安裝程式][sap-ha-guide-figure-3030]

  ![圖 41: Hello SIOS DataKeeper 安裝第一頁][sap-ha-guide-figure-3031]

  _**圖 41:** hello SIOS DataKeeper 安裝第一頁_

2.  在 hello 42 圖所示的對話方塊中，選取 **是**。

  ![圖 42：DataKeeper 通知將停用某個服務][sap-ha-guide-figure-3032]

  _**圖 42：**DataKeeper 通知將停用某個服務_

3.  在 hello 43 圖所示的對話方塊中，我們建議您選取**網域或伺服器的帳戶**。

  ![圖 43：SIOS DataKeeper 的使用者選項][sap-ha-guide-figure-3033]

  _**圖 43：**SIOS DataKeeper 的使用者選項_

4.  輸入 hello 網域帳戶使用者名稱和密碼 SIOS DataKeeper 所建立。

  ![圖 44： 輸入 hello 網域使用者名稱和密碼 hello SIOS DataKeeper 安裝][sap-ha-guide-figure-3034]

  _**圖 44:**輸入 hello SIOS DataKeeper 安裝 hello 網域使用者名稱和密碼_

5.  安裝 SIOS DataKeeper 執行個體中 45 圖所示為 hello 授權金鑰。

  ![圖 45：輸入您的 SIOS DataKeeper 授權金鑰][sap-ha-guide-figure-3035]

  _**圖 45：**輸入您的 SIOS DataKeeper 授權金鑰_

6.  出現提示時，重新啟動 hello 虛擬機器。

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> 設定 SIOS DataKeeper

兩個節點上安裝 SIOS DataKeeper 之後，您會需要 toostart hello 組態。 hello 組態 hello 目標是 toohave hello 額外的磁碟之間的同步的資料複寫附加 tooeach hello 虛擬機器。

1.  啟動 hello DataKeeper 管理和組態工具，然後選取**連線伺服器**。 (在圖 46 中，此選項是用紅色圈起來的部分。)

  ![圖 46：SIOS DataKeeper 管理和組態工具][sap-ha-guide-figure-3036]

  _**圖 46：**SIOS DataKeeper 管理和組態工具_

2.  輸入 hello 名稱或 TCP/IP 位址的 hello 第一個節點 hello 管理和設定工具應該連接，並在第二個步驟中，hello 第二個節點。

  ![圖 47： 插入 hello 名稱或 TCP/IP 位址 hello 第一個節點 hello 管理和設定工具應該連接，然後在第二個步驟，hello 第二個節點][sap-ha-guide-figure-3037]

  _**圖 47:**插入 hello 名稱或 TCP/IP 位址 hello 第一個節點 hello 管理和設定工具應該連接，然後在第二個步驟，hello 第二個節點_

3.  建立 hello hello 兩個節點之間的複寫作業。

  ![圖 48：建立複寫作業][sap-ha-guide-figure-3038]

  _**圖 48：**建立複寫作業_

  精靈會引導您完成建立複寫作業的 hello 程序。
4.  定義 hello 名稱、 TCP/IP 位址和磁碟區的 hello 來源節點。

  ![圖 49： 定義 hello hello 複寫作業名稱][sap-ha-guide-figure-3039]

  _**圖 49:** hello 複寫作業定義 hello 名稱_

  ![圖 50： 定義 hello hello 節點，它應該 hello 目前的來源節點的基底的資料][sap-ha-guide-figure-3040]

  _**圖 50:**定義 hello hello 節點，它應該 hello 目前的來源節點的基底資料_

5.  定義 hello 名稱、 TCP/IP 位址和磁碟區的 hello 目標節點。

  ![圖 51： 定義 hello hello 節點，它應該 hello 目前的目標節點的基底的資料][sap-ha-guide-figure-3041]

  _**圖 51:**定義 hello hello 節點，它應該 hello 目前的目標節點的基底資料_

6.  定義 hello 壓縮演算法。 在本例中，我們建議您壓縮 hello 複寫資料流。 重新同步處理的情況下，尤其是在 hello 複寫資料流的 hello 壓縮會大幅減少重新同步處理時間。 請注意，壓縮會使用 hello 虛擬機器的 CPU 和 RAM 資源。 隨著 hello 壓縮率增加，因此沒有 hello 使用的 CPU 資源數量。 您也可以稍後調整此設定。

7.  另一個設定您需要 toocheck 是 hello 複寫是否進行非同步或同步。 *當您保護 SAP ASCS/SCS 組態時，您必須使用同步複寫*。  

  ![圖 52︰定義複寫詳細資料][sap-ha-guide-figure-3042]

  _**圖 52︰**定義複寫詳細資料_

8.  定義 hello 磁碟區複寫的 hello 複寫作業是否應為表示的 tooa 做為共用磁碟，Windows Server 容錯移轉叢集叢集組態。 Hello SAP ASCS/SCS 設定，請選取**是**使叢集會看見 hello Windows hello 與可作為叢集磁碟區的共用磁碟的複寫磁碟區。

  ![圖 53： 選取 [是] tooset hello 複寫磁碟區為叢集磁碟區][sap-ha-guide-figure-3043]

  _**圖 53:**選取**是**tooset hello 複寫磁碟區為叢集磁碟區_

  建立 hello 磁碟區之後，hello DataKeeper 管理和設定工具會顯示該 hello 複寫作業為作用中。

  ![圖 54: DataKeeper 同步鏡像 hello SAP ASCS/SCS 共用磁碟為作用中][sap-ha-guide-figure-3044]

  _**圖 54:**針對 hello SAP ASCS/SCS 共用磁碟 DataKeeper 同步鏡像為作用中_

  容錯移轉叢集管理員現在會顯示 hello 磁碟作為 DataKeeper 磁碟，如下圖 55 所示。

  ![圖 55： 容錯移轉叢集管理員顯示 hello 磁碟 DataKeeper 複寫][sap-ha-guide-figure-3045]

  _**圖 55:**容錯移轉叢集管理員顯示 hello 磁碟複寫該 DataKeeper_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>安裝 hello SAP NetWeaver 系統

由於龐大而有所不同 hello 您使用的 DBMS 系統，我們將不會說明 hello DBMS 安裝程式。 不過，我們假設 hello 不同 DBMS 廠商都支援適用於 Azure 的 hello 原有處理，以 hello DBMS 的高可用性考量。 例如，適用於 SQL Server 的 Always On 或資料庫鏡像，以及適用於 Oracle 資料庫的 Oracle Data Guard。 在本文章中我們使用 hello 案例中，我們並未新增更多的保護 toohello DBMS。

當不同的 DBMS 服務與 Azure 中這種叢集 SAP ASCS/SCS 組態互動時，沒有任何特殊的考量。

> [!NOTE]
> hello 的 SAP NetWeaver ABAP 系統、 Java 系統和 ABAP + Java 系統的安裝程序是幾乎完全相同。 hello 最大的差別在於 SAP ABAP 系統有一個 ASCS 執行個體。 hello SAP Java 系統有一個 SCS 執行個體。 hello SAP ABAP + Java 系統有一個 ASCS 執行個體和一個 SCS 執行個體中執行 hello 相同 Microsoft 容錯移轉叢集群組。 我們會明確說明每個 SAP NetWeaver 安裝堆疊的所有安裝差異。 您可以假設所有其他部分會 hello 相同。  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> 使用高可用性 ASCS/SCS 執行個體安裝 SAP

> [!IMPORTANT]
> 請務必的 tooplace DataKeeper 執行您的頁面檔案鏡像磁碟區。 DataKeeper 不支援鏡像磁碟區。 您可以將分頁檔 hello 暫存磁碟機 D 的 Azure 虛擬機器上 hello 預設值。 如果它已經不存在，請移動 hello Windows 分頁檔案 toodrive d： 的 Azure 虛擬機器。
>
>

使用高可用性 ASCS/SCS 執行個體安裝 SAP 包含下列工作︰

- 建立 hello 叢集化 SAP ASCS/SCS 執行個體的虛擬主機名稱
- 安裝 hello SAP 第一個叢集節點
- 修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔
- 新增探查連接埠
- 開啟 Windows 防火牆探查連接埠 hello

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>建立 hello 叢集化 SAP ASCS/SCS 執行個體的虛擬主機名稱

1.  在 hello Windows DNS 管理員中，建立 hello hello ASCS/SCS 執行個體的虛擬主機名稱的 DNS 項目。

  > [!IMPORTANT]
  > hello 分派 toohello hello ASCS/SCS 執行個體必須是虛擬的主機名稱的 IP 位址 hello 相同 hello IP 位址指派給 tooAzure 負載平衡器 (**<*SID*>-lb 集 ascs**).  
  >
  >

  hello hello 虛擬 SAP ASCS/SCS 主機名稱 IP 位址 (**pr1 ascs sap**) hello 相同作為 hello Azure 負載平衡器 IP 位址 (**pr1-lb 集 ascs**)。

  ![圖 56： 定義 hello hello SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目][sap-ha-guide-figure-3046]

  _**圖 56:**定義 hello hello SAP ASCS/SCS 叢集虛擬名稱和 TCP/IP 位址的 DNS 項目_

2.  toodefine hello IP 位址指派 toohello 虛擬主機名稱，選取**DNS 管理員** > **網域**。

  ![圖 57：SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址][sap-ha-guide-figure-3047]

  _**圖 57：**SAP ASCS/SCS 叢集組態的新虛擬名稱和 TCP/IP 位址_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>安裝 hello SAP 第一個叢集節點

1.  執行 hello 第一個叢集節點選項，在叢集節點 a。例如，在 hello **pr1 ascs 0**主機。
2.  tookeep hello 預設連接埠 hello Azure 內部負載平衡器中，選取：

  * **ABAP 系統**：**ASCS** 執行個體號碼 **00**
  * **Java 系統**：**SCS** 執行個體號碼 **01**
  * **ABAP+Java 系統**：**ASCS** 執行個體號碼 **00** 和 **SCS** 執行個體號碼 **01**

  toouse 執行個體數字而不是 00 hello ABAP ASCS 執行個體和 hello Java SCS 執行個體的 01、 toochange hello Azure 內部負載平衡器預設負載平衡中所述的規則先[變更 hello ASCS/SCS 預設負載平衡 hello Azure 內部負載平衡器規則][sap-ha-guide-8.9]。

hello 下一步幾項工作不 hello 標準 SAP 安裝文件所述。

> [!NOTE]
> hello SAP 安裝文件集說明如何 tooinstall hello 第一個 ASCS/SCS 叢集節點。
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>修改 hello ASCS/SCS 執行個體的 hello SAP 設定檔

您需要 tooadd 新的設定檔參數。 hello 設定檔參數可防止 SAP 工作程序與 hello enqueue 伺服器之間的連線關閉時，它們閒置的時間太長。 我們曾提及中的 hello 問題狀況[hello SAP ASCS/SCS 執行個體的兩個叢集節點上新增登錄項目][sap-ha-guide-8.11]。 在該區段中，我們也引進了兩個變更 toosome 基本 TCP/IP 連線參數。 在第二個步驟中，您需要 tooset hello enqueue 伺服器 toosend`keep_alive`發出訊號，以便 hello 連線未遇到 hello Azure 內部負載平衡器的閒置臨界值。

toomodify hello hello ASCS/SCS 執行個體的 SAP 設定檔：

1.  新增此設定檔參數 toohello SAP ASCS/SCS 執行個體的設定檔：

  ```
  enque/encni/set_so_keepalive = true
  ```
  在本例中，hello 路徑為：

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  例如，toohello SAP SCS 執行個體設定檔和對應的路徑：

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello 變更，重新啟動 hello /SCS SAP ASCS 執行個體。

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> 新增探查連接埠

使用 Azure 負載平衡器中的 hello 內部負載平衡器探查功能 toomake hello 整個叢集組態工作。 hello Azure 內部負載平衡器通常會參與虛擬機器之間的平均 hello 連入的工作負載。 不過，這對某些叢集組態不會產生作用，因為只有一個執行個體是主動的。 hello 其他執行個體為被動，無法接受 hello 工作負載。 Hello Azure 內部負載平衡器指派工作只有 tooan 作用中的執行個體時，可幫助探查功能。 Hello 探查功能，與 hello 內部負載平衡器可以偵測到哪些執行個體作用中，而只與 hello 工作負載的 hello 執行個體然後目標。

tooadd 探查連接埠：

1.  檢查目前的 hello **ProbePort**藉由執行下列 PowerShell 命令的 hello 設定。 執行從 hello 虛擬機器的其中一個內 hello 叢集組態中。

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  定義探查連接埠。 hello 預設探查連接埠號碼是**0**。 在我們的範例中，我們會使用探查連接埠 **62000**。

  ![圖 58: hello 叢集設定探查連接埠為預設值 0][sap-ha-guide-figure-3048]

  _**圖 58:** hello 預設叢集設定探查連接埠為 0_

  hello 連接埠號碼是 SAP 的 Azure Resource Manager 範本中定義。 您可以指定在 PowerShell 中的 hello 連接埠號碼。

  tooset hello 的新 ProbePort 值 **SAP <*SID*> IP * * 叢集資源，執行下列 PowerShell 指令碼的 hello。 更新您的環境的 hello PowerShell 變數。 Hello 指令碼執行之後，您將會提示的 toorestart hello SAP 叢集群組 tooactivate hello 的變更。

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  使 hello 之後 **SAP <*SID*> * * 叢集角色上線，請確認**ProbePort**設定 toohello 新值。

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![設定 hello 新值之後，圖 59： 探查 hello 叢集通訊埠][sap-ha-guide-figure-3049]

  _**圖 59:**探查 hello 叢集通訊埠設定 hello 新值之後_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>開啟 Windows 防火牆探查連接埠 hello

您需要 tooopen 兩個叢集節點上的 Windows 防火牆探查連接埠。 使用下列指令碼 tooopen Windows 防火牆的探查連接埠的 hello。 更新您的環境的 hello PowerShell 變數。

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

hello **ProbePort**設定得**62000**。 現在您可以存取 hello 檔案共用 **\\\ascsha-clsap\sapmnt**與其他主控件，例如在**ascsha dba**。

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>安裝 hello 資料庫執行個體

tooinstall hello 資料庫執行個體，請遵循 hello hello SAP 安裝文件中所述的程序。

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>安裝第二個叢集節點 hello

tooinstall hello 第二個叢集，遵循 hello hello SAP 安裝指南 》 中的步驟。

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>變更 hello hello SAP 端 Windows 服務執行個體的啟動類型

太變更 hello hello SAP 端 Windows 服務啟動類型**自動 （延遲開始）**兩個叢集節點上。

![圖 60： 變更 hello SAP 端執行個體 toodelayed 自動 hello 服務類型][sap-ha-guide-figure-3050]

_**圖 60:**變更 hello SAP 端執行個體 toodelayed 自動 hello 服務類型_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>安裝 hello SAP 主應用程式伺服器

安裝 hello 主應用程式伺服器 (PAS) 執行個體 <*SID*>-di-0 hello 所指定的虛擬機器上 toohost hello PA。 Azure 或 DataKeeper 特定的設定沒有相依性。

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>安裝 hello SAP 其他應用程式伺服器

所有 hello 虛擬機器，您已指定 toohost SAP 應用程式伺服器執行個體上安裝 SAP 其他應用程式伺服器 (AAS)。 例如，在 <*SID*>-di-1 太 <*SID*>-di-&lt;n&gt;。

> [!NOTE]
> 這樣就完成 hello 安裝高可用性的 SAP NetWeaver 系統。 接下來，繼續進行容錯移轉測試。
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>測試 hello SAP ASCS/SCS 執行個體容錯移轉和 SIOS 複寫
它是簡單 tootest，並使用容錯移轉叢集管理員 」 和 「 hello SIOS DataKeeper 管理和組態工具來監視 SAP ASCS/SCS 執行個體容錯移轉和 SIOS 磁碟複寫。

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> SAP ASCS/SCS 執行個體在叢集節點 A 上執行

hello **SAP PR1**叢集節點 a 上執行叢集群組例如，在**pr1 ascs 0**。 指派 hello 共用磁碟機 S，屬於的 hello **SAP PR1**叢集群組，以及哪些 hello ASCS/SCS 執行個體使用，toocluster 節點 a。

![圖 61： 容錯移轉叢集管理員： hello SAP < SID > 叢集群組在叢集節點 A 上執行][sap-ha-guide-figure-5000]

_**圖 61:**容錯移轉叢集管理員： hello SAP <*SID*> 叢集節點 A 上執行叢集群組_

在 hello SIOS DataKeeper 管理和組態工具，您可以看到資料以同步方式從 hello 來源磁碟區磁碟機 S 叢集節點 toohello 目標磁碟區上的磁碟機 S 叢集節點 b 上覆寫該 hello 共用的磁碟例如，從複寫**pr1 ascs 0 [10.0.0.40]**太**pr1 ascs 1 [10.0.0.41]**。

![圖 62： 在 SIOS DataKeeper 複製 hello 本機磁碟區從叢集節點的 toocluster 節點 B][sap-ha-guide-figure-5001]

_**圖 62:** SIOS DataKeeper 複寫 hello 本機磁碟區從叢集節點的 toocluster 節點 B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>從節點 A toonode B 容錯移轉

1.  選擇其中一個這些選項 tooinitiate hello SAP 的容錯移轉 <*SID*> 叢集群組從叢集節點 A toocluster 節點 b:
  - 使用容錯移轉叢集管理員  
  - 使用容錯移轉叢集 PowerShell

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  重新啟動叢集節點的 hello Windows 客體作業系統內 (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。  
3.  重新啟動叢集節點 A 從 hello Azure 入口網站 (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。  
4.  使用 Azure PowerShell 來重新啟動叢集節點 A (這會起始自動容錯移轉的 hello SAP <*SID*> 叢集群組從節點 A toonode B)。

  容錯移轉之後，hello SAP <*SID*> 叢集節點 b 上執行叢集群組例如，在上執行**pr1 ascs 1**。

  ![圖 63： 在容錯移轉叢集管理員中，hello SAP < SID > 叢集群組節點上執行叢集 B][sap-ha-guide-figure-5002]

  _**圖 63**： 在容錯移轉叢集管理員 hello SAP <*SID*> 叢集節點 B 上執行叢集群組_

  hello 共用的磁碟現在裝載在叢集節點 B SIOS DataKeeper 從來源磁碟區磁碟機 S 叢集節點 B tootarget 磁碟區磁碟機 S 上的叢集節點 a 上複寫的資料例如，從複寫**pr1 ascs 1 [10.0.0.41]**太**pr1 ascs 0 [10.0.0.40]**。

  ![圖 64: SIOS DataKeeper 複寫 hello 本機磁碟區的叢集節點 B toocluster 節點 A][sap-ha-guide-figure-5003]

  _**圖 64:** SIOS DataKeeper 從叢集節點 B toocluster 節點 A 複寫 hello 本機磁碟區_
