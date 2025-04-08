./kompose convert -f docker-compose.yml -o k8s/all-configs.yaml

./kompose convert -f docker-compose-minio.yml -o k8s/minio.yaml

kubectl exec -it minio-d89d64cd5-zcn7z -n thu-restricted -- /bin/sh -c "/usr/bin/mc config host add dmlminio http://localhost:9000 minioadmin minioadmin && /usr/bin/mc ls dmlminio"

kubectl get service -n thu-restricted -o wide | grep webserver
minio             ClusterIP   10.150.164.173   <none>        9000/TCP,9001/TCP   5m43s   io.kompose.service=minio

❌ Các Pod đang lỗi:
Pod Name	Trạng thái	Ghi chú thêm
schema-registry	CrashLoopBackOff	Container crash liên tục
spark-master	Error	Không khởi động được
webserver	CrashLoopBackOff	Container crash
minio-setup	ContainerCreating	Có thể đang chờ volume, image


kubectl get jobs -n thu-restricted


1. Xem tất cả Pod trong tất cả namespace:
bash
Copy
Edit
kubectl get pods --all-namespaces
2. Kiểm tra xem Deployment có tạo ra Pod không:
bash
Copy
Edit
kubectl get deployment
3. Xem trạng thái Pod chi tiết:
bash
Copy
Edit
kubectl get pods -o wide
4. Nếu thấy Pod Pending, CrashLoopBackOff, hoặc Error, thì kiểm tra logs:
bash
Copy
Edit
kubectl describe pod <tên-pod>
kubectl logs <tên-pod>
🧪 Ví dụ:
Giả sử bạn thấy Pod schema-registry-xxx-yyy đang lỗi:

bash
Copy
Edit
kubectl describe pod schema-registry-xxx-yyy
kubectl logs schema-registry-xxx-yyy