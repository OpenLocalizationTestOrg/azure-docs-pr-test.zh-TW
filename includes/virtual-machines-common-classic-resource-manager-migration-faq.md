# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>關於傳統 tooAzure 資源管理員移轉的常見問題集

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>此移轉計劃是否會影響任何在 Azure 虛擬機器上執行的現有服務或應用程式？ 

否。 hello Vm （傳統） 是中的正式運作的完整支援的服務。 您可以繼續 toouse 這些資源 tooexpand 洁 Microsoft Azure 上的。

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>如果我不打算在 hello 附近未來移轉會怎樣 toomy Vm？ 

我們不會淘汰 hello 現有傳統 Api 和資源的模型。 我們想要 toomake 移轉更容易使用，請考慮 hello 進階 hello Resource Manager 部署模型中可用的功能。 我們強烈建議您檢閱[hello 拉大距離的某些](../articles/azure-resource-manager/resource-manager-deployment-model.md)是的 IaaS 資源管理員 」 底下的一部分。

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>對於我現有的工具來說，此移轉計劃有何意義？ 

更新工具 toohello Resource Manager 部署模型是一種您的移轉計劃中有針對 tooaccount hello 最重要變更。

## <a name="how-long-will-hello-management-plane-downtime-be"></a>保留時間長度將 hello 管理平面停機時間？ 

Hello 要移轉的資源數目而定。 較小的部署 （數十 Vm），hello 整個移轉花費時間不超過一小時。 對於大規模的部署 （數百個 Vm），hello 移轉可能需要幾小時的時間。

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>在 Resource Manager 中認可移轉中的資源之後，是否還可以回復？ 

只要 hello 資源位於 hello 備妥狀態，您可以中止移轉。 Hello 資源已成功移轉到 hello 認可作業之後，不支援復原。

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>可以復原我移轉如果 hello 認可作業失敗？ 

如果 hello 認可作業失敗，無法中止移轉。 所有移轉作業，包括 hello 認可作業，都是等冪。 因此，建議您重試 hello 一小段時間後的作業。 如果您仍然要面對錯誤，建立支援票證或以 hello ClassicIaaSMigration 標記建立論壇文章我們[VM 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows)。

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>我是否必須 toobuy 另一個快速路由迴路如果我有 toouse IaaS 在資源管理員？ 

否。 我們最近啟用[hello 傳統 toohello Resource Manager 部署模型中移動的 ExpressRoute 電路](../articles/expressroute/expressroute-move.md)。 如果您已經有您不需要指定 toobuy 新的 ExpressRoute 電路。

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>如果我已為傳統 IaaS 資源設定角色型存取控制原則，該怎麼辦？ 

在移轉期間，hello 資源轉換從傳統 tooResource 管理員。 因此我們建議您計劃移轉之後需要 toohappen hello RBAC 原則更新。

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>我已在備份保存庫中備份我的傳統 VM。 我的 Vm 將從傳統模式 tooResource 管理員模式移轉和復原服務保存庫來保護它們？ 

當您移動 hello VM 從傳統 tooResource 管理員模式下，傳統備份保存庫中的 VM 復原點不自動移轉 tooa 復原服務保存庫。 請遵循這些步驟 tootransfer 您 VM 的備份：

1. 在 hello 備份保存庫中，移 toohello**受保護項目**索引標籤並選取 hello VM。 按一下[停止保護](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines)。 讓 [刪除相關聯的備份資料] 選項保持 [未核取] 狀態。
2. 刪除 hello VM hello 快照集備份/擴充功能。
3. 從傳統模式 tooResource 管理員模式移轉 hello 虛擬機器。 請確定 hello 儲存體和網路資訊也是對應的 toohello 虛擬機器移轉 tooResource 管理員模式。
4. 建立復原服務保存庫和設定虛擬機器使用的備份在 hello 移轉**備份**在保存庫儀表板頂端的動作。 詳細資訊，在備份 VM tooa 復原服務保存庫，請參閱 hello 文章[保護與復原服務保存庫的 Azure Vm](../articles/backup/backup-azure-vms-first-look-arm.md)。

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>可以我確認我的訂用帳戶或資源 toosee 如果它們能夠移轉？ 

是。 在 hello 平台支援的移轉選項，hello 準備進行移轉的第一個步驟是 toovalidate hello 資源可移轉。 萬一 hello 驗證作業將會失敗，您會收到 hello 移轉無法完成所有 hello 原因的訊息。

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>如果我執行到配額錯誤移轉準備 hello IaaS 資源會怎樣？ 

我們建議您中止您的移轉，並再登入您所在的移轉 hello Vm 的 hello 地區的 支援要求 tooincrease hello 配額。 Hello 配額要求核准後，您可以啟動一次執行 hello 移轉步驟。

## <a name="how-do-i-report-an-issue"></a>如何回報問題？ 

張貼您的問題與疑問移轉 tooour [VM 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows)，與 hello 關鍵字 ClassicIaaSMigration。 建議您將所有問題都張貼在此論壇上。 如果您有支援合約時，您  褖畫惎 toolog 支援票證。

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>如果我不想要的 hello 平台的 hello 資源的 hello 名稱在移轉期間選擇？ 

在移轉期間，仍會保留您明確地提供名稱 hello 傳統部署模型中的所有 hello 資源。 在某些情況下，則會建立新的資源。 例如︰會為每個 VM 建立一個網路介面。 我們目前不支援在移轉期間建立這些新資源的 hello 能力 toocontrol hello 名稱。 記錄這項功能在 hello 您投票[Azure 的意見反應論壇](http://feedback.azure.com)。

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>可以透過授權連結移轉跨訂用帳戶使用的 ExpressRoute 線路嗎？ 

無法在不停機的情況下，自動移轉使用跨訂用帳戶授權連結的 ExpressRoute 線路。 我們提供使用手動步驟移轉這些項目的指引。 請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../articles/expressroute/expressroute-migration-classic-resource-manager.md)步驟的詳細資訊。

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>我收到一則訊息*」 VM 報告 hello 整體的代理程式狀態為未就緒。因此，無法移轉 hello VM。確定該 hello VM 代理程式報告為已備妥的整體代理程式狀態 」*或 *"VM 包含其狀態不從 hello VM 所報告的副檔名。 因此，無法移轉此 VM。」 *

Hello VM 沒有傳出連線 toohello 時，會收到此訊息網際網路。 hello VM 代理程式會使用輸出連線 tooreach hello Azure 儲存體帳戶，每隔五分鐘更新 hello 代理程式狀態。
