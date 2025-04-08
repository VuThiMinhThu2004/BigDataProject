https://grok.com/chat/fcf399df-13e3-49b8-9c43-844ea2083f03

Bạn có thể kiểm tra các NodePort bằng lệnh:
```kubectl get svc

Và truy cập qua:
    http://<NODE_IP>:32181  # Zookeeper
    http://<NODE_IP>:30992  # Kafka broker
    http://<NODE_IP>:30081  # Schema Registry

Run các container:
    make apply

Delete: make delete

base) thu@bcm10-headnode01:~/BigDataProject/k8s$ kubectl get svc
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)             AGE
broker            ClusterIP   10.150.111.32    <none>        9092/TCP,9101/TCP   58m
control-center    ClusterIP   10.150.21.64     <none>        9021/TCP            58m
ollama-service    NodePort    10.150.131.250   <none>        11434:32413/TCP     17d
postgres          NodePort    10.150.78.189    <none>        5432:32447/TCP      58m
schema-registry   ClusterIP   10.150.139.135   <none>        8081/TCP            58m
webserver         NodePort    10.150.157.235   <none>        8080:31040/TCP      58m
zookeeper         ClusterIP   10.150.113.113   <none>        2181/TCP            62m
(base) thu@bcm10-headnode01:~/BigDataProject/k8s$ 


(base) thu@bcm10-headnode01:~/BigDataProject/k8s$ kubectl get pods -n thu-restricted
NAME                               READY   STATUS                       RESTARTS         AGE
broker-788f6fc689-fjcg5            1/1     Running                      6 (3m7s ago)     67m
control-center-65677b9c78-pkfmq    0/1     CrashLoopBackOff             15 (5m8s ago)    67m
ollama-65586bcc55-wp76r            1/1     Running                      0                17d
postgres-66544bcd96-2h4m6          1/1     Running                      0                67m
scheduler-7dcbbc74f4-mxznp         0/1     CreateContainerConfigError   0                59m
schema-registry-869d4b6dc7-qkjs2   0/1     CrashLoopBackOff             16 (2m45s ago)   67m
spark-master-576fd9449b-ckc59      0/1     CrashLoopBackOff             6 (84s ago)      9m15s
spark-worker-79cf89cd65-czm75      0/1     CrashLoopBackOff             6 (101s ago)     9m15s
webserver-595f68dbb-6mzwf          0/1     CreateContainerConfigError   0                64m
zookeeper-dffd5d9db-72vrd          1/1     Running                      0                68m
(base) thu@bcm10-headnode01:~/BigDataProject/k8s$ 