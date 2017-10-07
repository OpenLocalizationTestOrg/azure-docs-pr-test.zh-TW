---
title: "aaaChange StorSimple 密碼 |Microsoft 文件"
description: "描述如何 toouse 會 hello StorSimple 裝置管理員服務 toochange StorSimple Snapshot Manager 」 和 「 裝置系統管理員密碼。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: cf884be31b4bbf9e372c0aa11b9da2eadcda35dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toochange-your-storsimple-passwords"></a>使用 hello StorSimple 裝置管理員服務 toochange StorSimple 密碼

## <a name="overview"></a>概觀
hello Azure 入口網站**裝置設定**選項包含所有您可以重新設定 StorSimple 裝置管理員服務所管理的 StorSimple 裝置的 hello 裝置參數。 本教學課程說明如何使用 hello**安全性**選項在**裝置設定**toochange 您裝置的系統管理員或 StorSimple Snapshot Manager 密碼。

## <a name="change-hello-device-administrator-password"></a>變更 hello 裝置系統管理員密碼
當您使用 Windows PowerShell 介面 tooaccess hello StorSimple 裝置時，您就需要的 tooenter 裝置系統管理員密碼。 當服務中註冊第一個 StorSimple 裝置 hello 時，此介面的 hello 預設密碼是*Password1*。 Hello 資料的安全性，您對於需要的 toochange 這個密碼 hello hello 註冊程序的結尾。 您無法結束 hello 註冊程序，而不需要變更這個密碼。 如需詳細資訊，請參閱[步驟 3： 設定和註冊 hello 裝置透過 Windows PowerShell for StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)。

在註冊期間第一次設定 hello Windows PowerShell 介面透過 hello 密碼可以稍後變更透過 hello Azure 入口網站。 執行下列步驟 toochange hello 裝置系統管理員密碼的 hello。

#### <a name="toochange-hello-device-administrator-password"></a>toochange hello 裝置系統管理員密碼
1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。

2. 從 hello 表格清單中的裝置，選取，然後按一下 hello 裝置密碼想 toochange。

    ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. 在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 安全性**。

    ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. 在 hello**安全性設定**刀鋒視窗中，按一下 **密碼**toochange hello 裝置系統管理員密碼。

    ![](./media/storsimple-8000-change-passwords/changepwd3.png)

5. 在 hello**密碼**刀鋒視窗中，提供系統管理員密碼包含 8 too15 個字元。 hello 密碼必須是 3 個以上的大寫、 小寫、 數字及特殊字元的組合。

6. 確認 hello 的密碼。

    ![](./media/storsimple-8000-change-passwords/changepwd4.png)

7. 按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。

    ![](./media/storsimple-8000-change-passwords/changepwd6.png)

hello 裝置系統管理員密碼現在應已更新。 您可以使用這個修改過的密碼 tooaccess hello Windows PowerShell 介面。

## <a name="set-hello-storsimple-snapshot-manager-password"></a>設定 hello StorSimple Snapshot Manager 密碼
StorSimple Snapshot Manager 軟體位於您的 Windows 主機上，而且可讓系統管理員 toomanage 備份您的 StorSimple 裝置在 hello 表單的本機和雲端快照。

時設定 StorSimple Snapshot Manager 中的裝置，您將看到 tooprovide hello 裝置 IP 位址和密碼 tooauthenticate 存放裝置。

您可以設定或變更 hello 密碼 StorSimple Snapshot Manager 透過 hello Azure 入口網站。 執行下列步驟 tooset hello 或變更 hello StorSimple Snapshot Manager 密碼。

#### <a name="tooset-hello-storsimple-snapshot-manager-password"></a>tooset hello StorSimple Snapshot Manager 密碼
1. 移 tooyour StorSimple 裝置管理員服務，然後按一下**裝置**。

2. 從 hello 表格清單中的裝置，選取，然後按一下 hello 裝置想 tooset，或變更其 StorSimple Snapshot Manager 密碼。

     ![](./media/storsimple-8000-change-passwords/changepwd1.png)

3. 在 hello**設定**刀鋒視窗中，跳過**裝置設定 > 安全性**。

     ![](./media/storsimple-8000-change-passwords/changepwd2.png)

4. 在 hello**安全性設定**刀鋒視窗中，按一下 **密碼**tooset 或變更 hello StorSimple Snapshot Manager 密碼。

     ![](./media/storsimple-8000-change-passwords/changepwd3.png) 

5. 在 hello**密碼**刀鋒視窗中，輸入 14 或 15 個字元的密碼。 請確定該 hello 密碼包含 3 個以上的大寫、 小寫、 數字及特殊字元的組合。

6. 確認 hello 的密碼。

     ![](./media/storsimple-8000-change-passwords/changepwd5.png)

7. 按一下 [儲存]，當系統提示您進行確認時，按一下 [是]。

     ![](./media/storsimple-8000-change-passwords/changepwd6.png)

hello StorSimple Snapshot Manager 密碼現在應已更新。

## <a name="next-steps"></a>後續步驟
* 深入了解 [StorSimple 安全性](storsimple-8000-security.md)。
* [深入了解修改您的裝置組態](storsimple-8000-modify-device-config.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。

