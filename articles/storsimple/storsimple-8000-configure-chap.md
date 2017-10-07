---
title: "StorSimple 8000 系列裝置的 aaaConfigure CHAP |Microsoft 文件"
description: "描述如何 tooconfigure hello StorSimple 裝置上的 Challenge Handshake 驗證通訊協定 (CHAP)。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a>為 StorSimple 裝置設定 CHAP

本教學課程說明如何 tooconfigure CHAP 您 StorSimple 裝置。 此文件中詳述的 hello 程序適用於 8000 系列裝置 tooStorSimple。

CHAP 代表 Challenge Handshake 驗證通訊協定。 它是伺服器 toovalidate hello 身分識別的遠端用戶端所使用的驗證配置。 hello 驗證根據共用的密碼或密碼。 CHAP 可以是單向 (單向) 或相互 (雙向)。 單向 CHAP 時，hello 目標驗證啟動器。 在相互或反向 CHAP hello 目標驗證啟動器 hello，然後 hello 啟動器驗證目標 hello。 不需要目標驗證也能實作啟動器驗證。 不過，必須同時實作啟動器驗證，才能實作目標驗證。

最佳做法，我們建議您使用 CHAP tooenhance iSCSI 安全性。

> [!NOTE]
> 請記住，StorSimple 裝置目前不支援 IPSEC。

hello hello StorSimple 裝置上的 CHAP 設定可以在 hello 下列方式設定：

* 單向驗證
* 雙向、相互或反向驗證

在每個這種情況下，hello hello 裝置與 hello 伺服器 iSCSI 啟動器軟體的入口網站會需要 toobe 設定。 hello 詳細的步驟，此組態中有描述 hello 教學課程。

## <a name="unidirectional-or-one-way-authentication"></a>單向驗證

在單向驗證中，hello 目標驗證啟動器 hello。 此驗證，您必須設定 hello CHAP 啟動器設定 hello StorSimple 裝置和 hello iSCSI 啟動器軟體 hello 主機上。 接下來說明 Windows 主機及 hello StorSimple 裝置的詳細程序。

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a>tooconfigure 單向驗證您的裝置

1. 在 hello Azure 入口網站，移 tooyour StorSimple 裝置管理員服務。 按一下**裝置**並選取，然後按一下您想 tooconfigure CHAP 裝置的。 跳過**裝置設定 > 安全性**。 在 hello**安全性設定**刀鋒視窗中，按一下  **CHAP**。
   
    ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. 在 hello **CHAP**刀鋒視窗中，在 hello **CHAP 啟動器**> 一節：
   
   1. 提供 CHAP 啟動器的使用者名稱。
   2. 提供 CHAP 啟動器的密碼。
      
    > [!IMPORTANT]
    > hello CHAP 使用者名稱必須包含少於 233 個字元。 hello CHAP 密碼必須介於 12 到 16 個字元。 較長的使用者名稱或密碼會導致 hello Windows 主機上的驗證失敗。
   
   3. 確認 hello 的密碼。

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. 按一下 [儲存] 。 隨即顯示確認訊息。 按一下**確定**toosave hello 變更。

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a>tooconfigure hello Windows 上的單向驗證主機伺服器
1. Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。
2. 在 hello **iSCSI 啟動器屬性**視窗中，執行下列步驟的 hello:
   
   1. 按一下 hello**探索** 索引標籤。
      
       ![iSCSI 啟動器屬性](./media/storsimple-configure-chap/IC740944.png)
   2. 按一下 [探索入口網站] 。
3. 在 hello**探索目標入口網站**對話方塊：
   
   1. 指定您的裝置 hello IP 位址。
   2. 按一下 [進階] 。
      
       ![探索目標入口網站](./media/storsimple-configure-chap/IC740945.png)
4. 在 hello**進階設定**對話方塊：
   
   1. 選取 hello**啟用 CHAP 登入**核取方塊。
   2. 在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。
   3. 在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。
   4. 按一下 [確定] 。
      
       ![進階設定 - 一般](./media/storsimple-configure-chap/IC740946.png)
