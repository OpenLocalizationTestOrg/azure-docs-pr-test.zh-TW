---
title: "aaaSecure Service Fabric 叢集 |Microsoft 文件"
description: "說明 Service Fabric 叢集和 hello 所用的不同技術 tooimplement hello 安全性案例的情況。"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 26b58724-6a43-4f20-b965-2da3f086cf8a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: chackdan
ms.openlocfilehash: 249a9e85b8fbe174e2accee85a94d95b2872a3af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-security-scenarios"></a>Service Fabric 叢集安全性案例
Service Fabric 叢集是您所擁有的資源。 叢集必須是安全的 tooprevent 未經授權的使用者連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載。 雖然可能 toocreate 不安全的叢集，這樣做可讓匿名使用者 tooconnect tooit，如果它會公開管理端點 toohello 公用網際網路。 

本文概述 hello 安全性案例的叢集在 Azure 或獨立執行，且 hello 各種所用技術 tooimplement 的情況。 hello 叢集安全性案例包括：

* 節點對節點安全性
* 用戶端對節點安全性
* 角色型存取控制 (RBAC)

## <a name="node-to-node-security"></a>節點對節點安全性
保護 hello Vm 或 hello 叢集中的機器之間的通訊。 這可確保只有授權的 toojoin hello 叢集的電腦可以參與裝載應用程式和服務 hello 叢集中。

![節點對節點通訊的圖表][Node-to-Node]

在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://msdn.microsoft.com/library/ff649801.aspx)或針對 Windows Server 機器使用 [Windows 安全性](https://msdn.microsoft.com/library/ff649396.aspx)。

### <a name="node-to-node-certificate-security"></a>節點對節點憑證安全性
服務網狀架構會使用 X.509 伺服器憑證，當您建立叢集時，您指定為 hello 節點型別組態的一部分。 這篇文章的 hello 結尾會提供這些憑證是什麼，以及如何取得，或建立它們的快速概觀。

