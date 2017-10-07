---
title: "aaaConnect 遠端 tooyour StorSimple 裝置 |Microsoft 文件"
description: "說明如何 tooconfigure 進行遠端管理裝置以及如何 tooconnect tooWindows PowerShell for StorSimple 透過 HTTP 或 HTTPS。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>從遠端連線 tooyour StorSimple 8000 系列裝置

## <a name="overview"></a>概觀
您可以使用 Windows PowerShell 遠端執行功能 tooconnect tooyour StorSimple 裝置。 當您以這種方式連線時，將不會看到功能表。 （您看到功能表只有當您使用 hello 序列主控台上 hello 裝置 tooconnect。）使用 Windows PowerShell 遠端功能，您可以連接 tooa 特定 runspace。 您也可以指定 hello 顯示語言。 

如需有關如何使用 Windows PowerShell 遠端執行功能 toomanage 裝置的詳細資訊，請移至太[使用 Windows PowerShell for StorSimple tooadminister StorSimple 裝置](storsimple-windows-powershell-administration.md)。

本教學課程說明如何 tooconfigure 您的裝置進行遠端管理，然後如何 tooconnect tooWindows PowerShell for StorSimple。 您可以使用 HTTP 或 HTTPS tooconnect 透過 Windows PowerShell 遠端功能。 不過，當您在決定如何 tooconnect tooWindows PowerShell for StorSimple，請考量下列 hello: 

* 直接連接 toohello 裝置序列主控台安全，但不是透過網路交換器連接 toohello 序列主控台。 請小心 hello 安全性風險的 toohello 裝置序列主控台連接的網路交換器上時。 
* 透過 HTTP 工作階段連線，可能會提供更高的安全性，比起透過序列主控台的 hello hello 網路上。 雖然這不是 hello 最安全的方法，它是受信任的網路接受。 
* 透過使用自我簽署憑證的 HTTPS 工作階段連接是最安全的 hello 與 hello 建議的選項。

您可以從遠端連線 toohello Windows PowerShell 介面。 不過，預設不會啟用透過 hello Windows PowerShell 介面的遠端存取 tooyour StorSimple 裝置。 您首先需要 tooenable hello 裝置上的啟用遠端管理，然後在 hello 用戶端，其使用的 tooaccess 您的裝置。

這篇文章中所述的 hello 步驟未執行 Windows Server 2012 R2 的主機系統上執行。

## <a name="connect-through-http"></a>透過 HTTP 連線
透過 HTTP 工作階段已連線的 tooWindows PowerShell for StorSimple 提供更高的安全性，比起透過 hello StorSimple 裝置序列主控台。 雖然這不是 hello 最安全的方法，它是受信任的網路接受。

您可以使用 hello Azure 傳統入口網站或 hello 序列主控台 tooconfigure 遠端管理。 選取從下列程序的 hello:

