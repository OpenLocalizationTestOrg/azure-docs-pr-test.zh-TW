---
title: "aaaHow tootroubleshoot 常見問題 VHD 建立期間 |Microsoft 文件"
description: "答案 toocommon 疑難排解問題，並在 VHD 建立期間發出。"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>VHD 建立期間遇到 tootroubleshoot 一般問題的方式
這篇文章會提供 toohelp Azure Marketplace 發行者及/或共同管理員可能會遇到的問題或已發行或管理其虛擬機器的方案時的常見問題。

1. 如何變更 hello hello 主機名稱？
   
    一旦建立 VM 之後，使用者無法更新 hello hello 主機名稱。
2. 如何 tooreset hello 遠端桌面服務或其登入密碼嗎？
   
   * [Windows VM 的參考](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Linux VM 的參考](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. 如何新 toogenerate ssh 憑證嗎？
   
   請參閱 toohello 連結： [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. 如何開啟的 VPN 憑證 tooconfigure 嗎？
   
   請參閱 toohello 連結： [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. Hello hello Microsoft Azure 虛擬機器環境 （基礎結構做為服務） 中執行 Microsoft 伺服器軟體的支援原則為何？
   
   請參閱 toohello 連結： [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. 虛擬機器是否有任何唯一識別碼？
   
   Azure 會編碼每個 VM 中的 Azure VM 唯一識別碼。 請參閱這個部落格和文件中的詳細資料。
7. 在 VM 中如何管理 hello hello 啟動工作中的自訂指令碼延伸？
   
   請參閱 toohello 連結： [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. 如何將 VM 從 Azure 入口網站中，使用 hello hello 之 VHD 的 toocreate 上傳 toopremium 儲存體？
   
   我們尚未支援這項功能。
9. Hello Azure Marketplace 中支援的 32 位元應用程式？
   
   如需 hello 支援原則的詳細資訊，請參閱 toohello 連結： [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. 每當我試著 toocreate 映像從我的 Vhd，我會收到 hello 錯誤 」。VHD 已向映像儲存機制 hello 資源為 「 在 PowerShell 中。 我之前未建立任何映像，也在 Azure 中找不到任何具有這個名稱的映像。 如何解決這個問題？
    
    如果 hello 使用者佈建 VM，以透過這個 VHD，而且該 VHD 上沒有鎖定，這通常會發生。 請確認未從這個 VHD 配置任何 VM。 如果 hello 錯誤仍然存在，則請引發支援票證，請使用以下連結或從 hello 發行這個入口網站 （hello 回應的問題 11 下提供詳細資料）。
