---
title: "aaaManage 已加入網域的 HDInsight 叢集 Azure |Microsoft 文件"
description: "了解如何 toomanage 已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="d507f-103">管理已加入網域的 HDInsight 叢集 (預覽)</span><span class="sxs-lookup"><span data-stu-id="d507f-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="d507f-104">了解 hello 中使用者與 hello 角色加入網域的 HDInsight 及如何 toomanage 已加入網域的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d507f-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="d507f-105">已加入網域的 HDInsight 叢集的使用者</span><span class="sxs-lookup"><span data-stu-id="d507f-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="d507f-106">是未加入網域的 HDInsight 叢集有兩個 hello 叢集建立期間建立的使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="d507f-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="d507f-107">**Ambari 系統管理員**：此帳戶亦稱為「Hadoop 使用者」或「HTTP 使用者」。</span><span class="sxs-lookup"><span data-stu-id="d507f-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="d507f-108">此帳戶可以在 https:// tooAmbari 上的使用的 toolog&lt;clustername >。.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="d507f-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="d507f-109">同時，也是使用的 toorun Ambari 檢視上的查詢、 執行外部工具 （也就是 PowerShell、 Templeton，Visual Studio），透過作業並 hello hive 控制檔的 ODBC 驅動程式與 BI 工具 （也就是 Excel、 power Bi 或 Tableau） 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d507f-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="d507f-110">**SSH 使用者**︰此帳戶可以搭配 SSH 使用，執行 sudo 命令。</span><span class="sxs-lookup"><span data-stu-id="d507f-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="d507f-111">它擁有根權限 toohello Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="d507f-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="d507f-112">已加入網域的 HDInsight 叢集在加法 tooAmbari Admin 和 SSH 使用者有三個新的使用者。</span><span class="sxs-lookup"><span data-stu-id="d507f-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="d507f-113">**Ranger admin**： 此帳戶是 hello 本機 Apache Ranger 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="d507f-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="d507f-114">不是 Active Directory 網域使用者。</span><span class="sxs-lookup"><span data-stu-id="d507f-114">It is not an active directory domain user.</span></span> <span data-ttu-id="d507f-115">此帳戶可以是使用的 toosetup 原則，並讓其他使用者的系統管理員或委派系統管理員 （如此這些使用者可以管理原則）。</span><span class="sxs-lookup"><span data-stu-id="d507f-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="d507f-116">根據預設，hello 使用者名稱為*管理員*和 hello 密碼是 hello 與 hello Ambari 管理密碼相同。</span><span class="sxs-lookup"><span data-stu-id="d507f-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="d507f-117">hello 密碼可以更新從廣 hello [設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d507f-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="d507f-118">**叢集系統管理員的網域使用者**： 此帳戶是指定為 hello 包括 Ambari 和廣的 Hadoop 叢集管理的 active directory 網域使用者。</span><span class="sxs-lookup"><span data-stu-id="d507f-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="d507f-119">您必須在叢集建立期間提供此使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="d507f-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="d507f-120">此使用者擁有下列權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="d507f-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="d507f-121">加入機器 toohello 網域，並將它們放在 hello 您在叢集建立期間指定的 OU 內。</span><span class="sxs-lookup"><span data-stu-id="d507f-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="d507f-122">建立 hello 您在叢集建立期間指定的 OU 中所有服務主體。</span><span class="sxs-lookup"><span data-stu-id="d507f-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="d507f-123">建立反向 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="d507f-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="d507f-124">請注意 hello 其他 AD 使用者也具備這些權限。</span><span class="sxs-lookup"><span data-stu-id="d507f-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="d507f-125">有一些結束點 hello 叢集 (例如，Templeton) 內的未受廣，而因此並不安全。</span><span class="sxs-lookup"><span data-stu-id="d507f-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="d507f-126">這些端點已鎖定的所有使用者，除了 hello 叢集系統管理員的網域使用者。</span><span class="sxs-lookup"><span data-stu-id="d507f-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="d507f-127">**一般**︰在叢集建立期間，您可以提供多個 Active Directory 群組。</span><span class="sxs-lookup"><span data-stu-id="d507f-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="d507f-128">這些群組中的 hello 使用者將無法同步處理的 tooRanger 和 Ambari。</span><span class="sxs-lookup"><span data-stu-id="d507f-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="d507f-129">這些使用者是網域使用者，而且必須存取 tooonly 廣受管理端點 (例如，Hiveserver2)。</span><span class="sxs-lookup"><span data-stu-id="d507f-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="d507f-130">所有 hello RBAC 原則和稽核將會適用 toothese 使用者。</span><span class="sxs-lookup"><span data-stu-id="d507f-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="d507f-131">已加入網域的 HDInsight 叢集的角色</span><span class="sxs-lookup"><span data-stu-id="d507f-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="d507f-132">已加入網域的 HDInsight 有下列角色的 hello:</span><span class="sxs-lookup"><span data-stu-id="d507f-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="d507f-133">叢集系統管理員</span><span class="sxs-lookup"><span data-stu-id="d507f-133">Cluster Administrator</span></span>
* <span data-ttu-id="d507f-134">叢集操作員</span><span class="sxs-lookup"><span data-stu-id="d507f-134">Cluster Operator</span></span>
* <span data-ttu-id="d507f-135">服務管理員</span><span class="sxs-lookup"><span data-stu-id="d507f-135">Service Administrator</span></span>
* <span data-ttu-id="d507f-136">服務操作員</span><span class="sxs-lookup"><span data-stu-id="d507f-136">Service Operator</span></span>
* <span data-ttu-id="d507f-137">叢集使用者</span><span class="sxs-lookup"><span data-stu-id="d507f-137">Cluster User</span></span>

<span data-ttu-id="d507f-138">**這些角色 toosee hello 權限**</span><span class="sxs-lookup"><span data-stu-id="d507f-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="d507f-139">開啟 hello Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="d507f-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="d507f-140">請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="d507f-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="d507f-141">從 hello 左窗格中，按一下 **角色**。</span><span class="sxs-lookup"><span data-stu-id="d507f-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="d507f-142">按一下 hello 藍色問號 toosee hello 權限：</span><span class="sxs-lookup"><span data-stu-id="d507f-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![已加入網域的 HDInsight 角色權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="d507f-144">開啟 hello Ambari 管理 UI</span><span class="sxs-lookup"><span data-stu-id="d507f-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="d507f-145">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d507f-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d507f-146">在刀鋒視窗中開啟您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d507f-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="d507f-147">請參閱[列出和顯示叢集](hdinsight-administer-use-management-portal.md#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="d507f-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="d507f-148">按一下**儀表板**從 hello 上方功能表 tooopen Ambari。</span><span class="sxs-lookup"><span data-stu-id="d507f-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="d507f-149">登入 tooAmbari 使用 hello 叢集系統管理員的網域使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d507f-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="d507f-150">按一下 hello **Admin**從 hello 右上角，然後再按一下下拉式功能表**管理 Ambari**。</span><span class="sxs-lookup"><span data-stu-id="d507f-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![已加入網域的 HDInsight 管理 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="d507f-152">hello UI 看起來像：</span><span class="sxs-lookup"><span data-stu-id="d507f-152">hello UI looks like:</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="d507f-154">從您的 Active Directory 同步處理清單 hello 網域使用者</span><span class="sxs-lookup"><span data-stu-id="d507f-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="d507f-155">開啟 hello Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="d507f-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="d507f-156">請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="d507f-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="d507f-157">從 hello 左窗格中，按一下 **使用者**。</span><span class="sxs-lookup"><span data-stu-id="d507f-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="d507f-158">您應該會看到所有的 hello 使用者進行同步處理從 Active Directory toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d507f-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出使用者](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="d507f-160">從您的 Active Directory 同步處理清單 hello 網域群組</span><span class="sxs-lookup"><span data-stu-id="d507f-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="d507f-161">開啟 hello Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="d507f-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="d507f-162">請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="d507f-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="d507f-163">從 hello 左窗格中，按一下 **群組**。</span><span class="sxs-lookup"><span data-stu-id="d507f-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="d507f-164">您應該會看到所有的 hello 群組進行同步處理從 Active Directory toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="d507f-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出群組](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="d507f-166">設定 Hive 檢視權限</span><span class="sxs-lookup"><span data-stu-id="d507f-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="d507f-167">開啟 hello Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="d507f-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="d507f-168">請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="d507f-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="d507f-169">從 hello 左窗格中，按一下 **檢視**。</span><span class="sxs-lookup"><span data-stu-id="d507f-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="d507f-170">按一下**HIVE** tooshow hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d507f-170">Click **HIVE** tooshow hello details.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="d507f-172">按一下 hello **Hive 檢視**連結 tooconfigure hive 控制檔的檢視。</span><span class="sxs-lookup"><span data-stu-id="d507f-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="d507f-173">捲動 toohello**權限**> 一節。</span><span class="sxs-lookup"><span data-stu-id="d507f-173">Scroll down toohello **Permissions** section.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視設定權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="d507f-175">按一下**新增使用者**或**加入群組**，然後指定 hello 使用者或群組，可以使用 hive 控制檔的檢視。</span><span class="sxs-lookup"><span data-stu-id="d507f-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="d507f-176">設定使用者的 hello 角色</span><span class="sxs-lookup"><span data-stu-id="d507f-176">Configure users for hello roles</span></span>
 <span data-ttu-id="d507f-177">toosee 清單的角色和其權限，請參閱[角色的網域的 HDInsight 叢集](#roles-of-domain---joined-hdinsight-clusters)。</span><span class="sxs-lookup"><span data-stu-id="d507f-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="d507f-178">開啟 hello Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="d507f-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="d507f-179">請參閱[開啟 hello Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="d507f-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="d507f-180">從 hello 左窗格中，按一下 **角色**。</span><span class="sxs-lookup"><span data-stu-id="d507f-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="d507f-181">按一下**新增使用者**或**加入群組**tooassign toodifferent 角色的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="d507f-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d507f-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d507f-182">Next steps</span></span>
* <span data-ttu-id="d507f-183">如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="d507f-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="d507f-184">如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="d507f-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="d507f-185">若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。</span><span class="sxs-lookup"><span data-stu-id="d507f-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
