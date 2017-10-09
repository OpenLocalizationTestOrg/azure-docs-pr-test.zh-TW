---
title: "在 StorSimple aaaManage 存取控制記錄 |Microsoft 文件"
description: "描述 toouse 存取控制記錄 (Acr) toodetermine 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>使用 hello StorSimple Manager 服務 toomanage 存取控制記錄
## <a name="overview"></a>概觀
存取控制記錄 (Acr) 可讓您 toospecify 哪些主機可連接 tooa hello StorSimple 裝置上的磁碟區。 Acr tooa 特定磁碟區，並設定包含 hello iSCSI hello 主機的限定名稱 （iqn 相關聯）。 當主機嘗試 tooconnect tooa 磁碟區時，hello 裝置會檢查的 hello 與 hello IQN 名稱，如果沒有符合項目，然後 hello 建立連接該磁碟區相關聯的 ACR。 hello 存取控制記錄區段 hello**設定**頁面會顯示以 hello 對應 iqn 相關聯的 hello 主機的所有 hello 存取控制記錄。

本教學課程將說明下列 ACR 相關的一般工作的 hello:

* 加入存取控制記錄 
* 編輯存取控制記錄 
* 刪除存取控制記錄 

> [!IMPORTANT]
> * 指派的 ACR tooa 磁碟區時，小心，hello 存取磁碟區不同時由多個非叢集主機因為這可能會損毀 hello 磁碟區。 
> * 當從磁碟區刪除 ACR，請確定該 hello 對應的主機未存取 hello 磁碟區，因為 hello 刪除可能會導致讀寫中斷。
> 
> 

## <a name="add-an-access-control-record"></a>加入存取控制記錄
使用 hello StorSimple Manager 服務**設定**頁面 tooadd Acr。 一般而言，您會讓一個 ACR 與一個磁碟區產生關聯。

執行下列步驟 tooadd ACR hello。

#### <a name="tooadd-an-access-control-record"></a>tooadd 存取控制記錄
1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。
2. 在表格式底下列出的 hello**存取控制記錄**、 提供**名稱**acr。
3. 提供 hello 下 Windows 主機的 IQN 名稱**iSCSI 啟動器名稱**。 tooget hello 您 Windows Server 主機的 IQN，請勿 hello 遵循：
   
   * 在 Windows 主機上啟動 hello Microsoft iSCSI 啟動器。
   * 在 hello **iSCSI 啟動器屬性**視窗的 hello**組態**索引標籤上，選取並複製 hello 字串 hello 從**啟動器名稱**欄位。
   * 貼上此字串在 hello **iSCSI 啟動器名稱**hello Azure 傳統入口網站中的 hello Acr 資料表上的欄位。
4. 按一下**儲存**toosave hello 新建立的 ACR。 hello 表格式清單將會更新的 tooreflect 此新增功能。

## <a name="edit-an-access-control-record"></a>編輯存取控制記錄
使用 hello**設定**hello Azure 傳統入口網站 tooedit Acr 中的頁面。 

> [!NOTE]
> 您只能修改目前未在使用中的 ACR。 tooedit 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。
> 
> 

執行下列步驟 tooedit ACR hello。

#### <a name="tooedit-an-access-control-record"></a>tooedit 存取控制記錄
1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。
2. 在 hello 表格清單中的 hello 存取控制記錄，請將滑鼠停留在 hello 想 toomodify 的 ACR。
3. Hello ACR 提供新的名稱和/或 IQN。
4. 按一下**儲存**toosave hello 修改 ACR。 hello 表格式清單將會更新的 tooreflect 這項變更。

## <a name="delete-an-access-control-record"></a>刪除存取控制記錄
使用 hello**設定**hello Azure 傳統入口網站 toodelete Acr 中的頁面。 

> [!NOTE]
> 您只能刪除目前未在使用中的 ACR。 toodelete 與目前正在使用的磁碟區相關聯的 ACR，您必須先進行 hello 磁碟區離線。
> 
> 

執行下列步驟 toodelete 存取控制記錄的 hello。

#### <a name="toodelete-an-access-control-record"></a>toodelete 存取控制記錄
1. 在 hello 服務登陸頁面上，選取您的服務、 按兩下 hello 的服務名稱，然後按一下 hello**設定** 索引標籤。
2. 在 hello 表格清單中的 hello 存取控制記錄 (Acr)，請將滑鼠停留在 hello 想 toodelete 的 ACR。
3. 刪除圖示 (**x**) 會出現在 hello 極端右側的欄 hello 您選取的 ACR。 按一下 hello **x**圖示 toodelete hello ACR。
4. 當提示確認，請按一下**是**toocontinue 與 hello 刪除。 hello 表格式清單將會更新的 tooreflect hello 刪除。

## <a name="next-steps"></a>後續步驟
* 深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

