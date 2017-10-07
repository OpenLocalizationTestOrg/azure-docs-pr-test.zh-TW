---
title: "有效的 Azure 虛擬機器上的 SQL Server 的 aaaManage 成本 |Microsoft 文件"
description: "選擇 hello 右 SQL Server 虛擬機器定價模型提供最佳作法。"
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>SQL Server Azure VM 的定價指導方針

本主題提供 Azure 中 SQL Server 虛擬機器的定價指導方針。 有幾個選項會影響成本，而且重要 toopick hello 右側影像成本的商務需求之間取得平衡。

## <a name="free-licensed-sql-server-editions"></a>免費授權的 SQL Server 版本

如果您想 toodevelop，測試，或建立概念證明，然後使用 hello 釋出授權**SQL Server Developer edition**。 這個版本的所有項目已在 SQL Server Enterprise edition 中，因此您可以使用它 toobuild 任何您想要的應用程式。 在生產環境中就不允許 toorun。 SQL Server 開發人員 VM 了 hello hello VM，不適用於 SQL Server 授權成本時，將只會收取費用。

如果您想要在生產環境中的輕量工作負載 toorun (< 4 核心，< 1 GB 的記憶體 < 10 GB/資料庫)，然後使用 釋放授權 hello **SQL Server Express edition**。 SQL Express 的 VM 將會只收取 hello VM，hello 成本不 SQL 授權。

針對這些開發/測試或輕量型生產環境工作負載，您也可以選擇符合這些工作負載的較小 VM 大小來節省成本。 hello DS1v2 可能是不錯的選擇，這些工作負載。

toocreate SQL Server 2016 Azure VM 與其中一個這些映像，請參閱下列連結查看 hello:

