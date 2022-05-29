for testing:

kubectl run -it --rm --image nginx:alpine svc-test -- sh

nc -v -z -w 5 redis-scv.database 6379