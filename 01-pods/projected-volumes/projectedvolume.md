<h2>Projected Volumes</h2>
Projected Volume, mevcutta bulunan birçok volume kaynağını aynı dizine map etme işlemidir.
Şu anda, aşağıdaki volume kaynak türleri kullanılabilir durumdadır.

	• secret
	• configMap
	• downwardAPI
	• serviceAcoountToken

Tüm kaynakların ilgili Pod ile aynı namespace'te bulunması gerekmektedir.

Şimdi bu kaynakları ortak bir dizine nasıl map edebileceğimizi inceleyelim.

Öncelikle localimizde bulunan dosyalarla birlikte username ve password Secret'ları oluşturacağız. Ardından, bu Secret'ları ortak bir dizine map edeceğimiz, içerisinde tek bir container barındıran bir Pod ayağa kaldıracağız.

Pod'u oluşturmak için kullanacağımız Pod definition dosyamız projected.yaml

Bu yaml dosyasını incelediğimizde, user ve pass adındaki secret objelerini kullanarak Projected Volumes tanımlandığını ve bunların Pod içerisinde "/projected-volume" dizinine mount edildiğini görüntülemekteyiz.

Pod'u create etmeden önce Secret'ları oluşturalım.

Öncelikle sırasıyla, username ve password bilgilerinin tutulacağı username.txt ve password.txt adında iki local dosya oluşturalım.

	Ø echo -n "admin" > ./username.txt
	Ø echo -n "123456" > ./password.txt

Şimdi bu dosyaları kullanarak Kubernetes Secret objelerini oluşturalım.

	Ø kubectl create secret generic user --from-file=./username.txt
	Ø kubectl create secret generic pass --from-file=./password.txt

Secret'lar oluştuktan sonra Pod'u create edelim.

	Ø kubectl apply -f projected.yaml 

Pod'u oluşturup, running duruma geldiğinden emin olduktan sonra bu pod'un içerisine girip kullandığımız Secret objelerinin Pod'un içerisindeki dizinde map edilip edilmediğini kontrol edelim.

	Ø kubectl exec -it test-projected-volume -- /bin/sh
	
Pod'un içine girdikten sonra " ls /projected-volume/ " komutu ile kontrol sağlayabiliriz. Mount ettiğimiz Secret objelerinin bu dizinde olduğunu görüntülüyoruz. 
