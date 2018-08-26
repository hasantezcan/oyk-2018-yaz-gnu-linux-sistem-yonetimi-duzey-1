### ÖYYK 2018 - GNU/Linux Sistem Yönetimi 1.Düzey - (GÜN 2)
---
- ***echo*** - Ekrana herhangi bir string basar.
```BASH
 echo "Selam"
```
- ***cat*** - Herhangi bir dosyayıının içeriğini ekrana basmaya yarar

## **Alias (takma isimler)**
  Bir komutu ve onun parametrelerini fakrlı şekilde çağırmamızı sağlar.

  ```BASH
  alias lan="ls --all -l"
  ```
  Artık bundan sonra ***"lan"*** yazınca **"ls -la"** komutu çalışmış olacak.

  - **unalias** : alias ile ayarladığımız komutu kaldırmamızı sağlar.

  ```BASH
  unalias lan
  ```

  - Tüm kayıtlı aliasları görüntülemek için
  ```BASH
  alias
  ```

## Komut Satırında Kullanılan Kısayollar

> "~" = tilda işareti

**cd ~**  : ev dizinimize gideriz

**cd ..** : bir önceki dizine geçer

**history** : kullandığımız komutların geçimişini verir

**SHIFT + pageUp/pageDown** : Terminalde yukarı aşşağı gezinmemizi sağlar.

**TAB tuşu** : otomatik tamamlama yapar

**CTRL + D** : Kabuk oturmunu kapatır. ***-logout -exit***

## Metin Editörleri

 Dosyaların içine yazı yazmamızı sağlarlar. En yaygın kulanılan metin editorü ***"vim"***dir.

