---
title: "Visual Studio 的應用程式 tooa 遠端叢集 aaaPublish |Microsoft 文件"
description: "了解如何使用 Visual Studio toopublish 應用程式 tooa 遠端服務網狀架構叢集。"
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>使用 Visual Studio 來部署和移除應用程式
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [FabricClient API](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

hello Azure Service Fabric Visual Studio 擴充功能提供簡單、 可重複、 可編寫指令碼的方式 toopublish 應用程式 tooa Service Fabric 叢集。

## <a name="hello-artifacts-required-for-publishing"></a>為發行所需的 hello 成品
### <a name="deploy-fabricapplicationps1"></a>Deploy-FabricApplication.ps1
這是 PowerShell 指令碼，使用發佈設定檔路徑做為參數，以發佈 Service Fabric 應用程式。 此指令碼是您的應用程式的一部分，因為您是  褖畫惎 toomodify 它視您的應用程式。

### <a name="publish-profiles"></a>發佈設定檔
Hello Service Fabric 應用程式專案的資料夾內呼叫**PublishProfiles**包含 XML 檔案來儲存重要資訊發佈應用程式，例如：

* Service Fabric 叢集連線參數
* 路徑 tooan 應用程式參數檔案
* 升級設定

根據預設，您的應用程式會包含三個發佈設定檔：Local.1Node.xml、Local.5Node.xml 和 Cloud.xml。 您可以加入多個設定檔複製並貼上的其中一個 hello 預設檔案。

### <a name="application-parameter-files"></a>應用程式參數檔案
Hello Service Fabric 應用程式專案的資料夾內呼叫**ApplicationParameters**包含使用者指定的應用程式資訊清單的參數值的 XML 檔案。 應用程式資訊清單檔案可以參數化，讓您可以針對部署設定使用不同的值。 toolearn 更多關於參數化您的應用程式，請參閱[管理多個環境中 Service Fabric](service-fabric-manage-multiple-environment-app-configuration.md)。

> [!NOTE]
> 針對行動服務，您應該建立 hello 專案第一次嘗試 tooedit hello 檔案在編輯器中或透過 hello 發行 web 對話方塊。 這是因為 hello 建置期間，將產生的 hello 資訊清單檔案的一部分。

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish 應用程式使用 hello 發行 Service Fabric 應用程式 對話方塊
hello 下列步驟示範如何使用應用程式的 toopublish hello**發行 Service Fabric 應用程式**hello Visual Studio Service Fabric 工具所提供的對話方塊。

1. Hello hello Service Fabric 應用程式專案的捷徑功能表，選擇 **發行...** tooview hello**發行 Service Fabric 應用程式** 對話方塊。
   
    ![hello * * 發行 Service Fabric 應用程式 * * 對話方塊][0]
   
    hello 中選取的 hello 檔案**profile 當做目標**下拉式清單方塊是 where 所有 hello 設定，除了**資訊清單版本**，會儲存。 您可以重複使用現有的設定檔，或建立一個新選擇**< 管理設定檔...>**在 hello **profile 當做目標**下拉式清單方塊。 當您選擇的發行設定檔時，其內容會顯示 hello hello 對話方塊中的對應欄位中。 toosave 您的變更，也可以隨時選擇 hello**儲存設定檔**連結。    
2. 在 hello**連接端點**區段中，指定本機或遠端 Service Fabric 叢集的發行端點。 tooadd 或變更 hello 連接端點上，按一下 hello**連接端點**下拉式清單中。 hello 清單會顯示 hello 可用 Service Fabric 叢集連線端點 toowhich 可以發佈根據您的 Azure 訂閱。 請注意，是否您沒有已登入 tooVisual Studio，您將會提示的 toodo 因此。
   
    使用 hello 叢集選取範圍對話方塊方塊 toochoose 從 hello 組可用的訂閱和叢集。
   
    ![hello * * 選取 Service Fabric 叢集 * * 對話方塊][1]
   
   > [!NOTE]
   > 如果您想要 toopublish tooan 任意端點 （例如合作對象叢集），請參閱 hello**發佈 tooan 任意叢集端點**下一節。
   > 
   > 
   
    一旦您選擇端點時，Visual Studio 會驗證 hello 連接 toohello 選取 Service Fabric 叢集。 如果 hello 叢集不安全，Visual Studio 就可以立即連線 tooit。 不過，如果 hello 叢集是安全的您必須先 tooinstall 憑證後再繼續在本機電腦上。 請參閱[tooconfigure 如何保護連線](service-fabric-visualstudio-configure-secure-connections.md)如需詳細資訊。 當您完成時，選擇 hello**確定** 按鈕。 hello 選的叢集會出現在 hello**發行 Service Fabric 應用程式** 對話方塊。
3. 在 hello**應用程式參數檔案**下拉式清單方塊中，瀏覽 tooan 應用程式參數檔案。 應用程式參數檔案保存 hello 應用程式資訊清單檔中的使用者指定之參數的值。 tooadd 或變更參數，選擇 [hello**編輯**] 按鈕。 輸入或變更 hello 參數的值，在 hello**參數**方格。 當您完成時，選擇 hello**儲存** 按鈕。
   
    ![hello * * 編輯參數 * * 對話方塊][2]
4. 使用 hello**升級 hello 應用程式**核取方塊 toospecify 是否此發行動作會升級。 升級發佈動作不同於一般發佈動作。 如需差異清單，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。 tooconfigure 升級設定中，選擇 hello**設定升級設定**連結。 hello 升級參數編輯器隨即出現。 請參閱[設定 Service Fabric 應用程式的 hello 升級](service-fabric-visualstudio-configure-upgrade.md)toolearn 更多關於升級的參數。
5. 選擇 hello**資訊清單版本...** 按鈕 tooview hello**編輯版本** 對話方塊。 您需要 tooupdate 應用程式和服務版本與升級 tootake 位置。 請參閱[Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)toolearn 如何應用程式與服務資訊清單版本會影響升級的程序。
   
    ![hello * * 編輯版本 * * 對話方塊][3]
   
    如果 hello 應用程式和服務版本使用語意版本設定，例如 1.0.0 或數值的 1.0.0.0 hello 格式中，選取 hello**自動更新應用程式和服務版本**選項。 當您選擇此選項，hello 服務和應用程式版本號碼時會自動更新程式碼、 組態中，或資料封裝版本已更新。 如果您手動偏好 tooedit hello 版本，請清除 hello 核取方塊 toodisable 這項功能。
   
   > [!NOTE]
   > 所有動作項目專案的封裝項目 tooappear，第一次建立 hello 專案 toogenerate hello hello 服務資訊清單檔案中的項目。
   > 
   > 
6. 當您完成指定所有必要的設定，hello 選擇 hello**發行**按鈕選取您的應用程式 toohello toopublish Service Fabric 叢集。 您指定的 hello 設定會套用 toohello 發佈程序。

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>發行 tooan 任意叢集端點 （包括合作對象叢集）
hello Visual Studio 發行經驗最適合用於發行 tooremote 叢集與其中一個 Azure 訂用帳戶相關聯。 不過，它是可能 toopublish tooarbitrary 端點 （例如 Service Fabric 合作對象的叢集） 直接編輯 hello 發行設定檔 XML。 如上面所述，三個發行設定檔所提供的預設值-**Local.1Node.xml**， **Local.5Node.xml**，和**Cloud.xml**-卻  褖畫惎 toocreate不同環境的其他設定檔。 比方說，您可能希望 toocreate 設定檔發佈 tooparty 叢集，可能名為**Party.xml**。

如果您要連接不安全叢集的 tooan，只需要是 hello 叢集連接的端點，如`partycluster1.eastus.cloudapp.azure.com:19000`。 大小寫，在 hello hello 連接端點發行設定檔看起來可能像這樣：

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  如果您要連接 tooa 受保護的叢集，您也需要從 hello 用於驗證的本機存放區 toobe hello 用戶端憑證的 tooprovide hello 詳細資料。 如需詳細資訊，請參閱[設定安全連接 tooa Service Fabric 叢集](service-fabric-visualstudio-configure-secure-connections.md)。

  一旦設定您的發行設定檔之後，您可以在中參考它 hello 發行 web 對話方塊，如下所示。

  ![發佈對話方塊中的新發行設定檔][4]

  請注意，在此情況下，新的 hello 發行設定檔點 tooone hello 預設應用程式參數檔案。 這是適當 toopublish 如果您想 hello 相同應用程式組態 tooa 數目的環境。 相反地，在您希望每個環境，您想要 toopublish toohave 不同組態的情況下，它會使意義 toocreate 相對應的應用程式參數檔案。

## <a name="next-steps"></a>後續步驟
如何 tooautomate hello 發佈程序在持續整合環境中，請參閱的 toolearn[設定 Service Fabric 連續整合](service-fabric-set-up-continuous-integration.md)。

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
