# NLP_Tweet_IDentify | Tweet Metin Yazar Tanıma Uygulaması

## <b> Hedef </b>
İngilizce tweet metinlerinin incelenerek, metinlerin kim tarafından yazıldığının bulunması hedeflenmiştir. Bu işlem için kullanılan ver seti, canlı olarak Twitter[1] sosyal medya platformundan sağlanmıştır.
Her tweet, tweet id, text, userid, location gibi pek çok nitelik tanımlayıcı nitelik içerir. Ancak analiz işlemi için yalnızca, tweet id ve tweet text’i kullanılmıştır. Proje içerisinde, analiz işlemi uygulandıkça çıkarım yapılan bilgiler bir sınıf nesnesi içinde tutulmuştur.
Projenin kodlanma aşamasında, python[2] programlama dili ve Jupyter Notebook [3] geliştirici ortamı kullanılmıştır.
## <b>Araştırma Öncesi Yapılan Çalışmalar</b>
Tweet metinleri, kullanıcı temelli yapısız metinlerdir. Dolayısıyla duygusal ifadeler, emojilerin kullanımı, yazım ve noktalama işaretlerine uyulmaması ve dilbilgisi kurallarına uygun metin içeriklerinin Tweet içeriğinde olma ihtimali oldukça düşüktür.İçerikler yapısal değildir. Bu sebeple analiz işlemine başlamadan önce pek çok normalizasyon işlemi yapılmıştır. Bu işlem için, textacy[4] python kütüphanesinden yararlanılmıştır.

<b>Textacy Kütüphanesi</b> 

SpaCy[5] kütüphanesi üzerine kurulu çeşitli doğal dil işleme görevlerini yerine getiren bir Python kütüphanesidir. Temel ilkeleri, tokenization, POS(part of speech tagger), bağımlılık, ayrıştırma vb. gibi işlemlerdir.
Yapılan Ön İşlemler
Ön işleme herhangi bir makine öğrenmesi veya derin öğrenme görevinden önce metin içerikli dökümanların hazırlanmasında en kritik adımdır. Tokenlara ayırma, gereksiz sık kullanılan kelimelerin(stop words) atılması ve kelime köklerinin bulunması en yaygın kullanılan ön işleme yöntemleridir.

<b>Ana Adımlar </b>
- Bir metin dokümanını analiz etmek için, ilk olarak tokenlara ayırma işlemi yapılmalı ve kelime grupları elde edilmelidir.
- Tüm ortak ayırıcılar, işleçler, noktalama işaretleri ve yazdırılamayan karakterler kaldırılır.
- Daha sonra, en sık kullanılan kelimeleri filtrelemeyi amaçlayan stop-words filtreleme gerçekleştirilir. Örnekler: “ama, belki, acaba”.
- Son olarak, kelime hakkında dil-bilgisel veya sözcüksel bilgiler sunan son-eklerin çıkarılmasıyla morfolojik kökün elde edilmesini amaçlayan stemming ve / veya lemmatization uygulanır. Makalede, bu adımlar atlanmıştır.

<b>Yapılan İşlemler </b>
- Küçük harfe çevirme işlemi
- Url silme işlemi
- Email hesap silme işlemi
- Telefon numarası silme işlemi
- Para birimi silme işlemi
- Tırnak kullanımının kaldırılması işlemi
- Aksan içeren Unicode kullanımların kaldırılması işlemi

![Resim1-Ön İşlem Öncesi](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu1.png)

![Resim2-Ön işlem sonrası](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu2.png)

<b>Veri Gösterimi-Pandas Kütüphanesi</b>

Twitter API kullanılarak elde edilen veriler yine bir Python kütüphanesi olan Pandas[6] kullanılarak kullanıcıya sunulmuştur. Pandas, veri analizi ve veri ön işlemeyi kolaylaştıran açık kaynak kodlu bir kütüphanedir. Dağıtık çalışmaya uygun değildir bu sebeple üzerinde işlem yapılan verinin büyüklüğü makinenin kapasitesiyle sınırlıdır özellikle de ana belleğin.

