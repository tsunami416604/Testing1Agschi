<properties
    pageTitle="CloudServices RCA"
    description="MachineKey 업데이트 인사이트"
    infoBubbleText="컴퓨터 키 상태와 관련된 정보를 찾았습니다 오른쪽에서 세부 정보를 참조하세요"
    service="microsoft.classiccompute"
    resource="domainnames"
    authors="mmccrory"
    displayOrder=""
    articleId="MachineKey_NeedsMitigation"
    diagnosticScenario="MachineKeyUpdates"
    selfHelpType="rca"
    supportTopicIds=""
    resourceTags=""
    productPesIds="13185"
    cloudEnvironments="public"
/>

# <a name="we-ran-diagnostics-on-your-resource-and-found-an-issue"></a>리소스에서 진단을 실행하여 문제를 발견했습니다.

<!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime--> 부터 **DeploymentName** 은 향상된 알고리즘을 사용하여 컴퓨터 키를 암호화하지 않습니다. <!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime--> 이후에는 Cloud Service 배포를 재배포하거나 삭제하지 않는 한 이 상태가 올바릅니다.

향상된 알고리즘을 사용하려면 이 [공지](https://aka.ms/azuremachinekeyinfo)에 제공된 단계를 수행합니다. 또한 이 [공지](https://aka.ms/azuremachinekeyinfo)를 통해 배포에서 향상된 알고리즘을 사용하는지 확인할 수 있습니다.

구독에 추가 Cloud Service 배포가 있는 경우 <!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime-->부터 현재 MachineKey 상태와 함께 여기에 나열됩니다.
## <a name="list-of-azure-cloud-service-deployments"></a>Azure Cloud Service 배포 목록
<!--$DeploymentList-->DeploymentList<!--/$DeploymentList--> 
