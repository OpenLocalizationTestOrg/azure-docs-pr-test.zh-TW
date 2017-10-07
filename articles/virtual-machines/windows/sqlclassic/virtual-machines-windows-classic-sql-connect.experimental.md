---
title: "aaaConnect tooa Azure （傳統） 上的 SQL Server 虛擬機器 |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 伺服器在 Azure 中的虛擬機器上執行。 本主題使用 hello 傳統部署模型。 hello 案例 hello 網路設定與 hello 用戶端 hello 位置而有所不同。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 9577e4bdad79435e34a64fc669ec4848649fc945
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>連接 tooa Azure （傳統部署） 上的 SQL Server 虛擬機器
> [!div class="op_single_selector"]
> * [資源管理員](../sql/virtual-machines-windows-sql-connect.md)
> * [傳統](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>概觀
本主題描述如何 tooconnect tooyour SQL Server 執行個體在 Azure 虛擬機器上執行。 其中涵蓋一些[一般連線案例](#connection-scenarios)並提供[在 Azure VM 中設定 SQL Server 連線的詳細步驟](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 如果您使用資源管理員的 Vm，請參閱[連接 tooa 使用資源管理員的 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-sql-connect.md)。

## <a name="connection-scenarios"></a>連接案例
hello 方式用戶端連接的 tooSQL 虛擬機器上執行的伺服器 hello hello 的用戶端和 hello 電腦/網路組態的位置而有所不同。 這些案例包括：

* [連接 tooSQL 伺服器 hello 在相同雲端服務](#connect-to-sql-server-in-the-same-cloud-service)
* [連接 tooSQL 伺服器 hello 透過網際網路](#connect-to-sql-server-over-the-internet)
* [連接中 hello tooSQL 伺服器相同的虛擬網路](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> 在連線與任何一種方法之前，您必須遵循 hello[此發行項 tooconfigure 連接中的步驟](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>連接 tooSQL 伺服器 hello 在相同雲端服務
多部虛擬機器中可建立 hello 相同雲端服務。 toounderstand 此虛擬機器案例中，請參閱[如何 tooconnect 虛擬機器與虛擬網路或雲端服務](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service)。 在此案例中，一部虛擬機器上的用戶端會嘗試執行 tooconnect tooSQL 伺服器 hello 內的另一部虛擬機器上相同雲端服務。

在此案例中，您可以使用連線 hello VM**名稱**(也會顯示為**電腦名稱**或**hostname** hello 入口網站中)。 這是您在建立期間提供 hello VM hello 名稱。 例如，如果您已命名為您的 SQL VM **mysqlvm**，hello 可以使用相同的雲端服務中的用戶端 VM hello 下列連接字串 tooconnect:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>連線透過網際網路 hello tooSQL 伺服器
如果您想從 hello 網際網路 tooconnect tooyour SQL Server 資料庫引擎，您必須建立虛擬機器端點內送 TCP 通訊。 這個 Azure 組態步驟，指示內送 TCP 連接埠流量 tooa TCP 通訊埠是可存取 toohello 虛擬機器。

透過 tooconnect hello 網際網路，您必須使用 hello VM 的 DNS 名稱和 hello VM 端點連接埠號碼 （本文中稍後設定）。 toofind hello DNS 名稱，瀏覽 toohello Azure 入口網站，然後選取**虛擬機器 （傳統）**。 然後選取您的虛擬機器。 hello **DNS 名稱**如下所示 hello**概觀**> 一節。

例如，假設名為 **mysqlvm** 的傳統虛擬機器，其 DNS 名稱為 **mysqlvm7777.cloudapp.net**，且 VM 端點是 **57500**。 假設已正確設定的連線，下列連接字串 hello 可能是從任何地方使用的 tooaccess hello 虛擬機器上 hello 網際網路：

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

雖然這個連接字串啟用用戶端的連線，透過 hello 網際網路，這不表示任何人都可以連線 tooyour SQL Server。 外部用戶端具備 toohello 正確的使用者名稱和密碼。 為了增加安全性，請勿將 hello 已知通訊埠 1433年用於 hello 公用虛擬機器端點。 如果可能，請考慮您端點 toorestrict 流量只有 toohello 用戶端上您允許新增 ACL。 如需有關使用具有端點 Acl 的指示，請參閱[端點上的管理 hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。

> [!NOTE]
> 您可以使用這個技巧 toocommunicate 搭配 SQL Server，hello Azure 資料中心內的所有傳出資料時，主體 toonormal[上輸出資料傳輸定價](https://azure.microsoft.com/pricing/details/data-transfers/)。
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>連接中 hello tooSQL 伺服器相同的虛擬網路
[虛擬網路](../../../virtual-network/virtual-networks-overview.md) 讓其他案例變得可行。 您可以在相同虛擬網路，即使這些 Vm 存在於不同的雲端服務中的 hello 連接 Vm。 [站對站 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)可讓您建立能將 VM 連接至內部部署網路和電腦的混合式架構。

虛擬網路也可讓您 toojoin 您的 Azure Vm tooa 網域。 網域聯結 tooa 是唯一的方式 toouse hello 與 SQL Server 的 Windows 驗證。 hello 其他連線案例則需要 SQL 驗證的使用者名稱和密碼。

如果您計劃 tooconfigure 網域環境及 Windows 驗證，您不需要 tooconfigure hello 公用端點或 hello SQL 驗證和登入。 在此案例中，您可以藉由指定 hello 連接字串中的 hello SQL Server VM 名稱連接 tooyour SQL Server 執行個體。 hello 下列範例會假設已設定了 Windows 驗證，而且該 hello 使用者已授與存取 toohello SQL Server 執行個體。

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Azure VM 中設定 SQL Server 連線的步驟
hello 下列步驟示範如何透過 tooconnect toohello SQL Server 執行個體 hello 網際網路使用 SQL Server Management Studio (SSMS)。 不過，hello 相同的步驟套用 toomaking SQL Server 虛擬機器可對於您的應用程式中，然後再執行這兩個內部部署和 Azure 中存取。

您可以從另一個 VM 連接 toohello SQL Server 執行個體或 hello 網際網路之前，您必須完成下列工作的 hello:

* [建立 hello 虛擬機器的 TCP 端點](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Hello Windows 防火牆中開啟 TCP 通訊埠](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [設定 SQL Server toolisten hello TCP 通訊協定](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [設定 SQL Server 以進行混合模式驗證](#configure-sql-server-for-mixed-mode-authentication)
* [建立 SQL Server 驗證登入](#create-sql-server-authentication-logins)
* [判斷 hello hello 虛擬機器的 DNS 名稱](#determine-the-dns-name-of-the-virtual-machine)
* [從另一部電腦連接 toohello Database Engine](#connect-to-the-database-engine-from-another-computer)

下列圖表中的 hello 的摘要 hello 連線路徑：

![連接 tooa SQL Server 虛擬機器](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>後續步驟
如果您打算也針對高可用性和災害復原 toouse AlwaysOn 可用性群組，您應該考慮實作接聽程式。 資料庫用戶端連線 toohello 接聽程式，而非直接 tooone hello SQL Server 執行個體。 hello 接聽程式路由用戶端 toohello 主要複本 hello 可用性群組中。 如需詳細資訊，請參閱 [設定 Azure 中 AlwaysOn 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。

很重要的 tooreview 所有 hello 適用於 Azure 的虛擬機器上執行的 SQL Server 的安全性最佳作法。 如需詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 安全性考量](../sql/virtual-machines-windows-sql-security.md)。

[瀏覽 hello 學習路徑](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/)Azure 虛擬機器上的 SQL server。 

如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