![Resim 3-Pandas Kütüphanesi Tablo Kullanımı](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu3.png)


<b> Analiz İşlemi-Vektör Kullanımı</b>

Projenin gerçekleştirilmesi aşamasında kullanılan veri seti Tweet metinleridir. Tweet metinleri yapısal metinler değildir. Yapısal olmayan bu metinler üzerinde makine öğrenmesi modellerinin uygulanabilmesi için öncelikle metinlerin işlenmesi gerekmektedir. Kabaca şu adımlar izlenir, metin içerikleri özniteliklere yani yapısal bir formata çevrilir, öznitelikler ise vektörlere çevrilir.

## <b>Öznitelik/Terim Temsili ve BoW Modeli </b>

Kelime/Sözcük Çantası (BoW) modeli, bir dokümandaki terimlerin oluşum şeklini (Örneğin: terim sayılarını) belirten metnin temsil biçimidir. Bu modelde; terim pozisyonu ve sözcük sıralaması dikkate alınmaz.
Vektör Uzay Modeli (VUM), her bir metin dokümanının bir vektör olarak temsil edildiği gelişmiş bir BoW sürümüdür ve her bir boyut ayrı bir terime (özniteliğe) karşılık gelir. Dokümanda bir terim yer almışsa, ilgili doküman vektöründe terimin değeri sıfırdan farklı olur.

![Resim 4-Pandas Kütüphanesi Tablo Kullanımı](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu4.png)

<b>TF x IDF Skorlama Modeli</b>

Terim sıklıklarının sayılması ile ilgili en önemli sorun, sık kullanılan terimlerin dokümanda baskın olmaları ve artık dokümanı temsil eder hale gelmeleridir. Bu terimler çok değerli bilgiler içermese dahi özellik kümesindeki diğer niteliklerin etkisiz olmasına sebep olur.
Bu problemi çözmek için, “Terim Frekansı x Ters Belge Frekansı” anlamına gelen “TF x IDF” modelini ve skorlama yöntemi kullanılabilir. Hesaplamada iki ölçüt kullanılır: terim sıklığı (tf) ve ters belge sıklığı (idf). TF x IDF’nin matematiksel denklemleri şöyledir:

- j’ninci dokümandaki i’ninci terim için TF x IDF skoru = TF(i, j) * IDF(i)
- TF(i, j) = (Dokümandaki i’ninci terimin sıklığı) / (Dokümandaki toplam terim sayısı)
- IDF(i) = log2(Toplam doküman sayısı/i’ninci terimi içeren doküman sayısı)
- Kodlama adımında dokümanlarımızı bir TFxIDF özellik matrisine dönüştürebilmek için TfidfVectorizer sınıfı kullanılmıştır.

## <b>Konu Modelleme</b>

Tweet metninin kime ait olduğunu anlayabilmek için, metin içeriği üzerinde modelleme işlemi yapılır. Bu işlem için metin içeriğindeki anahtar kelimelerin bulunup ortaya çıkarılması gerekmektedir. Çıkartılan konular bir terim koleksiyonu olarak temsil edilirler. Metin dokümanlarının büyük bir kısmını özetlemek için çok değerlidirler, dahası, verilerde gizli kalıpları/anlamsallığı ortaya çıkarırlar.
Metin içeriklerinin birbirine olan benzerliğini kontrol etmek için LDA (Latent Dirichlet Allocation) [7] modeli kullanılır.

<b>LDA</b>: Verilerdeki bazı bölümlerin neden benzer olduğunu tarif etmek amacıyla, gözlem gruplarının gözlemlenmemiş gruplar tarafından açıklanmasına izin veren bir üretken istatistik modelidir. Python’da gensim[8] ve sklearn kütüphanelerini kullanarak LDA modelinin oluşturulması mümkündür. Proje kapsamında sklearn kütüphanesi kullanılmıştır.

