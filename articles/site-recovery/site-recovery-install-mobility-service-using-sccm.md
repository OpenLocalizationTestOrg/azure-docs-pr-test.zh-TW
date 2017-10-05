---
title: "使用軟體部署工具將適用於 Azure Site Recovery 的行動服務安裝進行自動化 | Microsoft Docs"
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
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="cfff0-103">使用軟體部署工具將行動服務安裝進行自動化</span><span class="sxs-lookup"><span data-stu-id="cfff0-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="cfff0-104">本文件假設您是使用 **9.9.4510.1** 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cfff0-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="cfff0-105">本文提供範例說明如何使用 System Center Configuration Manager，將 Azure Site Recovery 行動服務部署在資料中心。</span><span class="sxs-lookup"><span data-stu-id="cfff0-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="cfff0-106">使用 Configuration Manager 之類的軟體部署工具有下列優點：</span><span class="sxs-lookup"><span data-stu-id="cfff0-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="cfff0-107">在您規劃的軟體更新維護期間，排程全新安裝和升級的部署</span><span class="sxs-lookup"><span data-stu-id="cfff0-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="cfff0-108">同時大規模部署至數百個伺服器</span><span class="sxs-lookup"><span data-stu-id="cfff0-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="cfff0-109">本文使用 System Center Configuration Manager 2012 R2 示範部署活動。</span><span class="sxs-lookup"><span data-stu-id="cfff0-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="cfff0-110">您也可以使用 [Azure 自動化和期望的狀態設定](site-recovery-automate-mobility-service-install.md)，將行動服務安裝進行自動化。</span><span class="sxs-lookup"><span data-stu-id="cfff0-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfff0-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="cfff0-111">Prerequisites</span></span>
1. <span data-ttu-id="cfff0-112">環境中已部署的軟體部署工具，例如 Configuration Manager。</span><span class="sxs-lookup"><span data-stu-id="cfff0-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="cfff0-113">建立兩個[裝置集合](https://technet.microsoft.com/library/gg682169.aspx)，一個用於所有 **Windows 伺服器**，另一個用於所有 **Linux 伺服器** (都是您想要使用 Site Recovery 保護的伺服器)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="cfff0-114">已向 Site Recovery 註冊的設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="cfff0-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="cfff0-115">Configuration Manager 伺服器可存取的安全網路檔案共用 (伺服器訊息區共用)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="cfff0-116">在執行 Windows 的電腦上部署行動服務</span><span class="sxs-lookup"><span data-stu-id="cfff0-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="cfff0-117">本文假設設定伺服器的 IP 位址為 192.168.3.121，且安全網路檔案共用是 \\\ContosoSecureFS\MobilityServiceInstallers。</span><span class="sxs-lookup"><span data-stu-id="cfff0-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="cfff0-118">步驟 1︰準備部署</span><span class="sxs-lookup"><span data-stu-id="cfff0-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="cfff0-119">在網路共用上建立資料夾，並命名為 **MobSvcWindows**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="cfff0-120">登入設定伺服器，然後將系統管理命令提示字元開啟。</span><span class="sxs-lookup"><span data-stu-id="cfff0-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="cfff0-121">執行下列命令來產生複雜密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="cfff0-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="cfff0-122">將 **MobSvc.passphrase** 檔案複製到網路共用上的 **MobSvcWindows** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfff0-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="cfff0-123">執行下列命令，以瀏覽至設定伺服器上的安裝程式存放庫：</span><span class="sxs-lookup"><span data-stu-id="cfff0-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="cfff0-124">將 **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** 複製到網路共用上的 **MobSvcWindows** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfff0-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="cfff0-125">複製下列程式碼，儲存為 **install.bat** 放在 **MobSvcWindows** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="cfff0-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cfff0-126">將此指令碼中的 [CSIP] 預留位置取代為設定伺服器 IP 位址的實際值。</span><span class="sxs-lookup"><span data-stu-id="cfff0-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="cfff0-127">步驟 2：建立套件</span><span class="sxs-lookup"><span data-stu-id="cfff0-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="cfff0-128">登入您的 Configuration Manager 主控台。</span><span class="sxs-lookup"><span data-stu-id="cfff0-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="cfff0-129">瀏覽至 [軟體程式庫] > [應用程式管理] > [套件]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="cfff0-130">以滑鼠右鍵按一下 [套件]，然後選取 [建立套件]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="cfff0-131">提供 [名稱]、[描述]、[製造商]、[語言] 和 [版本] 的值。</span><span class="sxs-lookup"><span data-stu-id="cfff0-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="cfff0-132">選取 [此套件包含來源檔案] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cfff0-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="cfff0-133">按一下 [瀏覽]，選取儲存安裝程式的網路共用 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="cfff0-135">在 [選擇您要建立的程式類型] 頁面上，選取 [標準程式]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="cfff0-137">在 [指定此標準程式的相關資訊] 頁面上，提供下列輸入，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="cfff0-138">(其他輸入可以使用其預設值。)</span><span class="sxs-lookup"><span data-stu-id="cfff0-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="cfff0-139">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="cfff0-139">**Parameter name**</span></span> | <span data-ttu-id="cfff0-140">**值**</span><span class="sxs-lookup"><span data-stu-id="cfff0-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="cfff0-141">名稱</span><span class="sxs-lookup"><span data-stu-id="cfff0-141">Name</span></span> | <span data-ttu-id="cfff0-142">安裝 Microsoft Azure 行動服務 (Windows)</span><span class="sxs-lookup"><span data-stu-id="cfff0-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="cfff0-143">命令列</span><span class="sxs-lookup"><span data-stu-id="cfff0-143">Command line</span></span> | <span data-ttu-id="cfff0-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="cfff0-144">install.bat</span></span> |
  | <span data-ttu-id="cfff0-145">程式可以執行</span><span class="sxs-lookup"><span data-stu-id="cfff0-145">Program can run</span></span> | <span data-ttu-id="cfff0-146">使用者是否登入</span><span class="sxs-lookup"><span data-stu-id="cfff0-146">Whether or not a user is logged on</span></span> |

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="cfff0-148">在下一頁，選取目標作業系統。</span><span class="sxs-lookup"><span data-stu-id="cfff0-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="cfff0-149">行動服務可以安裝在 Windows Server 2012 R2、Windows Server 2012 和 Windows Server 2008 R2。</span><span class="sxs-lookup"><span data-stu-id="cfff0-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="cfff0-151">按兩次 [下一步] 以完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="cfff0-152">指令碼支援全新安裝行動服務代理程式，以及升級至已安裝的代理程式。</span><span class="sxs-lookup"><span data-stu-id="cfff0-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="cfff0-153">步驟 3︰部署套件</span><span class="sxs-lookup"><span data-stu-id="cfff0-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="cfff0-154">在 Configuration Manager 主控台，以滑鼠右鍵按一下套件，然後選取 [發佈內容]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="cfff0-155">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="cfff0-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="cfff0-156">選取應該將套件複製過去的**[發佈點](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="cfff0-157">完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-157">Complete the wizard.</span></span> <span data-ttu-id="cfff0-158">套件便會開始複寫至指定的發佈點。</span><span class="sxs-lookup"><span data-stu-id="cfff0-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="cfff0-159">完成套件發佈後，以滑鼠右鍵按一下套件，然後選取 [部署]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="cfff0-160">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="cfff0-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="cfff0-161">選取您在必要條件一節所建立的 Windows Server 裝置集合，作為部署的目標集合。</span><span class="sxs-lookup"><span data-stu-id="cfff0-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="cfff0-163">在 [指定內容目的地] 頁面上，選取您的**發佈點**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="cfff0-164">在 [指定控制此軟體部署方式的設定] 頁面上，確定目的為**必要**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="cfff0-166">在 [指定此部署的排程] 頁面上指定排程。</span><span class="sxs-lookup"><span data-stu-id="cfff0-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="cfff0-167">如需詳細資訊，請參閱 [排程套件](https://technet.microsoft.com/library/gg682178.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="cfff0-168">根據資料中心的需求，在 [發佈點] 頁面上設定屬性。</span><span class="sxs-lookup"><span data-stu-id="cfff0-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="cfff0-169">然後完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="cfff0-170">為了避免不必要的重新開機，請排定在每月維護期間或軟體更新期間安裝套件。</span><span class="sxs-lookup"><span data-stu-id="cfff0-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="cfff0-171">您可以使用 Configuration Manager 主控台來監視部署進度。</span><span class="sxs-lookup"><span data-stu-id="cfff0-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="cfff0-172">移至 [監視] > [部署] > *[套件名稱]*。</span><span class="sxs-lookup"><span data-stu-id="cfff0-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![監視部署的 Configuration Manager 選項螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="cfff0-174">在執行 Linux 的電腦上部署行動服務</span><span class="sxs-lookup"><span data-stu-id="cfff0-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="cfff0-175">本文假設設定伺服器的 IP 位址為 192.168.3.121，且安全網路檔案共用是 \\\ContosoSecureFS\MobilityServiceInstallers。</span><span class="sxs-lookup"><span data-stu-id="cfff0-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="cfff0-176">步驟 1︰準備部署</span><span class="sxs-lookup"><span data-stu-id="cfff0-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="cfff0-177">在網路共用上建立資料夾，並命名為 **MobSvcLinux**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="cfff0-178">登入設定伺服器，然後將系統管理命令提示字元開啟。</span><span class="sxs-lookup"><span data-stu-id="cfff0-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="cfff0-179">執行下列命令來產生複雜密碼檔案：</span><span class="sxs-lookup"><span data-stu-id="cfff0-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="cfff0-180">將 **MobSvc.passphrase** 檔案複製到網路共用上的 **MobSvcLinux** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cfff0-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="cfff0-181">執行命令以瀏覽至設定伺服器上的安裝程式存放庫：</span><span class="sxs-lookup"><span data-stu-id="cfff0-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="cfff0-182">將下列檔案複製到網路共用上的 **MobSvcLinux** 資料夾：</span><span class="sxs-lookup"><span data-stu-id="cfff0-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="cfff0-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="cfff0-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cfff0-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cfff0-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cfff0-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cfff0-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cfff0-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="cfff0-189">複製下列程式碼，儲存為 **install_linux.sh** 放在 **MobSvcLinux** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="cfff0-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="cfff0-190">將此指令碼中的 [CSIP] 預留位置取代為設定伺服器 IP 位址的實際值。</span><span class="sxs-lookup"><span data-stu-id="cfff0-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="cfff0-191">步驟 2：建立套件</span><span class="sxs-lookup"><span data-stu-id="cfff0-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="cfff0-192">登入您的 Configuration Manager 主控台。</span><span class="sxs-lookup"><span data-stu-id="cfff0-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="cfff0-193">瀏覽至 [軟體程式庫] > [應用程式管理] > [套件]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="cfff0-194">以滑鼠右鍵按一下 [套件]，然後選取 [建立套件]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="cfff0-195">提供 [名稱]、[描述]、[製造商]、[語言] 和 [版本] 的值。</span><span class="sxs-lookup"><span data-stu-id="cfff0-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="cfff0-196">選取 [此套件包含來源檔案] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cfff0-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="cfff0-197">按一下 [瀏覽]，選取儲存安裝程式的網路共用 (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="cfff0-199">在 [選擇您要建立的程式類型] 頁面上，選取 [標準程式]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="cfff0-201">在 [指定此標準程式的相關資訊] 頁面上，提供下列輸入，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="cfff0-202">(其他輸入可以使用其預設值。)</span><span class="sxs-lookup"><span data-stu-id="cfff0-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="cfff0-203">**參數名稱**</span><span class="sxs-lookup"><span data-stu-id="cfff0-203">**Parameter name**</span></span> | <span data-ttu-id="cfff0-204">**值**</span><span class="sxs-lookup"><span data-stu-id="cfff0-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="cfff0-205">名稱</span><span class="sxs-lookup"><span data-stu-id="cfff0-205">Name</span></span> | <span data-ttu-id="cfff0-206">安裝 Microsoft Azure 行動服務 (Linux)</span><span class="sxs-lookup"><span data-stu-id="cfff0-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="cfff0-207">命令列</span><span class="sxs-lookup"><span data-stu-id="cfff0-207">Command line</span></span> | <span data-ttu-id="cfff0-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="cfff0-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="cfff0-209">程式可以執行</span><span class="sxs-lookup"><span data-stu-id="cfff0-209">Program can run</span></span> | <span data-ttu-id="cfff0-210">使用者是否登入</span><span class="sxs-lookup"><span data-stu-id="cfff0-210">Whether or not a user is logged on</span></span> |

  ![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="cfff0-212">在下一個頁面上，選取 [可在任何平台上執行這個程式]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="cfff0-213">![建立套件和程式精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="cfff0-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="cfff0-214">按兩次 [下一步] 以完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="cfff0-215">指令碼支援全新安裝行動服務代理程式，以及升級至已安裝的代理程式。</span><span class="sxs-lookup"><span data-stu-id="cfff0-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="cfff0-216">步驟 3︰部署套件</span><span class="sxs-lookup"><span data-stu-id="cfff0-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="cfff0-217">在 Configuration Manager 主控台，以滑鼠右鍵按一下套件，然後選取 [發佈內容]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="cfff0-218">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="cfff0-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="cfff0-219">選取應該將套件複製過去的**[發佈點](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="cfff0-220">完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-220">Complete the wizard.</span></span> <span data-ttu-id="cfff0-221">套件便會開始複寫至指定的發佈點。</span><span class="sxs-lookup"><span data-stu-id="cfff0-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="cfff0-222">完成套件發佈後，以滑鼠右鍵按一下套件，然後選取 [部署]。</span><span class="sxs-lookup"><span data-stu-id="cfff0-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="cfff0-223">![Configuration Manager 主控台的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="cfff0-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="cfff0-224">選取您在必要條件一節所建立的 Linux 伺服器裝置集合，作為部署的目標集合。</span><span class="sxs-lookup"><span data-stu-id="cfff0-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="cfff0-226">在 [指定內容目的地] 頁面上，選取您的**發佈點**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="cfff0-227">在 [指定控制此軟體部署方式的設定] 頁面上，確定目的為**必要**。</span><span class="sxs-lookup"><span data-stu-id="cfff0-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![部署軟體精靈的螢幕擷取畫面](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="cfff0-229">在 [指定此部署的排程] 頁面上指定排程。</span><span class="sxs-lookup"><span data-stu-id="cfff0-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="cfff0-230">如需詳細資訊，請參閱 [排程套件](https://technet.microsoft.com/library/gg682178.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="cfff0-231">根據資料中心的需求，在 [發佈點] 頁面上設定屬性。</span><span class="sxs-lookup"><span data-stu-id="cfff0-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="cfff0-232">然後完成精靈。</span><span class="sxs-lookup"><span data-stu-id="cfff0-232">Then complete the wizard.</span></span>

<span data-ttu-id="cfff0-233">行動服務會根據您設定的排程，安裝在 Linux 伺服器裝置集合上。</span><span class="sxs-lookup"><span data-stu-id="cfff0-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="cfff0-234">安裝行動服務的其他方法</span><span class="sxs-lookup"><span data-stu-id="cfff0-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="cfff0-235">以下是一些安裝行動服務的其他選項︰</span><span class="sxs-lookup"><span data-stu-id="cfff0-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="cfff0-236">使用 GUI 手動安裝</span><span class="sxs-lookup"><span data-stu-id="cfff0-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="cfff0-237">使用命令列手動安裝</span><span class="sxs-lookup"><span data-stu-id="cfff0-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="cfff0-238">使用設定伺服器推送安裝</span><span class="sxs-lookup"><span data-stu-id="cfff0-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="cfff0-239">使用 Azure 自動化和期望的狀態設定來自動化安裝</span><span class="sxs-lookup"><span data-stu-id="cfff0-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="cfff0-240">將行動服務解除安裝</span><span class="sxs-lookup"><span data-stu-id="cfff0-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="cfff0-241">您可以建立 Configuration Manager 套件，將行動服務解除安裝。</span><span class="sxs-lookup"><span data-stu-id="cfff0-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="cfff0-242">若要這樣做，請使用下列指令碼︰</span><span class="sxs-lookup"><span data-stu-id="cfff0-242">Use the following script to do so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cfff0-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cfff0-243">Next steps</span></span>
<span data-ttu-id="cfff0-244">您現在可以對虛擬機器[啟用保護](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications)。</span><span class="sxs-lookup"><span data-stu-id="cfff0-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
