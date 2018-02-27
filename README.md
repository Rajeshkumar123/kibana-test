# kibana-test

This is a test for someone I can't say but it helps show how to get around a security restriction 

## As Developer

Do this as a developer

```
oc login -u developer
oc new-project mytest
oc project mytest
oc new-app https://github.com/christianh814/kibana-test --name=ktest
```

## As an Admin

Do this as an admin

```
oc login -u system:admin
oc project mytest
oc create serviceaccount useroot
oc adm policy add-scc-to-user anyuid -z useroot
oc patch dc/ktest --patch '{"spec":{"template":{"spec":{"serviceAccountName": "useroot"}}}}'
oc delete pods --all -n mytest
oc start build ktest -n mytest
```
