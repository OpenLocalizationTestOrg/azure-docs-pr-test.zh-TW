---
title: "設定為檔案伺服器的 StorSimple Virtual Array aaaSet |Microsoft 文件"
description: "此 StorSimple Virtual Array 部署中的第三個教學課程指示 tooset 虛擬裝置做為檔案伺服器。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>部署 StorSimple Virtual Array - 透過 Azure 入口網站設定為檔案伺服器
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>簡介
本文說明 tooperform 初始安裝時，如何註冊您的 StorSimple 檔案伺服器，完成 hello 裝置設定，以及建立和連接 tooSMB 共用。 這是 hello 最後一篇文章 hello 數列中的 部署教學課程所需 toocompletely 部署您的虛擬陣列做為檔案伺服器或 iSCSI 伺服器。

hello 安裝和設定程序可能需要約為 10 分鐘 toocomplete。 本文章中的 hello 資訊適用於僅 toohello 部署的 hello StorSimple Virtual Array。 StorSimple 8000 系列裝置 hello 部署，請移至：[部署執行更新 2 您 StorSimple 8000 系列裝置](storsimple-deployment-walkthrough-u2.md)。

## <a name="setup-prerequisites"></a>安裝的必要條件
在您設定及安裝 StorSimple Virtual Array 之前，請先確定：

* 您已佈建的虛擬陣列和連接中所述的 hello 為 tooit[佈建為 HYPER-V 中的 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-hyperv.md)或[佈建在 VMware 中的 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-vmware.md)。
* 您必須從您建立 toomanage StorSimple 虛擬陣列 hello StorSimple 裝置管理員服務的 hello 服務註冊金鑰。 如需詳細資訊，請參閱[步驟 2： 取得 hello 服務註冊金鑰](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)StorSimple 虛擬陣列。
* 如果這是 hello 第二或後續虛擬陣列，您會註冊現有的 StorSimple 裝置管理員服務時，您應該 hello 服務資料加密金鑰。 此服務已成功註冊 hello 第一個裝置時，所產生此金鑰。 如果您遺失了金鑰，請參閱[Get hello 服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)為 StorSimple 虛擬陣列。

## <a name="step-by-step-setup"></a>安裝的逐步指示
使用遵循逐步指示 tooset hello 並設定您的 StorSimple Virtual Array。

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>步驟 1： 完成 hello 本機 web UI 安裝並註冊您的裝置
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete hello 安裝和註冊的裝置 hello
1. 開啟瀏覽器視窗，並連接 toohello 本機 web UI。 輸入：
   
   `https://<ip-address of network interface>`
   
   使用 hello 上一個步驟中所述的 hello 連接 URL。 您看到錯誤，指出 hello 網站的安全性憑證有問題。 按一下**繼續 toothis 網頁**。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. 登入 toohello web UI 的虛擬陣列做為**StorSimpleAdmin**。 輸入 hello 裝置系統管理員變更密碼。 您在步驟 3： 中的開始 hello 虛擬陣列[佈建為 HYPER-V 中的 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-hyperv.md)或[佈建在 VMware 中的 StorSimple Virtual Array](storsimple-virtual-array-deploy2-provision-vmware.md)。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. 即會進入 toohello**首頁**頁面。 此頁面描述 hello tooconfigure 和註冊 hello 與 hello StorSimple 裝置管理員服務的虛擬陣列所需的各種設定。 hello**網路設定**， **Web proxy 設定**，和**時間設定**是選擇性的。 hello 只需要設定**裝置設定**和**雲端設定**。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. 在 hello**網路設定**頁面**網路介面**，DATA 0 將會為您自動設定。 每個網路介面，會使用預設 tooget IP 位址自動設定 (DHCP)。 因此，系統會自動指派 IP 位址、子網路和閘道 (IPv4 和 IPv6 皆適用)。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   如果您加入多個網路介面 hello 佈建的 hello 裝置期間，您可以在此設定。 請注意，您可以將您的網路介面設定為僅 IPv4 或 IPv4 和 IPv6。 不支援僅 IPv6 組態。
