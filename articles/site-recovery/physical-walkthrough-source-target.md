---
title: "hello 來源和目標與 Azure Site Recovery 的實體伺服器複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset 以 hello Azure Site Recovery 服務的實體伺服器 tooAzure 存放裝置複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>步驟 7： 設定 hello 來源和目標的實體伺服器複寫 tooAzure

本文說明如何 tooconfigure 來源和目標設定複寫時使用在內部實體伺服器 tooAzure hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

設定 hello 組態伺服器、 註冊在保存庫 hello 和探索電腦。

1. 按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。
2. 如果您沒有設定伺服器，請按一下 [+設定伺服器]。
3. 在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。
4. 下載 hello Site Recovery 整合安裝程式安裝檔案。
5. 下載 hello 保存庫註冊金鑰。 您會在執行統一安裝時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

   ![設定來源](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Hello 保存庫中註冊伺服器 hello 組態

請勿 hello 下列之前啟動，然後執行整合安裝 tooinstall hello 組態伺服器、 hello 處理序伺服器，以及 hello 主要目標伺服器。 hello 視訊描述 hello VMware VM tooAzure 複寫元件的設定。 不過，hello 相同的程序僅適用於實體伺服器 tooAzure 複寫。

- 在 hello 組態伺服器 VM，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。 應該相符。 如果快慢誤差 15 分鐘，安裝可能會失敗。
- Hello 組態伺服器電腦上執行安裝程式做為本機系統管理員。
- 請確定 hello VM 上啟用 TLS 1.0。


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> 也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。




## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

您設定 hello 目標環境之前，請確定您有 Azure 儲存體帳戶和虛擬網路設定。

1. 按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。
2. 指定目標部署模型是以 Resource Manager 為基礎或傳統。
3. Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。

   ![目標](./media/physical-walkthrough-source-target/gs-target.png)

4. 如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**，toocreate 資源管理員帳戶或網路內嵌。

## <a name="next-steps"></a>後續步驟

跳過[步驟 8： 設定複寫原則](physical-walkthrough-replication.md)
