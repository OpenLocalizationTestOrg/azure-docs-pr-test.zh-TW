---
title: "在 Azure 中的 SQL Server 的考量 aaaSecurity |Microsoft 文件"
description: "本主題提供一般指導方針來保護在 Azure 虛擬機器中執行的 SQL Server。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server 安全性考量

本主題包含協助建立 Azure 虛擬機器 (VM) 中的安全存取 tooSQL 伺服器執行個體的整體安全性指導方針。

Azure 符合多種業界規範及標準，可讓您 toobuild 相容解決方案與 SQL Server 虛擬機器中執行。 如需 Azure 的法規相符性資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/)。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>控制存取 toohello SQL VM

當您建立您的 SQL Server 虛擬機器時，請考慮如何 toocarefully 控制誰可以存取 toohello 電腦和 tooSQL 伺服器。 一般情況下，您應該做下列 hello:

- 限制存取 tooSQL 伺服器 tooonly hello 應用程式與需要的用戶端。
- 遵循用來管理使用者帳戶和密碼的最佳做法。

下列各節的 hello 考慮這些點上提供建議。

## <a name="secure-connections"></a>安全連線

當您建立 SQL Server 虛擬機器圖庫映像時，hello **SQL Server 連接性**選項可讓您 hello 選擇**（在 VM) 內本機**，**私用 （在虛擬網路）**，或**公用 （網際網路）**。

![SQL Server 連線](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Hello 最佳的安全性，請選擇 hello 最嚴格的選項，您的案例。 例如，如果您正在存取 SQL Server 的應用程式然後 hello 相同的 VM**本機**hello 最安全的選擇。 如果您正在執行的 Azure 應用程式需要存取 toohello SQL Server，然後**私人**保護通訊 tooSQL 伺服器只在指定的 hello [Azure 虛擬網路](../../../virtual-network/virtual-networks-overview.md)。 如果您需要**公用**(internest) 存取 toohello SQL Server VM，然後請確定 toofollow 其他最佳作法在這個主題 tooreduce 攻擊面。

hello hello 入口網站中選取的選項使用連入的安全性規則 hello Vm 上[網路安全性群組](../../../virtual-network/virtual-networks-nsg.md)(NSG) tooallow 或拒絕網路流量 tooyour 虛擬機器。 您可以修改或建立新的輸入的 NSG 規則 tooallow 流量 toohello SQL Server 連接埠 （預設值 1433年）。 您也可以指定特定 toocommunicate 允許透過此連接埠的 IP 位址。

![網路安全性群組規則](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

此外 tooNSG 規則 toorestrict 網路流量，您也可以使用 Windows 防火牆 hello hello 虛擬機器上。

如果您使用端點與 hello 傳統部署模型，移除 hello 虛擬機器上的任何端點，如果您不要使用它們。 如需有關使用具有端點 Acl 的指示，請參閱[端點上的管理 hello ACL](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint)。 不需要使用 hello 資源管理員的 Vm。

最後，請考慮啟用 hello Azure 的虛擬機器中的 hello SQL Server Database Engine 執行個體的加密的連接。 使用簽署的憑證設定 SQL Server 執行個體。 如需詳細資訊，請參閱[啟用加密連接 toohello Database Engine](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine)和[連接字串語法](https://msdn.microsoft.com/library/ms254500.aspx)。

## <a name="use-a-non-default-port"></a>使用非預設連接埠

根據預設，SQL Server 會在已知的通訊埠 1433 上接聽。 為了提高安全性，請在非預設連接埠，例如 1401年上設定 SQL Server toolisten。 如果您佈建 hello Azure 入口網站中的 SQL Server 組件庫映像，您可以指定此連接埠 hello **SQL Server 設定**刀鋒視窗。

tooconfigure 此佈建之後，您有兩個選項：

- 針對資源管理員的 Vm，您可以選取**SQL Server 組態**從 hello VM 概觀刀鋒視窗。 這可讓選擇 toochange hello 連接埠。

  ![在入口網站中變更 TCP 連接埠](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- 傳統的 Vm 或 hello 入口網站未佈建的 SQL Server Vm，您可以從遠端連線 toohello VM 來手動設定 hello 連接埠。 Hello 組態步驟，請參閱[特定 TCP 通訊埠上設定伺服器 tooListen](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port)。 如果您使用此手動技巧，您也需要 tooadd Windows 防火牆規則 tooallow 連入流量的 TCP 連接埠上。

> [!IMPORTANT]
> 指定非預設連接埠是個不錯的主意，如果您的 SQL Server 連接埠是開啟 toopublic 網際網路連線。

SQL Server 是在非預設連接埠上接聽，您必須指定 hello 連接埠，當您連線時。 例如，假設其中 hello 伺服器 IP 位址是 13.55.255.255，而 SQL Server 接聽連接埠 1401年。 tooconnect tooSQL 伺服器，您會指定`13.55.255.255,1401`hello 連接字串中。

## <a name="manage-accounts"></a>管理帳戶

您不想攻擊者 tooeasily 猜測帳戶名稱或密碼。 使用下列秘訣 toohelp hello:

- 建立不是名為 **Administrator**的唯一本機系統管理員帳戶。

- 為您的所有帳戶使用複雜的強式密碼。 如需有關如何 toocreate 強式密碼，請參閱[建立強式密碼](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password)發行項。

- 根據預設，Azure 會在 SQL Server 虛擬機器安裝期間選取 Windows 驗證。 因此，hello **SA**已停用登入和安裝程式會指派密碼。 我們建議您該 hello **SA**登入不應該用或啟用。 如果您必須具有 SQL 登入，請使用下列策略 hello 的其中一個：

  - 使用具有 **sysadmin** 成員資格的唯一名稱建立 SQL 帳戶。 您可以從 hello 入口網站啟用**SQL 驗證**佈建期間。

    > [!TIP] 
    > 如果您在佈建期間未啟用 SQL 驗證，您必須手動變更 hello 驗證模式太**SQL Server 和 Windows 驗證模式**。 如需詳細資訊，請參閱 [變更伺服器驗證模式](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode)。

  - 如果您必須使用 hello **SA**登入，啟用 hello 登入之後佈建並指派新的增強式密碼。

## <a name="follow-on-premises-best-practices"></a>遵循內部部署最佳做法

此外，本主題中所述的 toohello 作法建議您檢閱並實作 hello 傳統內部部署安全性作法，在適用情況。 如需詳細資訊，請參閱 [SQL Server 安裝的安全性考量](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>後續步驟

如果您也想了解關於效能的最佳作法，請參閱 [Azure 虛擬機器中 SQL Server 的效能最佳作法](virtual-machines-windows-sql-performance.md)。

如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。

