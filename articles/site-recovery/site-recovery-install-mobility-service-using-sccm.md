---
title: "使用軟體部署工具的行動服務安裝 Azure Site recovery aaaAutomate |Microsoft 文件"
description: "本文協助您使用 System Center Configuration Manager 之類的軟體部署工具，將行動服務安裝進行自動化。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="d9114-103">使用軟體部署工具將行動服務安裝進行自動化</span><span class="sxs-lookup"><span data-stu-id="d9114-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="d9114-104">本文件假設您是使用 **9.9.4510.1** 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d9114-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="d9114-105">這篇文章會提供如何使用 System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility 服務，以及在資料中心中的範例。</span><span class="sxs-lookup"><span data-stu-id="d9114-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="d9114-106">使用像 Configuration Manager 的軟體部署工具有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d9114-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="d9114-107">在您規劃的軟體更新維護期間，排程全新安裝和升級的部署</span><span class="sxs-lookup"><span data-stu-id="d9114-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="d9114-108">同時調整伺服器部署的 toohundreds</span><span class="sxs-lookup"><span data-stu-id="d9114-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="d9114-109">本文使用 System Center Configuration Manager 2012 R2 toodemonstrate hello 部署活動。</span><span class="sxs-lookup"><span data-stu-id="d9114-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="d9114-110">您也可以使用 [Azure 自動化和期望的狀態設定](site-recovery-automate-mobility-service-install.md)，將行動服務安裝進行自動化。</span><span class="sxs-lookup"><span data-stu-id="d9114-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9114-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9114-111">Prerequisites</span></span>
1. <span data-ttu-id="d9114-112">環境中已部署的軟體部署工具，例如 Configuration Manager。</span><span class="sxs-lookup"><span data-stu-id="d9114-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="d9114-113">建立兩個[裝置集合](https://technet.microsoft.com/library/gg682169.aspx)，一個用於所有**Windows 伺服器**，而另一個用於所有**Linux 伺服器**，要 tooprotect 使用站台復原。</span><span class="sxs-lookup"><span data-stu-id="d9114-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="d9114-114">已向 Site Recovery 註冊的設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9114-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="d9114-115">安全的網路檔案共用 （伺服器訊息區共用） hello Configuration Manager 伺服器可存取。</span><span class="sxs-lookup"><span data-stu-id="d9114-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="d9114-116">在執行 Windows 的電腦上部署行動服務</span><span class="sxs-lookup"><span data-stu-id="d9114-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="d9114-117">本文章假設 hello hello 組態伺服器 IP 位址是 192.168.3.121，而且 hello 安全的網路檔案共用，且\\\ContosoSecureFS\MobilityServiceInstallers。</span><span class="sxs-lookup"><span data-stu-id="d9114-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="d9114-118">步驟 1︰準備部署</span><span class="sxs-lookup"><span data-stu-id="d9114-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="d9114-119">Hello 網路共用上建立資料夾並將其命名**MobSvcWindows**。</span><span class="sxs-lookup"><span data-stu-id="d9114-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="d9114-120">登入 tooyour 組態伺服器上，開啟 系統管理命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="d9114-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="d9114-121">執行下列命令 toogenerate 複雜密碼檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9114-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="d9114-122">複製 hello **MobSvc.passphrase**檔案 hello **MobSvcWindows**網路共用上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d9114-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="d9114-123">瀏覽 toohello hello 組態伺服器上的安裝程式儲存機制，藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9114-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="d9114-124">複製 hello  **Microsoft ASR\_UA\_*版本*\_Windows\_GA\_*日期*\_Release.exe** toohello **MobSvcWindows**網路共用上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d9114-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="d9114-125">複製 hello 下列程式碼，並將它儲存成**install.bat**到 hello **MobSvcWindows**資料夾。</span><span class="sxs-lookup"><span data-stu-id="d9114-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d9114-126">此指令碼中的 hello [CSIP] 預留位置取代為 hello hello IP 位址的組態伺服器的實際值。</span><span class="sxs-lookup"><span data-stu-id="d9114-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="d9114-127">步驟 2：建立套件</span><span class="sxs-lookup"><span data-stu-id="d9114-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="d9114-128">登入 tooyour Configuration Manager 主控台。</span><span class="sxs-lookup"><span data-stu-id="d9114-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="d9114-129">瀏覽過**軟體程式庫** > **應用程式管理** > **封裝**。</span><span class="sxs-lookup"><span data-stu-id="d9114-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="d9114-130">以滑鼠右鍵按一下 [套件]，然後選取 [建立套件]。</span><span class="sxs-lookup"><span data-stu-id="d9114-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="d9114-131">提供的 hello 名稱、 描述、 製造商、 語言和版本值。</span><span class="sxs-lookup"><span data-stu-id="d9114-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="d9114-132">選取 hello**此套件包含來源檔案**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d9114-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="d9114-133">按一下**瀏覽**，並選取 hello hello 安裝程式所在的網路共用 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows)。</span><span class="sxs-lookup"><span data-stu-id="d9114-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="d9114-135">在 hello**選擇 hello 程式類型，而您想 toocreate**頁面上，選取**標準程式**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d9114-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="d9114-137">在 hello**指定此標準程式的相關資訊**頁面上，提供 hello 遵循輸入，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d9114-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="d9114-138">（hello 其他輸入可以使用其預設值）。</span><span class="sxs-lookup"><span data-stu-id="d9114-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="d9114-139">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="d9114-139">**Parameter name**</span></span> | <span data-ttu-id="d9114-140">**值**</span><span class="sxs-lookup"><span data-stu-id="d9114-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="d9114-141">名稱</span><span class="sxs-lookup"><span data-stu-id="d9114-141">Name</span></span> | <span data-ttu-id="d9114-142">安裝 Microsoft Azure 行動服務 (Windows)</span><span class="sxs-lookup"><span data-stu-id="d9114-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="d9114-143">命令列</span><span class="sxs-lookup"><span data-stu-id="d9114-143">Command line</span></span> | <span data-ttu-id="d9114-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="d9114-144">install.bat</span></span> |
  | <span data-ttu-id="d9114-145">程式可以執行</span><span class="sxs-lookup"><span data-stu-id="d9114-145">Program can run</span></span> | <span data-ttu-id="d9114-146">使用者是否登入</span><span class="sxs-lookup"><span data-stu-id="d9114-146">Whether or not a user is logged on</span></span> |

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="d9114-148">在 hello 下一個頁面上，選取目標作業系統 hello。</span><span class="sxs-lookup"><span data-stu-id="d9114-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="d9114-149">行動服務可以安裝在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2。</span><span class="sxs-lookup"><span data-stu-id="d9114-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="d9114-151">toocomplete hello 精靈] 中，按一下 [**下一步**兩次。</span><span class="sxs-lookup"><span data-stu-id="d9114-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="d9114-152">hello 指令碼支援的行動服務代理程式的這兩個新安裝，並更新已安裝的 tooagents。</span><span class="sxs-lookup"><span data-stu-id="d9114-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="d9114-153">步驟 3： 部署的 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="d9114-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="d9114-154">在 hello Configuration Manager 主控台中，以滑鼠右鍵按一下您的封裝，然後選取**發佈內容**。</span><span class="sxs-lookup"><span data-stu-id="d9114-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="d9114-155">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="d9114-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="d9114-156">選取 hello **[發佈點](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** hello 套件應該複製 toowhich 上。</span><span class="sxs-lookup"><span data-stu-id="d9114-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="d9114-157">Hello 完成精靈。</span><span class="sxs-lookup"><span data-stu-id="d9114-157">Complete hello wizard.</span></span> <span data-ttu-id="d9114-158">hello 封裝，然後啟動複寫 toohello 指定發佈點。</span><span class="sxs-lookup"><span data-stu-id="d9114-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="d9114-159">完成 hello 選套件發佈之後，hello 套件上按一下滑鼠右鍵，然後選取**部署**。</span><span class="sxs-lookup"><span data-stu-id="d9114-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="d9114-160">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="d9114-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="d9114-161">選取您要建立 hello 必要條件 > 一節中為部署的 hello 目標集合 hello Windows Server 裝置集合。</span><span class="sxs-lookup"><span data-stu-id="d9114-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="d9114-163">在 hello**指定 hello 內容目的地**頁面上，選取您**發佈點**。</span><span class="sxs-lookup"><span data-stu-id="d9114-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="d9114-164">在 hello**部署此軟體的方式指定設定 toocontrol**頁面上，確定 hello 用途是**需要**。</span><span class="sxs-lookup"><span data-stu-id="d9114-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="d9114-166">在 hello**指定此部署的 hello 排程**頁面上，指定的排程。</span><span class="sxs-lookup"><span data-stu-id="d9114-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="d9114-167">如需詳細資訊，請參閱 [排程套件](https://technet.microsoft.com/library/gg682178.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9114-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="d9114-168">在 hello**發佈點**頁面上，設定 hello 屬性，根據您的資料中心 toohello 需求。</span><span class="sxs-lookup"><span data-stu-id="d9114-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="d9114-169">然後完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="d9114-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="d9114-170">tooavoid 不需要重新開機期間您的每月維護期間或軟體更新期間的排程 hello 套件安裝。</span><span class="sxs-lookup"><span data-stu-id="d9114-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="d9114-171">您可以使用 hello Configuration Manager 主控台監視 hello 部署進度。</span><span class="sxs-lookup"><span data-stu-id="d9114-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="d9114-172">跳過**監視** > **部署** > *[封裝名稱]*。</span><span class="sxs-lookup"><span data-stu-id="d9114-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Configuration Manager 的螢幕擷取畫面選項 toomonitor 部署](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="d9114-174">在執行 Linux 的電腦上部署行動服務</span><span class="sxs-lookup"><span data-stu-id="d9114-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="d9114-175">本文章假設 hello hello 組態伺服器 IP 位址是 192.168.3.121，而且 hello 安全的網路檔案共用，且\\\ContosoSecureFS\MobilityServiceInstallers。</span><span class="sxs-lookup"><span data-stu-id="d9114-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="d9114-176">步驟 1︰準備部署</span><span class="sxs-lookup"><span data-stu-id="d9114-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="d9114-177">Hello 網路共用上建立資料夾並將它做為命名**MobSvcLinux**。</span><span class="sxs-lookup"><span data-stu-id="d9114-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="d9114-178">登入 tooyour 組態伺服器上，開啟 系統管理命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="d9114-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="d9114-179">執行下列命令 toogenerate 複雜密碼檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9114-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="d9114-180">複製 hello **MobSvc.passphrase**檔案 hello **MobSvcLinux**網路共用上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="d9114-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="d9114-181">瀏覽 toohello hello 組態伺服器上的安裝程式儲存機制，藉由執行 hello 命令：</span><span class="sxs-lookup"><span data-stu-id="d9114-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="d9114-182">複製 hello 下列檔案 toohello **MobSvcLinux**網路共用上的資料夾：</span><span class="sxs-lookup"><span data-stu-id="d9114-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="d9114-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="d9114-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9114-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9114-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9114-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="d9114-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="d9114-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="d9114-189">複製 hello 下列程式碼，並將它儲存成**install_linux.sh**到 hello **MobSvcLinux**資料夾。</span><span class="sxs-lookup"><span data-stu-id="d9114-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="d9114-190">此指令碼中的 hello [CSIP] 預留位置取代為 hello hello IP 位址的組態伺服器的實際值。</span><span class="sxs-lookup"><span data-stu-id="d9114-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="d9114-191">步驟 2：建立套件</span><span class="sxs-lookup"><span data-stu-id="d9114-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="d9114-192">登入 tooyour Configuration Manager 主控台。</span><span class="sxs-lookup"><span data-stu-id="d9114-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="d9114-193">瀏覽過**軟體程式庫** > **應用程式管理** > **封裝**。</span><span class="sxs-lookup"><span data-stu-id="d9114-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="d9114-194">以滑鼠右鍵按一下 [套件]，然後選取 [建立套件]。</span><span class="sxs-lookup"><span data-stu-id="d9114-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="d9114-195">提供的 hello 名稱、 描述、 製造商、 語言和版本值。</span><span class="sxs-lookup"><span data-stu-id="d9114-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="d9114-196">選取 hello**此套件包含來源檔案**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d9114-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="d9114-197">按一下**瀏覽**，並選取 hello hello 安裝程式所在的網路共用 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux)。</span><span class="sxs-lookup"><span data-stu-id="d9114-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="d9114-199">在 hello**選擇 hello 程式類型，而您想 toocreate**頁面上，選取**標準程式**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d9114-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="d9114-201">在 hello**指定此標準程式的相關資訊**頁面上，提供 hello 遵循輸入，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d9114-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="d9114-202">（hello 其他輸入可以使用其預設值）。</span><span class="sxs-lookup"><span data-stu-id="d9114-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="d9114-203">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="d9114-203">**Parameter name**</span></span> | <span data-ttu-id="d9114-204">**值**</span><span class="sxs-lookup"><span data-stu-id="d9114-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="d9114-205">名稱</span><span class="sxs-lookup"><span data-stu-id="d9114-205">Name</span></span> | <span data-ttu-id="d9114-206">安裝 Microsoft Azure 行動服務 (Linux)</span><span class="sxs-lookup"><span data-stu-id="d9114-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="d9114-207">命令列</span><span class="sxs-lookup"><span data-stu-id="d9114-207">Command line</span></span> | <span data-ttu-id="d9114-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="d9114-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="d9114-209">程式可以執行</span><span class="sxs-lookup"><span data-stu-id="d9114-209">Program can run</span></span> | <span data-ttu-id="d9114-210">使用者是否登入</span><span class="sxs-lookup"><span data-stu-id="d9114-210">Whether or not a user is logged on</span></span> |

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="d9114-212">在 hello 下一個頁面上，選取**此程式可以在任何平台上執行**。</span><span class="sxs-lookup"><span data-stu-id="d9114-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="d9114-213">![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="d9114-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="d9114-214">toocomplete hello 精靈] 中，按一下 [**下一步**兩次。</span><span class="sxs-lookup"><span data-stu-id="d9114-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="d9114-215">hello 指令碼支援的行動服務代理程式的這兩個新安裝，並更新已安裝的 tooagents。</span><span class="sxs-lookup"><span data-stu-id="d9114-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="d9114-216">步驟 3： 部署的 hello 封裝</span><span class="sxs-lookup"><span data-stu-id="d9114-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="d9114-217">在 hello Configuration Manager 主控台中，以滑鼠右鍵按一下您的封裝，然後選取**發佈內容**。</span><span class="sxs-lookup"><span data-stu-id="d9114-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="d9114-218">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="d9114-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="d9114-219">選取 hello **[發佈點](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** hello 套件應該複製 toowhich 上。</span><span class="sxs-lookup"><span data-stu-id="d9114-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="d9114-220">Hello 完成精靈。</span><span class="sxs-lookup"><span data-stu-id="d9114-220">Complete hello wizard.</span></span> <span data-ttu-id="d9114-221">hello 封裝，然後啟動複寫 toohello 指定發佈點。</span><span class="sxs-lookup"><span data-stu-id="d9114-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="d9114-222">完成 hello 選套件發佈之後，hello 套件上按一下滑鼠右鍵，然後選取**部署**。</span><span class="sxs-lookup"><span data-stu-id="d9114-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="d9114-223">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="d9114-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="d9114-224">選取 hello Linux 伺服器裝置集合，您在 hello 必要條件 > 一節中建立為部署的 hello 目標集合。</span><span class="sxs-lookup"><span data-stu-id="d9114-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="d9114-226">在 hello**指定 hello 內容目的地**頁面上，選取您**發佈點**。</span><span class="sxs-lookup"><span data-stu-id="d9114-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="d9114-227">在 hello**部署此軟體的方式指定設定 toocontrol**頁面上，確定 hello 用途是**需要**。</span><span class="sxs-lookup"><span data-stu-id="d9114-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="d9114-229">在 hello**指定此部署的 hello 排程**頁面上，指定的排程。</span><span class="sxs-lookup"><span data-stu-id="d9114-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="d9114-230">如需詳細資訊，請參閱 [排程套件](https://technet.microsoft.com/library/gg682178.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9114-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="d9114-231">在 hello**發佈點**頁面上，設定 hello 屬性，根據您的資料中心 toohello 需求。</span><span class="sxs-lookup"><span data-stu-id="d9114-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="d9114-232">然後完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="d9114-232">Then complete hello wizard.</span></span>

<span data-ttu-id="d9114-233">取得在 hello Linux 伺服器的裝置集合，根據您所設定的 toohello 排程上安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="d9114-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="d9114-234">其他方法 tooinstall 行動服務</span><span class="sxs-lookup"><span data-stu-id="d9114-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="d9114-235">以下是一些安裝行動服務的其他選項︰</span><span class="sxs-lookup"><span data-stu-id="d9114-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="d9114-236">使用 GUI 手動安裝</span><span class="sxs-lookup"><span data-stu-id="d9114-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="d9114-237">使用命令列手動安裝</span><span class="sxs-lookup"><span data-stu-id="d9114-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="d9114-238">使用設定伺服器推送安裝</span><span class="sxs-lookup"><span data-stu-id="d9114-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="d9114-239">使用 Azure 自動化和期望的狀態設定來自動化安裝</span><span class="sxs-lookup"><span data-stu-id="d9114-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="d9114-240">將行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="d9114-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="d9114-241">您可以建立 Configuration Manager 封裝 toouninstall 行動服務。</span><span class="sxs-lookup"><span data-stu-id="d9114-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="d9114-242">使用下列指令碼 toodo 因此 hello:</span><span class="sxs-lookup"><span data-stu-id="d9114-242">Use hello following script toodo so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="d9114-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9114-243">Next steps</span></span>
<span data-ttu-id="d9114-244">現在您已經準備就緒太[啟用保護](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications)您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d9114-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
