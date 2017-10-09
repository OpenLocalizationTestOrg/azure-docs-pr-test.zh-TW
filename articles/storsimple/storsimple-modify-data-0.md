---
title: "aaaModify hello DATA 0 上的 StorSimple 裝置的設定 |Microsoft 文件"
description: "深入了解如何 toouse Windows PowerShell for StorSimple tooreconfigure hello StorSimple 裝置上的 DATA 0 網路介面。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>修改您的 StorSimple 裝置上 hello DATA 0 網路介面設定
## <a name="overview"></a>概觀
Microsoft Azure StorSimple 裝置有六個網路介面，從 DATA 0 tooDATA 5。 hello DATA 0 介面一律透過 hello Windows PowerShell 介面或 hello 序列主控台中，設定，而且自動具備雲端功能。 請注意，您無法設定 DATA 0 網路介面，透過 hello Azure 傳統入口網站。 

hello DATA 0 介面先 hello 安裝精靈的 hello StorSimple 裝置的初始部署時設定。 作業模式 hello 裝置時，您可能需要 tooreconfigure DATA 0 的設定。 本教學課程提供兩種方法 toomodify DATA 0 網路設定，同時透過 Windows PowerShell for StorSimple。

閱讀本教學課程之後，您將能夠：

* 修改 DATA 0 網路設定透過 hello 安裝精靈
* 修改 DATA 0 網路設定，透過 hello `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>透過安裝精靈修改 DATA 0 網路設定
您可以重新設定 DATA 0 網路設定，連線 toohello 您的 StorSimple 裝置的 Windows PowerShell 介面並啟動安裝精靈工作階段。 執行下列步驟 toomodify DATA 0 的 hello 設定：

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>透過安裝精靈的 toomodify DATA 0 網路設定
1. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 當系統提示您提供 hello**裝置系統管理員密碼**。 hello 預設密碼為`Password1`。
2. 在 hello 命令提示字元中輸入：
   
    `Invoke-HcsSetupWizard`
3. 安裝程式精靈 隨即出現 toohelp 設定 hello DATA 0 介面，您的裝置。 提供新值給 hello IP 位址、 閘道和網路遮罩。

> [!NOTE]
> 固定的控制器 Ip 將需要重新設定透過 hello toobe hello**設定**hello 的 StorSimple 裝置 hello Azure 傳統入口網站中的頁面。 如需詳細資訊，請移至太[修改網路介面](storsimple-modify-device-config.md#modify-network-interfaces)。
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>透過 Set-HcsNetInterface cmdlet 修改 DATA 0 網路設定
替代方式 tooreconfigure DATA 0 網路介面是透過 hello hello 使用`Set-HcsNetInterface`cmdlet。 hello cmdlet 會從您的 StorSimple 裝置 hello Windows PowerShell 介面執行。 當使用此程序，也可以這裡設定 hello 控制器固定 Ip。 執行下列步驟 toomodify hello DATA 0 的 hello 設定： 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>透過 hello Set-hcsnetinterface cmdlet toomodify DATA 0 網路設定
1. 在 hello 序列主控台功能表中，選擇選項 1，**登入的完整存取**。 當系統提示您提供 hello 裝置系統管理員密碼。 hello 預設密碼為`Password1`。
2. 在 hello 命令提示字元中輸入：
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    在 hello 角度方括號中，輸入下列值的 DATA 0 的 hello:
   
   * IPv4 位址
   * IPv4 閘道
   * IPv4 子網路遮罩
   * 控制器 0 的固定的 IPv4 位址
   * 控制器 1 的固定的 IPv4 位址
     
     如需 hello 使用這個指令程式的詳細資訊，請移至太[Windows PowerShell for StorSimple cmdlet 參考](https://technet.microsoft.com/library/dn688161.aspx)。

## <a name="next-steps"></a>後續步驟
* tooconfigure 不同於 DATA 0 網路介面，您可以使用 hello [hello Azure 傳統入口網站中的 [設定] 頁面](storsimple-modify-device-config.md)。 
* 如果您遇到任何問題，設定您的網路介面時，請參閱太[部署問題進行疑難排解](storsimple-troubleshoot-deployment.md)。

