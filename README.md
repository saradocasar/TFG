# TFG
Despliegue de escenarios en Kubernetes para aplicar Chaos Computing en GKE con la herramienta Litmus

## Desplegar un escenario y experimento.

###### 1º Desplegamos el escenario, a ser posible en un namespaces distinto al default.

kubectl apply -f archivoescenario.yaml

###### 2º Creamos el archivo que dará permisos al experimento para poder realizar las modificaciones sobre el escenario para generar el chaos. A este documento lo llamamos rbac.yaml

kubectl apply -f rbac.yaml

###### 3º Añadir esta linea antes de crear el experimento.

kubectl annotate deploy/nombredeployment litmuschaos.io/chaos="true" -n nombrenamespace

###### 4º Por último, creamos el archivo del experimento al que llamaremos chaosengine.yaml. Asegurarse de que trabaja sobre el namespace del escenario, así como especificar bien las labels.

kubectl apply -f chaosengine.yaml

Para comprobar resultados:

(kubectl describe chaosresult <chaos-engine-name>-<chaos-experiment-name> -n nombrenamespace)

kubectl describe chaosresult nginx-chaos-pod-delete -n nginx

Si algo va mal, podemos comprobar los logs:

kubectl logs -f chaos-operator-ce-5c448b4dd5-k2vfj -n litmus

o bien, mirar dentro del fichero del experimento en busca del error:

(el nombre del chaosengine lo hemos definido nosotros en el archivo chaosengine.yaml)

kubectl describe chaosengine nombredelchaosengine -n nombrenamespace

