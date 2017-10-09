---
title: "設定 hello 來源環境 (VMware tooAzure) |Microsoft 文件"
description: "本文說明如何 tooset 上您在內部部署環境 toostart 複寫 VMware 虛擬機器 tooAzure。"
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>設定 hello 來源環境 (VMware tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [實體 tooAzure](./site-recovery-set-up-physical-to-azure.md)

本文說明如何 tooset 上您在內部部署環境 toostart 複寫虛擬機器正在執行 VMware tooAzure 上。

## <a name="prerequisites"></a>必要條件

hello 文件假設您已經建立：
- 復原服務保存庫中 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。
- 您 VMware vCenter 中可用來進行[自動探索](./site-recovery-vmware-to-azure.md)的專用帳戶。
- 哪些 tooinstall hello 組態伺服器上的虛擬機器。

## <a name="configuration-server-minimum-requirements"></a>組態伺服器最低需求
hello 設定伺服器軟體應該部署在高可用性的 VMware 虛擬機器。 hello 下表列出 hello 最低硬體、 軟體和組態伺服器的網路需求。
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Hello 組態伺服器不支援 HTTPS 為基礎的 proxy 伺服器。

## <a name="choose-your-protection-goals"></a>選擇您的保護目標

1. 在 hello Azure 入口網站，移 toohello**復原服務**保存庫刀鋒視窗，並選取您的保存庫。
2. 在 hello hello 保存庫的資源功能表上，前往 太**入門** > **Site Recovery** > **步驟 1： 準備基礎結構** > **保護目標**。

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. 在**保護目標**，選取**tooAzure**，然後選擇 **是的與 VMware vSphere Hypervisor**。 然後按一下 [確定] 。

    ![選擇目標](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境
設定 hello 來源環境牽涉到兩個主要的活動：

- 安裝組態伺服器並向 Site Recovery 服務註冊。
- 探索您的內部部署虛擬機器連線站台復原 tooyour 在內部部署 VMware vCenter 或 vSphere EXSi 主機。

### <a name="step-1-install-and-register-a-configuration-server"></a>步驟 1：安裝及註冊組態伺服器

1. 按一下 [步驟 1：準備基礎結構]  >  [來源]。 在**準備來源**，如果您不需要設定伺服器，按一下  **+ 設定伺服器**tooadd 其中一個。

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. 在 hello**新增伺服器**刀鋒視窗中，請檢查**組態伺服器**會出現在**伺服器類型**。
4. 下載 hello Site Recovery 整合安裝程式安裝檔案。
5. 下載 hello 保存庫註冊金鑰。 當您執行整合安裝程式時，您會需要 hello 註冊金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. 在您使用當作 hello 組態伺服器 hello 機器上執行**Azure Site Recovery 整合安裝**tooinstall hello 組態伺服器、 hello 處理序伺服器和 hello 主要目標伺服器。

#### <a name="run-azure-site-recovery-unified-setup"></a>執行 Azure Site Recovery 統一安裝

> [!TIP]
> 如果您電腦的系統時鐘 hello 時間不同於當地時間超過五分鐘，組態伺服器註冊將會失敗。 同步處理您的系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)開始 hello 安裝之前。

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> hello 組態伺服器可以透過命令列安裝。 如需詳細資訊，請參閱[安裝 hello 設定伺服器使用命令列工具](http://aka.ms/installconfigsrv)。

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>新增自動探索的 hello VMware 帳戶

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>步驟 2：新增 vCenter
在內部部署環境中執行 tooallow Azure Site Recovery toodiscover 虛擬機器，您需要 tooconnect，您的 VMware vCenter Server 或 vSphere ESXi 主機與 Site Recovery。

選取**+ vCenter** toostart VMware vCenter server 或 VMware vSphere ESXi 主機連接。

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>常見問題
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>後續步驟
在 Azure 中[設定您的目標環境](./site-recovery-prepare-target-vmware-to-azure.md)。
