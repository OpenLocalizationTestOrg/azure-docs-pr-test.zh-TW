---
title: "aaaMonitoring Operations Management Suite 安全性和稽核解決方案中的資源 |Microsoft 文件"
description: "這份文件可協助 toouse OMS 安全性和稽核功能 toomonitor 資源，並找出安全性問題。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="b88ae-103">在 Operations Management Suite 安全性和稽核內監視資源</span><span class="sxs-lookup"><span data-stu-id="b88ae-103">Monitoring resources in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="b88ae-104">這份文件可協助您使用 OMS 安全性和稽核功能 toomonitor 資源，並找出安全性問題。</span><span class="sxs-lookup"><span data-stu-id="b88ae-104">This document helps you use OMS Security and Audit capabilities toomonitor your resources and identify security issues.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="b88ae-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="b88ae-105">What is OMS?</span></span>
<span data-ttu-id="b88ae-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="b88ae-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="b88ae-107">關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b88ae-107">For more information about OMS, read hello article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="monitoring-resources"></a><span data-ttu-id="b88ae-108">監視資源</span><span class="sxs-lookup"><span data-stu-id="b88ae-108">Monitoring resources</span></span>
<span data-ttu-id="b88ae-109">只要可能，您會想 tooprevent 安全性事件發生在 hello 第一個位置。</span><span class="sxs-lookup"><span data-stu-id="b88ae-109">Whenever is possible, you will want tooprevent security incidents from happening in hello first place.</span></span> <span data-ttu-id="b88ae-110">不過，它是不可能 tooprevent 所有安全性事件。</span><span class="sxs-lookup"><span data-stu-id="b88ae-110">However, it is impossible tooprevent all security incidents.</span></span> <span data-ttu-id="b88ae-111">當發生安全性事件時，您必須 tooensure 其影響會降至最低。</span><span class="sxs-lookup"><span data-stu-id="b88ae-111">When a security incident does happen, you will need tooensure that its impact is minimized.</span></span>  <span data-ttu-id="b88ae-112">有三個重要的建議，可以使用的 toominimize hello 數字和 hello 安全性事件的影響：</span><span class="sxs-lookup"><span data-stu-id="b88ae-112">There are three critical recommendations that can be used toominimize hello number and hello impact of security incidents:</span></span>

* <span data-ttu-id="b88ae-113">定期評估您環境內的弱點。</span><span class="sxs-lookup"><span data-stu-id="b88ae-113">Routinely assess vulnerabilities in your environment.</span></span>
* <span data-ttu-id="b88ae-114">定期檢查所有電腦的系統和網路裝置 tooensure 他們擁有的所有安裝 hello 最新修補程式。</span><span class="sxs-lookup"><span data-stu-id="b88ae-114">Routinely check all computer systems and network devices tooensure that they have all of hello latest patches installed.</span></span>
* <span data-ttu-id="b88ae-115">定期檢查所有記錄檔和記錄機制，包括作業系統事件記錄檔、應用程式特定記錄檔,以及入侵偵測系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b88ae-115">Routinely check all logs and logging mechanisms, including operating system event logs, application specific logs and intrusion detection system logs.</span></span>

<span data-ttu-id="b88ae-116">OMS 安全性和稽核解決方案讓 IT tooactively 監視所有的資源，可協助安全性事件的 hello 影響降到最低。</span><span class="sxs-lookup"><span data-stu-id="b88ae-116">OMS Security and Audit solution enables IT tooactively monitor all resources, which can help minimize hello impact of security incidents.</span></span> <span data-ttu-id="b88ae-117">OMS 安全性和稽核俱備可用來監視資源的安全性網域。</span><span class="sxs-lookup"><span data-stu-id="b88ae-117">OMS Security and Audit has security domains that can be used for monitoring resources.</span></span> <span data-ttu-id="b88ae-118">hello 安全性網域提供快速存取 tooa 選項，將更多詳細資料中涵蓋下列網域安全性監視 hello:</span><span class="sxs-lookup"><span data-stu-id="b88ae-118">hello security domains provides quick access tooa options, for security monitoring hello following domains will be covered in more details:</span></span>

