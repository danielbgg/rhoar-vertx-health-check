# RHOAR Vert.x Health Check
Vert.x Health Check Microservice - RHOAR course

## Compile Application
```
mvn clean package
```

## Openshift Deployment
```
export HEALTHCHECK_PROJECT_NAME=healthcheck-demo
oc new-project $HEALTHCHECK_PROJECT_NAME
mvn clean fabric8:deploy -Popenshift
```

### Deployment Test
```
export HEALTHCHECK_DEMO_URL=http://$(oc get route health-check-vertx -n $HEALTHCHECK_PROJECT_NAME -o template --template='{{.spec.host}}')
curl -X GET "${HEALTHCHECK_DEMO_URL}/api/greeting"
curl -X GET "${HEALTHCHECK_DEMO_URL}/api/killme"
curl -X GET "${HEALTHCHECK_DEMO_URL}/api/greeting"
oc get pods -w
```

### Edit ConfigMap
```
oc edit configmap app-config
curl "${CONFIGMAP_DEMO_URL}/api/greeting"
```
