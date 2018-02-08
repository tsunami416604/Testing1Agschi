<properties
    pageTitle="VMA RCA"
    description="RCA - Correção do Serviço de Nó - Falha do Nó"
    infoBubbleText="Reinicialização recente encontrada. Confira detalhes à direita."
    service="microsoft.compute"
    resource="virtualmachines"
    authors="ScottAzure"
    displayOrder=""
    articleId="UnexpectedVMReboot_9F9DD6CF-8AA8-42C4-AC73-623EA43F1593"
    diagnosticScenario="UnexpectedVMReboot"
    selfHelpType="rca"
    supportTopicIds="32411816"
    resourceTags="windows, linux"
    productPesIds="14749"
    cloudEnvironments="public"
/>
# <a name="we-ran-diagnostics-on-your-resource-and-found-an-issue"></a>Executamos o diagnóstico em seu recurso e encontramos um problema
 
<!--issueDescription-->
## <a name="vm-availability-incident-diagnostic-information-for---vmname--virtual-machine--vmname--"></a>**Informações de diagnóstico de incidentes da Disponibilidade de VM para <!--$vmname-->Máquina virtual<!--/$vmname-->:** ##

Identificamos que sua VM ficou indisponível à(s) **<!--$StartTime--> StartTime <!--/$StartTime--> (UTC)** e a disponibilidade foi restaurada à(s) **<!--$EndTime--> EndTime <!--/$EndTime--> (UTC)**. Esta ocorrência inesperada foi causado por uma **ação de reinicialização do nó de host iniciada pelo Azure**.
<!--/issueDescription-->

A ação de reinicialização do nó de host foi acionada por nossos sistemas de monitoramento do Azure ao detectar uma condição de falha devido a uma alta carga do tráfego de rede, revelando um bug em um driver de rede no nó físico onde a máquina virtual estava hospedada. Isso fez sua VM ser reinicializada também. As conexões RDP e SSH para a VM ou solicitações para quaisquer outros serviços em execução dentro da VM podem ter falhado durante esse tempo. 
 
Nossos engenheiros da plataforma principal identificaram o bug e atualmente estão trabalhando em uma correção do problema. Depois que a solução tiver sido verificada e concluído o teste, ela será implantada em todos os nós afetados.  

Para garantir um nível maior de proteção e redundância para o aplicativo no Azure, é recomendável que você agrupe duas ou mais máquinas virtuais em um conjunto de disponibilidade.<br>
Para saber mais sobre opções de alta disponibilidade, confira os seguintes artigos:<br>
* [Gerencie a disponibilidade de máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability)<br>
* [Configurar a disponibilidade das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-how-to-configure-availability)<br>

O Microsoft Azure também fornece acesso a informações de integridade de recursos e solução de problemas no Portal do Azure.<br>
Para saber mais sobre o Azure Resource Health, confira o seguinte artigo:<br>
* [Entender e usar o Resource Health Center para solucionar esse cenário no futuro](https://docs.microsoft.com/azure/resource-health/resource-health-overview)

Pedimos desculpas por qualquer inconveniência que isso possa ter causado. Estamos trabalhando continuamente na melhoria da plataforma para reduzir os incidentes de disponibilidade das Máquinas Virtuais devido a problemas da plataforma.
