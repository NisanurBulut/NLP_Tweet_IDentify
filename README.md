# NLP_Tweet_IDentify | Twwet Metin Yazar Tanıma Uygulaması

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

![Resim1-Ön İşlem Öncesi](https://github.com/NisanurBulut/NLP_Tweet_IDentify/master/Photos/Goruntu1.JPG)

![Resim2-Ön işlem sonrası](https://github.com/NisanurBulut/NLP_Tweet_IDentify/master/Photos/Goruntu2.JPG)

<b>Veri Gösterimi-Pandas Kütüphanesi</b>

Twitter API kullanılarak elde edilen veriler yine bir Python kütüphanesi olan Pandas[6] kullanılarak kullanıcıya sunulmuştur. Pandas, veri analizi ve veri ön işlemeyi kolaylaştıran açık kaynak kodlu bir kütüphanedir. Dağıtık çalışmaya uygun değildir bu sebeple üzerinde işlem yapılan verinin büyüklüğü makinenin kapasitesiyle sınırlıdır özellikle de ana belleğin.
