<properties
    pageTitle="CloudServices RCA"
    description="Conclusión de actualización de la clave de máquina"
    infoBubbleText="Se ha encontrado información relacionada con el estado de la clave de máquina. Consulte los detalles de la derecha."
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
# <a name="we-ran-diagnostics-on-your-resource-and-found-an-issue"></a>Hemos ejecutado un diagnóstico en el recurso y detectado un problema

Desde las <!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime-->, **<!--$DeploymentName-->DeploymentName<!--/$DeploymentName-->** no usa el algoritmo mejorado para cifrar la clave del equipo. A menos que haya vuelto a implementar o haya eliminado las implementaciones del servicio en la nube desde las <!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime-->, es probable que este estado sea correcto.

Para usar el algoritmo mejorado, realice los pasos indicados en este [aviso](https://aka.ms/azuremachinekeyinfo). En este [aviso](https://aka.ms/azuremachinekeyinfo) también puede consultar las instrucciones para identificar si las implementaciones utilizan el algoritmo mejorado.

Si hay otras implementaciones del servicio en la nube en su suscripción, se mostrarán aquí con el estado actual de MachineKey a las <!--$LastRefreshTime-->LastRefreshTime<!--/$LastRefreshTime-->:
## <a name="list-of-azure-cloud-service-deployments"></a>Lista de implementaciones del servicio en la nube de Azure
<!--$DeploymentList-->DeploymentList<!--/$DeploymentList--> 
