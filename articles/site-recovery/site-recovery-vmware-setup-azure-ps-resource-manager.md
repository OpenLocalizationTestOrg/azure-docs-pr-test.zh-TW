---
title: " 管理在 Azure 中執行的處理伺服器 (Resource Manager) | Microsoft Doc"
description: "本文說明如何 tooset 向上容錯回復程序 （資源管理員） 在 Azure 中。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>管理在 Azure 中執行的處理伺服器 (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [傳統](./site-recovery-vmware-setup-azure-ps-classic.md)

容錯回復期間建議 toodeploy 處理序伺服器在 Azure 中的如果有高延遲 hello Azure 虛擬網路與內部部署網路之間。 本文說明如何設定、 設定和管理在 Azure 中執行的 hello 處理序伺服器。

> [!NOTE]
> 本文是如果您使用使用 toobe**資源管理員**為 hello 虛擬機器在容錯移轉期間的 hello 部署模型。 如果您使用**傳統**為 hello 部署模型，請依照下列中的 hello 步驟[如何 tooset 向上及設定容錯移轉處理伺服器 （傳統）](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>必要條件

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>在 Azure 上部署處理伺服器
1. 在 hello 保存庫 > **Site Recovery 基礎結構**（在 hello 「 管理 」 標題） >**設定伺服器**（在 「 適用於 VMware 和實體機器 」 標題下），選取 hello 組態伺服器。
2. 在開啟的 hello 組態伺服器詳細資料頁面中按一下"+ 處理伺服器 」

  ![新增處理伺服器資源庫](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  在 hello**新增處理序伺服器**頁面上，選取下列值的 hello

  ![新增處理伺服器資源庫項目](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**欄位名稱**|**值**|
|-|-|
|選擇您希望 toodeploy 處理序伺服器|選取 hello 值**部署在 Azure 中的容錯回復處理序伺服器** |
|訂用帳戶|選取 hello 容錯 hello 虛擬機器的 Azure 訂用帳戶|
|資源群組|您可以建立資源群組 toodeploy 此處理序伺服器，或在現有的資源群組中選擇 toodeploy hello 處理序伺服器|
|位置|Hello Azure 資料中心選取成哪一個 hello 虛擬機器在容錯移轉至|
|Azure 網路|選取 hello Azure hello 虛擬機器的虛擬 Network(VNet) 容錯移轉到其中。 如果將虛擬機器容錯回復到多個 Azure VNet，則您需要在每個 VNet 上部署一部處理伺服器|

4. 在 hello 之處理序伺服器 hello 屬性 hello 其餘部分填滿

  ![新增處理伺服器摘要](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**欄位名稱**|**值**|
|-|-|
|伺服器名稱|處理伺服器虛擬機器的顯示名稱與主機名稱|
| 使用者名稱|會成為該虛擬機器上系統管理員的使用者名稱|
|儲存體帳戶|Hello 放置 hello 虛擬機器的虛擬磁碟的儲存體帳戶的名稱|
|子網路|hello hello Azure VNet toowhich hello 虛擬機器的子網路連線|
| IP 位址|IP 位址，您想要的 hello 處理序伺服器 tooassume 一次它開機。|
5. 按一下 hello 「 確定 」 按鈕 toostart hello 處理序伺服器的虛擬機器部署。

> [!NOTE]
> toobe 無法 toouse 此處理序伺服器進行容錯回復，您需要 tooregister 它與 hello 在內部部署組態伺服器。

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>註冊 hello 處理序伺服器 （在 Azure 中執行） tooa 組態伺服器 （執行內部部署）

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>升級 hello 處理序伺服器 toolatest 版本。

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>取消註冊 hello 處理序伺服器 （在 Azure 中執行），從組態伺服器 （執行內部部署）

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
