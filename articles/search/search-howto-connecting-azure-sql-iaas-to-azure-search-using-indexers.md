---
title: "aaaSQL VM 連接 tooAzure 搜尋 |Microsoft 文件"
description: "啟用加密的連接和 Azure 虛擬機器 (VM) 從 Azure 搜尋索引子上設定 hello 防火牆 tooallow 連線 tooSQL 伺服器。"
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>在 Azure VM 上設定來自 Azure 搜尋索引子 tooSQL 伺服器的連接
如中所述[連接 Azure SQL Database tooAzure 搜尋使用索引子](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq)，建立針對索引子**Azure Vm 上的 SQL Server** (或**SQL Azure Vm**縮寫) 是Azure 搜尋所支援但有一些安全性相關的必要條件 tootake care of 第一個。 

**工作持續時間：**約 30 分鐘，假設您已經 hello VM 上安裝憑證。

## <a name="enable-encrypted-connections"></a>啟用加密的連線
Azure 搜尋服務會針對透過公用網際網路連接的所有索引子要求加密的通道。 此區段會列出 hello 步驟 toomake 這項工作。

1. 檢查 hello hello 憑證 tooverify hello 主體名稱屬性的 hello Azure VM 的 hello 完整的網域名稱 (FQDN)。 您可以使用這類工具 CertUtils 或 hello 憑證嵌入式管理單元 tooview hello 屬性。 您可以從 hello VM 服務刀鋒視窗的基本資訊區段中，在 hello 取得 hello FQDN**公用 IP 位址 /DNS 名稱標籤**欄位中，以 hello [Azure 入口網站](https://portal.azure.com/)。
   
   * 對於使用 hello 較新建立的 Vm**資源管理員**hello FQDN 會格式化為範本， `<your-VM-name>.<region>.cloudapp.azure.com`。 
   * 對於較舊的 Vm 建立為**傳統**VM，hello FQDN 格式為`<your-cloud-service-name.cloudapp.net>`。 
2. 設定 SQL Server toouse hello 憑證使用 hello 登錄編輯程式 (regedit)。 
   
    雖然通常會在這項工作中使用 SQL Server 組態管理員，但您在此案例中無法使用它。 它不會尋找 hello 匯入憑證，因為 hello hello Azure 上的 VM 的 FQDN 不符合 hello 由 hello （它會識別為 hello 本機電腦或它所聯結的 hello 網路網域 toowhich hello 網域） 的 VM 的 FQDN。 名稱不相符，當使用 regedit toospecify hello 憑證。
   
   * 在 regedit 中瀏覽 toothis 登錄機碼： `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`。
     
     hello`[MSSQL13.MSSQLSERVER]`一部分視版本和執行個體名稱。 
   * 設定 hello hello 值**憑證**金鑰 toohello**指紋**hello toohello VM 已匯入的 SSL 憑證。
     
     一些較有數種方式 tooget hello 指紋。 如果複製 hello**憑證**嵌入式管理單元 MMC 中，您可能拾取不可見的前置字元[支援本文中所述](https://support.microsoft.com/kb/2023869/)，當您嘗試時導致錯誤連接。 有數個因應措施可修正此問題。 最簡單的 hello toobackspace 透過且然後重新輸入 hello 的 hello 指紋 tooremove hello 前置字元在 regedit hello 索引鍵的值欄位中的第一個字元。 或者，您可以使用不同的工具 toocopy hello 指紋。
3. 授與權限 toohello 服務帳戶。 
   
    請確定 hello SQL Server 服務帳戶會授與適當的權限 hello 私密金鑰 hello SSL 憑證。 如果您忽略此步驟，SQL Server 將會無法啟動。 您可以使用 hello**憑證**嵌入式管理單元或**CertUtils**這項工作。
4. 重新啟動 hello SQL Server 服務。

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>在 hello VM 中設定 SQL Server 連線
您 hello 加密連接 Azure 搜尋所需的設定之後，有額外的設定步驟內建 tooSQL Azure Vm 上的伺服器。 如果還沒有這麼做，hello 下一個步驟是使用其中一個這些文件 toofinish 組態：

* 如**資源管理員**VM，請參閱[連接 tooa 使用資源管理員的 Azure 上的 SQL Server 虛擬機器](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md)。 
* 如**傳統**VM，請參閱[連接 SQL Server 虛擬機器，在 Azure 傳統 tooa](../virtual-machines/windows/classic/sql-connect.md)。

特別是，檢閱 hello > 一節中的每一個發行項"透過連線 hello 網際網路"。

## <a name="configure-hello-network-security-group-nsg"></a>設定網路安全性群組 (NSG) hello
不是異常 tooconfigure hello NSG 和對應的 Azure 端點或存取控制清單 (ACL) toomake 您 Azure VM 存取 tooother 合作對象。 有可能是您完成此動作之前 tooallow 您自己的應用程式邏輯 tooconnect tooyour SQL Azure VM。 它是相同的 Azure 搜尋連線 tooyour SQL Azure VM。 

hello 下列連結提供 NSG VM 部署組態的指示。 使用這些指示 tooACL Azure 搜尋端點根據其 IP 位址。

> [!NOTE]
> 若為背景，請參閱 [什麼是網路安全性群組？](../virtual-network/virtual-networks-nsg.md)
> 
> 

* 如**資源管理員**VM，請參閱[如何 toocreate Nsg ARM 部署](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。 
* 如**傳統**VM，請參閱[如何 toocreate Nsg 傳統部署](../virtual-network/virtual-networks-create-nsg-classic-ps.md)。

IP 位址，可能會造成會容易克服，如果您知道的 hello 問題和可能的因應措施的一些挑戰。 hello 其餘各節提供處理問題相關的 tooIP 位址 hello ACL 中的建議。

#### <a name="restrict-access-toohello-search-service-ip-address"></a>限制存取 toohello 搜尋服務 IP 位址
我們強烈建議您限制您 hello ACL 中的搜尋服務的 hello 存取 toohello IP 位址，而不是做出寬開啟 tooany 連線要求您 SQL Azure Vm。 您可以輕鬆地找出 hello IP 位址 ping hello FQDN (例如， `<your-search-service-name>.search.windows.net`) 的搜尋服務。

#### <a name="managing-ip-address-fluctuations"></a>管理 IP 位址的變動
如果您的搜尋服務有只有一個搜尋單位 （也就是一個複本和一個資料分割），hello IP 位址將會變更期間常式服務重新啟動時，讓失效搜尋服務的 IP 位址與現有 ACL 中。

其中一種方式 tooavoid hello 後續連線錯誤是 toouse 超過一個複本和 Azure 搜尋中的一個資料分割。 這樣做會增加 hello 成本，但它也可以解決 hello IP 位址的問題。 在 Azure 搜尋服務中，當您有多個搜尋單位時，IP 位址不會變更。

第二種方法是 tooallow hello 連接 toofail，，然後再重新設定 hello NSG 中的 hello Acl。 平均而言，您可以預期 IP 位址 toochange 每隔幾週。 對於頻繁地進行控制編製索引的客戶，此方法可能可行。

第三個可行的 （但不是 hello 的特別安全的） 方法是 hello 的 toospecify hello IP 位址範圍搜尋服務 hello 的佈建的 Azure 區域。 hello IP 範圍清單的公用 IP 位址配置 tooAzure 資源從中發行在[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>包括 hello Azure 搜尋入口網站的 IP 位址
如果您使用 hello Azure 入口網站 toocreate 索引子，Azure 搜尋入口網站的邏輯會建立期間也需要存取 tooyour SQL Azure VM。 Ping `stamp2.search.ext.azure.com`，即可找到 Azure 搜尋服務入口網站 IP 位址。

## <a name="next-steps"></a>後續步驟
使用超出 hello 方式設定時，您現在可以指定 SQL Server 在 Azure VM 上 hello Azure 搜尋索引子的資料來源。 請參閱[連接 Azure SQL Database tooAzure 搜尋使用索引子](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)如需詳細資訊。