* [透過 HTTP 使用 hello Azure 傳統入口網站 tooenable 遠端管理](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [透過 HTTP 使用 hello 序列主控台 tooenable 遠端管理](#use-the-serial-console-to-enable-remote-management-over-http)

啟用遠端管理之後，使用下列程序的遠端連線 tooprepare hello 用戶端 hello。

* [準備 hello 用戶端的遠端連線](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>透過 HTTP 使用 hello Azure 傳統入口網站 tooenable 遠端管理
執行下列步驟在 hello Azure 傳統入口網站 tooenable 遠端管理透過 HTTP 的 hello。

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>tooenable 透過 hello Azure 傳統入口網站的遠端管理
1. 針對您的裝置存取 [裝置] > [設定]。
2. 捲動 toohello**遠端管理**> 一節。
3. 設定**啟用遠端管理**太**是**。
4. 您現在可以選擇使用 HTTP tooconnect。 （hello 預設會為 tooconnect over HTTPS）。請確定已選取 HTTP。
   
   > [!NOTE]
   > 只有受信任的網路上才接受透過 HTTP 來連接。
   > 
   > 
5. 按一下**儲存**hello hello 頁底端。

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>透過 HTTP 使用 hello 序列主控台 tooenable 遠端管理
執行下列步驟 hello 裝置序列主控台 tooenable 遠端管理的 hello。

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>透過裝置序列主控台時，hello tooenable 遠端管理
1. 在 hello 序列主控台功能表中，選取選項 1。 如需 hello 裝置上使用 hello 序列主控台的詳細資訊，請移太[tooWindows PowerShell for StorSimple 透過裝置序列主控台](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。
2. 在 hello 提示字元中，輸入：`Enable-HcsRemoteManagement –AllowHttp`
3. 您會告知使用 HTTP tooconnect toohello 裝置 hello 安全性弱點。 出現提示時，輸入 **Y**確認。
4. 確認 HTTP 已啟用，做法是輸入: `Get-HcsSystem`
5. 請確認該 hello **RemoteManagementMode**  欄位會顯示**HttpsAndHttpEnabled**.hello 下列圖例會在 PuTTY 中顯示這些設定。
   
     ![序列 HTTPS 和 HTTP 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>準備 hello 用戶端的遠端連線
執行下列步驟在 hello 的用戶端 tooenable 遠端管理的 hello。

#### <a name="tooprepare-hello-client-for-remote-connection"></a>tooprepare hello 用戶端的遠端連線
1. 以系統管理員的身分開啟 Windows PowerShell工作階段。
2. 輸入下列命令 tooadd hello 的 hello StorSimple 裝置 toohello 用戶端的信任的主機清單的 IP 位址的 hello: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     取代 <*device_ip*> hello IP 位址，為您的裝置; 例如： 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. 輸入下列命令 toosave hello 裝置認證的變數中的 hello: 
   
    ```
    $cred = Get-Credential
    ```
    
4. 在 [hello] 對話方塊中，會出現：
   
   1. 輸入 hello 的使用者名稱格式如下： *device_ip\SSAdmin*。
   2. 輸入 hello 裝置系統管理員密碼設定 hello 安裝精靈中的 hello 裝置時所設定。 hello 預設密碼為*Password1*。
5. 啟動 Windows PowerShell 工作階段 hello 裝置上，輸入下列命令：
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > hello StorSimple 虛擬裝置搭配使用的 Windows PowerShell 工作階段的 toocreate 附加 hello`–Port`參數並指定您要設定遠端處理中 StorSimple 虛擬應用裝置 hello 公用連接埠。
   > 
   > 
   
     此時，您應該有作用中遠端 Windows PowerShell 工作階段 toohello 裝置。
   
    ![使用 HTTPS 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>透過 HTTP 連線
連接 tooWindows PowerShell for StorSimple，透過 HTTPS 工作階段是 hello 最安全且為建議的遠端連線 tooyour Microsoft Azure StorSimple 裝置的方法。 hello 下列程序說明如何設定 tooset hello 序列主控台及用戶端電腦以便您可以使用 HTTPS tooconnect tooWindows PowerShell for StorSimple。

您可以使用 hello Azure 傳統入口網站或 hello 序列主控台 tooconfigure 遠端管理。 選取從下列程序的 hello:

* [使用透過 HTTPS 的 hello Azure 傳統入口網站 tooenable 遠端管理](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [使用透過 HTTPS 的 hello 序列主控台 tooenable 遠端管理](#use-the-serial-console-to-enable-remote-management-over-https)

啟用遠端管理之後，請使用下列程序 tooprepare hello 主機遠端管理的 hello，並從 hello 遠端主機連接 toohello 裝置。

* [準備 hello 主機遠端管理](#prepare-the-host-for-remote-management)
* [從 hello 遠端主機連接 toohello 裝置](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>使用透過 HTTPS 的 hello Azure 傳統入口網站 tooenable 遠端管理
執行下列步驟在 hello Azure 傳統入口網站 tooenable 遠端管理透過 HTTPS 的 hello。

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>tooenable 從遠端管理透過 HTTPS hello Azure 傳統入口網站
1. 針對您的裝置存取 [裝置] > [設定]。
2. 捲動 toohello**遠端管理**> 一節。
3. 設定**啟用遠端管理**太**是**。
4. 您現在可以選擇 tooconnect 使用 HTTPS。 （hello 預設會為 tooconnect over HTTPS）。請確定已選取 HTTPS。 
5. 按一下 [ **下載遠端管理憑證**]。 指定位置 toosave 這個檔案。 您將需要 tooinstall hello 用戶端或主機電腦上的，您將使用 tooconnect toohello 裝置此憑證。
6. 按一下**儲存**hello hello 頁底端。

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>使用透過 HTTPS 的 hello 序列主控台 tooenable 遠端管理
執行下列步驟 hello 裝置序列主控台 tooenable 遠端管理的 hello。

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>透過裝置序列主控台時，hello tooenable 遠端管理
1. 在 hello 序列主控台功能表中，選取選項 1。 如需 hello 裝置上使用 hello 序列主控台的詳細資訊，請移太[tooWindows PowerShell for StorSimple 透過裝置序列主控台](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)。
2. 在 hello 提示字元中，輸入： 
   
     `Enable-HcsRemoteManagement`
   
    這應該會在您的裝置上啟用 HTTPS。
3. 確認 HTTPS 已啟用，做法是輸入： 
   
     `Get-HcsSystem`
   
    請確定該 hello **RemoteManagementMode**  欄位會顯示**HttpsEnabled**.hello 下列圖例會在 PuTTY 中顯示這些設定。
   
     ![序列 HTTPS 已啟用](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. 從 hello 輸出`Get-HcsSystem`、 複製 hello 裝置 hello 序號，並將它儲存供稍後使用。
   
   > [!NOTE]
   > hello 數列數字對應 toohello hello 憑證中的 CN 名稱。
   > 
   > 
5. 取得遠端管理憑證，做法是輸入： 
   
     `Get-HcsRemoteManagementCert`
   
    會出現類似 toohello 後的憑證。
   
    ![取得遠端管理憑證](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. 從 hello 憑證中複製 hello 資訊**---BEGIN CERTIFICATE---**太**---憑證結尾---**到文字編輯器例如記事本，並將它儲存為.cer 檔案。 （您將可以複製此檔案 tooyour 遠端主機當您準備 hello 主機）。
   
   > [!NOTE]
   > toogenerate 新憑證時，使用 hello `Set-HcsRemoteManagementCert` cmdlet。
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>準備 hello 主機遠端管理
tooprepare hello 主機電腦的遠端連線使用 HTTPS 工作階段，執行下列程序的 hello:

* [匯入 hello.cer 檔案的 hello 用戶端或遠端主機的 hello 根存放區](#to-import-the-certificate-on-the-remote-host)。
* [Hello 裝置序號 toohello 主機將檔案加入您的遠端主機上](#to-add-device-serial-numbers-to-the-remote-host)。

以下說明上述各程序。

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>hello 遠端主機上的 tooimport hello 憑證
1. Hello.cer 檔案上按一下滑鼠右鍵，然後選取**安裝憑證**。 這會啟動 hello 憑證匯入精靈。
   
    ![憑證匯入精靈 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. 存放區位置 請選取 本機電腦，然後按一下下一步。
3. 選取**將所有憑證都放入下列存放區的 hello**，然後按一下**瀏覽**。 巡覽至遠端主機，toohello 根存放區，然後按一下**下一步**。
   
    ![憑證匯入精靈  2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. 按一下 [完成] 。 出現訊息，告訴您 hello 匯入成功。
   
    ![憑證匯入精靈  3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>tooadd 裝置序號 toohello 遠端主機
1. 身為管理員，啟動 [記事本]，然後開啟位於 \Windows\System32\Drivers\etc 的 hello 主機檔案。
2. 新增下列三個項目 tooyour 主機檔 hello: **DATA 0 IP 位址**，**控制器 0 固定 IP 位址**，和**控制器 1 固定 IP 位址**。
3. 輸入您稍早儲存的 hello 裝置序列值。 將這個 toohello IP 位址 hello 下列影像所示。 針對控制器 0 及控制器 1，請附加**Controller0**和**Controller1**結尾 hello hello 序號 （CN 名稱）。
   
    ![正在將 CN 名稱 toohosts 檔案](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. 儲存 hello 主機檔案。

### <a name="connect-toohello-device-from-hello-remote-host"></a>從 hello 遠端主機連接 toohello 裝置
使用 Windows PowerShell 及 SSL tooenter 從遠端主機或用戶端裝置上的 SSAdmin 工作階段。 hello SSAdmin 工作階段對應 toooption 1 在 hello[序列主控台](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console)功能表上，您的裝置。

執行下列程序 hello 要從中 toomake hello 遠端 Windows PowerShell 連線的電腦上的 hello。

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>使用 Windows PowerShell 及 SSL hello 裝置上的 SSAdmin 工作階段的 tooenter
1. 以系統管理員的身分開啟 Windows PowerShell工作階段。
2. 輸入以新增 hello 裝置 IP 位址 toohello 用戶端的受信任的主機：
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    其中 <*device_ip*> 是您的裝置 hello IP 位址。 例如： 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. 建立新認證，做法是： 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    其中 <*目標裝置的 IP*> 是的 DATA 0 為您的裝置; hello IP 位址，例如**10.126.173.90** hello 前面 hello 主機檔案的映像中所示。 此外，提供您的裝置 hello 系統管理員密碼。
4. 建立工作階段，做法是輸入：
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Hello 指令程式中的 hello-ComputerName 參數，提供 hello <*的目標裝置的序號*>。 這個序號對應 toohello hello 遠端主機; 上的 hosts 檔案中的 DATA 0 的 IP 位址例如， **SHX0991003G44MT** hello 下列影像所示。
5. 輸入： 
   
     `Enter-PSSession $session`
6. 您將需要 toowait 幾分鐘的時間，就能透過 SSL 透過 HTTPS 連線的 tooyour 裝置。 您會看到一個訊息，指出您是連接的 tooyour 裝置。
   
    ![使用 HTTPS 和 SSL 進行 PowerShell 遠端處理](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>後續步驟
* 深入了解[使用您的 StorSimple 裝置的 Windows PowerShell tooadminister](storsimple-windows-powershell-administration.md)。
* 深入了解[使用您的 StorSimple 裝置 hello StorSimple Manager 服務 tooadminister](storsimple-manager-service-administration.md)。

