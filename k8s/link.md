MinIO: http://10.200.2.34:32087/browser
Control-center: http://10.200.2.34:31661

MinIO: http://10.200.2.34:32087/browser






(base) thu@bcm10-headnode01:~/BigDataProject/k8s$ kubectl get svc
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE
broker            ClusterIP   10.150.59.176    <none>        9092/TCP,9101/TCP               39s
control-center    NodePort    10.150.176.88    <none>        9021:32090/TCP                  39s
minio             NodePort    10.150.148.214   <none>        9000:30161/TCP,9001:32087/TCP   10m
ollama-service    NodePort    10.150.131.250   <none>        11434:32413/TCP                 17d
postgres          NodePort    10.150.205.102   <none>        5432:32293/TCP                  39s
schema-registry   NodePort    10.150.150.146   <none>        8081:31542/TCP                  39s
spark-master      NodePort    10.150.152.38    <none>        9090:31574/TCP,7077:31434/TCP   39s
webserver         NodePort    10.150.53.39     <none>        8080:31960/TCP                  39s
zookeeper         NodePort    10.150.118.224   <non


(base) thu@bcm10-headnode01:~$ kubectl get node -owide
NAME      STATUS   ROLES                  AGE   VERSION    INTERNAL-IP   EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION       CONTAINER-RUNTIME
dgx01     Ready    worker                 18d   v1.30.11   10.200.2.34   <none>        Ubuntu 22.04.4 LTS   5.15.0-1063-nvidia   containerd://1.7.21
knode01   Ready    control-plane,master   18d   v1.30.11   10.200.2.36   <none>        Ubuntu 22.04.4 LTS   5.15.0-113-generic   containerd://1.7.21
knode02   Ready    control-plane,master   18d   v1.30.11   10.200.2.38   <none>        Ubuntu 22.04.4 LTS   5.15.0-113-generic   containerd://1.7.21
knode03   Ready    control-plane,master   18d   v1.30.11   10.200.2.37   <none>        Ubuntu 22.04.4 LTS   5.15.0-113-generic   containerd://1.7.21