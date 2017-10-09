---
title: "aaaChange 密碼透過 StorSimple 裝置管理員 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple Manager 服務 toochange StorSimple Snapshot Manager 」 和 「 裝置系統管理員密碼。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f178509c-f4e1-48a8-90b2-d4ad050eeb30
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b2836eb4d3a05e1d2a5eeeeefe66c75f63ba38ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toochange-your-storsimple-passwords"></a>使用 hello StorSimple Manager 服務 toochange StorSimple 密碼
## <a name="overview"></a>概觀
hello Azure 傳統入口網站**設定**頁面包含您可以重新設定 StorSimple Manager 服務所管理的 StorSimple 裝置的所有 hello 裝置參數。 本教學課程說明如何使用 hello**設定**頁面 toochange，您的裝置系統管理員或 StorSimple Snapshot Manager 密碼。

## <a name="change-hello-device-administrator-password"></a>變更 hello 裝置系統管理員密碼
當您使用 Windows PowerShell 介面 tooaccess hello StorSimple 裝置時，您就需要的 tooenter 裝置系統管理員密碼。 當服務中註冊第一個 StorSimple 裝置 hello 時，此介面的 hello 預設密碼是*Password1*。 Hello 資料的安全性，您對於需要的 toochange 這個密碼 hello hello 註冊程序的結尾。 您無法結束 hello 註冊程序，而不需要變更這個密碼。 如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。

第一次設定透過 hello Windows PowerShell 介面註冊期間的 hello 密碼然後可以透過 hello Azure 傳統入口網站變更。 執行下列步驟 toochange hello 裝置系統管理員密碼的 hello。

#### <a name="toochange-hello-device-administrator-password"></a>toochange hello 裝置系統管理員密碼
1. 在 hello 傳統入口網站，按一下 **裝置** > **設定**為您的裝置。
2. 捲動 toohello**裝置系統管理員密碼**> 一節。 提供系統管理員密碼包含 8 too15 個字元。 hello 密碼必須是 3 個以上的大寫、 小寫、 數字及特殊字元的組合。
3. 確認 hello 的密碼。
4. 按一下**儲存**hello hello 頁底端。

hello 裝置系統管理員密碼現在應已更新。 您可以使用這個修改過的密碼 tooaccess hello Windows PowerShell 介面。

## <a name="change-hello-storsimple-snapshot-manager-password"></a>變更 hello StorSimple Snapshot Manager 密碼
StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。

時設定 StorSimple Snapshot Manager 中的裝置，您將看到 tooprovide hello 裝置 IP 位址和密碼 tooauthenticate 存放裝置。 透過 hello Windows PowerShell 介面，會先設定這個密碼。 如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。

第一次設定透過 hello Windows PowerShell 介面註冊期間的 hello 密碼然後可以透過 hello 傳統入口網站變更。 執行下列步驟 toochange hello StorSimple Snapshot Manager 密碼 hello。

#### <a name="toochange-hello-storsimple-snapshot-manager-password"></a>toochange hello StorSimple Snapshot Manager 密碼
1. 在 hello 傳統入口網站，按一下 **裝置** > **設定**為您的裝置。
2. 捲動 toohello **StorSimple Snapshot Manager** > 一節。 輸入 14 或 15 個字元的密碼。 請確定該 hello 密碼包含 3 個以上的大寫、 小寫、 數字及特殊字元的組合。
3. 確認 hello 的密碼。
4. 按一下**儲存**hello hello 頁底端。

hello StorSimple Snapshot Manager 密碼現在應已更新。

## <a name="next-steps"></a>後續步驟
* 深入了解 [StorSimple 安全性](storsimple-security.md)。
* [深入了解修改您的裝置組態](storsimple-modify-device-config.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

