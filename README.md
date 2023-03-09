
# Deploy av Observerbarhet plattform via ArgoCD

## Obserbarhet services

Observerbarhet består av tre olika delar, log, metrics och trace. För att få en microtjänst att leverera data inom de tre olika delarna används Opentelemetry sdk och api som utgångspunkt.

En ingående del är att ta emot data från microtjänst och det görs via Opentelemtry collector. Denna service är en en del av observerbarhets-plattform.

Opentelemtry collector tar emot data från microtjänst och eventuellt berikar data för att skicka vidare data till en plathållare iform av Grafan Tempo för trace data, Grfana Loki för log data och Grfan prometheus för metrics.

För att kunna använda sig av data som finns lagrat i de tre olika platshållarna återfinns Grafana som användargränsnitt för att ställa frågor mot data.

De olika service är:

- OTEL collector
- Grafan Tempo, trace
- Grfana Loki, log
- Grafana Prometheus, metrics

## Argocd

Argocd är ett service som är en del av GitOps-koncept där Argocd står för "deploument"-delen i GitOps.

För att kunna tillhandahålla services kommer Argocd och apps-in-apps mönster.

Detta för att det finns beroende mellan services och en service i sig ger ingent värde.

### Argocd apps-in-apps

Argocd apps-in-apps är ett mönster som gör det möjligt att gruppera applikationer/services och installera dessa som en enhet.

### Argocd katalogstruktur

När det existerar många olika miljöer som microtjänster skall är "best practises" att använda sig av en katalogstruktur som återspeglar de olika miljöerna som services ska finnas tillgägnliga.

Genom att strukturera kataloger enligt miljöer gör det enklet att hantara förändringar för tjänst samt att kunna på enkelt sätt uppdatera ev. "roll back" i de olika miljöerna.