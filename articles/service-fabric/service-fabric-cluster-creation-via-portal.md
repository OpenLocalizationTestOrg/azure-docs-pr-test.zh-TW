---
title: "aaaCreate Service Fabric 叢集 hello Azure 入口網站 |Microsoft 文件"
description: "本文說明如何在 Azure 中，使用安全的 Service Fabric 叢集 tooset hello Azure 入口網站與 Azure 金鑰保存庫。"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>使用 hello Azure 入口網站在 Azure 中建立 Service Fabric 叢集
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure 入口網站](service-fabric-cluster-creation-via-portal.md)
> 
> 

這是引導您設定安全 Service Fabric 叢集使用 hello Azure 入口網站在 Azure 中的 hello 步驟的逐步指南。 本指南會引導您 hello 下列步驟：

* 設定叢集安全性金鑰保存庫 toomanage 索引鍵。
* 在 Azure 中建立受保護的叢集，透過 hello Azure 入口網站。
* 使用憑證驗證系統管理員。

> [!NOTE]
> 如需更進階的安全性選項 (例如使用 Azure Active Directory 進行使用者驗證及設定應用程式安全性的憑證)，請參閱[使用 Azure Resource Manager 建立您的叢集][create-cluster-arm]。
> 
> 

需要安全的叢集，叢集來防止未經授權的存取 toomanagement 作業，包括部署、 升級和刪除應用程式、 服務和 hello 它們包含的資料。 不安全的叢集是叢集的任何人都可以用來連接 tooat 任何時間，並執行管理作業。 雖然您可能 toocreate 不安全的叢集，它是**強烈建議安全叢集 toocreate**。 不安全的叢集 **無法在事後保護其安全** - 必須建立新的叢集。

hello 概念是 hello 相同的 hello 叢集 Linux 叢集或 Windows 叢集是否建立安全的叢集。 如需建立安全 Linux 叢集的詳細資訊和協助程式指令碼，請參閱[在 Linux 上建立安全叢集](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters)。 hello hello 所提供的協助程式指令碼所取得的參數可以輸入 hello 入口網站直接在 hello > 一節中所述[hello Azure 入口網站中建立叢集](#create-cluster-portal)。

## <a name="log-in-tooazure"></a>登入 tooAzure
本指南使用 [Azure PowerShell][azure-powershell]。 當啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，然後選取您的訂用帳戶，然後再執行 Azure 的命令。

登入 tooyour azure 帳戶：

```powershell
Login-AzureRmAccount
```

選取您的訂用帳戶：

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>設定金鑰保存庫
Hello 指南的這個部分會引導您建立金鑰保存庫在 Azure 中的 Service Fabric 叢集和 Service Fabric 應用程式。 在金鑰保存庫的完整指南，請參閱 hello[金鑰保存庫快速入門指南][key-vault-get-started]。

服務網狀架構會使用 X.509 憑證 toosecure 叢集。 Azure 金鑰保存庫是使用的 toomanage 憑證在 Azure 中的 Service Fabric 叢集。 在 Azure 中部署叢集時，hello Azure 資源提供者負責建立 Service Fabric 叢集會提取從金鑰保存庫的憑證，並 hello 叢集 Vm 上進行安裝。

hello 下列圖表說明 hello 金鑰保存庫、 Service Fabric 叢集和使用憑證時它會建立叢集儲存在金鑰保存庫中的 hello Azure 資源提供者之間的關聯性：

![憑證安裝][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>建立資源群組
hello 第一個步驟是 toocreate 特別針對金鑰保存庫的新資源群組。 將金鑰保存庫放入自己的資源群組建議，讓您可以移除-例如 hello 有 Service Fabric 叢集資源群組-運算和存放裝置資源群組，而不會遺失您的金鑰和密碼。 hello 具有您金鑰保存庫的資源群組必須在 hello 與正在使用它的 hello 叢集相同的區域。

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>建立金鑰保存庫
Hello 新資源群組中建立金鑰保存庫。 金鑰保存庫 hello**必須為部署啟用**tooallow hello Service Fabric 資源提供者從它的 tooget 憑證並安裝在叢集節點上：

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

如果您有現有金鑰保存庫，可以使用 Azure CLI 將它啟用以用於部署：

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>新增憑證 tooKey 保存庫
憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。 如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例][service-fabric-cluster-security]。

### <a name="cluster-and-server-certificate-required"></a>叢集和伺服器憑證 (必要)
此憑證是必要的 toosecure 叢集，並防止未經授權的存取 tooit。 它會透過幾種方式提供叢集安全性：

* **叢集驗證：** 驗證叢集同盟的節點對節點通訊。 可以證明其身分識別與此憑證的節點可以加入 hello 叢集。
* **伺服器驗證：** hello 叢集管理端點 tooa 管理會用戶端驗證，以便 hello 管理用戶端會知道它正在交涉 toohello 實際叢集。 此憑證也可提供 SSL hello HTTPS 管理 API 與 Service Fabric 總管透過 HTTPS。

這些的考量，hello 憑證必須符合下列需求的 hello tooserve:

* hello 憑證必須包含私密金鑰。
* 金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。
* hello 憑證的主體名稱必須符合 hello 用網域 tooaccess hello Service Fabric 叢集。 這是必要的 tooprovide SSL hello 叢集 HTTPS 管理端點和 Service Fabric 總管。 您無法從 hello 的憑證授權單位 (CA) 取得 SSL 憑證`.cloudapp.azure.com`網域。 為您的叢集取得自訂網域名稱。 當您要求的憑證，CA hello 憑證的主體名稱必須符合 hello 自訂網域名稱用於您的叢集。

### <a name="client-authentication-certificates"></a>用戶端驗證憑證
其他用戶端憑證會驗證系統管理員以執行叢集管理工作。 Service Fabric 有兩個存取層級：[系統管理員] 和 [唯讀使用者]。 您至少應使用一個單一憑證以用於進行系統管理存取。 若要進行其他使用者層級存取，則必須提供個別憑證。 如需存取角色的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)][service-fabric-cluster-security-roles]。

