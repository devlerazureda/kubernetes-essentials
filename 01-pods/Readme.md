```bash
alias k=kubectl
kubectl apply -f 02-pod.yaml
kubectl delete -f 02-pod.yaml

kubectl port-forward kuard 8080:8080

kubectl apply -f 04-pods-resources.yaml
kubectl delete -f 04-pods-resources.yaml

kubectl apply -f 07-nodeselector.yaml
kubectl describe pod nginx
kubectl label node xxx cpu=kotu
kubectl get pods -w
kubectl delete -f 07-nodeselector.yaml
```

```bash
kubectl run nginx --image=nginx --restart=Never --command -it -- env
kubectl run nginx --image=nginx --restart=Never --command -it -- env > command-pod.yaml
kubectl apply -f command-pod.yaml
kubectl run nginx --image=nginx --restart=Never  --command --dry-run=true -o yaml
k run nginx --image=nginx --port=80 --dry-run=true -o yaml
kubectl set image pod/nginx nginx=nginx:1.7.9
kubectl get pods -o=jsonpath='{.items[*].spec.containers[*].image}{"\n"}'
```





#### Todo

- Aşağıdaki konularda çalışabilmek için öncelikle kendi reponuza bu repoyu fork edip daha sonra pull request ile merge isteği yollayabilirsiniz. Aşağıdaki linkten inceleyebilirsiniz
    - https://www.youtube.com/watch?v=G1I3HF4YWEw
- Quality of Service for Pods
    - Aşağıdaki özelliğin tanıtılması için bir qoqClass.md içine bir yazı eklenilmesi.
    - qosClass özelliğinin tanıtılması.
    - https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/
- Projected Volume
    - Aşağıdaki özelliğin tanıtılması için bir projectedvolume.md içine bir yazı eklenilmesi.
    - Readme dosyasına projected volume nedir nasıl kullanılır.
    - https://kubernetes.io/docs/tasks/configure-pod-container/configure-projected-volume-storage/
- ImagePull Policy
    - - Aşağıdaki özelliğin tanıtılması için bir images.md içine bir yazı eklenilmesi.
    - ImagePullPolicy özelliğinin tanıtılması
    - https://kubernetes.io/docs/concepts/containers/images/

- Share Process Namespace between Containers in a Pod
- kompose
    - Aşağıdaki özelliğin tanıtılması için bir kompose.md içine bir yazı eklenilmesi.
    - Docker-compose dosyalarının otomatik kubernetes yamllarına dönüştürülmesi
    - https://kompose.io/
- terminationGracePeriodSeconds
    - Aşağıdaki özelliğin tanıtılması için bir signals.md içine bir yazı eklenilmesi.
    - terminationGracePeriodSeconds özelliği nedir neden kullanılır. Containerlara yollanan SIGTERM ve SIGKILL sinyallari ile ilgisi nedir?
    - https://pracucci.com/graceful-shutdown-of-kubernetes-pods.html
    - https://tasdikrahman.me/2019/04/24/handling-singals-for-applications-in-kubernetes-docker/
- termination yönetimi
    - Aşağıdaki iki özelliğin tanıtılması için bir termination.md içine bir yazı eklenilmesi.
    - terminationMessagePath: /dev/termination-log
    - terminationMessagePolicy: File
    
