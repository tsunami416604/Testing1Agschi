<properties
    pageTitle="Site Recovery (Hyper-V Site to Azure)/Failover: Test failover"
    description="Site Recovery(Hyper-V 사이트 대 Azure)/장애 조치: 테스트 장애 조치"
    service="microsoft.recoveryservices"
    resource="vaults"
    authors="prateek9us"
    displayOrder=""
    selfHelpType="generic"
    supportTopicIds="32536460"
    resourceTags=""
    productPesIds="15207"
    cloudEnvironments="public"
/>

# <a name="run-a-test-failover-in-site-recovery---hyper-v-to-azure"></a>Site Recovery 테스트 장애 조치 실행 - Hyper-V에서 Azure로
## <a name="recommended-steps"></a>**권장되는 단계**

- [Azure로 **테스트 장애 조치**를 실행하는 방법](https://docs.microsoft.com/azure/site-recovery/site-recovery-test-failover-to-azure)<br>
- [**테스트 장애 조치(Failover)를 위해 네트워크**를 만드는 방법](https://docs.microsoft.com/azure/site-recovery/site-recovery-test-failover-to-azure#create-a-network-for-test-failover)<br>
- [**프로덕션 네트워크에 VM을 장애 조치**하기 위한 테스트 장애 조치 고려 사항](https://docs.microsoft.com/azure/site-recovery/site-recovery-test-failover-to-azure#test-failover-to-a-production-network-in-the-recovery-site)<br>
- [**단일 VM에 대해 테스트 장애 조치**를 실행하는 방법](https://docs.microsoft.com/azure/site-recovery/tutorial-dr-drill-azure#verify-vm-properties)<br>
- [**응용 프로그램 테스트를 위해 장애 조치**를 실행하는 **Active Directory에 대한 테스트 장애 조치 고려 사항**](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#test-failover-considerations)<br>
- [장애 조치 이후 **VM에 연결**하는 방법](https://docs.microsoft.com/azure/site-recovery/site-recovery-test-failover-to-azure#prepare-to-connect-to-azure-vms-after-failover)<br>
- [테스트 장애 조치 이후 VM에 **공용 IP 주소 추가**](https://aka.ms/addpublicip)<br>
- [문제] [*VM에서 연결 단추가 회색으로 표시됩니다.*](https://aka.ms/unabletordpssh)<br>
- [문제] [*연결 단추를 사용하거나 사용하지 않고 VM에 RDP/SSH합니다.*](https://aka.ms/unabletordpssh)<br>
- [방법] [Windows VM에 대한 RDP 연결 문제 해결](https://docs.microsoft.com/azure/virtual-machines/windows/troubleshoot-rdp-connection)<br>
- [방법] [ Linux VM에 대한 SSH 연결 문제 해결[<br>
- [문제] [*장애 조치에 사용할 수 있는 충분한 코어가 없습니다.* 할당량을 늘리려면 다음 단계를 수행합니다. ](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)<br>
- [문제] [*구독에서 VM을 만드는 데 선택한 대상 위치를 사용할 수 없습니다.* 위치를 변경하거나 다음 지침을 따라 VM을 만들 수 있습니다.](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request)<br>
- [문제] [오류 ID 28031](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover-to-azure-troubleshoot#failover-failed-with-error-id-28031), [오류 ID 28092](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover-to-azure-troubleshoot#failover-failed-with-error-id-28092), [오류 ID 70038](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover-to-azure-troubleshoot#failover-failed-with-error-id-70038) 메시지를 표시하는 장애 조치 오류 코드 문제 해결<br>

**Active Directory 및 DNS**<br>
- [문제] [VM 생성 ID가 장애 조치 후 변경됩니다.](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#issues-caused-by-virtualization-safeguards)<br>
- [문제] [호출 ID가 장애 조치 후 변경됩니다](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#issues-caused-by-virtualization-safeguards)<br>
- [문제] [장애 조치 후 Sysvol 및 Netlogon 공유를 사용할 수 없습니다](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#issues-caused-by-virtualization-safeguards)<br>
- [문제] [장애 조치 후 DFSR 데이터베이스를 찾을 수 없습니다.](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#issues-caused-by-virtualization-safeguards)<br>
- [문제] [테스트 장애 조치(failover)를 수행하는 동안 도메인 컨트롤러 문제를 해결하는 방법](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory#troubleshoot-domain-controller-issues-during-test-failover)<br>


## <a name="recommended-documents"></a>**권장되는 문서**

**Automation**<br>

- 복구 계획을 사용자 지정하여 장애 조치의 일부로 자동화 스크립트를 실행하는 방법 [복구 계획에 Azure Automation Runbook 추가](https://docs.microsoft.com/azure/site-recovery/site-recovery-runbook-automation)<br>
- [장애 조치 중 다른 작업을 자동화하는 샘플 스크립트](https://github.com/Azure/azure-quickstart-templates/tree/master/asr-automation-recovery/scripts)<br>
- [공용 IP 주소를 장애 조치된 VM에 할당하는 스크립트](https://github.com/Azure/azure-quickstart-templates/blob/master/asr-automation-recovery/scripts/ASR-AddPublicIp.ps1)<br>
- [장애 조치된 VM의 DNS 레코드를 업데이트하는 스크립트](https://github.com/Azure/azure-quickstart-templates/blob/master/asr-automation-recovery/scripts/ASR-DNS-UpdateIP.ps1)<br>

**장애 조치(Failover)**<br>
- [Hyper-V VM에서 Azure로 장애 조치하는 방법에 대한 단계별 지침](https://docs.microsoft.com/azure/site-recovery/site-recovery-failover)<br>
- [Azure에 장애 조치하는 동안 고정 IP 주소를 유지하는 방법](https://docs.microsoft.com/azure/site-recovery/concepts-on-premises-to-azure-networking#retaining-ip-addresses)<br>
- [장애 조치 후 VM에 새 IP 주소를 할당하는 방법](https://azure.microsoft.com/blog/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/)<br>
- [Azure에 장애 조치하는 경우 데이터 디스크의 드라이브 문자를 유지하는 방법](https://support.microsoft.com/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-a)<br>

**장애 복구**<br>
- [Azure에서 온-프레미스 Hyper-V 사이트로 장애 복구하는 방법에 대한 단계별 지침](https://docs.microsoft.com/azure/site-recovery/site-recovery-failback-from-azure-to-hyper-v)<br>

**AD DNS 보호**<br>

- [Active Directory 및 DNS 보호](https://docs.microsoft.com/azure/site-recovery/site-recovery-active-directory)<br>