## <b>NGram Algoritması</b>

Mevcut veri seti kontrol edilerek,  yazarı belli olmayan tweet metinlerine dair yazar tahmini yapmak hedefine ulaşmak için, kontrol edilmek istenen verinin eldeki veriye olan yakınlığının hesaplanması sürecinde sklearn kütüphanesinin ngram sınıfından yararlanılır.
Ngram aslında bir dil modelidir. Tahmine ve olasılığa dayanır. Karakter ve kelime bazlı olmak üzere iki kategoride incelenir. Bir karakter ya da kelimenin kendinden önce gelen birkaç karaktere ya da kelimeye bağlı olarak, bulunduğu yerde olma olasılığını hesaplar.
- Projede ngram karakter temelinde kullanılmıştır.

## <b>Logistic Regression </b>

Yalnızca iki değere sahip veriseti üzerinde olaılık hesaplama işlemidir. Veri setinde her kelimenin ağırlıkları hesaplanmıştır. Bu ağırlıklı veri üzerinde lojistik resgresyon işlemi yapılır.

## <b>Model Seçimi-GridSearchCV </b>

Eğitim veri seti üzerinde yapılan önişleme, ngram ağaç oluşumu, matris ve vektör dönüşümlerinin ile lojistik regresyon işleminin ardından model seçimi aşamasına geçilir. Model seçiminde, eşlemenin 
kullanılacağı algoritmanın başarısını yükseltmek için en iyi parametrelerin belirlenmesi gibi işlemler 
için Python Sklearn kütüphanesinin GridSearchCV sınıfından yararlanılmıştır.

Çapraz eşleme işlemleriyle birlikte eğitim seti 10 ile çarpılıp bölünür. Böylece 200 tweet metni içinde elde 2000 veri bulunur. Bu veri üzerinde çalışacak algoritma için gerekli en iyi parametreler elde edilmiş olunur.

![Resim 5-Model Seçimi](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu5.png)

## <b> Uygulama </b>

Projenin uygulanması aşamasında, iki adet tweet metni  uygulamaya girdi olarak verilir. Her metnin 2 kullanıcıdan hangisine ait olduğu olasılık değerleriyle gösterilir. 

- 	Metinler test işlemi için öncelikle Tfidf vektör yapısına getirilir.

![Resim 6-Uygulama 1](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu6.png)

![Resim 7-Uygulama 2](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu7.png)

![Resim 8-Uygulama 3](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu8.png)

Eldeki tüm tweet metinleri birleştirilir ve Model kullanılarak hangi kullanıcıya ait olduğu test edilir. Tweet metninin gerçekten kime ait olduğu handle sütununda gösterilmiştir. Model kullanımının ardından kime ait olduğunun olasılıklı değerleri ise tablonun son iki sütununda gösterilmiştir. Bu test işleminin amacı modelin ne derece doğru çalıştığını gözlemlemektir.

![Resim9- Uygulama 4](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu9.png)

Birleştirilmiş olan tweet metinlerinde, her iki kullanıcı için olasılık değeri en yüksek olan tweet metinleri resim 10’da gösterilmiştir.


![Resim10- Uygulama 5](https://github.com/NisanurBulut/NLP_Tweet_IDentify/blob/master/Photos/Goruntu10.png)


Kaynakça
1.	https://shiftdelete.net/twitter-nedir-nasil-kullanilir-10080
2.	https://www.python.tc/python-nedir/
3.	http://www.veridefteri.com/2017/10/30/jupyter-notebook-nedir-2/
4.	https://pypi.org/project/textacy/
5.	https://pypi.org/project/spacy/
6.	http://www.datascience.istanbul/2017/05/21/python-pandas-ile-temel-islemler-1/
7.	https://scikitlearn.org/stable/modules/generated/sklearn.discriminant_analysis.LinearDiscriminantAnalysis.html
8.	https://radimrehurek.com/gensim/

