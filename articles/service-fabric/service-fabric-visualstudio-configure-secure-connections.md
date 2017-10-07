---
title: "aaaConfigure 保護 Azure Service Fabric 叢集連線 |Microsoft 文件"
description: "了解如何 toouse Visual Studio tooconfigure 保護 hello Azure Service Fabric 叢集所支援的連線。"
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>設定從 Visual Studio 的安全連線 tooa Service Fabric 叢集
了解如何 toouse Visual Studio toosecurely 存取 Azure Service Fabric 叢集的存取控制原則設定。

## <a name="cluster-connection-types"></a>叢集連線類型
Hello Azure Service Fabric 叢集所支援兩種連線類型：**不安全**連線和**x509 憑證為基礎**保護連線。 (如果是裝載在內部部署環境的 Service Fabric 叢集，則也支援 **Windows** 和 **dSTS** 驗證。)正在建立 hello 叢集時，您會有 tooconfigure hello 叢集連線類型。 一旦建立之後，就無法變更 hello 連接類型。

hello Visual Studio Service Fabric 工具支援所有的驗證類型進行發佈的連線 tooa 叢集。 請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)如需有關指示 tooset 安全的 Service Fabric 叢集。

## <a name="configure-cluster-connections-in-publish-profiles"></a>在發行設定檔中設定叢集連接
如果您發行 Service Fabric 專案從 Visual Studio 時，使用 hello**發行 Service Fabric 應用程式**對話方塊方塊 toochoose Azure Service Fabric 叢集。 在 [連線端點] 之下，選取您訂用帳戶下的現有叢集。

![hello * * 發行 Service Fabric 應用程式 * * 對話方塊會使用的 tooconfigure Service Fabric 連線。][publishdialog]

hello**發行 Service Fabric 應用程式**對話方塊會自動驗證 hello 叢集連線。 如果出現提示，請登入 tooyour Azure 帳戶。 如果驗證成功，則表示您的系統已正確安裝憑證，tooconnect toohello 叢集安全地儲存，或您的叢集已不安全的 hello。 網路問題，或沒有正確地設定系統 tooconnect tooa 安全叢集，可能被造成驗證失敗。

![hello * * 發行 Service Fabric 應用程式 * * 對話方塊會驗證現有的正確設定 Service Fabric 叢集連線。][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa 安全叢集
1. 請確定您可以存取其中一個 hello hello 目的地叢集信任的用戶端憑證。 hello 憑證通常會為個人資訊交換 (.pfx) 檔案共用。 請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)如 tooconfigure hello 伺服器 toogrant 存取 tooa 用戶端的方式。
2. 安裝 hello 受信任的憑證。 toodo，按兩下 hello.pfx 檔案，或使用 hello PowerShell 指令碼 Import-pfxcertificate tooimport hello 憑證。 安裝 hello 憑證太**Cert: \LocalMachine\My**。 它是確定 tooaccept 匯入 hello 憑證時的所有預設設定。
3. 選擇 hello**發行...** hello 專案 tooopen hello hello 快顯功能表上的命令**發行 Azure 應用程式**對話方塊，然後選取 hello 目標叢集。 hello 工具會自動解析 hello 連線，並儲存在 hello 參數將發行的 hello 安全連線設定檔。
4. 選用： 您可以編輯 hello 發行設定檔 toospecify 安全叢集連線。
   
   因為您手動編輯 hello 發行設定檔 XML 檔 toospecify hello 憑證資訊，請確定 toonote hello 憑證存放區名稱，儲存位置和憑證指紋。 您將需要的 tooprovide hello 憑證存放區的這些值的名稱和儲存體位置。 請參閱[How to： 擷取 hello 憑證的指紋](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx)如需詳細資訊。
   
   您可以使用 hello *ClusterConnectionParameters*參數 toospecify hello PowerShell 參數 toouse 連接 toohello Service Fabric 叢集時。 有效的參數是可接受的 hello Connect-servicefabriccluster cmdlet。 如需可用參數的清單，請參閱 [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) 。
   
   如果您要發行 tooa 遠端叢集，您會需要針對該特定群集 toospecify hello 適當的參數。 hello 以下是連接 tooa 不安全叢集的範例：
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   連接 tooan x509 憑證為基礎安全叢集的範例如下：
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. 編輯任何其他必要的設定，例如升級參數和應用程式參數檔案的位置，然後應用程式並發行從 hello**發行 Service Fabric 應用程式**Visual Studio 中的對話方塊。

## <a name="next-steps"></a>後續步驟
如需有關存取 Service Fabric 叢集的詳細資訊，請參閱 [使用 Service Fabric 總管視覺化叢集](service-fabric-visualizing-your-cluster.md)。

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
