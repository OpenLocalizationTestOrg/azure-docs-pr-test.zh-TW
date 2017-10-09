---
title: "為 StorSimple Virtual Array aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toomanage 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple Virtual Array 上的磁碟區的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>StorSimple Virtual Array 的使用 StorSimple 裝置管理員 toomanage 存取控制記錄

## <a name="overview"></a>概觀

存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple Virtual Array （也稱為 hello StorSimple 內部部署虛擬裝置） 上的磁碟區。 Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。 Hello 裝置當主機嘗試 tooconnect tooa 磁碟區時，會檢查 hello 與 hello IQN 名稱，該磁碟區相關聯的 ACR，如果沒有相符項目，然後 hello 建立連接。 hello**存取控制記錄**刀鋒視窗內 hello**組態**您的裝置管理員服務 區段會顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。

![管理存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

本教學課程將說明下列 ACR 相關的一般工作的 hello:

* 取得 hello IQN
* 加入存取控制記錄
* 編輯存取控制記錄
* 刪除存取控制記錄

> [!IMPORTANT]
> 
> * 指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。
> * 當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。


## <a name="get-hello-iqn"></a>取得 hello IQN

執行下列步驟 tooget hello 執行 Windows Server 2012 的 Windows 主機的 IQN hello。

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>加入 ACR

您使用**存取控制記錄**刀鋒視窗內 hello**組態**您 StorSimple 裝置管理員服務 tooadd Acr 的區段。 一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。

如需將一個 ACR 與磁碟區產生關聯的資訊，請太[加入磁碟區](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。

> [!IMPORTANT]
> 指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。


執行下列步驟 tooadd ACR hello。

#### <a name="tooadd-an-acr"></a>tooadd ACR

1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態**區段中，按一下**存取控制記錄**。
2. 在 hello**存取控制記錄**刀鋒視窗中，按一下 **新增**。
3. 在 hello**新增 ACR**刀鋒視窗中，請勿遵循 hello:
   
    1. 提供 ACR 的 [名稱]  。
    
    2. 在下**iSCSI 啟動器名稱**，提供 hello Windows 主機的 IQN 名稱。 tooget hello 您 Windows Server 主機的 IQN，請勿 hello 遵循：
   
    3. 在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。 Hello iSCSI 啟動器屬性 視窗中，在 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。
    貼上此字串在 hello **IQN**欄位 hello**新增 ACR**刀鋒視窗。
   
    6. 按一下**新增**tooadd hello ACR。  
   
        ![新增存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. hello 表格清單是更新的 tooreflect 這個額外功能。

## <a name="edit-an-acr"></a>編輯 ACR

使用 hello**存取控制記錄**刀鋒視窗內 hello**組態**您的裝置管理員服務在 Azure 入口網站 tooedit Acr hello > 一節。

> [!NOTE]
> 請勿修改目前正在使用的 ACR。 tooedit 與目前正在使用的磁碟區相關聯的 ACR，您應該先進行 hello 磁碟區離線。


執行下列步驟 tooedit ACR hello。

#### <a name="tooedit-an-acr"></a>tooedit ACR

1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態** 區段中，**存取控制記錄**。
2. 在 hello**存取控制記錄**刀鋒視窗中，從 hello 表格清單中的 hello 存取控制記錄，連按兩下您想 toomodify ACR hello。
3. 在 hello**編輯存取控制記錄**刀鋒視窗中，執行下列 hello:
   
    1. 提供 hello IQN hello ACR。
   
    2. 按一下**儲存**頂端的 hello 刀鋒視窗 toosave hello hello 修改 ACR。 您會看到下列確認訊息的 hello:
   
        ![編輯存取控制記錄](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>刪除存取控制記錄

使用 hello**組態**hello Azure 入口網站 toodelete Acr 中的頁面。

> [!NOTE]
> 
> * 請勿刪除目前正在使用的 ACR。 toodelete 與目前正在使用的磁碟區相關聯的 ACR，您應該先進行 hello 磁碟區離線。
> * 當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。


執行下列步驟 toodelete 存取控制記錄的 hello。

#### <a name="toodelete-an-access-control-record"></a>toodelete 存取控制記錄

1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 服務名稱，然後再內 hello**組態** 區段中，**存取控制記錄**。

2. 在 hello**存取控制記錄**刀鋒視窗中，從 hello 表格清單中的 hello 存取控制記錄，連按兩下您想 toodelete ACR hello。

3. 在 hello 編輯存取控制記錄刀鋒視窗中，按一下 **刪除**。
   
    ![刪除 ACR](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. 當提示確認，請按一下**刪除**toocontinue 與 hello 刪除。 hello 表格清單是更新的 tooreflect hello 刪除。
   
   ![警告訊息](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>後續步驟

* 深入了解[新增和設定 ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume)。