您不需要 tooupload 用戶端驗證憑證 tooKey 保存庫 toowork 以 Service Fabric。 這些憑證只需要提供叢集管理已獲授權 toousers toobe。 

> [!NOTE]
> Azure Active Directory 是 hello 建議叢集方式 tooauthenticate 用戶端管理作業。 您必須 toouse Azure Active Directory，[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。
> 
> 

### <a name="application-certificates-optional"></a>應用程式憑證 (選用)
您可以針對應用程式安全性目的，在叢集上安裝任何數目的其他憑證。 之前建立您的叢集，請考慮需要這類 hello 節點上安裝憑證 toobe hello 應用程式安全性案例：

* 加密和解密應用程式組態值
* 在複寫期間跨節點加密資料 

建立叢集，以透過 hello Azure 入口網站時，無法設定應用程式憑證。 您必須在叢集安裝程式階段 tooconfigure 應用程式憑證，[使用 Azure Resource Manager 建立叢集][create-cluster-arm]。 一旦建立後，您也可以新增應用程式憑證 toohello 叢集。

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>設定憑證格式以供 Azure 資源提供者使用
私密金鑰檔案 (.pfx) 可以直接透過金鑰保存庫來新增及使用。 不過，hello Azure 資源提供者需要索引鍵 toobe 儲存在特殊的 JSON 格式，其中包含 hello.pfx 做為 base 64 編碼字串和 hello 私用金鑰的密碼。 這些需求，金鑰必須放在 JSON 字串，並儲存為 tooaccommodate*密碼*金鑰保存庫中。

此程序會更容易 toomake，PowerShell 模組是[github][service-fabric-rp-helpers]。 請遵循這些步驟 toouse hello 模組：

1. Hello 的 hello 儲存機制的整個內容下載至本機目錄中。 
2. 匯入您的 PowerShell 視窗中的 hello 模組：

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

hello`Invoke-AddCertToKeyVault`此 PowerShell 模組中的命令自動將憑證的私密金鑰格式化為 JSON 字串，並將它上載 tooKey 保存庫。 Tooadd hello 叢集憑證與任何其他應用程式憑證 tooKey 保存庫，請使用它。 任何額外的憑證，您要在叢集中的 tooinstall 重複此步驟。

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

這些是所有 hello 金鑰保存庫必要條件設定的節點驗證，管理端點的安全性和驗證，以及任何其他應用程式的安全性憑證會安裝 Service Fabric 叢集資源管理員範本使用 X.509 憑證的功能。 此時，您現在應該有下列安裝程式在 Azure 中的 hello:

* 金鑰保存庫資源群組
  * 金鑰保存庫
    * 叢集伺服器驗證憑證

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立叢集
### <a name="search-for-hello-service-fabric-cluster-resource"></a>搜尋 hello Service Fabric 叢集資源
![搜尋 hello Azure 入口網站上的 Service Fabric 叢集範本。][SearchforServiceFabricClusterTemplate]

1. 登入 toohello [Azure 入口網站][azure-portal]。
2. 按一下**新增**tooadd 新的資源範本。 搜尋在 hello hello Service Fabric 叢集範本**Marketplace**下**一切**。
3. 選取**Service Fabric 叢集**從 hello 清單。
4. 瀏覽 toohello **Service Fabric 叢集**刀鋒視窗中，按一下 **建立**，
5. hello**建立 Service Fabric 叢集**分頁有四個步驟的 hello。

#### <a name="1-basics"></a>1.基本概念
![建立新資源群組的螢幕擷取畫面。][CreateRG]

在 hello 基本概念刀鋒視窗中，您會需要 tooprovide hello 基本詳細資料為您的叢集。

1. 輸入 hello 叢集的名稱。
2. 輸入**使用者名**和**密碼**hello Vm 的遠端桌面。
3. 請確定 tooselect hello**訂用帳戶**您想部署，您叢集 toobe，特別是如果您有多個訂用帳戶。
4. 建立 **新的資源群組**。 它是最佳 toogive 它 hello hello 叢集相同的名稱，因為它可協助在更新版本中，找到這些物件，特別是當您嘗試 toomake 變更 tooyour 部署或刪除您的叢集。
   
   > [!NOTE]
   > 雖然您可以決定 toouse 現有的資源群組，是很好的作法 toocreate 新的資源群組。 這可讓您不需要的簡單 toodelete 叢集。
   > 
   > 
5. 選取 hello**區域**想 toocreate hello 叢集。 您必須使用您的金鑰保存庫的同一個地區處於的 hello。

#### <a name="2-cluster-configuration"></a>2.叢集組態
![建立節點類型][CreateNodeType]

設定您的叢集節點。 節點型別定義 hello VM 大小、 hello 的 Vm，以及它們的屬性。 您的叢集可以有一個以上的節點類型，但 hello 主要節點類型 (hello hello 入口網站上定義的第一個) 必須至少五個 Vm，因為這是一個 hello 節點型別放置 Service Fabric 系統服務。 請勿設定 [放置屬性]，因為會自動新增 "NodeTypeName" 預設放置屬性。

> [!NOTE]
> 多個節點類型的常見案例是包含前端服務和後端服務的應用程式。 您想 tooput hello 前端上的服務連接埠開啟 toohello 網際網路，具有較小的 Vm （例如 D2 的 VM 大小），但是您想 tooput hello 後端服務在較大的 Vm (例如 D4、 D6、 D15，以及其他 VM 大小） 上開啟任何網際網路的連接埠。
> 
> 

1. 選擇您的節點型別 （1 too12 字元包含字母和數字） 的名稱。
2. 最小的 hello**大小**hello 主要節點的 Vm 的類型由 hello 所驅動**持久性**層您選擇 hello 叢集。 hello 持久性層的 hello 預設值是青銅卡。 如需有關持久性的詳細資訊，請參閱[toochoose hello Service Fabric 叢集化的可靠性和持久性][service-fabric-cluster-capacity]。
3. 選取 hello VM 大小與定價層。 D 系列 VM 擁有 SSD 磁碟機，且強烈建議用於具狀態應用程式。 請勿使用只有部分核心或可用磁碟容量少於 7 GB 的任何 VM SKU。 
4. 最小的 hello**數目**hello 主要節點的 Vm 的類型由 hello 所驅動**可靠性**層選擇。 hello 可靠性層的 hello 預設值為銀級。 如需可靠性的詳細資訊，請參閱[toochoose hello Service Fabric 叢集化的可靠性和持久性][service-fabric-cluster-capacity]。
5. 選擇 hello Vm 數目 hello 節點型別。 您可以在稍後相應增加或減少 Vm 的節點型別中的 hello 數字，但 hello 主要節點類型，最小的 hello 由您所選擇的 hello 可靠性層級所驅動。 其他節點類型可以有 1 個 VM 的下限。
6. 設定自訂端點。 此欄位可讓您以逗號分隔清單的連接埠，您想要透過 hello Azure 負載平衡器 toohello tooexpose tooenter 公用網際網路應用程式。 例如，如果您計劃 toodeploy web 應用程式 tooyour 叢集時，輸入"80"這裡 tooallow 到您的叢集中的連接埠 80 上的流量。 如需端點的詳細資訊，請參閱[與應用程式通訊][service-fabric-connect-and-communicate-with-services]
7. 設定叢集**診斷**。 根據預設，在您的問題進行疑難排解的叢集 tooassist 上啟用診斷。 如果您想要 toodisable 診斷變更 hello**狀態**太切換**關閉**。 **不**建議將診斷關閉。
8. 選取的 hello 網狀架構升級您的叢集設定為您想要的模式。 選取**自動**，如果您想 hello 系統 tooautomatically 取用 hello 最新可用版本，然後再次嘗試 tooupgrade 叢集 tooit。 將 hello 模式設定為太**手動**，如果您想 toochoose 支援的版本。

> [!NOTE]
> 我們支援的叢集限於執行支援的 Service Fabric 版本。 藉由選取 hello**手動**模式中，您就可以在 hello 責任 tooupgrade 您叢集 tooa 支援版本。 如需 hello Fabric 升級模式的詳細資訊，請參閱 hello [service fabric 叢集-升級文件。][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3.安全性
![Azure 入口網站中安全性組態的螢幕擷取畫面。][SecurityConfigs]

hello 最後一個步驟是 tooprovide 憑證資訊 toosecure hello 叢集使用金鑰保存庫 hello 和資訊稍早建立的憑證。

* Hello 主要憑證欄位中填入取自上載 hello hello 輸出**叢集憑證**tooKey 保存庫使用 hello `Invoke-AddCertToKeyVault` PowerShell 命令。

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* 檢查 hello**設定進階設定**方塊 tooenter 用戶端憑證**管理用戶端**和**唯讀用戶端**。 在這些欄位中，輸入 hello 您管理用戶端憑證指紋和 hello 您唯讀使用者用戶端憑證指紋，如果適用的話。 當系統管理員嘗試 tooconnect toohello 叢集時，則會授與存取擁有 hello 指紋值相符的指模的憑證時，才可以在此處輸入。  

#### <a name="4-summary"></a>4.摘要
![螢幕擷取畫面的 hello 開始面板顯示 「 部署 Service Fabric 叢集 」。 ][Notifications]

toocomplete hello 建立叢集，按一下 **摘要**toosee hello 設定，您已提供，或下載 hello Azure Resource Manager 範本，用 toodeploy 您的叢集。 提供 hello 必要設定之後，hello**確定**按鈕會變成綠色，而您可以按一下它，以啟動 hello 叢集建立程序。

您可以看到在 hello 通知 hello 建立進度。 （按一下 hello 狀態列會在 hello 右上角螢幕附近的 hello"鈴鐺 」 圖示）。如果您按下**Pin tooStartboard**同時建立 hello 叢集，您會看到**部署 Service Fabric 叢集**釘選 toohello**啟動**面板。

### <a name="view-your-cluster-status"></a>檢視叢集狀態
![螢幕擷取畫面： hello 儀表板中的叢集詳細資料。][ClusterDashboard]

一旦建立您的叢集，您可以檢查您的叢集 hello 入口網站中：

1. 跳過**瀏覽**按一下**服務網狀架構叢集**。
2. 找出您的叢集，然後按一下它。
3. 您現在可以看到您的叢集 hello 儀表板，包括 hello 叢集的公用端點及連結 tooService Fabric 總管中的 hello 詳細資料。

hello**節點監視**hello 叢集儀表板 刀鋒視窗的區段指出 hello 為狀況良好和狀況不良的 Vm 數目。 您可以找到更多詳細 hello 叢集健全狀況在[服務網狀架構健全狀況模型簡介][service-fabric-health-introduction]。

> [!NOTE]
> Service Fabric 叢集需要一律 toomaintain 可用性節點 toobe 數目，並保留狀態-參照 tooas 「 維持仲裁 」。 Therfore，通常是不安全關閉 hello 叢集中的所有機器 tooshut 除非您先執行[狀態的完整備份][service-fabric-reliable-services-backup-restore]。
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>遠端連接 tooa 虛擬機器擴展集的執行個體或叢集節點
每個 hello NodeTypes 您指定在虛擬機器規模集中取得安裝您叢集的結果。 請參閱[tooa 虛擬機器擴展集的執行個體的遠端連接][ remote-connect-to-a-vm-scale-set]如需詳細資訊。

## <a name="next-steps"></a>後續步驟
此時，您擁有一個使用憑證來管理驗證的安全叢集。 下一步 [tooyour 叢集連線](service-fabric-connect-to-secure-cluster.md)並了解如何太[管理應用程式密碼](service-fabric-application-secret-management.md)。  同時，了解 [Service Fabric 支援選項](service-fabric-support.md)。

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