5. 因為它們由您的裝置嘗試與您的雲端儲存體服務提供者或 tooresolve toocommunicate 您的裝置時名稱設定為檔案伺服器時，都需要 DNS 伺服器。 在 hello**網路設定**頁面下 hello **DNS 伺服器**:
   
   1. 系統會自動設定主要及次要 DNS 伺服器。 如果您選擇 tooconfigure 靜態 IP 位址，您可以指定 DNS 伺服器。 為了達到高可用性，我們建議您設定主要及次要 DNS 伺服器。
   2. 按一下**套用**tooapply 並驗證 hello 網路設定。
6. 在 hello**裝置設定**頁面：
   
   1. 指派一個唯一**名稱**tooyour 裝置。 這個名稱可以有 1 至 15 個字元，且可以包含字母、數字和連字號。
   2. 按一下 hello**檔案伺服器**圖示![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png)hello**類型**裝置所建立。 檔案伺服器可讓您 toocreate 共用資料夾。
   3. 因為您的裝置是檔案伺服器，您將需要 toojoin hello 裝置 tooa 網域。 輸入 [網域名稱] 。
   4. 按一下 [Apply (套用)] 。
7. 此時畫面會出現對話方塊。 Hello 指定的格式輸入您的網域認證。 按一下 [hello] 核取圖示。 hello 網域認證經過驗證。 如果 hello 認證不正確，您會看到一則錯誤訊息。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. 按一下 [Apply (套用)] 。 這將會套用並驗證 hello 裝置設定。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > 請確認虛擬陣列是在它自己的組織單位 (OU) 的 Active Directory 群組原則物件 (GPO) 所套用的 tooit 或繼承。 群組原則可能 hello StorSimple Virtual Array 上安裝應用程式，例如防毒軟體。 安裝其他軟體不支援，而且可能會導致 toodata 損毀。 
   > 
   > 
9. (可省略) 設定 Web Proxy 伺服器。 雖然 Web Proxy 設定是選用的，但請注意，如果您使用 Web Proxy，就只能在此處設定它。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   在 hello **Web proxy**頁面：
   
   1. 供應 hello **Web proxy URL**格式如下： *http://&lt;主機 IP 位址或 FDQN&gt;： 連接埠號碼*。 請注意，此處不支援 HTTPS URL。
   2. 將 [驗證] 指定為 [基本] 或 [無]。
   3. 如果使用驗證，則必須同時 tooprovide **Username**和**密碼**。
   4. 按一下 [Apply (套用)] 。 這將會驗證並套用 hello 設定 web proxy 設定。
10. （選擇性） 設定您的裝置，例如時區的 hello 時間設定與 hello 主要和次要 NTP 伺服器。 NTP 伺服器是必要的，因為您的裝置必須讓時間同步，才能與您的雲端服務提供者進行驗證。
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    在 hello**時間設定**頁面：
    
    1. 從 hello 下拉式清單中，選取 hello**時區**根據裝置正在部署中的 hello hello 地理位置。 hello 裝置的預設時區是太平洋標準時間。 裝置將針對所有排程的操作使用這個時區。
    2. 指定**主要 NTP 伺服器**為您的裝置，或接受 time.windows.com hello 預設值。請確定您的網路允許 NTP 流量 toopass 從您的資料中心 toohello 網際網路。
    3. (選擇性) 指定裝置的 [次要 NTP 伺服器]  。
    4. 按一下 [Apply (套用)] 。 這將會驗證並套用設定的 hello 時間設定。
