---
title: "aaaLog StorSimple 8000 系列的支援票證 |Microsoft 文件"
description: "了解如何 toocreate 支援要求並啟動您的 StorSimple 裝置上的支援工作階段。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>連絡 Microsoft 支援服務以解決 StorSimple 問題
如果您使用 Microsoft Azure StorSimple 解決方案時遇到任何問題，您可以向技術支援人員提出服務要求。 在線上工作階段與支援工程師，您也可能需要支援工作階段的 toostart StorSimple 裝置上。 本文將引導您：

* Toocreate 支援的要求。
* 如何支援工作階段中 toostart hello 您的 StorSimple 裝置的 Windows PowerShell 介面。

檢閱 hello [StorSimple 8000 系列支援 Sla 和資訊](https://msdn.microsoft.com/library/mt433077.aspx)建立支援要求之前。

## <a name="create-a-support-request"></a>建立支援要求
執行下列步驟 toocreate 支援要求的 hello:

#### <a name="toocreate-a-support-request"></a>toocreate 支援要求
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)hello 右上角，按一下您的帳戶名稱，然後按**請連絡 Microsoft 支援**。
   
    ![透過 ManagementPortal 連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. 您將會重新導向的 toohello 新版 Azure 入口網站 (portal.azure.com)。 按一下 hello**新增支援要求**磚。
   
    ![透過新的入口網站連絡 MS 支援服務](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    右側 hello 囉 」 畫面，hello**新增支援要求** 窗格隨即出現。 
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. 在 hello**基本概念**對話方塊中，下列的完整 hello:                                
   
   1. 從 hello**發出型別**下拉式清單中，選取**技術**。
   2. 選取**訂用帳戶**hello 下拉式清單中。
   3. 從 hello**服務**下拉式清單中，選取**StorSimple**。 
   4. 選取**支援計劃**hello 下拉式清單中。 您需要付費的支援計劃 tooenable 技術支援。
4. 按一下 [下一步] 。 hello**問題** 對話方塊隨即出現。
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. 在 hello**問題**對話方塊中，下列的完整 hello:
   
   1. 選取**嚴重性**hello 下拉式清單中的層級。
   2. 選取**問題類型**hello 下拉式清單中。
   3. 選取**類別**hello 下拉式清單中。 
   4. 在 hello**詳細資料**方塊中，簡要描述您的問題。
   5. 在 hello**時間範圍**方塊中，表示 hello 日期、 時間和時區對應 toohello 最近發生的問題。
   6. 在下**檔案上傳**，按一下 hello 資料夾圖示 toobrowse tooyour 支援封裝。
   7. 選取 hello**共用診斷資訊**核取方塊。
6. 按一下 [下一步] 。 hello**連絡資訊** 對話方塊隨即出現。
   
    ![新的支援要求窗格](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. 輸入您的連絡資訊，並選取一個連絡方法 (電話或電子郵件)。 
8. 選取 hello**儲存連絡人變更，以供後續支援要求**核取方塊。
9. 按一下 [建立] 。

提交您的要求之後，支援工程師會與您連絡儘速 tooproceed 您的要求。

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>在 Windows PowerShell for StorSimple 中啟動支援工作階段
tootroubleshoot 所有問題，您可能會遇到與 hello StorSimple 裝置，您將需要 tooengage 與 hello Microsoft 技術支援小組。 Microsoft 支援服務可能需要 toouse 支援工作階段 toolog tooyour 裝置上。 

執行下列 hello toostart 支援工作階段的步驟：

#### <a name="toostart-a-support-session"></a>toostart 支援工作階段
1. 存取 hello 裝置直接使用 hello 序列主控台或透過 telnet 工作階段從遠端電腦。 toodo 中的，遵循 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)。
2. 在開啟的 hello 工作階段，請按 hello **Enter**金鑰 tooget 命令提示字元。
3. 在 hello 序列主控台功能表中，選取選項 1，**登入的完整存取**。
4. 在 hello 提示字元中輸入下列密碼 hello: 
   
    `Password1`
5. 在 hello 提示字元中輸入下列命令的 hello:
   
    `Enable-HcsSupportAccess`
6. 加密的字串將會出現 tooyou。 將此字串複製到 [記事本] 之類的文字編輯器。
7. 儲存這個字串，並將它傳送電子郵件訊息 tooMicrosoft 支援。 

> [!IMPORTANT]
> 您可以執行 `Disable-HcsSupportAccess` 來停用支援存取。 hello StorSimple 裝置也會嘗試 toodisable 支援服務存取 8 小時 hello 工作階段起始後。 啟動支援工作階段後認證您的 StorSimple 裝置的最佳作法 toochange 它。
> 
> 

