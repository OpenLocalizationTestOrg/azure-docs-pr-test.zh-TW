---
title: "管理 StorSimple 儲存體帳戶 | Microsoft Docs"
description: "說明如何使用 StorSimple Manager 的 [設定] 頁面來加入、編輯、刪除或替換儲存體帳戶的安全性金鑰。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 68b767c9c93f2daff476a21029b9813f347590b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-storage-account"></a>使用 StorSimple Manager 服務管理儲存體帳戶
## <a name="overview"></a>概觀
[設定]  頁面會顯示所有可在 StorSimple Manager 服務中建立的全域服務參數。 這些參數可以套用到與該服務連線的所有裝置，還包括：

* 儲存體帳戶 
* 頻寬範本 
* 存取控制記錄 

本教學課程說明如何使用 [設定]  頁面來新增、 編輯或刪除儲存體帳戶或替換儲存體帳戶的安全性金鑰。

 ![[設定] 頁面](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

儲存體帳戶包含的認證可供裝置用來存取雲端服務提供者的儲存體帳戶。 對於 Microsoft Azure 儲存體帳戶，像是帳戶名稱與主要存取金鑰就屬於這些認證。 

在 [設定]  頁面上，為訂用帳戶計費而建立的所有儲存體帳戶都會以表格顯示，其中包含下列資訊：

* **名稱** – 帳戶建立時獲指派的唯一名稱。
* **啟用 SSL** – 是否已啟用 SSL 並透過安全通道進行裝置對雲端的通訊。
* **使用者** – 使用該儲存體帳戶的的磁碟區數目。

最常見可在 [設定]  頁面上執行與儲存體帳戶相關的工作如下：

* 新增儲存體帳戶 
* 編輯儲存體帳戶 
* 刪除儲存體帳戶 
* 替換儲存體帳戶的金鑰 

## <a name="types-of-storage-accounts"></a>儲存體帳戶類型
有三種儲存體帳戶類型能與 StorSimple 裝置搭配使用。

* **自動產生的儲存體帳戶** – 正如其名，這類型的儲存體帳戶是在初次建立服務時自動產生。 若要深入了解如何建立此儲存體帳戶，請參閱[部署您的內部部署 StorSimple 裝置](storsimple-deployment-walkthrough.md)中的[步驟 1：建立新的服務](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service)。 
* **服務訂用帳戶中的儲存體帳戶** – 這些是與相同服務訂用帳戶相關聯的 Azure 儲存體帳戶。 若要深入了解如何建立這些儲存體帳戶，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 
* **服務訂用帳戶外的儲存體帳戶** – 這些是與服務毫無關聯的 Azure 儲存體帳戶，而且可能在服務建立之前便已存在 。

## <a name="add-a-storage-account"></a>新增儲存體帳戶
您可以提供唯一的易記名稱以及與儲存體帳戶(搭配指定的雲端服務提供者) 連結的存取認證來新增儲存體帳戶。 您也能選擇啟用安全通訊端層 (SSL) 模式，建立裝置與雲端之間網路通訊的安全通道。

您可以為指定的雲端服務提供者建立多個帳戶。 不過，請注意，建立儲存體帳戶之後，您無法變更雲端服務提供者。

儲存體帳戶在儲存時，服務會嘗試與您的雲端服務提供者通訊。 此時會驗證您提供的認證與存取資料。 只有當驗證成功時，才會建立儲存體帳戶。 如果驗證失敗，則會顯示適當的錯誤訊息。

在 Azure 入口網站中建立的 Resource Manager 儲存體帳戶也支援 StorSimple。 嘗試建立磁碟區容器時，下拉式清單中將不會顯示 Resource Manager 儲存體帳戶供選取，只會顯示在 Azure 傳統入口網站中建立的儲存體帳戶。 Resource Manager 儲存體帳戶必須使用如下所述的新增儲存體帳戶的程序來新增。

> [!NOTE]
> 新增儲存體帳戶的程序將因為使用的軟體版本而有所不同。 請務必依照您 StorSimple 版本適用的程序執行。
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>編輯儲存體帳戶
您可以編輯磁碟區容器所使用的儲存體帳戶。 如果您編輯的儲存體帳戶目前正在使用中，唯一可修改的欄位就是儲存體帳戶的存取金鑰。 您可以提供新的儲存體存取金鑰，並儲存更新的設定。

#### <a name="to-edit-a-storage-account"></a>若要編輯儲存體帳戶
1. 在服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [設定] 。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在 [新增/編輯儲存體帳戶]  對話方塊中：
   
   1. 在 [儲存體帳戶] 下拉式清單中，選擇您想要修改的現有帳戶。 這也包含服務初次建立時自動產生的儲存體帳戶。
   2. 如有必要，您可以修改 [啟用 SSL 模式]  選項。
   3. 您可以選擇替換儲存體帳戶存取金鑰。 如需如何執行金鑰替換的詳細資訊，請參閱 [替換儲存體帳戶的金鑰](#key-rotation-of-storage-accounts) 。
   4. 按一下核取圖示 ![核取圖示](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) 以儲存設定。 [設定]  頁面上的設定隨即更新。 按一下 [儲存]  以儲存剛更新的設定。
      
      ![編輯儲存體帳戶](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>刪除儲存體帳戶
> [!IMPORTANT]
> 只有在其未由磁碟區容器使用時，您才可以刪除儲存體帳戶。 如果磁碟區容器正在使用儲存體帳戶，請先刪除磁碟區容器，然後再刪除相關聯的儲存體帳戶。
> 
> 

#### <a name="to-delete-a-storage-account"></a>若要刪除儲存體帳戶
1. 在 StorSimple Manager 服務登陸頁面上，選取您的服務，連按兩下該服務名稱，然後按一下 [設定] 。
2. 在儲存體帳戶的表格式清單中，將滑鼠停留在您想要刪除的帳戶上方。
3. 刪除圖示 (**x**) 會出現在該儲存體帳戶資料行的最右邊。 按一下 [x]  圖示，以刪除認證。
4. 當系統提示您確認時，按一下 [是]  繼續進行刪除。 表格式清單會更新以反映所做的變更。

## <a name="key-rotation-of-storage-accounts"></a>替換儲存體帳戶的金鑰
基於安全性理由，通常是在資料中心內才需要替換金鑰。 

> [!NOTE]
> 下面的金鑰輪替資訊和程序僅適用於 Microsoft Azure 儲存體帳戶。 若您使用的是其他雲端服務提供者，可以透過該提供者的儀表板管理儲存體帳戶金鑰。
> 
> 

每個 Microsoft Azure 訂用帳戶可以有一或多個相關聯的儲存體帳戶。 訂用帳戶與每個儲存體帳戶的存取金鑰可以控制這些帳戶的存取權。 

當您建立儲存體帳戶時，Azure 會產生兩個 512 位元的儲存體存取金鑰，可在存取儲存體帳戶時用於驗證。 有這兩個儲存體存取金鑰，您不需要中斷儲存體服務或對該服務的存取，就能重新產生金鑰。 目前使用中的金鑰是「主要」金鑰，而備份金鑰則稱為「次要」金鑰。 當 Microsoft Azure StorSimple 裝置存取您的雲端儲存體服務提供者時必須提供這些兩個機碼之一。

## <a name="what-is-key-rotation"></a>什麼是替換金鑰？
一般而言，應用程式只使用其中一個金鑰來存取您的資料。 經過一段時間之後，您可以讓應用程式切換為使用第二個金鑰。 在您將應用程式切換至次要金鑰之後，可以淘汰第一個金鑰，然後產生新的金鑰。 這種使用兩個金鑰的方式可讓您的應用程式存取資料，卻不會產生任何停機時間。

儲存體帳戶金鑰一律以加密的格式儲存在服務中。 不過，您可以透過 StorSimple Manager 服務來重設。 服務可為相同訂用帳戶中的所有儲存體帳戶取得主要金鑰與次要金鑰，包括儲存體服務中建立的帳戶以及 StorSimple Manager 服務初次建立時產生的預設儲存體帳戶。 StorSimple Manager 服務將一律從 Azure 傳統入口網站取得這些金鑰，再以加密的方式儲存。

## <a name="rotation-workflow"></a>替換工作流程
Microsoft Azure 系統管理員可以直接存取儲存體帳戶 (透過 Microsoft Azure 儲存體服務) 來重新產生或變更主要金鑰或次要金鑰。 StorSimple Manager 服務不會自動發現這項變更。

若要通知 StorSimple Manager 服務所做的變更，您需要存取 StorSimple Manager 服務，存取儲存體帳戶，然後同步處理主要或次要金鑰 (根據哪一個有變更而定)。 服務接著會取得最新的金鑰，將金鑰加密，然後將加密的金鑰傳送給裝置。

#### <a name="to-synchronize-keys-for-storage-accounts-in-the-same-subscription-as-the-service-azure-only"></a>若要同步服務 (僅限 Azure only) 之訂用帳戶中的儲存體帳戶金鑰
1. 在 [服務] 頁面上，按一下 [設定] 索引標籤。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在對話方塊中，執行下列動作：
   
   1. 選取您要同步處理其金鑰的儲存體帳戶。 儲存體帳戶金鑰是以加密的狀態顯示。
   2. 在 StorSimple Manager 服務中，您需要更新先前在 Microsoft Azure 儲存體服務中變更的金鑰。 如果主要存取金鑰有所變更 (已重新產生)，按一下 [同步處理主要金鑰] 。 如果次要金鑰有所變更，按一下 [同步處理次要金鑰] 。
      
      ![同步處理金鑰](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="to-synchronize-keys-for-storage-accounts-outside-of-the-service-subscription"></a>若要同步處理服務訂用帳戶外的儲存體帳戶金鑰
1. 在 [服務] 頁面上，按一下 [設定] 索引標籤。
2. 按一下 [新增/編輯儲存體帳戶] 。
3. 在對話方塊中，執行下列動作：
   
   1. 選取您要更新其存取金鑰的儲存體帳戶。
   2. 您必須更新 StorSimple Manager 服務中的儲存體存取金鑰。 在此情況下，您可以看到儲存體存取金鑰。 在 [ **儲存體帳戶存取金鑰**] 方塊中，輸入新的金鑰。 
   3. 儲存您的變更。 現在應已更新您的儲存體帳戶存取金鑰。

## <a name="next-steps"></a>後續步驟
* 深入了解 [StorSimple 安全性](storsimple-security.md)。
* 深入了解 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

