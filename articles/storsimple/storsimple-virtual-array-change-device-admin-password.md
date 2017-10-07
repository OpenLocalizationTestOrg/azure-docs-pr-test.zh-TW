---
title: "aaaChange StorSimple Virtual Array 裝置系統管理員密碼 |Microsoft 文件"
description: "描述如何 toouse 或是 hello Azure 入口網站或 StorSimple Virtual Array web UI toochange hello 裝置系統管理員密碼。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 11490814-d9fd-4dc7-9c3b-55dd2c23eaf1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 531b395df7aeade0a909360797c6b0f0abd9fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-storsimple-virtual-array-device-administrator-password-via-storsimple-device-manager"></a>變更 hello StorSimple Virtual Array 裝置系統管理員密碼透過 StorSimple 裝置管理員

## <a name="overview"></a>概觀

當您使用 hello Windows PowerShell 介面 tooaccess hello StorSimple Virtual Array，您會需要的 tooenter 裝置系統管理員密碼。 當 hello StorSimple 裝置就會先佈建並啟動時，hello 預設密碼是*Password1*。 Hello 資料的安全性，如 hello 預設密碼到期 hello 登入的第一次，而且您會需要的 toochange 這個密碼。

您也可以在任何時間之後 hello 裝置部署在生產環境使用任一 hello 本機 web UI 或 hello Azure 入口網站 toochange hello 裝置系統管理員密碼。 本文章說明上述各程序。

 ![裝置刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-devices-blade.png)

## <a name="use-hello-azure-portal-toochange-hello-password"></a>使用 hello Azure 入口網站 toochange hello 密碼

執行下列步驟 toochange hello 裝置系統管理員密碼透過 hello Azure 入口網站的 hello。

#### <a name="toochange-hello-device-administrator-password-via-hello-azure-portal"></a>透過 Azure 入口網站 hello toochange hello 裝置系統管理員密碼

1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**管理**區段中，按一下**裝置**。 這會開啟 hello**裝置**刀鋒視窗，其中列出所有 StorSimple Virtual Array 裝置。

2. 在 hello**裝置**刀鋒視窗中，按兩下 hello 裝置需要密碼的變更。

3. 在 hello**設定**刀鋒視窗，您的裝置，請按一下**安全性**。

4. 在 hello**安全性設定**刀鋒視窗中，請勿遵循 hello:
   
   1. 捲動 toohello**裝置系統管理員密碼**> 一節。 提供系統管理員密碼包含 8 too15 個字元。
   2. 確認 hello 的密碼。
   3. 按一下**儲存**在 hello hello 刀鋒視窗最上方。

現在更新 hello 裝置系統管理員密碼。 您可以在本機上使用這個修改過的密碼 tooaccess hello 裝置。

![安全性設定刀鋒視窗](./media/storsimple-virtual-array-change-device-admin-password/ova-change-device-pwd.png)

## <a name="use-hello-local-web-ui-toochange-hello-password"></a>使用 hello 本機 web UI toochange hello 密碼

執行下列步驟 toochange hello 裝置系統管理員密碼透過 hello 本機 web UI 的 hello。

#### <a name="toochange-hello-device-administrator-password-via-hello-local-web-ui"></a>透過 hello 本機 web UI toochange hello 裝置系統管理員密碼

1. 在 hello 本機 web UI，按一下 **維護** > **密碼變更**為您的裝置。
   
    ![變更 password1](./media/storsimple-virtual-array-change-device-admin-password/image40.png)
2. 輸入 hello**目前密碼**。
3. 提供 **新密碼**。 hello 密碼必須至少 8 個字元。 它必須包含 3，4 個 hello 下列： 大寫字母、 小寫、 數字及特殊字元。
   
    請注意，您的密碼不能 hello 與 hello 最後 24 個密碼相同。
4. 重新輸入 hello 密碼 tooconfirm 它。
   
    ![變更 password2](./media/storsimple-virtual-array-change-device-admin-password/image41.png)
5. 在 hello hello 頁面底部，按一下**套用**。 hello 新密碼會立即套用。 如果不成功 hello 密碼變更時，您會看見 hello 下列錯誤：
   
    ![密碼錯誤](./media/storsimple-virtual-array-change-device-admin-password/image42.png)
   
    已成功更新 hello 密碼之後，您會收到通知。 您接著可以在本機使用這個修改過的密碼 tooaccess hello 裝置。


## <a name="next-steps"></a>後續步驟
了解如何太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

