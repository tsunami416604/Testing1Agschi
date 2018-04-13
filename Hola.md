<properties 
  pageTitle="Element docelowy trasy — Internet" 
  description="Element docelowy trasy — Internet" 
  infoBubbleText="Wykryto problemy z routingiem ruchu sieciowego. Szczegółowe informacje można znaleźć po prawej stronie."
  service="microsoft.network" 
  resource="virtualnetworks" 
  authors="anavinahar" 
  displayOrder="" 
  articleId="CantRDP_RouteTargetInternet" 
  diagnosticScenario="Internet traffic" 
  selfHelpType="Diagnostics" 
  supportTopicIds="32511135, 32411835, 32584250, 32584252" 
  resourceTags="windows" 
  productPesIds="16342, 14745, 15571, 15797, 14749, 15526"
  cloudEnvironments="Public"
/>

# <a name="we-ran-connectivity-diagnostics-on-your-resource-and-found-an-issue"></a>Firma Microsoft przeprowadziła diagnostykę połączeń Twojego zasobu i wykryła problem.

<!--issueDescription-->
Platforma Microsoft Azure zidentyfikowała problem z routingiem, który uniemożliwia dostęp zdalny do maszyny wirtualnej <!--$vmname-->[vmname]<!--/$vmname-->.
Routing wykonuje akcję <!--$action-->[action]<!--/$action--> względem tego ruchu <!--$TrafficDirection-->[TrafficDirection]<!--/$TrafficDirection--> w przypadku kierowania do Internetu.
Usługa Access Control stosuje akcję <!--$action-->[action]<!--/$action--> do tego ruchu <!--$TrafficDirection-->[TrafficDirection]<!--/$TrafficDirection--> zgodnie z regułą zabezpieczeń zdefiniowaną przez klienta: {rule.Replace("UserRule_", string.Empty)}
<!--/issueDescription-->

Jeśli nie chcesz, aby ruch do tego miejsca docelowego był kierowany bezpośrednio przez Internet, skonfiguruj prefiks trasy obejmujący to miejsce docelowe w bramie lokalnej sieci VPN, skontaktuj się z administratorem sieci w celu anonsowania prefiksu za pomocą protokołu BGP (jeśli chcesz włączyć obwód usługi ExpressRoute lub połączenie VPN lokacja-lokacja z włączonym routingiem BGP) lub dodaj prefiks w trasie zdefiniowanej przez użytkownika (jeśli chcesz wysyłać ruch do wirtualnego urządzenia sieciowego — WUS).

Jeśli wynik kontroli dostępu (reguł zabezpieczeń) jest niepożądany, należy przejrzeć [aktywne reguły zabezpieczeń](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-troubleshoot-portal) w celu ustalenia, czy reguła zabezpieczeń zdefiniowana przez klienta wymaga modyfikacji. Jeśli ten ruch powinien być dozwolony, utwórz podstawową regułę <!--$TrafficDirection-->[TrafficDirection]<!--/$TrafficDirection--> z wyższym priorytetem (niższym numerem) niż istniejące reguły, określając port {this.destinationPort}. Jeśli ten ruch nie powinien być dozwolony, utwórz zaawansowaną regułę <!--$TrafficDirection-->[TrafficDirection]<!--/$TrafficDirection--> z wyższym priorytetem (niższym numerem) niż istniejące reguły, określając żądane źródłowe i docelowe adresy IP, port {this.destinationPort} i akcję Zablokuj.
