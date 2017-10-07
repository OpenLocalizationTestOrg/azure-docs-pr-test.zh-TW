---
title: "aaaManage StorSimple 磁碟區容器上 hello StorSimple 8000 系列裝置 |Microsoft 文件"
description: "說明如何使用 hello StorSimple 裝置管理員服務磁碟區容器頁面 tooadd、 修改或刪除磁碟區容器。"
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
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>使用 hello StorSimple 裝置管理員服務 toomanage StorSimple 磁碟區容器

## <a name="overview"></a>概觀
本教學課程將說明 toouse hello StorSimple 裝置管理員服務 toocreate 並管理 StorSimple 磁碟區容器。

Microsoft Azure StorSimple 裝置中的磁碟區容器包含一個或多個可共用儲存體帳戶、加密和頻寬耗用量設定的磁碟區。 一個裝置可以有多個磁碟區容器，供其所有磁碟區使用。 

磁碟區容器具有下列屬性的 hello:

* **磁碟區**– hello 分層或固定在本機 hello 磁碟區容器內包含的 StorSimple 磁碟區。 
* **加密** – 可以為每個磁碟區容器定義的加密金鑰。 此金鑰用來加密從您的 StorSimple 裝置 toohello 雲端傳送 hello 資料。 軍事等級 aes-256 位元金鑰可搭配 hello 使用者輸入的金鑰。 toosecure 您的資料，我們建議您一律啟用雲端儲存體加密。
* **儲存體帳戶**– hello 使用的 toostore hello 資料的 Azure 儲存體帳戶。 所有位於磁碟區容器中的 hello 磁碟區共用這個儲存體帳戶。 您可以從現有的清單，請選擇儲存體帳戶，或建立新的帳戶，當您建立 hello 磁碟區容器，然後指定該帳戶的 hello 存取認證。
* **雲端頻寬**– hello hello 裝置所傳送嗨裝置中的 hello 資料 toohello 雲端時所使用的頻寬。 當您建立此容器時，可以指定一個介於 1 Mbps 到 1000 Mbps 之間的值，以強制執行頻寬控制。 如果您想 hello 裝置 tooconsume 所有可用的頻寬，請將此欄位太**Unlimited**。 您也可以建立和套用頻寬範本 tooallocate 頻寬排程為基礎。

hello 下列程序說明如何 toouse hello StorSimple**磁碟區容器**刀鋒視窗 toocomplete hello 下列常見作業：

* 新增磁碟區容器
* 修改磁碟區容器
* 刪除磁碟區容器

## <a name="add-a-volume-container"></a>新增磁碟區容器
執行下列步驟 tooadd 磁碟區容器的 hello。

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>修改磁碟區容器
執行下列步驟 toomodify 磁碟區容器的 hello。

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>刪除磁碟區容器
磁碟區容器內具有磁碟區。 先刪除所有包含在它的 hello 磁碟區時，才可以刪除它。 執行下列步驟 toodelete 磁碟區容器的 hello。

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>後續步驟
* 深入了解 [管理 StorSimple 磁碟區](storsimple-8000-manage-volumes-u2.md)。 
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。