- [SQL Server 2016 Developer Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [SQL Server 2016 Express Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>付費的 SQL Server 版本

如果您有非輕量型生產工作負載時，使用下列 SQL Server 版本的 hello 的其中一個：

| SQL Server 版本 | 工作負載 |
|-----|-----|
| Web | 小型網站 |
| 標準 | 小型 toomedium 工作負載 |
| Enterprise | 大型或任務關鍵性工作負載|

您有兩個選項 toopay 對於這些版本的 SQL Server 授權：*每使用量付費*或*自備授權*。

### <a name="pay-per-usage"></a>依使用量付費

**每個使用量付費 hello SQL Server 授權**表示執行 hello Azure VM 中的 hello 每分鐘成本包括 hello hello 的 SQL Server 授權成本。 您可以看到 hello 定價 hello 不同 SQL Server 版本 （Web、 Standard、 Enterprise） 在 hello [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)。 hello 成本是 hello 相同的所有版本的 SQL Server (2008 R2 too2016)。 一般情況下，授權 hello 與 SQL Server 授權成本的每分鐘視 hello VM 核心的數目。

支付 hello SQL Server 授權使用量每則建議基於：

- 暫時或定期的工作負載。 例如，應用程式需要 toosupport 事件在幾個月的每個年份或業務分析，從星期一。
- 存留期或規模不明的工作負載。 例如，有幾個月不需用到或依需求可能需要較多或較少運算能力的應用程式。

toocreate SQL Server 2016 Azure VM 與其中一個這些支付每次使用量映像，請參閱下列連結查看 hello:

- [SQL Server 2016 Web Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [SQL Server 2016 Standard Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> 當您在 hello Azure 入口網站中建立 SQL Server 虛擬機器時，hello 估計 hello 上顯示的每月成本**大小選擇 「**刀鋒視窗中不包含 SQL Server 授權成本。 這是 hello VM 單獨 hello 成本。
>
> ![選擇 VM 大小刀鋒視窗](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Hello 釋出授權 Express 和 Developer edition 的 SQL Server，這是 hello 總估計的成本。 但如 Web、 Standard 和 Enterprise，hello 尋找其他 SQL 授權成本上 hello [Windows 虛擬機器定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/windows/)。 在 hello 定價頁面，選取您目標的 SQL Server 版本。

### <a name="bring-your-own-license-byol"></a>自備授權 (BYOL)

**攜帶您自己的 SQL Server 授權的授權流動性透過**，也稱為 tooas **BYOL**、 使用現有的 SQL Server 大量授權與 Azure VM 中的軟體保證的方式。 假設您已取得授權和軟體保證透過大量授權方案 hello 執行成本的 hello VM，不適用於 SQL Server 授權，只會收取使用 BYOL 的 SQL Server VM。

針對下列情況，建議採用透過「授權行動性」自備 SQL 授權：

- 持續性工作負載。 例如，需要 toosupport 24x7 的企業營運應用程式。
- 存留期和規模已知的工作負載。 例如，hello 整個年度和已預測哪些需求將需要的應用程式。

toouse BYOL 與 SQL Server VM，您必須擁有的授權 SQL Server Standard 或 Enterprise 和[軟體保證](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1)，這是必要的選項，透過一些[大量授權](https://www.microsoft.com/en-us/download/details.aspx?id=10585)程式以及選用性購買與其他人。  hello 定價提供透過大量授權方案層級會根據合約和 hello 數量，或承諾 tooSQL 伺服器 hello 類型而不同。 但根據經驗法則，請為攜帶自己的授權以連續生產工作負載具有 hello 下列優點：

| BYOL 優點 | 說明 |
|-----|-----|
| **節省成本** | 如果工作負載將持續執行 SQL Server Standard 或 Enterprise 長達「10 個月以上」的時間，則與依使用量付費相比，自備 SQL Server 授權較符合經濟效益。 |
| **長期節省** | 平均而言，它是*便宜每年的 30%* toobuy 或更新 SQL Server 授權 hello，第一個 3 年。 此外，3 年之後，您不需要 toorenew hello 授權失效，for Software Assurance 的只是付費。 屆時，將可「節省 200% 的費用」。 |
| **免費的被動次要複本** | 攜帶您自己的授權的另一個優點為 hello[免費授權一個被動的次要複本](https://azure.microsoft.com/pricing/licensing-faq/)每部 SQL Server 的高可用性 」 用途。 這在授權 （例如，使用 Alwayson 可用性群組） 的高可用性 SQL Server 部署的成本的一半 hello 剪下。 透過 hello 容錯移轉伺服器軟體保證權益提供 hello 權限 toorun hello 被動次要資料庫。 |

toocreate SQL Server 2016 Azure VM 與其中一個這些帶您-擁有-授權映像，請參閱加上"{BYOL}"hello Vm:

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [SQL Server 2016 Standard Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> 請在 10 天內告訴我們您將在 Azure 中使用多少個 SQL Server 授權。 hello 連結 toohello 先前映像具有指示如何 toodo 這。

## <a name="avoid-unecessary-costs"></a>避免不必要的費用

如果您將不會持續執行的任何工作負載，請考慮在 hello 非作用中期間關閉 hello 虛擬機器。 您只需依據使用量付費。

例如，如果您只嘗試在 Azure VM 上的 SQL Server 時，您不想 tooincur 費用意外保留週中執行它。 其中一個解決方案是 toouse hello[自動關閉功能](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)。

![SQL VM 自動關閉](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

自動關閉是 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab) 所提供的較大一組相似功能的一部分。

針對其他工作負載，請考慮使用指令碼解決方案 (例如 [Azure 自動化](https://azure.microsoft.com/services/automation/)) 來自動關閉並重新啟動 Azure VM。

> [!IMPORTANT]
> 正在關閉和解除配置 VM 是 hello 唯一方式 tooavoid 費用。 只停止，或使用電源選項 tooshut 向 hello VM 仍會產生使用費用。

## <a name="next-steps"></a>後續步驟

如需一般的 Azure 定價指導方針，請參閱[使用 Azure 計費與成本管理避免非預期的成本](../../../billing/billing-getting-started.md)。

Hello 最新的虛擬機器定價，包括 SQL Server，請參閱 hello [Azure VM 定價頁面](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)。

請檢閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)中的其他「SQL Server 虛擬機器」主題。
