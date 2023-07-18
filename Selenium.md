# Selenium 
<img src="selenium-img/Selenium-automation-testing.png"
     alt="Markdown Monster icon"
     style="margin-left:20px" />



## Selenium Nedir?

Farklı tarayıcılarda yada ortamda web uygulamalarını test etmek için kullanılan test çerçevesidir(framework). Başka bir deyişle, web uygulamalarının kalite güvencesi için kullanılan yazılım test otomasyon araçlar paketidir. Ayrıca açık kaynaklı yazılım olduğu için ücretsizdir. Test Komut Dosyaları için C#, Pyhton, Java gibi birden fazla programlama dili kullanılır. Günümüzde ise Google, Netflix, HubSpot gibi büyük ve gelişmiş şirketlerde üretim için kullanılmaktadır.  Bu paket test kaynaklı sorunları ve ihtiyaçları için farklı çözümler sunar. Selenium Testi, Selenium test araçlarını kullanılarak yapılan testlerin genel ismidir.


### Test otomasyonu;
* Regresyon testlerini destekler.
* Geliştiriciler için hızlı geri bildirim sağlar.
* Test durumlarını tekrarlamayı sağlar.


Selenium’u birden fazla tarayıcıda yeniden çalıştırmak için Javascript kütüphanesi geliştirildi. Bunun sonucunda Selenium IDE ve Selenium RC (Remote Control)’nin temeli olan Selenium Core meydana geldi. Tarayıcıların Javascript için güvenlik kısıtlamaları Selenium için bazı durumları imkansız hale getirdi. Bunun için de WebDriver geliştirildi.


### Selenium Araçları;

* **Selenium IDE:** Test komutlarını oluşturmak için kullanılan Firefox eklentisi olan bir araçtır. Selenium IDE kullanarak test durumları kaydedilerek yürütülür ve böylece yeniden kullanılabilir test komutları ortaya çıkar.
* **Selenium RC:** Birden fazla testin sürekli olarak yapılmasını sağlar. Bir Selenium RC sunucusu ile çalışır.
*  **Selenium Grid:** Selenium RC’ye benzer şekilde birden fazla sunucu ile çalışabilir. Paralellik ön plandadır. Yani aynı anda farklı testler farklı uzak makinelerde çalıştırılabilir.
* **Selenium WebDriver:** Selenium RC’nin yöntemi olarak Javascript fonksiyonlarını tarayıcıya göndermez.


## Selenium kütüphanesini indirme


```python
pip install selenium
```

## İlk selenium script

### Sekiz Temel Bileşenler  
Selenium'un yaptığı her şey, bir şeyler yapmak için tarayıcı komutlarını göndermek veya bilgi istekleri göndermektir. Selenium ile yapacaklarınızın çoğu şu temel komutların bir birleşimidir:

1. Oturum Başlatma (Start the session)

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/drivers/">driver sessions</a>
```python
from selenium import webdriver
from selenium.webdriver.common.by import By

driver = webdriver.Chrome()
```

2. Tarayıcıda işlem yapma (Take action on browser)

Tarayıcıda açmak istediğiniz siteyi kolaylıkla aşağıda kod ile açabilirsiniz.

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/interactions/navigation/">navigating</a>

```python
driver.get("https://github.com/MuhammedCubukcu")
```
3. Tarayıcı bilgilerini isteme (Request browser information )

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/interactions/"> information about the browser </a>

```python
title = driver.title
```

4. Bekleme Stratejisi Oluşturun (Establish Waiting Strategy )

Kodu tarayıcının mevcut durumuyla senkronize etmek Selenium'daki en büyük zorluklardan biridir ve bunu iyi yapmak ileri düzeyde bir konudur.

Temel olarak, öğenin yerini belirlemeye çalışmadan önce sayfada olduğundan ve onunla etkileşime girmeden önce öğenin etkileşimli bir durumda olduğundan emin olmak istersiniz.

Gizli bir bekleme nadiren en iyi çözümdür, ancak burada gösterilmesi en kolay olanıdır, bu yüzden onu yer tutucu olarak kullanacağız.

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/waits/">Waiting strategies.</a>

```python
driver.implicitly_wait(0.5)
```
5. Bir öğe bulma (Find an element)

Çoğu Selenium oturumundaki komutların çoğu öğeyle ilgilidir ve önce bir öğe bulmadan biriyle etkileşim kuramazsınız.

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/elements/">finding an element.</a>

```python
text_box = driver.find_element(by=By.NAME, value="my-text")
submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")
```

6. Öğe üzerinde etkileşim (Take action on element)
   
Bir öğe üzerinde gerçekleştirilecek yalnızca birkaç eylem vardır, ancak bunları sık sık kullanacaksınız.

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/elements/interactions/">actions to take on an element</a>

```python
text_box.send_keys("Muhammed")
submit_button.click()
```
7. Öğe bilgilerini isteyin (Request element information)

Öğeler, talep edilebilecek birçok bilgiyi depolar.

Detaylı bilgi için: <a href="https://www.selenium.dev/documentation/webdriver/elements/information/">information that can be requested.</a>

```python
value = message.text
```

8. Oturumu sonlandırın
   
Bu, varsayılan olarak tarayıcıyı da kapatan sürücü işlemini sonlandırır. Bu sürücü örneğine daha fazla komut gönderilemez.

```python
driver.quit()
```

## Her şeyi bir arada kullanmak. (Putting everything together)

Bu 8 şeyi, bir test çalıştırıcısı tarafından yürütülebilecek iddialarla eksiksiz bir komut dosyasında birleştirelim.

```python
from selenium import webdriver
from selenium.webdriver.common.by import By


def test_eight_components():
    driver = webdriver.Chrome()

    driver.get("https://www.selenium.dev/selenium/web/web-form.html")

    title = driver.title
    assert title == "Web form"

    driver.implicitly_wait(0.5)

    text_box = driver.find_element(by=By.NAME, value="my-text")
    submit_button = driver.find_element(by=By.CSS_SELECTOR, value="button")

    text_box.send_keys("Selenium")
    submit_button.click()

    message = driver.find_element(by=By.ID, value="message")
    value = message.text
    assert value == "Received!"

    driver.quit()
```


### Daha fazlası için yaptığım projeye göz atabilirsiniz: <a href="https://github.com/MuhammedCubukcu/WebFormsSeleniumProject">WebFormsSeleniumProject </a>   