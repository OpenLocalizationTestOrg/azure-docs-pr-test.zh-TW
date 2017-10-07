---
title: "aaaManage StorSimple 磁碟區容器 |Microsoft 文件"
description: "說明如何使用 hello StorSimple Manager 服務磁碟區容器頁面 tooadd、 修改或刪除磁碟區容器。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>使用 hello StorSimple Manager 服務 toomanage StorSimple 磁碟區容器
## <a name="overview"></a>概觀
本教學課程將說明 toouse hello StorSimple Manager 服務 toocreate 並管理 StorSimple 磁碟區容器。

Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。 一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。 

磁碟區容器具有下列屬性的 hello:

* **磁碟區**– hello 分層或固定在本機 hello 磁碟區容器內包含的 StorSimple 磁碟區。 磁碟區容器可包含 too256 StorSimple 磁碟區。
* **加密** – 可以為每個磁碟區容器定義的加密金鑰。 此金鑰用來加密從您的 StorSimple 裝置 toohello 雲端傳送 hello 資料。 軍事等級 aes-256 位元金鑰可搭配 hello 使用者輸入的金鑰。 toosecure 您的資料，我們建議您一律啟用雲端儲存體加密。
* **儲存體帳戶**– hello 是連結的 tooyour 雲端儲存體服務提供者的儲存體帳戶。 所有位於磁碟區容器中的 hello 磁碟區共用這個儲存體帳戶。 您可以從現有的清單，請選擇儲存體帳戶，或建立新的帳戶，當您建立 hello 磁碟區容器，然後指定該帳戶的 hello 存取認證。
* **雲端頻寬**– hello hello 裝置所傳送嗨裝置中的 hello 資料 toohello 雲端時所使用的頻寬。 當您定義此容器時，可以指定一個介於 1 與 1000 Mbps 之間的值，以強制執行頻寬控制。 如果您想要 hello 裝置 tooconsume 所有可用的頻寬，設定此欄位 tooUnlimited。 您也可以建立和套用頻寬範本 tooallocate 頻寬排程為基礎。

![磁碟區容器頁面](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

此下列的程序說明如何 toouse hello StorSimple**磁碟區容器**頁面 toocomplete hello 下列常見作業：

* 新增磁碟區容器 
* 修改磁碟區容器 
* 刪除磁碟區容器 

## <a name="add-a-volume-container"></a>新增磁碟區容器
執行下列步驟 tooadd 磁碟區容器的 hello。

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>修改磁碟區容器
執行下列步驟 toomodify 磁碟區容器的 hello。

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>刪除磁碟區容器
磁碟區容器內具有磁碟區。 先刪除所有包含在它的 hello 磁碟區時，才可以刪除它。 執行下列步驟 toodelete 磁碟區容器的 hello。

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>後續步驟
* 深入了解 [管理 StorSimple 磁碟區](storsimple-manage-volumes.md)。 
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

