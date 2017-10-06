---
title: "包含執行 Windows Azure Vm 叢集 aaaCreate 獨立 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理執行 Windows Server 的 Azure 虛擬機器上的 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>建立三個具有執行 Windows Server 之 Azure 虛擬機器的節點獨立 Service Fabric 叢集
本文說明如何 toocreate 的 windows Azure 虛擬機器 (Vm) 上的叢集，使用 hello 獨立 Service Fabric 安裝程式的 Windows 伺服器。 hello 案例是特殊案例[建立和管理 Windows Server 上執行叢集](service-fabric-cluster-creation-for-windows-server.md)hello Vm 所在[執行 Windows Server 的 Azure Vm](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，但是您不需要建立[Azure以雲端為基礎的 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)。 遵循此模式中的 hello 差異並沒有那麼 hello 步驟所建立的 hello 獨立 Service Fabric 叢集完全受您，而管理的 hello Azure 雲端服務網狀架構叢集，並由 hello Service Fabric 升級資源提供者。

## <a name="steps-toocreate-hello-standalone-cluster"></a>步驟 toocreate hello 獨立叢集
1. 登入 toohello Azure 入口網站，並在資源群組中建立新的 Windows Server 2012 R2 Datacenter 或 Windows Server 2016 資料中心的 VM。 閱讀文章 hello [hello Azure 入口網站中建立的 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)如需詳細資訊。
2. 加入一些其他的 Vm toohello 相同的資源群組。 請確定每個 hello Vm 有 hello 相同的系統管理員使用者名稱和密碼時建立。 您應該會看見 hello 中的所有三個 Vm 建立之後相同的虛擬網路。
3. 連接的 hello Vm tooeach 並關閉 Windows 防火牆使用 hello hello[伺服器管理員 中，本機伺服器儀表板](https://technet.microsoft.com/library/jj134147.aspx)。 這可確保 hello 網路流量，可以 hello 機器之間進行通訊。 連接的 tooeach 機器時，請開啟命令提示字元並輸入取得 hello 的 IP 位址`ipconfig`。 或者，您可以看到 hello IP hello 入口網站中，選取 hello hello 資源群組的虛擬網路資源，並檢查這些機器的每個建立的 hello 網路介面上的每部機器的位址。
4. 連接的 hello Vm tooone 和測試，您可以 ping 成功 hello 其他兩個 Vm。
5. 連接的 hello Vm tooone 和[hello 獨立 Service Fabric 封裝下載適用於 Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) hello 上的新資料夾到電腦，並擷取 hello 封裝。
6. 開啟 hello *ClusterConfig.Unsecure.MultiMachine.json* [記事本] 中，並編輯 hello 機器 hello 三個 IP 位址與每個節點。 變更在 hello 頂端 hello 叢集名稱，並儲存 hello 檔案。  Hello 叢集資訊清單的部分範例如下所示。
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. 如果您想要這個 toobe 安全的叢集，決定 hello 安全性措施，toouse 然後遵循 hello hello 步驟相關聯的連結： [X509 憑證](service-fabric-windows-cluster-x509-security.md)或[Windows 安全性](service-fabric-windows-cluster-windows-security.md)。 如果設定使用 Windows 安全性的 hello 叢集，您必須設定 Active Directory 網域控制站 toomanage tooset。 請注意，不支援使用網域控制站電腦做為 Service Fabric 節點。
8. 開啟 [PowerShell ISE 視窗](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。 瀏覽 toohello 資料夾您擷取 hello 下載的獨立安裝程式封裝並儲存 hello 叢集組態檔。 執行下列 PowerShell 命令 toodeploy hello 叢集 hello:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

hello 指令碼都會從遠端設定 hello Service Fabric 叢集，而且應該報告進度，因為透過復原部署。

9. 約一分鐘，您可以檢查如果 hello 叢集運作藉由連接 toohello 之後 Service Fabric 總管使用其中一種 hello 機器的 IP 位址，例如使用`http://10.1.0.5:19080/Explorer/index.html`。 

## <a name="next-steps"></a>後續步驟
* [在 Windows Server 或 Linux 上建立獨立的 Service Fabric 叢集](service-fabric-deploy-anywhere.md)
* [新增或移除節點 tooa 獨立 Service Fabric 叢集](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)
* [使用 Windows 安全性保護 Windows 上的獨立叢集](service-fabric-windows-cluster-windows-security.md)
* [使用 X509 憑證保護 Windows 上的獨立叢集](service-fabric-windows-cluster-x509-security.md)

