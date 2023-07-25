
<img src="redis-img/redis.png"
     style="margin-left:20px" />

# Redis Nedir ? 

* Redis, geliştiriciler tarafından en çok kullanılan ve bilinen NoSQL veritabanlarından birisidir. 
* Redis, açık kaynaktır ve kaynak kodlarına GitHub üzerinden erişilebilmektedir. 
* C dili ile yazıldığı için yüksek performanslı sonuçlar vermektedir.
* Linux ve türevi işletim sistemleri tarafından desteklenmekte fakat Windows tarafı için resmi bir destek olmasa da community tarafından desteklenmektedir.
* Redis günümüz sistemlerinde en çok kullanılan anahtar-değer veritabanıdır ve genellikle caching, session yönetimi, pub/sub, message broker amacıyla kullanılmaktadır.

# Redisin Bize Sağladığı Avantajlar:
## Yüksek Performans

* Redis, verileri disklerde (HDD veya SSD) tutan veri tabanlarının akside bellek (RAM) üzerinde tutar bu sayede disklere erişim ihtiyacını ortadan kaldırarak gecikmeleri, I/O bağlantılarını önler ve daha az CPU kullanan basit algoritmalar ile verilere erişir.
  
## Veri yapıları : 
* Redis verileri bellek üzerinde ```<key,value>``` çifti olarak tutmaktadır, burada herbir anahtara denk gelen değerler farklı veri yapılarında tutulabilmektedir.
* Bu veri yapıları; String, List, Hash, Set, Sorted Set, Bitmaps, HyperLogLogs, Geospatial Indexes
  

## Persistance (Veri Kalıcılığı)

* Redis’te verilerin RAM üzerinde saklandığından bahsettik, olası bir elektrik kesintisi, sunucu kapanması gibi durumlarda veriler silinecektir. Redis bize iki yöntem sunmaktadır verinin kalıcılığını sağlamak için. Bunlar; point-in-time Snapshots ve Append Only File (AOF).
* Snapshots yönteminde belirli zaman aralıkları ile RAM üzerindeki verinin kaydı, kopyası diske kayıt edilir bu sayede olası bir elektrik kesintisi gibi durumlarda disk üzerinden verilere tekrar geri dönülebilir.
* Append Only File yönteminde ise her değişikliği dosyanın sonuna yazarak oluşan veri değişikliklerinin kaydını tutar.

## Bir çok dil desteği sağlar: 

* Redis birçok dil tarafından desteklenmektedir, bunlar; Java, Python, PHP, C, C ++, C#, JavaScript, Node.js, Ruby, R, Go gibi dillerdir ve bunların yanı sıra daha fazla da dil bulunmaktadır.

# Redis’in Bazı Kullanım Senaryoları:

## Caching (Önbellek) Mekanizması

* Sıkça kullanılan verilerimizi sürekli veritabanına ya da diğer kaynaklara gidip çağırmak yerine ön belleğe almak performans açısından olumlu bir katkı sağlayacaktır. Dağıtık mimaride çalışabilen Redis, dağıtık cache(distributed caching) yönetimi için birçok uygulamada kullanılmaktadır.

## Session Yönetimi

* Uygulamalarımızı kullanırken kullanıcılara ya da diğer yapılara ait verilerimizi sayfalar arasında taşımak için session’dan sıkça yararlanmaktayız fakat uygulamamız büyüdükçe bu verilerin tutulması artan bellek alanına neden olmaktadır. Redis; sosyal medya, e-ticaret uygulamaları, oyun gibi alanlarda session bilgilerinin tutulmasında da rol almaktadır.

## Pub/Sub

* Redis, pub/sub işlevini destekleyen komutlara da sahiptir ve Redis’in broadcast yayını yapmasına olanak sağlar. Bu, mesajı tek bir istemcinin bir kanala bağlı diğer birçok istemciye yayınlamasına olanak tanır.

## Queues (Kuyruklar)

* Redis, gerçekleşmesi zaman alacak işleri bir kuyruk yapısına alınmasını ve daha sonradan işlenmesini destekler.

# Veri türü

## Strings 
* Verilerin string formatı olarak tutulduğu veri yapısıdır. ```<key,value>``` çiftinde değer kısmı maksimum 512 MB yer tutar.

String veri ekleme komutu:
```
SET firstName muhammed
```

* Anahtar değeri ile string veriyi alma komutu:
```GET <key>```
```
 GET firstName
```
* Değerin sonuna string ekleme komutumuz:
APPEND ```<key> <text>```

