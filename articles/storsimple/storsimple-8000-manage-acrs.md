---
title: "在 StorSimple aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toouse 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>使用 hello StorSimple Manager 服務 toomanage 存取控制記錄

## <a name="overview"></a>概觀
存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區。 Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。 當主機嘗試 tooconnect tooa 磁碟區時，hello 裝置會檢查的 hello 與 hello IQN 名稱，如果沒有符合項目，然後 hello 建立連接該磁碟區相關聯的 ACR。 hello hello 中的存取控制記錄**組態**您 StorSimple 裝置管理員服務刀鋒視窗的區段顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。

本教學課程將說明下列 ACR 相關的一般工作的 hello:

* 加入存取控制記錄
* 編輯存取控制記錄
* 刪除存取控制記錄

> [!IMPORTANT]
> * 指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。
> * 當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。

## <a name="get-hello-iqn"></a>取得 hello IQN

執行下列步驟 tooget hello 執行 Windows Server 2012 的 Windows 主機的 IQN hello。

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>加入存取控制記錄
使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 tooadd Acr > 一節。 一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。

執行下列步驟 tooadd ACR hello。

#### <a name="tooadd-an-acr"></a>tooadd ACR

1. 移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。
2. 在 hello**存取控制記錄**刀鋒視窗中，按一下  **+ 新增 ACR**。

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr1.png)

3. 在 hello**新增 ACR**刀鋒視窗中，執行下列步驟 hello:

    1. 提供 ACR 的名稱。
    
    2. 提供在 Windows Server 主機 hello IQN 名稱**iSCSI 啟動器名稱 (IQN)**。

    3. 按一下**新增**toocreate hello ACR。

        ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  hello 新增 ACR 會顯示在 hello 表格 Acr 清單。

    ![按一下 [新增 ACR]](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>編輯存取控制記錄
使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 tooedit Acr > 一節。

> [!NOTE]
> 建議您只修改目前未在使用中的 ACR。 tooedit 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。

執行下列步驟 tooedit ACR hello。

#### <a name="tooedit-an-access-control-record"></a>tooedit 存取控制記錄
1.  移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. 在 hello 表格清單中的 hello 存取控制記錄，按一下並選取您想 toomodify ACR hello。

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr1.png)

3. 在 hello**編輯存取控制記錄**刀鋒視窗中，提供不同的 IQN 對應 tooanother 主機。

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr2.png)

4. 按一下 [儲存] 。 系統提示您進行確認時，按一下 [是] 。 

    ![編輯存取控制記錄](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Hello ACR 更新時，會通知您。 hello 表格清單也會更新 tooreflect hello 變更。

   
## <a name="delete-an-access-control-record"></a>刪除存取控制記錄
使用 hello**組態**hello StorSimple 裝置管理員服務刀鋒視窗 toodelete Acr > 一節。

> [!NOTE]
> 您只能刪除目前未在使用中的 ACR。 toodelete 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。

執行下列步驟 toodelete 存取控制記錄的 hello。

#### <a name="toodelete-an-access-control-record"></a>toodelete 存取控制記錄
1.  移 tooyour StorSimple 裝置管理員服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/createacr1.png)

2. 在 hello 表格清單中的 hello 存取控制記錄，按一下並選取您想 toodelete ACR hello。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Tooinvoke hello 操作功能表上按一下滑鼠右鍵，然後選取**刪除**。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. 當提示確認時，檢閱 hello 資訊，然後按一下**刪除**。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Hello 刪除完成時，會通知您。 hello 表格清單是更新的 tooreflect hello 刪除。

    ![移 tooaccess 控制記錄](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>後續步驟
* 深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-8000-manager-service-administration.md)。