* <span data-ttu-id="b88ae-119">惡意程式碼評估</span><span class="sxs-lookup"><span data-stu-id="b88ae-119">Malware assessment</span></span>
* <span data-ttu-id="b88ae-120">更新評估</span><span class="sxs-lookup"><span data-stu-id="b88ae-120">Update assessment</span></span>
* <span data-ttu-id="b88ae-121">身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="b88ae-121">Identity and Access</span></span>

> [!NOTE]
> <span data-ttu-id="b88ae-122">如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b88ae-122">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="monitoring-system-protection"></a><span data-ttu-id="b88ae-123">監視系統保護</span><span class="sxs-lookup"><span data-stu-id="b88ae-123">Monitoring system protection</span></span>
<span data-ttu-id="b88ae-124">在防禦深度方法中，每個圖層的保護是很重要的 hello 整體的安全性狀態的資產。</span><span class="sxs-lookup"><span data-stu-id="b88ae-124">In a defense in depth approach, every layer of protection is important for hello overall security state of your asset.</span></span> <span data-ttu-id="b88ae-125">具有電腦偵測到威脅及保護效力不足的電腦會顯示在 hello 安全性網域底下的 [惡意程式碼評估] 磚。</span><span class="sxs-lookup"><span data-stu-id="b88ae-125">Computers with detected threats and computers with insufficient protection are shown in hello Malware Assessment tile under Security Domains.</span></span> <span data-ttu-id="b88ae-126">藉由使用 hello 惡意程式碼評估 hello 資訊，您可以識別計劃 tooapply 保護 toohello 需要伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b88ae-126">By using hello information on hello Malware Assessment, you can identify a plan tooapply protection toohello servers that need it.</span></span> <span data-ttu-id="b88ae-127">tooaccess 這個選項後續 hello 的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="b88ae-127">tooaccess this option follow hello steps below:</span></span>

1. <span data-ttu-id="b88ae-128">在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="b88ae-128">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="b88ae-130">在 hello**安全性和稽核**儀表板，按一下**反惡意程式碼評定**下**安全性網域**。</span><span class="sxs-lookup"><span data-stu-id="b88ae-130">In hello **Security and Audit** dashboard, click **Antimalware Assessment** under **Security Domains**.</span></span> <span data-ttu-id="b88ae-131">hello**反惡意程式碼評定**儀表板隨即出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b88ae-131">hello **Antimalware Assessment** dashboard appears as shown below:</span></span>