***Vim :*** Vim'in iki ana modu vardır. Bunlar
1. **Insert (Girdi)** -  (Insert Moddan Command moda çıkmak için ESC'ye basılır.)
2. **Command (Komut)**


 Vim öntanımlı olarak Command modda açılır. Biz dökümana müdahale etmek istersek **"i"** ya da **"a"** tuşuna basıp ***insert moda*** geçmeliyiz.

 Vim de kaydetme, geri alma, çıkma gibi işler **komut modunda** yazacağımız komutlar ile gerçekleşir.

- Dosyaya yazma  
  ***:w***

  Eğer doyayı **ilk** defa oluşturuyorsak

  ***:w dosya_adi***

- Dosyaya yazma ve çıkmak  
  ***:wq***

- Kaydetmeden çıkma  
***:q***   >>  kaydetmeden çıkar  ve bu sırada sizi uyarır.  
***:q!***  >> çıkmaya zorlar ve uyarı vermez!

- Döküman içinde kelime arama  
***/aranacak_kelime***

Eğer bu kelime(string) birden fazla defa mevcut ise "**N**" (next) tuşu ile tüm sonuçları sırası ile gezinebilirsiniz.

- Bir dökümanı vim ile açmak içine

```BASH
vim dokuman_adi
```

- Yapılan bir değişikliği geri almak için de (ctrl+Z  gibi)  
****u (yıldız u)***

- Kesmek için >> **dd**

- Yapıştırmak için >> **p**

- Kopyalamk için >> **yy**

>Visiual modda da bu işlemleri yapabilirsiniz.


## Ortam değişkenleri (Environment Variables)
> (OKU!)https://cihanbozkurt.wordpress.com/2016/11/12/linux-ortam-degiskenleri/

- Değişken adları büyük harf ile yazılır.
  ```SHELL
  echo $DEGISKEN_ADI
  ```
  Bir değişkenin bulunduğu dizini görmek için:

  ```BASH
  echo $SHELL
  /bin/bash
  ```

  >aslında çıkan bu **"/bin/bash"** sonuçu ortam değişkenimizin değeridir.
---

- **Ek-Bilgi**  
   Nasıl echo ile **$SHELL** yazdırız?

  **1.Yöntem** - vim ile yeni bir dosya oluşturn ve içine ***$SHELL*** yazın sonra bu dosyayı "*echo*" ile okuttuğunuzda konsolda "$SHELL" yazısını göreceksiniz..

  **2.Yöntem** - escape character >> **\**
    > echo '\$SHELL'
---
- **whereis KOMUT**  - Komutun sistemde nerde olduğunu gösterir. Aynı zamanda komutun man sayfasının dizinini de verir.

- **which KOMUT** - Görevi whereis ile aynı olsa da whereis e göre daha az detay verir. Daha kullanışlıdır.

- **env** - Kullanıcıların sistemde kulandığı ortam değişkenlerini görüntüler

#### **PATH Ortam Değişkeni**

ls komutunun dosyalarının nerde olduğunu öğrenmek için

  ```BASH
  $ which ls
  /bin/ls
  ```
Aslında **ls** ile **/bin/ls** aynı şey eğer biz terminale **/bin/ls** dersek yine bize o dizinin içini listeleyecekdir. Çünkü aslında biz konsola **/bin/ls** yazdığımız da bash'e diyoruz ki ***"git sen bu dizini bize çalıştır"***.

- Bir ortam değişkeninin değerini değiştirmek için :

  ```bash
  $ echo $HOME
  /home/kullanıcı

  $ HOME=/etc

  $ echo $HOME
  /etc
  ```

### PATH değişkenini kavramak için bir uygulama
- **cat** komutunun görevi bilindiği üzere bir dökümanı içeriğini terminale basmaktır. Ve her bir komutun olduğu gibi cat komutunun da buluduğu bir dizin vardır.

Bunu öğrenmek için:
```
$ which cat
/bin/cat
```
gelin şimdi bu komutun yerini değiştirelim. Ve cat komutunun kendi kulanıcı dizinimize **mv** ile taşıyalım.
```
# mv /bin/cat /home/hasantezcan
```
Bu andan sonra cat komutu çalışmayacaktır.  

Çünkü sisteminin **cat'i aradığı dizinde** artık cat yok.

**>Peki ne yapmalıyız ??**

Sistemin **cat'i** bulabilmesi için sisteme bakması gereken **yeni bir adres** vermeliyiz.
Sistemde bulunan bütün ***komutların yerlerini*** tutan değişkenin adı **PATH** dir

PATH içinde sistemde kayıtlı ***çalıştırılabilirlerin dizinleri*** tutulur.

Biz cat'in bulunduğu dizini değiştirdiğimizden cat çalışmıyor. Fakat PATH'e ***cat'in bulunduğu yeni dizini ekleyip*** cat'i eskiden olduğu gibi çalışır hale getirebiliriz.

Bunu yaparken **export** komutunu kullanıcaz.
```BASH
export PATH=$PATH:/home/hasantezcan/
```
Artık PATH'e cati araması için yeni bir dizin daha veridik. Ve PATH /home/hasantezcan dizi altında da arama yapınca /home/hasantezcan/cat 'i bulmuş oldu.

Artık cat komutu eskiden olduğu gibi çalışmaya devam edecek.

**>Peki değişen bir şey oldu mu?**

Evet oldu. **cat** in hangi dizinde olduğuna bakmıştık. Şimdi tekrar bakalım.

```BASH
$ which cat
/home/hasantezcan/cat
```
değişen şey **cat** çalıştırılabilirinin çalıştığı dizin.
**cat** çalıştırılabiliri artık ***/home/hasantezcan/cat*** dizini üzerinden çalıştırılıyor...

## PATH Nasıl çalışıyor..

PATH linux ve linux benzeri işletim sistemlerinde bulunan bir ***ortam değişkenidir.***
Kabuğa, bir kullanıcı tarafından verilen komutlara yanıt olarak hangi dizinlerin içinde çalıştırılabilir dosyalar araması gerektiğini söyler.

Simdi de "**which**" ile bir komutun yerini tespit etmek istediğimizde işler nasıl yürüyor şimdi ondan bahsedelim.

---
Öncelikle PATH ortam değişkeni içinde neler bulunur...

PATH'in içine bakmak için:

```BASH
echo $PATH
```
PATH içinde çalıştırılabilirleri arayacağı dizinleri görürüz. Bu dizinler arasına biz de **export** komutu ile dizinler ***ekleyip çıkartabiliriz.***

---
biz which cat yazdığımızda önce tanımlı bir alias var mı onlara bakıyor ardandan da PATH içindeki dizinlere bakarak çalıştırılabilirleri aramaya başlar. Eğer geçerli dizinler içinde çalıştırılabilir dosyayı bulursa onun dizini ekrana yazar. Ama bulamazsa da hata mesajını bize gösterir.

Bir çalıştırılabilirin iki farklı dizinde olması halinde de -tabiki iki dizinde path de olduğunu varsayıyoruz- PATH dizinleri sırası ile aradığından hangi dizin path de daha önce ise çalıştırılabilir o dizinden çalışacakdır ve dizin olrak da önce  olanın dizini gösterilir.



## Kabuk Ayar Dosyaları

**.bashrc** bash'in özelleştirme dosyalarıdır.Her kullanıcının home dizininin içinde gizli hale bulunurlar. İçine kaydedilen değişiklikler kabuk oturmu yeniden başladığında devreye girer. ya da kabuk oturumunu yeniden başlatmak yerine
```Bash
source .bashrc
```
yazarak sistemi yeniden başlatmamıza gerek kalmadan değiştirdiğimiz özelleştirmeleri görebiliriz. ("Source .bashrc" komutu .bashrc içindeki tüm komutları çalıştırır.)

**NOT:** .bashrc ya da .bash_profile içine tanımlanmamış tüm aliaslar, .bashrc ya da .bash_profile içine beliritmediğimiz tüm ortam değişkenleri değişiklikleri kabuk oturumu yeniden başladığında silinecektir. Bu yapılan değişiklikler ön bellekte tutulmakdadır. Herhangi bir kalıcılığı yoktur. Ama eğer kalsın isterseniz yapmak istediğiniz değiştirmeleri bu dosyalar içine kayıt etmelisiniz.

- .bashrc içine neler yazıla bilir...
  .bashrc içine nazar duasını ekleseniz kabuk oturmu her açıldığında nazar duasını sizlere gösterir.

- Mesela hocamız kendi dağıtımını ve sürümünü gösteren bir komutu .bashrc'sine kaydetmiş kabuk oturumunu her açtığında bu komut çalışıp bize sürümünü gösteriyordu.

### .bashrc ile .bash_profile dosyalarının farkı...

  - Kullanıcı adı ve parola ile giriş yaptığımızda .bash_profile çalışır.
  - Yeni bir terminal oturumu açtığımızda bashrc çalışır(yüklenir)
Fakat biz şuan kullandığımız sistemden ötürü kullanıcı adı ve parola ile giriş yaptığımızda aynı anda terminali de açmış oluyoruz

**.bash_history** Sistemde kullanılan komutların geçmişini tutar.

**.bash_logout** Kabuk oturumu sonlanırken kabuk bu dosyaların içini okur ve o işlemlere göre oturumu kapatır.
