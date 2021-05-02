
El escenario sobre el que se realizan las pruebas es la tienda Hipster de Google que está desplegada con la ayuda de Istio.
Su repositorio:
https://github.com/GoogleCloudPlatform/microservices-demo/blob/master/docs/service-mesh.md

En nuestro caso, la aplicacion está toda desplegada en el namespace default, al igual que todos los experimentos de Litmus.

IMPORTANTE

Una vez se despliega el escenario, para que los experimentos se puedan ejecutar en él será necesario anotar en todos los deployments:
kubectl annotate deploy/nombredeployment litmuschaos.io/chaos="true" -n nombrenamespace

Por cada schedule se deberán crear sus permisos correspondientes!! (son exactamente iguales que si fuera un chaos engine)

Cuando ya se han hecho esas dos cosas, se modifica el archivo chaos-schedule al gusto y se ejecuta con kubectl apply -f fichero-chaos-schedule.yaml

Al final de cada experimento, se generan los ficheros de resultados chaosresults correspondientes.

Para ver los logs:
kubectl logs chaos-scheduler-5877d9dbd6-9qfwf -n litmus