![惡意程式碼評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

<span data-ttu-id="b88ae-133">您可以使用 hello**惡意程式碼評估**儀表板 tooidentify hello 下列安全性問題：</span><span class="sxs-lookup"><span data-stu-id="b88ae-133">You can use hello **Malware Assessment** dashboard tooidentify hello following security issues:</span></span>

* <span data-ttu-id="b88ae-134">**作用中威脅**： 洩露和 hello 系統中有作用中威脅的電腦。</span><span class="sxs-lookup"><span data-stu-id="b88ae-134">**Active threats**: computers that were compromised and have active threats in hello system.</span></span>
* <span data-ttu-id="b88ae-135">**補救威脅**： 補救洩露但 hello 威脅的電腦。</span><span class="sxs-lookup"><span data-stu-id="b88ae-135">**Remediated threats**: computers that were compromised but hello threats were remediated.</span></span>
* <span data-ttu-id="b88ae-136">**簽章已過期**： 已啟用但 hello 簽章的惡意程式碼保護的電腦已過期。</span><span class="sxs-lookup"><span data-stu-id="b88ae-136">**Signature out of date**: computers that have malware protection enabled but hello signature is out of date.</span></span>
* <span data-ttu-id="b88ae-137">[沒有即時保護]：電腦並無安裝反惡意程式碼產品。</span><span class="sxs-lookup"><span data-stu-id="b88ae-137">**No real time protection**: computers that don’t have antimalware installed.</span></span>

### <a name="monitoring-updates"></a><span data-ttu-id="b88ae-138">監控更新</span><span class="sxs-lookup"><span data-stu-id="b88ae-138">Monitoring updates</span></span>
<span data-ttu-id="b88ae-139">套用最新安全性更新 hello 安全性最佳作法是，它應該納入更新管理策略中。</span><span class="sxs-lookup"><span data-stu-id="b88ae-139">Applying hello most recent security updates is a security best practice and it should be incorporated in your update management strategy.</span></span> <span data-ttu-id="b88ae-140">Microsoft Monitoring Agent 服務 (HealthService.exe) 讀取受監視電腦的更新資訊，並再將此更新的資訊 toohello OMS 服務傳送 hello 雲端進行處理。</span><span class="sxs-lookup"><span data-stu-id="b88ae-140">Microsoft Monitoring Agent service (HealthService.exe) reads update information from monitored computers and then sends this updated information toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="b88ae-141">hello Microsoft Monitoring Agent 服務設定為自動服務，就應該一律在 hello 目標電腦中執行。</span><span class="sxs-lookup"><span data-stu-id="b88ae-141">hello Microsoft Monitoring Agent service is configured as an automatic service and it should be always running in hello target computer.</span></span>

![監控更新](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

<span data-ttu-id="b88ae-143">邏輯是套用的 toohello 更新資料和 hello 雲端服務會記錄 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b88ae-143">Logic is applied toohello update data and hello cloud service records hello data.</span></span> <span data-ttu-id="b88ae-144">如果找到遺失的更新，它們會顯示在 hello**更新**儀表板。</span><span class="sxs-lookup"><span data-stu-id="b88ae-144">If missing updates are found, they are shown on hello **Updates** dashboard.</span></span> <span data-ttu-id="b88ae-145">您可以使用 hello**更新**儀表板 toowork 使用遺漏的更新及開發計劃 tooapply 它們 toohello 需要的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b88ae-145">You can use hello **Updates** dashboard toowork with missing updates and develop a plan tooapply them toohello servers that need them.</span></span> <span data-ttu-id="b88ae-146">請遵循以下 tooaccess hello hello 步驟**更新**儀表板：</span><span class="sxs-lookup"><span data-stu-id="b88ae-146">Follow hello steps below tooaccess hello **Updates** dashboard:</span></span>

1. <span data-ttu-id="b88ae-147">在 hello **Microsoft Operations Management Suite**主要儀表板按一下**安全性和稽核**磚。</span><span class="sxs-lookup"><span data-stu-id="b88ae-147">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="b88ae-148">在 hello**安全性和稽核**儀表板，按一下 **更新評估**下**安全性網域**。</span><span class="sxs-lookup"><span data-stu-id="b88ae-148">In hello **Security and Audit** dashboard, click **Update Assessment** under **Security Domains**.</span></span> <span data-ttu-id="b88ae-149">hello 更新儀表板會顯示如下所示：</span><span class="sxs-lookup"><span data-stu-id="b88ae-149">hello Update dashboard appears as shown below:</span></span>

![更新評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

<span data-ttu-id="b88ae-151">此儀表板中，您可以執行更新評估 toounderstand hello 目前狀態的電腦和地址 hello 最嚴重的威脅。</span><span class="sxs-lookup"><span data-stu-id="b88ae-151">In this dashboard you can perform an update assessment toounderstand hello current state of your computers and address hello most critical threats.</span></span> <span data-ttu-id="b88ae-152">使用 hello**重大或安全性更新**磚，IT 系統管理員都能 tooaccess 詳細的資訊遺失，如下所示的 hello 更新：</span><span class="sxs-lookup"><span data-stu-id="b88ae-152">By using hello **Critical or Security Updates** tile, IT administrators will be able tooaccess detailed information about hello updates that are missing as shown below:</span></span>

![搜尋結果](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

<span data-ttu-id="b88ae-154">此報表包含重要資訊，可以使用 tooidentify hello 威脅類型，此系統很容易，其中包括 hello 與 hello 安全性更新和 hello 具有更多詳細 hello MS 公告相關聯的 Microsoft 知識庫文章弱點。</span><span class="sxs-lookup"><span data-stu-id="b88ae-154">This report include critical information that can be used tooidentify hello type of threat this system is vulnerable to, which includes hello Microsoft KB articles associated with hello security update and hello MS Bulletin that has more details about hello vulnerability.</span></span>

### <a name="monitoring-identity-and-access"></a><span data-ttu-id="b88ae-155">監視身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="b88ae-155">Monitoring identity and access</span></span>
<span data-ttu-id="b88ae-156">由於使用者有隨處工作、使用不同裝置，以及存取大量雲端及內部部署應用程式的需求，因此務必確保他們的認證能受到保護。</span><span class="sxs-lookup"><span data-stu-id="b88ae-156">With users working from anywhere, using different devices and accessing a vast amount of cloud and on-premises apps, it is imperative that their credentials are protected.</span></span> <span data-ttu-id="b88ae-157">認證遭竊的攻擊是指在這一開始攻擊者存取 tooa 一般使用者的認證 tooaccess hello 網路內的系統。</span><span class="sxs-lookup"><span data-stu-id="b88ae-157">Credential theft attacks are those in which an attacker initially gains access tooa regular user’s credentials tooaccess a system within hello network.</span></span> <span data-ttu-id="b88ae-158">許多次，這個初始攻擊是只方式 tooget toohello 網路存取，hello 最終目標 toodiscover 權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b88ae-158">Many times, this initial attack is only a way tooget access toohello network, hello ultimate goal is toodiscover privilege accounts.</span></span> 

<span data-ttu-id="b88ae-159">攻擊者會保留在 hello 網路使用免費工具 tooextract hello 工作階段的其他登入帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="b88ae-159">Attackers will stay in hello network, using freely available tooling tooextract credentials from hello sessions of other logged-on accounts.</span></span> <span data-ttu-id="b88ae-160">根據 hello 系統設定，這些認證可以擷取 hello 形式雜湊、 票證或甚至純文字密碼。</span><span class="sxs-lookup"><span data-stu-id="b88ae-160">Depending on hello system configuration, these credentials can be extracted in hello form of hashes, tickets, or even plaintext passwords.</span></span>  

> [!NOTE]
> <span data-ttu-id="b88ae-161">機器的直接公開網際網路，將會看到許多失敗，嘗試使用所有類型的已知使用者名稱 （例如系統管理員），再試一次 toologin toohello。</span><span class="sxs-lookup"><span data-stu-id="b88ae-161">machines that are directly exposed toohello Internet will see many failed attempts that try toologin using all kind of well-known usernames (e.g. Administrator).</span></span> <span data-ttu-id="b88ae-162">在大部分情況下它是 [確定]，如果 hello 已知的使用者名稱不會使用而且 hello 密碼效力不夠。</span><span class="sxs-lookup"><span data-stu-id="b88ae-162">In most cases it is OK if hello well-known usernames are not used and if hello password is strong enough.</span></span>
> 
> 

<span data-ttu-id="b88ae-163">它是可能 tooidentify 這些入侵者之前它們危害權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b88ae-163">It is possible tooidentify these intruders before they compromise a privilege account.</span></span> <span data-ttu-id="b88ae-164">您可以利用**OMS 安全性和稽核解決方案**toomonitor 身分識別和存取。</span><span class="sxs-lookup"><span data-stu-id="b88ae-164">You can leverage **OMS Security and Audit Solution** toomonitor identity and access.</span></span> <span data-ttu-id="b88ae-165">請遵循以下 tooaccess hello hello 步驟**身分識別和存取**儀表板：</span><span class="sxs-lookup"><span data-stu-id="b88ae-165">Follow hello steps below tooaccess hello **Identity and Access** dashboard:</span></span>

1. <span data-ttu-id="b88ae-166">在 hello **Microsoft Operations Management Suite**主要儀表板按一下 安全性和稽核磚。</span><span class="sxs-lookup"><span data-stu-id="b88ae-166">In hello **Microsoft Operations Management Suite** main dashboard click Security and Audit tile.</span></span>
2. <span data-ttu-id="b88ae-167">在 hello**安全性和稽核**儀表板，按一下**身分識別和存取**下**安全性網域**。</span><span class="sxs-lookup"><span data-stu-id="b88ae-167">In hello **Security and Audit** dashboard, click **Identity and Access** under **Security Domains**.</span></span> <span data-ttu-id="b88ae-168">hello**身分識別和存取**儀表板隨即出現，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b88ae-168">hello **Identity and Access** dashboard appears as shown below:</span></span>

![身分識別與存取](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

<span data-ttu-id="b88ae-170">作為定期監視策略的一部分，您必須包含身分識別監視。</span><span class="sxs-lookup"><span data-stu-id="b88ae-170">As part of your regular monitoring strategy, you must include identity monitoring.</span></span> <span data-ttu-id="b88ae-171">IT 系統管理員應查看是否有特定的有效使用者名稱，出現多次登入嘗試的情況。</span><span class="sxs-lookup"><span data-stu-id="b88ae-171">IT Admin should look if there is a specific valid username that has many attempts.</span></span> <span data-ttu-id="b88ae-172">這可能表示可能是攻擊者取得 hello 實際使用者名稱，然後再次嘗試 toobrute force 或自動的工具，會使用硬式編碼的密碼已過期。</span><span class="sxs-lookup"><span data-stu-id="b88ae-172">This might indicate either attacker that acquired hello real username and try toobrute force or an automatic tool that uses hard-coded password that expired.</span></span>

<span data-ttu-id="b88ae-173">此儀表板啟用 IT tooquickly 識別潛在威脅相關的 tooidentity 及存取 toocompany 的資源。</span><span class="sxs-lookup"><span data-stu-id="b88ae-173">This dashboard enable IT tooquickly identify potential threats related tooidentity and access toocompany’s resources.</span></span> <span data-ttu-id="b88ae-174">它是特定重要 tooalso 找出潛在的趨勢，例如 hello 登入一段時間在磚中，您可以看到經過一段時間執行的失敗登入嘗試的次數。</span><span class="sxs-lookup"><span data-stu-id="b88ae-174">It is particular important tooalso identify potential trends, for example in hello Logons Over Time tile, you can see over period of time how many times a failed logon attempt was performed.</span></span> <span data-ttu-id="b88ae-175">在此情況下 hello 電腦**FileServer**收到 35 登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="b88ae-175">In this case hello computer **FileServer** received 35 logon attempts.</span></span> <span data-ttu-id="b88ae-176">只要按一下該項目，您就可以瞭解更多關於此電腦的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b88ae-176">You can explore more details about this computer by clicking on it.</span></span> 

![其他詳細資訊](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

<span data-ttu-id="b88ae-178">此電腦所產生的 hello 報表會使此模式有關的重要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b88ae-178">hello report generated for this computer brings valuable details about this pattern.</span></span> <span data-ttu-id="b88ae-179">注意到該 hello**帳戶**hello 已使用的 tootry tooaccess 的使用者帳戶的資料行提供 hello 系統，hello **TIMEGENERATED** hello 中的 hello 嘗試將已完成的時間間隔的資料行提供和hello **LOGONTYPENAME** hello 了這項嘗試位置的資料行提供。</span><span class="sxs-lookup"><span data-stu-id="b88ae-179">Noticed that hello **ACCOUNT** column gives you hello user account that was used tootry tooaccess hello system, hello **TIMEGENERATED** column gives you hello time interval in which hello attempt was done and hello **LOGONTYPENAME** column gives you hello location where this attempt was done.</span></span> <span data-ttu-id="b88ae-180">如果這些嘗試執行本機 hello 系統中的程式，hello**程序**hello 處理序的名稱會顯示資料行。</span><span class="sxs-lookup"><span data-stu-id="b88ae-180">If these attempts were performed locally in hello system by a program, hello **PROCESS** column would be showing hello process’s name.</span></span> <span data-ttu-id="b88ae-181">在 hello 登入嘗試從程式所在的情況下，您已經有可用的 hello 處理序名稱，現在您可以執行進一步調查 hello 目標系統中。</span><span class="sxs-lookup"><span data-stu-id="b88ae-181">In scenarios where hello logon attempt is coming from a program, you already have hello process name available and now you can perform further investigation in hello target system.</span></span>

## <a name="see-also"></a><span data-ttu-id="b88ae-182">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b88ae-182">See also</span></span>
<span data-ttu-id="b88ae-183">在本文件中，您學到如何 toouse OMS 安全性和稽核解決方案 toomonitor 您的資源。</span><span class="sxs-lookup"><span data-stu-id="b88ae-183">In this document, you learned how toouse OMS Security and Audit solution toomonitor your resources.</span></span> <span data-ttu-id="b88ae-184">toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="b88ae-184">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="b88ae-185">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="b88ae-185">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="b88ae-186">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="b88ae-186">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="b88ae-187">監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="b88ae-187">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)