11. 設定您的裝置 hello 雲端設定。 在此步驟中，您將完成 hello 本機裝置設定，並再將 hello 裝置註冊 StorSimple 裝置管理員服務。
    
    1. 輸入 hello**服務註冊金鑰**您取得[步驟 2： 取得 hello 服務註冊金鑰](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key)的 StorSimple Virtual Array。
    2. 如果這是您的第一個裝置向此服務時，會顯示以 hello**服務資料加密金鑰**。 複製這個金鑰，並將它儲存在安全的位置。 與 hello 服務註冊金鑰 tooregister 其他裝置以 hello StorSimple 裝置管理員服務需要此金鑰。 
       
       如果這不是您要向此服務的 hello 第一個裝置，您將需要 tooprovide hello 服務資料加密金鑰。 如需詳細資訊，請參閱 tooget hello[服務資料加密金鑰](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key)您的本機 web UI。
    3. 按一下 [註冊] 。 這會重新啟動裝置 hello。 您可能需要 toowait 2-3 分鐘，hello 裝置註冊成功。 Hello 裝置重新啟動之後，您將會進入 toohello 登在頁面中。
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. 傳回 toohello Azure 入口網站。 跳過**所有資源**，搜尋您的 StorSimple 裝置管理員服務。
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Hello 篩選在清單中，選取您的 StorSimple 裝置管理員服務，然後瀏覽過**管理 > 裝置**。 在 hello**裝置**刀鋒視窗中，確認該 hello 裝置已成功連接 toohello 服務，且 hello 狀態**已 tooset 準備註冊**。
    
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>步驟 2： 設定 hello 裝置為檔案伺服器
執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)toocomplete hello 所需裝置設定。

