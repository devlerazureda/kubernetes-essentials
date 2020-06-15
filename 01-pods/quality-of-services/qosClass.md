<h2>Quality of Service for Pods</h2> 
Kubernetes, Pod'ları uygun şartlar altında schedule etmek veya silmek için Quality of Service (QoS) sınıflarını kullanır.
Kubernetes yeni bir Pod objesi yarattıktan sonra aşağıdaki QoS sınıflarından bir tanesini ilgili Pod'a atar.

	• Guaranteed
	• Burstable
	• BestEffort

Bu çalışmamızda yapacağımız örnekleri uygulayacağımız yeni bir namespace oluşturalım.

	Ø kubectl create namespace qos-example

<h4>Guaranteed</h4>
Guaranteed tipinde QoS sınıfı atanmış bir pod oluşturalım.

Bu poddaki her bir container için eşit memory limit ve memory request değerleri belirlenmelidir.
Aynı zamanda, CPU limit ve CPU request değerlerinin eşit olarak belirlenmesi gerekmektedir.

Örnek bir Pod Definiton yaml dosyası için dosyalardaki 01-qos-pod.yaml adlı dosyayı inceleyebiliriz.
Bu dosyada tek bir container tanımlaması yapılmış Memory için 200Mi, CPU için ise 700m değerleri belirlenmiştir. Guaranteed tipinde bir QoS sınıfı ataması istediğimiz için request ve limit değerleri eşit olmalıdır.

Bu definition yaml dosyasını kullanarak pod'u oluşturalım.

	Ø kubectl apply -f 01-qos-pod.yaml --namespace qos-example

Pod oluştuktan sonra -o yaml parametresi ile birlikte pod'un qosClass değerini kontrol edelim.

	Ø kubectl get pods qos-demo -o yaml --namespace qos-example

spec:
  containers:
    ...
    resources:
      limits:
        cpu: 700m
        memory: 200Mi
      requests:
        cpu: 700m
        memory: 200Mi
...
  qosClass: Guaranteed

Görüleceği gibi pod'umuz Guaranteed sınıfında oluşmuş durumdadır.

Şimdi bu podu silebiliriz.

	Ø kubectl delete pod qos-demo --namespace qos-example

<h4>Burstable</h4>
Burstable tipinde QoS sınıfı atanmış bir pod oluşturalım.

Eğer Pod Guaranteed sınıfı kriterlerini sağlamıyorsa ve Pod'un içindeki en az bir container'ın CPU veya memory request değeri mevcut ise Burstable tipinde bir pod oluşturulur.

Burstable tipinde QoS sınıfına sahip bir Pod oluşturmak için örnek bir pod definition yaml dosyası oluşturalım: 02-qos-pod-2.yaml

Bu dosyayı kullanarak Pod'u schedule edelim ve yeniden output'u inceleyelim

	Ø kubectl apply -f 02-qos-pod-2.yaml --namespace qos-example
	Ø kubectl get pods qos-demo-2 -o yaml --namespace qos-example

spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: qos-demo-2-ctr
    resources:
      limits:
        memory: 200Mi
      requests:
        memory: 100Mi
...
  qosClass: Burstable

Burada gördüğümüz gibi pod'umuz Burstable tipinde bir QoS sınıfına sahiptir.

Şimdi bu podu silebiliriz.

	Ø kubectl delete pod qos-demo-2 --namespace qos-example

<h4>BestEffort</h4>
BestEffort tipinde QoS sınıfı atanmış bir pod oluşturalım.

Pod'un içinde yer alan containerların herhangi bir CPU veya Memory request, limitlerinin tanımlı olmasına gerek olmadığı durumlarda Best effort tipinde QoS sınıfına sahip Podlar oluşur.

BestEffort tipinde QoS sınıfına sahip bir Pod oluşturmak için örnek bir pod definition yaml dosyası oluşturalım: 03-qos-pod-3.yaml

Bu dosyayı kullanarak Pod'u schedule edelim ve yeniden output'u inceleyelim

	Ø kubectl apply -f 03-qos-pod-3.yaml --namespace qos-example
	Ø kubectl get pods qos-demo-3 -o yaml --namespace qos-example

spec:
  containers:
    ...
    resources: {}
  ...
  qosClass: BestEffort

Görüldüğü gibi pod'umuz BestEffort tipinde bir QoS sınıfına sahiptir.

Şimdi bu podu silebiliriz.

	Ø kubectl delete pod qos-demo-3 --namespace qos-example

<h4>Example</h4>
Şimdi ise bir Pod tanımı yapalım. Bu pod tanımında iki farklı container bulunduralım ve nginx image'nın çalışacağı container için memory request tanımı yapalım. Fakat redis image'nın çalışacağı container için herhangi bir tanımda bulunmuyoruz. Dosyamızın adı: 04-qos-pod-4.yaml

Bu dosyayı kullanarak Pod'u schedule edelim ve yeniden output'u inceleyelim

	Ø kubectl apply -f 04-qos-pod-4.yaml --namespace qos-example
	Ø kubectl get pods qos-demo-4 -o yaml --namespace qos-example

Bu Pod, Guaranteed sınıfının gerekliliklerini karşılamıyor fakat Burstable sınıfının gerekliliğini bir container'da Memory request tanımı olduğu için sağlıyor.

spec:
  containers:
    ...
    name: qos-demo-4-ctr-1
    resources:
      requests:
        memory: 200Mi
    ...
    name: qos-demo-4-ctr-2
    resources: {}
    ...
  qosClass: Burstable

Output'ta da göreceğimiz gibi Pod'un QoS sınıfı Burstable olarak ayarlanmış durumdadır.


