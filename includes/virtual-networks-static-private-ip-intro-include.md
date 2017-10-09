您的 IaaS 虛擬機器 (Vm) 和虛擬網路中的 PaaS 角色執行個體自動接收私人 IP 位址範圍從您指定的 hello 子網路連線到。 該位址不會保留 hello Vm 和角色執行個體，直到委任。 您可以解除委任的 VM 或角色執行個體，來停止從 PowerShell，hello Azure CLI 或 hello Azure 入口網站。 在這些情況下，一旦 hello VM 或再次角色執行個體啟動時，它會從 hello Azure 基礎結構，這可能不是 hello 接收可用的 IP 位址相同它先前有。 如果您關閉 hello VM 或角色執行個體從 hello 客體作業系統，它會保留 hello IP 位址。  

在某些情況下，您想 VM 或角色的執行個體 toohave 靜態的 IP 位址，例如，如果 VM 即將 toorun DNS，或將網域控制站。 您可以設定靜態的私人 IP 位址來這麼做。

