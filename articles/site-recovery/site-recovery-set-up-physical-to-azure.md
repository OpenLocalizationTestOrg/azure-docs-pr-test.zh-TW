---
title: "設定 hello 來源環境 (實體伺服器 tooAzure) |Microsoft 文件"
description: "本文說明如何註冊您複寫至 Azure 中執行 Windows 或 Linux 實體伺服器的內部部署環境 toostart tooset。"
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>設定 hello 來源環境 (實體伺服器 tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [實體 tooAzure](./site-recovery-set-up-physical-to-azure.md)

本文說明如何註冊您複寫至 Azure 中執行 Windows 或 Linux 實體伺服器的內部部署環境 toostart tooset。

## <a name="prerequisites"></a>必要條件

hello 文章假設您已經：
1. 復原服務保存庫中 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。
3. 哪些 tooinstall hello 組態伺服器上的實體電腦。

### <a name="configuration-server-minimum-requirements"></a>組態伺服器最低需求
hello 下表列出 hello 最低硬體、 軟體和組態伺服器的網路需求。
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Hello 組態伺服器不支援 HTTPS 為基礎的 proxy 伺服器。

## <a name="choose-your-protection-goals"></a>選擇您的保護目標

1. 在 hello Azure 入口網站，移 toohello**復原服務**保存庫刀鋒視窗，然後選取您的保存庫。
2. 在 hello**資源**功能表 hello 保存庫中，按一下**入門** > **Site Recovery** > **步驟 1： 準備基礎結構** > **保護目標**。

    ![選擇目標](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. 中**保護目標**，選取**tooAzure**和**未虛擬化/其他**，然後按一下**確定**。

    ![選擇目標](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

1. 在**準備來源**，如果您不需要設定伺服器，按一下  **+ 設定伺服器**tooadd 其中一個。

  ![設定來源](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. 在 hello**新增伺服器**刀鋒視窗中，檢查**組態伺服器**會出現在**伺服器類型**。
4. 下載 hello Site Recovery 整合安裝程式安裝檔案。
5. 下載 hello 保存庫註冊金鑰。 當您執行整合安裝程式時，您會需要 hello 註冊金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. 在您使用當作 hello 組態伺服器 hello 機器上執行**Azure Site Recovery 整合安裝**tooinstall hello 組態伺服器、 hello 處理序伺服器和 hello 主要目標伺服器。

#### <a name="run-azure-site-recovery-unified-setup"></a>執行 Azure Site Recovery 統一安裝

> [!TIP]
> 組態伺服器註冊失敗，則電腦的系統時鐘 hello 時間超過五分鐘從本機時間。 同步處理您的系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)開始 hello 安裝之前。

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> hello 組態伺服器可以透過命令列安裝。 如需詳細資訊，請參閱[使用命令列工具安裝組態伺服器](http://aka.ms/installconfigsrv)。


## <a name="common-issues"></a>常見問題

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>後續步驟

下一個步驟是在 Azure 中[設定目標環境](./site-recovery-prepare-target-physical-to-azure.md)。