#### <a name="tooconfigure-hello-device-as-file-server"></a>tooconfigure hello 裝置為檔案伺服器
1. 移 tooyour StorSimple 裝置管理員服務，然後檢閱 太**管理 > 裝置**。 在 hello**裝置**刀鋒視窗中，選取 hello 您剛才建立的裝置。 此裝置會顯示為**已 tooset 準備註冊**。
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. 按一下 hello 裝置，您會看到指出該 hello 裝置準備好 toosetup 橫幅訊息。
   
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. 按一下**設定**hello 命令列上。 這會開啟 hello**設定**刀鋒視窗。 在 hello**設定**刀鋒視窗中，執行下列 hello:
   
    1. 自動填入 hello 檔案伺服器名稱。
    
    2. 請確定 hello 雲端儲存體加密設定得**啟用**。 這會對所有傳送 toohello 雲端的 hello 資料加密。 
    
    3. 256 位元 AES 金鑰可搭配 hello 加密的使用者定義索引鍵。 指定的 32 個字元的索引鍵，然後重新輸入 hello 金鑰 tooconfirm 它。 記錄 hello 金鑰在金鑰管理的應用程式中供日後參考。
    
    4. 按一下**設定必要設定**toospecify 儲存體帳戶認證 toobe 搭配您的裝置。 如果未設定儲存體帳戶認證，請按一下 [新增]。 **請確定您使用的 hello 儲存體帳戶支援區塊 blob。不支援分頁 Blob。** 關於 [區塊 Blob 和分頁 Blob](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) 的其他資訊。
   
    ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. 在 hello**新增儲存體帳戶認證**刀鋒視窗中，請勿遵循 hello: 

    1. 選擇目前的訂用帳戶，如果 hello 儲存體帳戶位於 hello hello 服務相同訂用帳戶。 指定另一個則 hello 儲存體帳戶超出 hello 服務訂用帳戶。 
    
    2. 從 hello 下拉式清單中，選擇現有的儲存體帳戶。 
    
    3. hello 位置會自動填入根據 hello 指定儲存體帳戶。 
    
    4. 啟用 SSL tooensure hello 裝置與 hello 雲端之間的安全網路通訊通道。
    
    5. 按一下**新增**tooadd 這個儲存體帳戶認證。 
   
        ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. 已成功建立 hello 儲存體帳戶認證，一旦 hello**設定**刀鋒視窗中將會更新 toodisplay hello 指定儲存體帳戶認證。 按一下 [設定] 。
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   您會看到正在建立檔案伺服器。 Hello 檔案伺服器已成功建立後，系統會通知您。
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   hello 裝置狀態也會變更太**線上**。
   
   ![設定檔案伺服器](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   您可以繼續 tooadd 共用。

## <a name="step-3-add-a-share"></a>步驟 3：新增共用
執行下列步驟在 hello hello [Azure 入口網站](https://portal.azure.com/)toocreate 共用。

#### <a name="toocreate-a-share"></a>toocreate 共用
1. 選取 hello 檔案伺服器裝置 hello 前面步驟中進行設定，然後按一下**...** （或以滑鼠右鍵按一下）。 在 [hello] 內容功能表選取**新增共用**。 或者，您可以按一下**+ 加入共用**hello 裝置命令列上。
   
   ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. 指定下列共用設定的 hello:

    1. 共用的唯一名稱。 hello 名稱必須是包含 3 too127 個字元的字串。
    
    2. 選擇性**描述**hello 共用。 hello 描述可協助識別 hello 共用擁有者。
    
    3. A**類型**hello 共用。 hello 類型可以是**分層**或**固定在本機**，與階層式正在 hello 預設值。 對於需要本機保證、低延遲，以及高效能的工作負載，請選取 [固定在本機]  共用。 對於所有其他資料，請選取 [階層式]  共用。
    固定在本機共用以佈建，並確保維持本機 toohello 裝置 hello hello 共用上的主要資料，並不 spill toohello 雲端。 階層式的共用上 hello 另一方面在精簡佈建。 當您建立階層式的共用時，hello 本機層上佈建的 hello 空間的 10%，90%的 hello 空間 hello 雲端中佈建。 比方說，如果您佈建 1 TB 磁碟區、 100 GB，也可以位於 hello 本機空間和 900GB 會用在 hello 雲端時 hello 資料層。 這會表示，如果您在 hello 裝置上執行所有 hello 的本機空間不足，您無法佈建階層式的共用。
   
    4. 在 hello**設為預設的完整權限**欄位中，指派 toohello hello 權限的使用者或正在存取此共用的 hello 群組。 指定 hello hello 使用者或群組的名稱 hello 使用者在 *john@contoso.com* 格式。 我們建議您使用使用者群組 （而非單一使用者） tooallow 系統管理員權限 tooaccess 這些共用。 您已指派 hello 權限之後，您可以使用檔案總管 toomodify 這些權限。
   
    5. 按一下**新增**toocreate hello 共用。 
    
        ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Hello 共用建立正在進行中，您會收到通知。
   
        ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Hello 共用建立以 hello 後指定設定，hello**共用**刀鋒視窗中將會更新 tooreflect hello 新共用。 根據預設，會啟用監視和備份 hello 共用。
   
    ![新增共用](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>步驟 4： 連接 toohello 共用
您現在需要 tooconnect tooone 或 hello 先前步驟中所建立的多個共用。 您的 Windows Server 主機連接 tooyour StorSimple Virtual Array 上執行這些步驟。

#### <a name="tooconnect-toohello-share"></a>tooconnect toohello 共用
1. 按![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png)+ 鍵。在 hello 執行視窗中，指定 hello *&#92; &#92;&lt;檔案伺服器名稱&gt;*為 hello 路徑，取代*檔案伺服器名稱*與 hello 裝置名稱，您指派的 tooyour 檔案伺服器。 按一下 [確定] 。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. 這會開啟 [檔案總管]。 您現在應該能夠 toosee hello 共用您建立的資料夾。 選取，然後按兩下共用 （資料夾） tooview hello 內容。
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. 您現在可以新增檔案 toothese 共用，並進行備份。

## <a name="next-steps"></a>後續步驟
了解如何 toouse hello 本機 web UI 太[管理您的 StorSimple Virtual Array](storsimple-ova-web-ui-admin.md)。

