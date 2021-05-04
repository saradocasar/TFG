# Trabajo Fin de Grado

Despliegue del escenario basado en microservicios de Google: microservices-demo en Kubernetes para aplicar Chaos Computing en GKE con la herramienta Litmus. 

## 1º Desplegamos el escenario.

kubectl apply -f archivoescenario.yaml

## 2º Creamos el archivo que dará permisos al experimento para poder realizar las modificaciones sobre el escenario para generar el chaos. A este documento lo llamamos Permisos.yaml

kubectl apply -f Permisos.yaml

## 3º Añadir esta linea antes de crear el experimento a los deployments que se les inyectará el Chaos.

**kubectl annotate deploy/nombredeployment litmuschaos.io/chaos="true" -n nombrenamespace**

## 4º Por último, creamos el archivo del experimento al que llamaremos ChaosScheduler.yaml. Asegurarse de que trabaja sobre el namespace del escenario, así como especificar bien las labels.

kubectl apply -f ChaosScheduler.yaml

**Para la monitorización se utiliza New Relic.** Además, se podrá comprobar con:

kubectl describe chaosresult <chaos-engine-name>-<chaos-experiment-name> 

Si algo va mal, podemos comprobar los logs:

kubectl logs -f chaos-operator-ce-5c448b4dd5-k2vfj -n litmus

o bien, mirar dentro del fichero del experimento en busca del error:

(el nombre del chaosengine lo hemos definido nosotros en el archivo ChaosScheduler.yaml)

kubectl describe chaosengine nombredelchaosscheduler 

