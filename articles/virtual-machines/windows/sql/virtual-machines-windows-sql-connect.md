---
title: "aaaConnect tooa SQL Server 虛擬機器 （資源管理員） |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 伺服器在 Azure 中的虛擬機器上執行。 本主題使用 hello 傳統部署模型。 hello 案例 hello 網路設定與 hello 用戶端 hello 位置而有所不同。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器
> [!div class="op_single_selector"]
> * [資源管理員](virtual-machines-windows-sql-connect.md)
> * [傳統](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>概觀

本主題描述如何 tooconnect tooyour SQL Server 執行個體在 Azure 虛擬機器上執行。 其中涵蓋一些[一般連線案例](#connection-scenarios)並提供[在 Azure VM 中設定 SQL Server 連線的詳細步驟](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm)。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

如需有關佈建和連線能力的完整逐步解說，請參閱 [在 Azure 上佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

## <a name="connection-scenarios"></a>連接案例

hello 方式用戶端連接的 tooSQL 虛擬機器上執行的伺服器 hello hello 的用戶端和 hello 網路設定的位置而有所不同。

如果您佈建 hello Azure 入口網站中的 SQL Server VM，您會有 hello 選項指定 hello 類型**SQL 連接性**。

![佈建期間的公用 SQL 連線能力選項](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

連線能力的選項包括：

| 選項 | 說明 |
|---|---|
| **公開** | 連接 tooSQL 伺服器 hello 透過網際網路 |
| **私用** | 連接中 hello tooSQL 伺服器相同的虛擬網路 |
| **本機** | 連接本機上 hello tooSQL 伺服器相同的虛擬機器 | 

hello 下列各節說明 hello**公用**和**私人**更多詳細資料中的選項。

## <a name="connect-toosql-server-over-hello-internet"></a>連線透過網際網路 hello tooSQL 伺服器

如果您想從 hello 網際網路 tooconnect tooyour SQL Server 資料庫引擎，請選取**公用**hello **SQL 連接性**hello 入口網站佈建期間中的型別。 自動 hello 入口網站未 hello 下列步驟：

* 讓 SQL Server 中的 hello TCP/IP 通訊協定。
* 設定防火牆規則 tooopen hello SQL Server TCP 連接埠 （預設值 1433年）。
* 可進行公用存取所需的 SQL Server 驗證。
* 設定網路安全性群組 hello hello hello SQL Server 連接埠上的 VM tooall TCP 流量。

> [!IMPORTANT]
> SQL Server Developer hello 虛擬機器映像和 Express 版本不會自動啟用 hello TCP/IP 通訊協定。 開發人員和 Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#manualtcp)之後建立 hello VM。

任何具有網際網路存取權的用戶端可以藉由指定 hello 虛擬機器的 hello 公用 IP 位址或 toothat IP 位址指定給任何 DNS 標籤連接 toohello SQL Server 執行個體。 Hello SQL Server 連接埠為 1433年，如果您不需要 toospecify hello 連接字串中。 下列連接字串 hello 與 DNS 標籤連接 tooa SQL VM 的`sqlvmlabel.eastus.cloudapp.azure.com`使用 SQL 驗證 （您也可以使用 hello 公用 IP 位址）。

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

雖然這會啟用連線用戶端透過 hello 網際網路，這不表示任何人都可以連線 tooyour SQL Server。 外部用戶端具備 toohello 正確的使用者名稱和密碼。 不過，為了增加安全性，您可以避免 hello 已知通訊埠 1433年。 比方說，如果您設定 SQL Server toolisten 上通訊埠 1500年建立適當的防火牆和網路安全性群組規則，您無法藉由附加 hello 通訊埠編號 toohello 伺服器名稱連接。 hello 下列範例會改變 hello 前一個藉由加入自訂連接埠編號， **1500年**，toohello 伺服器名稱：

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> 當您查詢在 VM 中的 SQL Server 透過 hello 網際網路，所有傳出資料從 hello Azure 資料中心是主體 toonormal[上輸出資料傳輸定價](https://azure.microsoft.com/pricing/details/data-transfers/)。

## <a name="connect-toosql-server-within-a-virtual-network"></a>連接虛擬網路內 tooSQL 伺服器

當您選擇**私人**hello **SQL 連接性**hello Azure 入口網站中的型別會設定大部分相同的 hello 設定太**公用**。 hello 其中一種差異是沒有任何網路安全性群組規則 tooallow 外 hello SQL Server 連接埠 （預設值 1433年） 上的流量。

> [!IMPORTANT]
> SQL Server Developer hello 虛擬機器映像和 Express 版本不會自動啟用 hello TCP/IP 通訊協定。 開發人員和 Express 版本中，您必須用於 SQL Server 組態管理員太[手動啟用 hello TCP/IP 通訊協定](#manualtcp)之後建立 hello VM。

私用連線能力通常與[虛擬網路](../../../virtual-network/virtual-networks-overview.md)搭配使用，可進行數個情節。 您可以在相同虛擬網路，即使這些 Vm 存在於不同的資源群組中的 hello 連接 Vm。 [站對站 VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)可讓您建立能將 VM 連接至內部部署網路和電腦的混合式架構。

虛擬網路也可讓您 toojoin 您的 Azure Vm tooa 網域。 這是 hello 唯一方式 toouse Windows 驗證 tooSQL 伺服器。 hello 其他連線案例則需要 SQL 驗證的使用者名稱和密碼。

假設您已在虛擬網路中設定 DNS，您可以藉由指定 hello 連接字串中的 hello SQL Server VM 的電腦名稱連接 tooyour SQL Server 執行個體。 下列範例也 hello 假設也已經設定 Windows 驗證，且該 hello 使用者已獲得存取 toohello SQL Server 執行個體。

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>變更 SQL 連線能力設定

您可以變更 hello Azure 入口網站中的 SQL Server 虛擬機器 hello 連線設定。

1. 在 hello Azure 入口網站，選取 **虛擬機器**。

2. 選取 SQL Server VM。

3. 在 [設定] 下，按一下 [SQL Server 組態]。

4. 變更 hello **SQL 連線層級**tooyour 所需的設定。 您可以選擇性地使用此區域 toochange hello SQL Server 連接埠或 hello SQL 驗證設定。

   ![變更 SQL 連線能力](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. 請等候幾分鐘的時間 hello 更新 toocomplete。

   ![SQL VM 更新通知](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> 針對 Developer 和 Express 版本啟用 TCP/IP

變更 SQL Server 連線設定，Azure 不會自動啟用 hello TCP/IP 通訊協定的 SQL Server Developer edition 和 Express edition。 hello 執行下列步驟說明如何 toomanually 啟用 TCP/IP 時，讓您可以從遠端連線的 IP 位址。

首先，使用遠端桌面連接 toohello SQL Server 電腦。

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

接下來，啟用 hello TCP/IP 通訊協定與**SQL Server 組態管理員**。

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>以 SSMS 連線

hello 下列步驟顯示如何 toocreate 選擇性 DNS 加上標籤的 Azure VM，然後連接的 SQL Server Management Studio (SSMS)。

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>後續步驟

toosee 佈建的指示，以及這些連線的步驟，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。
