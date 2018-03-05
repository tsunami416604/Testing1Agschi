<properties
    pageTitle="Site Recovery (Hyper-V Site to Azure)/Not able to conect to VM after failover"
    description="Site Recovery(Hyper-V 사이트 대 Azure)/장애 조치 후 VM에 연결할 수 없음"
    service="microsoft.recoveryservices"
    resource="vaults"
    authors="prateek9us"
    displayOrder=""
    selfHelpType="generic"
    supportTopicIds="32536423"
    resourceTags=""
    productPesIds="15207"
    cloudEnvironments="public"
/>

# <a name="unable-to-connect-to-vm-after-failover---hyper-v-to-azure"></a>장애 조치 후 VM에 연결할 수 없음 - Hyper-V에서 Azure로
## <a name="recommended-steps"></a>**권장되는 단계**

- [장애 조치 이후 **VM에 연결**하는 방법](https://docs.microsoft.com/azure/site-recovery/site-recovery-test-failover-to-azure#prepare-to-connect-to-azure-vms-after-failover)<br>
- [문제] [*VM에서 연결 단추가 회색으로 표시됩니다.*](https://aka.ms/unabletordpssh)<br>
- [문제] [*연결 단추를 사용하거나 사용하지 않고 VM에 RDP/SSH합니다.*](https://aka.ms/unabletordpssh)<br>
- [방법] [Windows VM에 대한 RDP 연결 문제 해결](https://docs.microsoft.com/azure/virtual-machines/windows/troubleshoot-rdp-connection)<br>
- [방법] [Linux VM에 대한 SSH 연결 문제 해결][<br>]


## <a name="recommended-documents"></a>**권장되는 문서**

**Automation** <br>
- 복구 계획을 사용자 지정하여 장애 조치의 일부로 자동화 스크립트를 실행하는 방법 [복구 계획에 Azure Automation Runbook 추가](https://docs.microsoft.com/azure/site-recovery/site-recovery-runbook-automation)<br>
- [장애 조치 중 다른 작업을 자동화하는 샘플 스크립트](https://github.com/Azure/azure-quickstart-templates/tree/master/asr-automation-recovery/scripts)<br>
- [공용 IP 주소를 장애 조치된 VM에 할당하는 스크립트](https://github.com/Azure/azure-quickstart-templates/blob/master/asr-automation-recovery/scripts/ASR-AddPublicIp.ps1)<br>
- [장애 조치된 VM의 DNS 레코드를 업데이트하는 스크립트](https://github.com/Azure/azure-quickstart-templates/blob/master/asr-automation-recovery/scripts/ASR-DNS-UpdateIP.ps1)<br>

**IP 주소**<br>
- [Azure에 장애 조치하는 동안 고정 IP 주소를 유지하는 방법](https://docs.microsoft.com/azure/site-recovery/concepts-on-premises-to-azure-networking#retaining-ip-addresses)<br>
- [장애 조치 후 VM에 새 IP 주소를 할당하는 방법](https://azure.microsoft.com/blog/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)<br>
