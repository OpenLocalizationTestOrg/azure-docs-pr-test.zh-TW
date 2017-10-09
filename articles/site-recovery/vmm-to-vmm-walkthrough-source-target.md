---
title: "aaaSet hello 來源和目標 HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "描述如何 tooset hello 來源及目標時複寫 HYPER-V Vm toosecondary VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>步驟 6： 設定 hello 複寫來源和目標


之後建立復原服務保存庫的 HYPER-V 複寫 tooa 次要 VMM 站台使用[Azure Site Recovery](site-recovery-overview.md)、 使用此發行項 tooset hello 來源和目標位置複寫。 

閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。




## <a name="set-up-hello-source-environment"></a>設定 hello 來源環境

Hello Azure Site Recovery Provider 安裝 VMM 伺服器上探索和 hello 保存庫中註冊伺服器。

1. 按一下 [步驟 1：準備基礎結構]  >  [來源]。

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. 在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. 在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件](#prerequisites).
4. 下載 hello Azure Site Recovery Provider 安裝檔案。
5. 下載 hello 登錄機碼。 您會在執行安裝程式時用到此金鑰。 hello 金鑰有效期為您產生它之後的五天。

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Hello VMM 伺服器上安裝 hello Azure Site Recovery Provider。 您不需要 tooexplicitly 則會在 HYPER-V 主機伺服器上安裝任何項目。


## <a name="install-hello-azure-site-recovery-provider"></a>安裝 Azure Site Recovery Provider hello

1. 執行每一部 VMM 伺服器上的 hello 提供者安裝程式檔案。 如果 VMM 部署在叢集中，請勿遵循您所安裝的第一次 hello hello:
    -  Hello 提供者上安裝的作用中的節點，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。
    - 然後，hello 提供者上安裝 hello 其他節點。 叢集節點應該執行所有 hello 相同版本的 hello 提供者。
2. 安裝程式會執行幾個必要條件檢查，並要求權限 toostop hello VMM 服務。 hello VMM 服務將會自動重新啟動安裝程式完成時。 如果您安裝在 VMM 叢集上，您提示的 toostop hello 叢集角色。
3. 在**Microsoft Update**，您也可以選擇 toospecify，根據 Microsoft Update 原則安裝 provider 更新。
4. 在**安裝**接受或修改 hello 預設安裝位置，然後按**安裝**。

    ![安裝位置](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. 安裝已完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。

    ![安裝位置](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. 在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。 按一下 [下一步] 。

    ![伺服器註冊](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. 在**網際網路連線**，指定 hello hello VMM 伺服器上執行的提供者如何連接 tooAzure。

    ![網際網路設定](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - 您可以指定該 hello 提供者應該連接直接 toohello 網際網路，或透過 proxy。
   - 指定 proxy 設定 (如有需要)。
   - VMM RunAs 帳戶 (DRAProxyAccount) 如果您使用 proxy，使用指定的 hello 自動會建立 proxy 認證。 設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。 hello RunAs 帳戶的設定可以修改 hello VMM 主控台中 >**設定** > **安全性** > **執行身分帳戶**。 重新啟動 hello VMM 服務 tooupdate 變更。
8. 在**登錄機碼**，選取您從 Azure Site Recovery 下載並複製 toohello VMM 伺服器的 hello 索引鍵。
9. 只有在您要在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時，才會使用 hello 加密設定。 如果您要複寫 tooa 次要站台不使用它。
10. 在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。 在叢集組態中指定 hello VMM 叢集角色名稱。
11. 在**同步處理雲端中繼資料**，選取是否要在 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端的 toosynchronize 中繼資料。 這個動作只需要 toohappen 每部伺服器上一次。 如果您不想 toosynchronize 所有雲端，您可以不勾選，此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。
12. 按一下**下一步**toocomplete hello 程序。 註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。 hello 伺服器顯示在 [hello **VMM 伺服器**] 索引標籤上 hello**伺服器**hello 保存庫中的頁面。

    ![伺服器](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Hello 伺服器可以使用在 hello 站台復原主控台中之後, 在**來源** > **準備來源**hello VMM 伺服器，並選取 hello 雲端中的 hello HYPER-V 主機所在的選取。 然後按一下 [確定] 。

您也可以從 hello 命令列安裝 hello 提供者：

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Hello 目標環境設定

選取 hello 目標 VMM 伺服器和雲端：

1. 按一下**準備基礎結構** > **目標**，和您想要 toouse hello 選取目標 VMM 伺服器。
2. 將會顯示 hello 伺服器上會同步處理與 Site Recovery 的雲端。 選取 hello 目標雲端。

   ![目標](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>後續步驟

跳過[步驟 7： 設定網路對應](vmm-to-vmm-walkthrough-network-mapping.md)。
