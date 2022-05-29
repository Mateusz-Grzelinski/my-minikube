
## setup voting app in kubernetes

kubectl.exe apply -f .\result.yml

kubectl.exe create -n result deployment --image pandaacademy/result:1.0  result  --dry-run=client -o yaml

kubectl.exe create service nodeport  vote-svc --namespace vote  --tcp 80:5000 --node-port=31000 --dry-run=client -o yaml

kubectl.exe create -n vote  service clusterip vote-svc --tcp 5000:80 --node-port 31000 --dry-run=client -o yaml

kubectl.exe port-forward -n result pods/result-66d48bd958-8x9w4 8080:80

## for testing:

kubectl run -it --rm --image nginx:alpine svc-test -- sh

nc -v -z -w 5 redis-scv.database 6379