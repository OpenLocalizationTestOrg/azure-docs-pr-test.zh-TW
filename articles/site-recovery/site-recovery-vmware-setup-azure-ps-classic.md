---
title: " 管理在 Azure 中執行的處理伺服器 (傳統) | Microsoft Docs"
description: "本文說明如何 tooset 容錯回復程序 Server(Classic) 在 Azure 上的。"
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>管理在 Azure 中執行的處理伺服器 (傳統)
> [!div class="op_single_selector"]
> * [Azure 傳統](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [資源管理員](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

容錯回復期間建議 toodeploy 在 Azure 中的處理序伺服器是否有高延遲 hello Azure 虛擬網路與內部部署網路之間。 本文說明如何設定、 設定和管理在 Azure 中執行的 hello 處理序伺服器。

> [!NOTE]
> 本文是 toobe 如果您使用傳統做 hello 部署模型為 hello 虛擬機器在容錯移轉期間使用。 如果您使用資源管理員部署模型後續 hello 步驟中的 hello[如何 tooset 向上及設定容錯移轉處理伺服器 （資源管理員）](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>必要條件

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>在 Azure 上部署處理伺服器

1. 在 Azure Marketplace 中建立虛擬機器使用 hello **Microsoft Azure 站台復原處理序伺服器 V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. 請確定您選取做為 hello 部署模型**傳統** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. 在 hello 建立虛擬機器精靈 > 基本設定，請確定您選取 hello 訂用帳戶和位置 toowhere 您容錯 hello 虛擬機器。</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. 請確認 hello 虛擬機器已連線 toohello Azure 虛擬網路 toowhich hello 容錯移轉虛擬機器已連線。</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Hello 處理序伺服器的虛擬機器已佈建之後，您需要在 toolog，並向 hello 組態伺服器。

> [!NOTE]
> toobe 無法 toouse 此處理序伺服器進行容錯回復，您需要 tooregister 它與 hello 在內部部署組態伺服器。

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>註冊 hello （在 Azure 中執行） 的處理序伺服器 tooa 組態伺服器 （執行內部部署）

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Hello 處理序伺服器 toolatest 版本升級。

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>正在移除註冊 hello 處理序伺服器 （在 Azure 中執行） 從組態伺服器 （執行內部部署）

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