憑證的安全性設定時建立 hello 叢集透過 hello Azure 入口網站、 Azure Resource Manager 範本或獨立 JSON 範本。 您可以指定用於憑證變換的主要憑證和選用次要憑證。 hello 您指定的主要和次要憑證應不同於 hello 管理用戶端以及您針對指定的唯讀用戶端憑證[用戶端對節點安全性](#client-to-node-security)。

讀取 Azure[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)toolearn tooconfigure 憑證安全性在叢集中的方式。

對於獨立 Windows Server，請參閱 [使用 X.509 憑證保護 Windows 上的獨立叢集 ](service-fabric-windows-cluster-x509-security.md)

### <a name="node-to-node-windows-security"></a>節點對節點 Windows 安全性
對於獨立 Windows Server，請參閱 [使用 Windows 安全性保護 Windows 上的獨立叢集](service-fabric-windows-cluster-windows-security.md)

## <a name="client-to-node-security"></a>用戶端對節點安全性
驗證用戶端，及保護在用戶端與 hello 叢集中的個別節點之間的通訊。 這種類型的安全性驗證，並保護可確保只有授權的使用者可以存取 hello 叢集和 hello 叢集上部署的 hello 應用程式的用戶端通訊。 用戶端是透過其 Windows 安全性認證或其憑證安全性認證唯一識別。

![用戶端對節點通訊的圖表][Client-to-Node]

在 Azure 上執行的叢集或在 Windows 上執行的獨立叢集可以使用[憑證安全性](https://msdn.microsoft.com/library/ff649801.aspx)或 [Windows 安全性](https://msdn.microsoft.com/library/ff649396.aspx)。

### <a name="client-to-node-certificate-security"></a>用戶端對節點憑證安全性
 用戶端對節點憑證的安全性設定時指定的系統管理員用戶端憑證及/或使用者的用戶端憑證，藉以建立 hello 叢集透過 hello Azure 入口網站中，資源管理員範本或獨立 JSON 範本。  hello 管理用戶端和使用者用戶端憑證指定應該與不同 hello 主要和次要憑證指定為[節點對節點安全性](#node-to-node-security)最佳作法。 根據預設，hello 叢集節點的安全性憑證會加入 toohello 允許用戶端管理的憑證清單。

連接 toohello 叢集使用 hello 管理憑證的用戶端具有完整存取 toomanagement 功能。  連接 toohello 叢集使用 hello 唯讀使用者用戶端憑證的用戶端擁有讀取權限 toomanagement 功能。 亦即這些憑證用於 hello 角色基底存取控制 (RBAC) 本文稍後所述。

讀取 Azure[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)toolearn tooconfigure 憑證安全性在叢集中的方式。

對於獨立 Windows Server，請參閱 [使用 X.509 憑證保護 Windows 上的獨立叢集 ](service-fabric-windows-cluster-x509-security.md)

### <a name="client-to-node-azure-active-directory-aad-security-on-azure"></a>Azure 上的用戶端對節點 Azure Active Directory (AAD)
在 Azure 上執行的叢集也可以保護存取使用 Azure Active Directory (AAD) toohello 管理端點。 請參閱[設定叢集，利用 Azure 資源管理員範本](service-fabric-cluster-creation-via-arm.md)如需如何 toocreate hello 需要 AAD 成品時，如何 toopopulate 期間叢集建立和 tooconnect toothose 之後叢集的方式。

## <a name="security-recommendations"></a>安全性建議
Azure 的叢集，建議您使用用戶端的安全性 tooauthenticate AAD 和憑證節點對節點的安全性。

對於獨立 Windows Server 叢集，如果您有 Windows Server 2012 R2 和 Active Directory，建議您使用 Windows 安全性與群組管理帳戶 (GMA)。 否則仍然使用 Windows 安全性與 Windows 帳戶。

## <a name="role-based-access-control-rbac"></a>角色型存取控制 (RBAC)
存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。 兩個不同的存取控制項類型支援連接 tooa 叢集的用戶端： 系統管理員角色和使用者角色。

系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。

您指定 hello 系統管理員和使用者用戶端角色 hello 叢集建立時提供不同的身分識別 （憑證，AAD 等） 針對每個。 如需有關 hello 預設存取控制設定，以及如何 toochange hello 預設設定的詳細資訊，請參閱[角色型存取控制服務網狀架構用戶端](service-fabric-cluster-security-roles.md)。

## <a name="x509-certificates-and-service-fabric"></a>X.509 憑證和 Service Fabric
X.509 數位憑證是常用的 tooauthenticate 用戶端和伺服器與 tooencrypt 以及數位簽署訊息。 如需有關這些憑證的詳細資訊，請移至太[使用憑證](http://msdn.microsoft.com/library/ms731899.aspx)。

一些重要事項 tooconsider:

* 執行生產環境工作負載之叢集中所使用的憑證應該是使用已正確設定的 Windows Server 憑證服務來建立，或是從已核准的 [憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority)取得。
* 絕對不要在生產環境中使用以 MakeCert.exe 這類工具建立的暫時或測試憑證。
* 您可以使用自我簽署憑證，但應該只用於測試叢集，不應該在生產環境中使用。

### <a name="server-x509-certificates"></a>伺服器的 X.509 憑證
伺服器憑證有 hello 主要工作就是驗證伺服器 （節點） tooclients，或驗證伺服器 （節點） tooa 伺服器 （節點）。 Toocheck hello 值 hello hello [主旨] 欄位中的一般名稱的其中一個 hello 初始檢查時用戶端或節點來驗證節點。 此一般名稱或其中一個 hello 憑證的主體別名中必須要有 hello 的允許通用名稱的清單。

hello 下列文章說明如何 toogenerate 憑證的主體別名 (SAN): [tooadd 主旨替代名稱 tooa 如何安全 LDAP 的憑證](http://support.microsoft.com/kb/931351)。

hello 主旨欄位只能包含數個值，每一個加上初始化 tooindicate hello 實值型別。 Hello 初始化大多數情況下，"CN"為一般名稱。例如，"CN = www.contoso.com"。 它也可能會 hello 主旨欄位 toobe 空白。 如果已填入 hello 選擇性主體替代名稱欄位，則必須包含 hello hello 憑證一般名稱和每個主體替代名稱的一個項目。 這些會被輸入為 DNS 名稱值。

hello hello hello 憑證使用目的欄位值應該包含適當的值，例如 「 伺服器驗證 」 或 「 用戶端驗證 」。

### <a name="client-x509-certificates"></a>用戶端 X.509 憑證
用戶端憑證通常不是由第三方憑證授權單位所發行。 相反地，hello hello 目前使用者位置的個人存放區通常包含用戶端憑證放在該處根授權單位，與目的為 「 用戶端驗證 」。 hello 用戶端需要相互驗證時，可以使用這類憑證。

> [!NOTE]
> Service Fabric 叢集上的所有管理作業都需要伺服器憑證。 用戶端憑證無法用於管理作業。
> 
> 

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->


## <a name="next-steps"></a>後續步驟
本文提供與叢集安全性有關的概念資訊。 接下來，


1.  [使用 Resource Manager 範本在 Azure 中建立叢集](service-fabric-cluster-creation-via-arm.md) 
2.  [Azure 入口網站](service-fabric-cluster-creation-via-portal.md)。

<!--Image references-->
[Node-to-Node]: ./media/service-fabric-cluster-security/node-to-node.png
[Client-to-Node]: ./media/service-fabric-cluster-security/client-to-node.png
