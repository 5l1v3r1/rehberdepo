Daha önceki Paket Üretimine Başlangıç-1 yazımızda talimat dosyasının ön tanıtımını yapmıştık. Bu yazımızda talimat dosyasını biraz daha detaylı tanıtacağız.

Aşağıda basit bir talimat dosyamız var. Bu talimat üzerinden anlatımı gerçekleştireceğiz.

	# Description: Testdisk güçlü ve özgür bir veri kurtarma yazılımıdır
	# URL: http://www.cgsecurity.org/wiki/TestDisk
	# Packager: yasarciv67@gmail.com
	# Depends on: ntfs-3g libjpeg-turbo

	name=testdisk
	version=7.0
	release=1
	source=(http://www.cgsecurity.org/$name-$version.tar.bz2)

	build() {

	cd $name-$version

	./configure --prefix=/usr

	make 
	make DESTDIR=$PKG install

	rm -r $PKG/usr/share/doc
	rm -r $PKG/usr/share/man/zh_CN
	}


==> # Description: Bu satırda paketimizin kısa bir açıklaması yer almaktadır. Kullanıcılar açısından Türkçe anlatımlar olması paketin ne olduğunun anlaşılması için faydalı olacaktır. Çünkü paket yöneticisinden mps ara (paket_adı) ile arama yapıldığında paket adından sonra bu açıklamalar görünmektedir.

==> # URL: Burada anlaşılacağı üzere ilgili paketin web adresi yer almalıdır. Web adresi yoksa bile geliştiricinin proje adresi verilebilir (Örn. github)

==> # Packager: Bu satırda talimatı oluşturan kişinin yani sizin adınız veya e-posta adresiniz yer almalı. Daha sonra paketle ilgili herhangi bir sorunda iletişim kurmak adına e-posta olması daha faydalı olacaktır.

==> # Depends on: Bu kısımda ilgili paketin bağımlılıkları yer almaktadır. Yani paketin derlenip kurulması veya kurulduktan sonra çalışması için gerekli olan paketler buraya yazılmaktadır. Burada dikkat etmemiz gereken husus, gerekli olan bağımlılıkların depomuzda olup olmadığının araştırılmasıdır. Bunu mps ara (paket_adı) ile arayabiliriz. Eğer paket depomuzda olmayan bir bağımlılık varsa önce onun talimatı oluşturulmalıdır. Ama önce talimatlarımızın olduğu dizinden kontrol etmek gerekebilir. Çünkü daha geliştirme aşamasında olduğumuz için talimatı olupta depoda olmayan paketler vardır.

==> name: Buraya oluşacak olan paketin tam adı yazılacaktır. Genelde geliştiricinin kaynak kodda verdiği isim kullanılmaktadır. Ancak daha sonraki rehberlerimizde daha farklı kullanımlar göreceğiz (örn. _name)

==> version: Burayada ilgili paketin versiyon numarası yazılacaktır. Genelde kaynak kodda versiyon numarası belirtilmektedir.

==> release: Devir olarak adlandırdığımız bu bölüme vereceğimiz değer tamamen bizimle alakalıdır. Yani paket için kaç kez düzenleme/güncelleme yapıldığını takip etmek için bir bilgidir. Genelde ilk yapılan talimatlarda 1 değeri verilmektedir.  Ancak pakette herhangi bir sebeple sonradan yapacağımız değişikliklerde bu sayıyı 2 yada 3 vs. şeklinde artırırız. Bu sayede paket için daha sonra yapılacak güncelleme olanağı sağlanmış olacaktır.

==> source: Bu bölüm, üzerinde çalışılacak olan dosyanın kaynağıdır. Genel olarak kaynak kodun indirme adresi yazılır. Bazen de, sonraki rehberlerimizde göreceğimiz kur-kos, patch vs. dosyalarının isimleri yazılabilmektedir. Burada dikkat etmemiz gereken bazı hususlar var. Yukarıdaki örnekte görüleceği gibi indirme adresinin içinde *$name-$version* ifadeleri var. Aslında web adreslerinde bu ifadeler olmuyor. Ancak paket sistemimiz talimat dosyasının içinde olan bu ifadelerin karşılığını indirme adresinin içine yerleştiriyor. Örneğin http://www.cgsecurity.org/$name-$version.tar.bz2 olan bu adresi http://www.cgsecurity.org/testdisk-7.0.tar.bz2 olarak değiştiriyor. Buradaki ($) harfi bu işlemi sağlıyor.

Bu bölümden sonrası internetten inen kaynak kod dizininin içinde gerçekleşen işlemlerdir. Yani "kaynak koddan derleme" işlemleridir. Ama sadece bununla sınırlı değildir. Kod derlenip sıkıştırılarak kurulabilir paket haline bu aşamada gelir.

Bu işlem "build() {" komutu ile başlayıp "}" komutu ile biter. Buradaki derleme işlemleri sonraki rehberlerimizde anlatılacağından ayrıntıya girmeyeceğiz. Genelde
	
	cd $name-$version
	./configure --prefix=/usr

	make 
	make DESTDIR=$PKG install
	
komutları çok sıklıkla karşılaşacağımız derleme yöntemidir. Buradaki $name-$version ifadesi yukarıda source: adımında gördüğümüz işlevin aynısıdır. "cd $name-$version" komutunun karşılığı "cd testdisk-7.0" yani testdisk-7.0 dizininin içine girme komutudur.

Bu adım içinde zaman zaman göreceğimiz 

	rm -r $PKG/usr/share/doc
	rm -r $PKG/usr/share/man/zh_CN
	
ifadeleri ise neredeyse hiç kullanılmayan ama fazla yer kaplayan doc ve man dosyalarının silinmesi içindir.

Buraya kadar gördüklerimiz genel olarak kullanılan, sıklıkla karşımıza çıkacak olan talimat oluşturma yöntemleridir. Ancak bu her pakette bu şekilde olmayıp daha karmaşık talimatlarla da karşılaşacağız. Ancak mantığı kavradıkça işlemlerin kolaylaştığını hissedeceksiniz.