```
APPEND firstName "Cbkc"
```

* Bütün anahtar değerlerini çağırma  komutu:
KEYS *

```
KEYS *
```
* Anahtar değeri ile veri silme komutu:
DEL ```<key>```
```
DEL firstName
```

* Bütün verileri silme komutu:
```
FLUSHALL
```
Not: Yukarıdaki komutlarda her ne kadar string işlemleri yapsak da sayılsa bir değeri string gibi tutup üzerinde matematiksel işlemler de gerçekleştirebiliriz.

* Sayısal değeri bir artırma komutu:
INCR ``<key>``

```
SET age 25

INCR age
(int) 26
```
Not: Yukarıdaki INCR komutu ile değer bir artırıldı. Bunun yanı sıra DECR, DECRBY, INCRBY gibi komutlar ile de artırım ya da azaltım işlemleri yapılabilmektedir.

* Oluşturulacak değere yaşam süresi ekleme komutu:
SETEX ```<key> <expire_time> <value>```

```
SETEX lastName 10 cbkc
TTL lastName
```
* TTL komutu verilen anahtar değerin süresinin bitmesine kaç saniye kaldığını söyler, verilen expire_time değeri saniye cinsindendir.


# Lists

* Burada veriler bağlı liste biçiminde tutulurlar. Bu listede, liste başını ifade etmek için L, liste sonunu ifade etmek için de R kullanılır.


* Listenin başına eleman ekleme komutu:
LPUSH ```<key> <value>```

```
LPUSH postList "Dependency Injection ve Ninject"
```

* Listenin sonuna eleman ekleme komutu:
RPUSH ```<key> <value>```

```
RPUSH postList "Object Oriented Programming"
```

* Listenin eleman sayısını öğrenme komutu:
LLEN ```<key>```
```
LLEN postList
```

* Listenin başından eleman silme komutu:
LPOP ```<key>```
```
LPOP postList
```

* Listenin sonundan eleman silme komutu:
RPOP ```<key>```
```
RPOP postList
```
* Listede belirli aralıktaki verileri alma komutu:
LRANGE ```<key> <start_index> <stop_index>```

```
LRANGE postList 0 2
```
* Liste üzerindeki eleman sayısını bilmediğimiz durumlarda start_index değerine 0 stop_index değerine -1 verirsek bütün verileri elde edebiliriz.
  
# Sets
* Set veri tipi, verileri sırasız (rastgele sırada eklenilen) ve unique (benzersiz) olarak tutan veri tipidir. Aynı veriden birden fazla bulunmamaktadır.
  
* Set’e eleman ekleme komutu:
SADD ```<key> <value>```

```
SADD friends ali cabbar
```
* Set içerisinden eleman silme komutu:
SREM ```<key> <value>```

```
SREM friends ali cabbar
```

* Set içerisindeki bütün elemanları getirme komutu:
SMEMBERS ```<key>```

```
SMEMBERS friends
```

# Sorted Sets
* Sorted Set veri yapısı, Set veri yapısının benzerdir. Verileri unique (benzersiz) olarak tutmakla beraber score dediğimiz değere göre sıralama işlemi yapmaktadır.

* Sorted Set’e eleman ekleme komutu:
ZADD ```<key> <score> <value>```

```
ZADD teams 74 "Besiktas"
```
* Sorted Set içerisinden eleman silme komutu:
ZREM ```<key> <value>```
```
ZREM teams Besiktas
```
* Sorted Set içerisindeki belirli aralıktaki verileri alma komutu:
ZRANGE ```<key> <start_index> <stop_index>```
```
ZRANGE teams 0 1
```
* Sorted Set üzerindeki eleman sayısını bilmediğimiz durumlarda start_index değerine 0 stop_index değerine -1 verirsek bütün verileri elde edebiliriz. Komutun sonuna WITHSCORES yazılarak score değerleri ile birlikte veriler elde edilmiş olur.

# Hashes

Hash veri tipi, bir key’e karşılık birden fazla field (alan tutmaya) yarayan veri tipidir.

* Hash’e eleman ekleme komutu:
HSET ```<key> <field> <value>```
```
HSET person firstName muhammed
```
* Hash içerisinden belirli alanı getirme komutu:
HGET ```<key> <field>```

```
HGET person firstName
```
* Hash içerisinden belirli alanı silme komutu:
HDEL ```<key> <field>```

```
HDEL person firstName
```

* Hash içerisindeki bütün alanı getirme komutu:
HGETALL ```<key>```

###  KAYNAKLAR: 
* https://redis.io/docs/