5. 在 [hello**目標**hello] 索引標籤**iSCSI 啟動器屬性**hello 裝置狀態應顯示視窗中，為**已連接**。 如果您使用 StorSimple 1200 裝置，則每個磁碟區會掛接為 iSCSI 目標。 步驟 3-4，因此，需要 toobe 重複每個磁碟區。
   
    ![做為個別目標掛接的磁碟區](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > 如果您變更 hello iSCSI 名稱，hello 新名稱會針對新的 iSCSI 工作階段。 您必須先登出再登入，現有的工作階段才會使用新的設定。

如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。

## <a name="bidirectional-or-mutual-authentication"></a>雙向或相互驗證

在雙向驗證 hello 目標驗證啟動器 hello，然後 hello 啟動器驗證目標 hello。 此程序需要 hello 使用者 tooconfigure hello CHAP 啟動器設定、 反向 CHAP 設定 hello 裝置和 iSCSI 啟動器軟體 hello 主機上。 hello 下列程序說明 hello 步驟 tooconfigure 相互驗證 hello 裝置上和 hello Windows 主機上。

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a>tooconfigure 您的裝置進行相互驗證

1. 在 hello Azure 入口網站，移 tooyour StorSimple 裝置管理員服務。 按一下**裝置**並選取，然後按一下您想 tooconfigure CHAP 裝置的。 跳過**裝置設定 > 安全性**。 在 hello**安全性設定**刀鋒視窗中，按一下  **CHAP**。
   
    ![CHAP 目標](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. 向下捲動這個頁面上，然後在 hello **CHAP 目標**> 一節：
   
   1. 提供裝置的 [反向 CHAP 使用者名稱]  。
   2. 提供裝置的 [反向 CHAP 密碼]  。
   3. 確認 hello 的密碼。
3. 在 hello **CHAP 啟動器**> 一節：
   
   1. 提供裝置的 [使用者名稱]  。
   2. 提供裝置的 [密碼]  。
   3. 確認 hello 的密碼。

       ![CHAP 啟動器](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. 按一下 [儲存] 。 隨即顯示確認訊息。 按一下**確定**toosave hello 變更。

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a>在 hello Windows tooconfigure 雙向驗證主機伺服器

1. Hello Windows 主機伺服器上，啟動 hello iSCSI 啟動器。
2. 在 [hello **iSCSI 啟動器屬性**視窗中，按一下 hello**組態**] 索引標籤。
3. 按一下 [CHAP] 。
4. 在 hello **iSCSI 啟動器相互 CHAP 密碼**對話方塊：
   
   1. 型別 hello**反向 CHAP 密碼**hello Azure 入口網站中設定。
   2. 按一下 [確定] 。
      
       ![iSCSI 啟動器相互 CHAP 密碼](./media/storsimple-configure-chap/IC740949.png)
5. 按一下 hello**目標** 索引標籤。
6. 按一下 hello**連接** 按鈕。 
7. 在 hello**連接 tooTarget**對話方塊中，按一下 **進階**。
8. 在 hello**進階屬性**對話方塊：
   
   1. 選取 hello**啟用 CHAP 登入**核取方塊。
   2. 在 hello**名稱**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 使用者名稱。
   3. 在 hello**目標密碼**欄位，您為 hello 傳統入口網站中的 hello CHAP 啟動器指定的供應 hello 密碼。
   4. 選取 hello**執行相互驗證**核取方塊。
      
       ![進階設定 - 相互驗證](./media/storsimple-configure-chap/IC740950.png)
   5. 按一下**確定**toocomplete hello CHAP 設定

如需 hello Windows 主機伺服器上設定 CHAP 的詳細資訊，請移至太[其他考量](#additional-considerations)。

## <a name="additional-considerations"></a>其他考量

hello**快速連線**功能不支援已啟用 CHAP 的連線。 啟用 CHAP 時，請確定您使用 hello**連接**按鈕上 hello**目標**標籤 tooconnect tooa 目標。

![連接 tootarget](./media/storsimple-configure-chap/IC740947.png)

在 hello**連接 tooTarget**對話方塊會呈現，請選取 hello**新增我的最愛目標連線 toohello 清單**核取方塊。 此選項可確保，每次 hello 電腦重新啟動，就會試著 toorestore hello 連接 toohello iSCSI 我的最愛目標。

## <a name="errors-during-configuration"></a>設定期間發生錯誤

如果您的 CHAP 設定不正確，則您必須有可能 toosee**驗證失敗**錯誤訊息。

## <a name="verification-of-chap-configuration"></a>CHAP 設定的驗證

您可以確認藉由完成下列步驟的 hello 使用 CHAP。

#### <a name="tooverify-your-chap-configuration"></a>tooverify 您的 CHAP 設定
1. 按一下 [我的最愛目標] 。
2. 選取您已啟用驗證的 hello 目標。
3. 按一下 [詳細資訊] 。
   
    ![iSCSI 啟動器屬性 - 我的最愛目標](./media/storsimple-configure-chap/IC740951.png)
4. 在 hello**我的最愛目標詳細資料**對話方塊中，注意 hello 項目在 hello**驗證**欄位。 Hello 設定是否成功，它應該**CHAP**。
   
    ![我的最愛目標詳細資料](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a>後續步驟

* 深入了解 [StorSimple 安全性](storsimple-8000-security.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple 裝置管理員服務 tooadminister](storsimple-8000-manager-service-administration.md)。

