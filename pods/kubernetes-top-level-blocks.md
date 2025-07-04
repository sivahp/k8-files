apiVersion:
kind:
metadata:
spec:

we can call these are 4 top level blocks any kubernetes manifest files

once pod has been created
kubectl get pods
kubectl describe pod my-app-pod

kubectl get pods -all-namespaces --no-headers | wc -l


In POD Definition, we have labels
it's a Key value Pair, mainly users for identificaation for the services and selectors

readiness 
- By using this we will check the Application readyness or not.


livenessprobes:
By using LivenessProbe, It will be used to check, if the Application is live or not.
