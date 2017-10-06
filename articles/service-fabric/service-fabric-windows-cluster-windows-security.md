---
title: "叢集執行於 Windows 上使用 Windows 安全性 aaaSecure |Microsoft 文件"
description: "了解如何在獨立的 tooconfigure 節點對節點和用戶端對節點安全性叢集執行於 Windows 上使用 Windows 安全性。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>使用 Windows 安全性保護 Windows 上的獨立叢集
tooprevent 未經授權存取 tooa Service Fabric 叢集，您必須保護 hello 叢集。 Hello 叢集中執行生產工作負載時，安全性是特別重要。 本文說明如何在 hello 中使用 Windows 安全性的 tooconfigure 節點對節點和用戶端對節點安全性*追蹤*檔案。  hello 程序對應 toohello 設定的安全性步驟[建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)。 如需有關 Service Fabric 如何使用 Windows 安全性的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。

> [!NOTE]
> 因為沒有從一個安全性選擇 tooanother 含叢集升級，您應該仔細思考 hello 選取的節點到節點的安全性。 toochange hello 安全性選取項目，您有 toorebuild hello 完整的叢集。
>
>

## <a name="configure-windows-security-using-gmsa"></a>使用 gMSA 設定 Windows 安全性  
hello 範例*ClusterConfig.gMSA.Windows.MultiMachine.JSON*下載組態檔，以 hello [Microsoft.Azure.ServiceFabric.WindowsServer。<version>。zip](http://go.microsoft.com/fwlink/?LinkId=730690)獨立叢集封裝包含的範本設定使用 Windows 安全性[群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **組態設定** | **說明** |  
| --- | --- |  
| WindowsIdentities |包含 hello 叢集和用戶端識別。 |  
| ClustergMSAIdentity |設定節點對節點安全性。 群組受管理服務帳戶。 |  
| ClusterSPN |gMSA 帳戶的完整網域名稱 SPN|  
| ClientIdentities |設定用戶端對節點安全性。 用戶端使用者帳戶的陣列。 |  
| 身分識別 |hello 用戶端身分識別，網域使用者。 |  
| IsAdmin |True 會指定該 hello 網域使用者具有系統管理員用戶端存取，讓使用者用戶端存取，則為 false。 |  
  
[節點 toonode 安全性](service-fabric-cluster-security.md#node-to-node-security)蒻謔設定**ClustergMSAIdentity**當 service fabric 需要 toorun 下 gMSA。 在訂單 toobuild 節點之間的信任關係，他們必須撰寫知道彼此的存在。 即可達成這兩個不同的方式： 指定 hello 群組受管理的服務帳戶，其中包含 hello 叢集中的所有節點，或指定都包含 hello 叢集中的所有節點的 hello 網域電腦群組。 我們強烈建議使用 hello[群組受管理服務帳戶 (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)方法，特別是針對較大叢集 （10 個以上的節點），或可能 toogrow 或縮小叢集。  
這個方法不需要 hello 建立網域群組的叢集系統管理員已授與存取權限 tooadd 和移除成員。 進行自動密碼管理時，這些帳戶也很有用。 如需詳細資訊，請參閱 [開始使用群組受管理的服務帳戶](http://technet.microsoft.com/library/jj128431.aspx)。  
 
[用戶端 toonode 安全性](service-fabric-cluster-security.md#client-to-node-security)已設定為使用**ClientIdentities**。 在用戶端與 hello 叢集之間的順序 tooestablish 信任，您必須設定 hello 叢集 tooknow 可以信任哪些用戶端身分識別。 這可以在兩個不同的方式完成： 指定 hello 網域群組使用者可以連接，或指定 hello 網域節點使用者可以連線。 Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集： 系統管理員和使用者。 存取控制提供 hello hello 能力叢集系統管理員 toolimit 存取 toocertain 類型的使用者，使 hello 叢集更安全的不同群組的叢集操作。  系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。 如需存取控制的詳細資訊，請參閱[角色型存取控制 (適用於 Service Fabric 用戶端)](service-fabric-cluster-security-roles.md)。  
 
下列範例 hello**安全性**區段設定使用 gMSA 的 Windows 安全性，並指定該 hello 機器中*ServiceFabric.clusterA.contoso.com* gMSA 屬於 hello 叢集，*CONTOSO\usera*具有系統管理員用戶端存取權：  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>使用電腦群組設定 Windows 安全性  
hello 範例*ClusterConfig.Windows.MultiMachine.JSON*下載組態檔，以 hello [Microsoft.Azure.ServiceFabric.WindowsServer。<version>。zip](http://go.microsoft.com/fwlink/?LinkId=730690)獨立叢集封裝包含的範本設定 Windows 安全性。  Windows 安全性設定中 hello**屬性**> 一節： 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **組態設定** | **說明** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType**設定得*Windows*如果 ClusterIdentity 指定 Active Directory 電腦群組名稱。 |  
| ServerCredentialType |設定得*Windows* tooenable 用戶端的 Windows 安全性。<br /><br />這表示 hello hello 叢集和 hello 叢集本身的用戶端正在執行 Active Directory 網域內。 |  
| WindowsIdentities |包含 hello 叢集和用戶端識別。 |  
| ClusterIdentity |使用電腦群組名稱、 domain\machinegroup、 tooconfigure 節點對節點安全性。 |  
| ClientIdentities |設定用戶端對節點安全性。 用戶端使用者帳戶的陣列。 |  
| 身分識別 |加入 hello 網域使用者，網域 \ 使用者名稱，如 hello 用戶端身分識別。 |  
| IsAdmin |Hello 網域使用者的設定 tootrue toospecify 具有系統管理員用戶端存取權或 false，供使用者用戶端存取。 |  

[節點 toonode 安全性](service-fabric-cluster-security.md#node-to-node-security)已設定使用**ClusterIdentity**如果您想 toouse Active Directory 網域內的電腦群組。 如需詳細資訊，請參閱[在 Active Directory 中建立電腦群組 (Create a Machine Group in Active Directory)](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx)。

[用戶端對節點安全性](service-fabric-cluster-security.md#client-to-node-security)是使用 **ClientIdentities** 來設定的。 tooestablish 之間的信任的用戶端與 hello 叢集中，您必須設定 hello 叢集 tooknow hello 用戶端 hello 叢集的身分識別可以信任。 您可以透過兩種不同方式建立信任︰

- 指定可以連接的 hello 網域群組使用者。
- 指定可以連接的 hello 網域節點使用者。

Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集： 系統管理員和使用者。 存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 類型的叢集操作的不同使用者群組，這會讓 hello 叢集更安全。  系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。  

下列範例 hello**安全性**區段設定 Windows 安全性，以指定該 hello 機器*ServiceFabric/clusterA.contoso.com*是 hello 叢集的一部分，並指定該*CONTOSO\usera*具有系統管理員用戶端存取權：

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> 不應在網域控制站上部署 Service Fabric。 請確定追蹤不會不使用電腦群組時，包含 hello hello 網域控制站的 IP 位址或群組受管理的服務帳戶 (gMSA)。
>
>

## <a name="next-steps"></a>後續步驟
在 hello 中設定 Windows 安全性之後*追蹤*檔案時，請繼續 hello 叢集建立程序中的[建立在 Windows 上執行的獨立叢集](service-fabric-cluster-creation-for-windows-server.md)。

如需有關節點對節點安全性、用戶端對節點安全性和角色型存取控制的詳細資訊，請參閱[叢集安全性案例](service-fabric-cluster-security.md)。

請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)如需使用 PowerShell 或 FabricClient 連接的範例。
