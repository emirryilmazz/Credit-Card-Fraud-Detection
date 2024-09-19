# Credit-Card-Fraud-Detection

# Projenin Amacı: 
Bu projenin amacı, bir finansal veri seti üzerinde sahtecilik (fraud) tespit etmek ve bu tespiti hem denetimli (supervised) hem de denetimsiz (unsupervised) öğrenme yaklaşımlarıyla optimize etmektir. Denetimli öğrenme kapsamında voting yöntemleriyle model performansı artırılırken, sahtecilik tespiti için recall metriği önceliklendirilmiştir. Denetimsiz öğrenmede ise anomaly detection kullanılarak etiketlenmemiş veri içindeki olası sahtecilik vakaları tespit edilmiş ve uygun metriklerle değerlendirilmiştir. Projenin genel amacı, sahtecilik vakalarını yüksek doğrulukla tespit eden bir sistem geliştirmektir.

# Veri Seti
Kullanılan dataset, ~1.3 milyon satırdan oluşmaktadır. Sütun isimleri ise sırasıyla şu şekilde: 

- **Unnamed: 0**: Bu sütun veri kümesindeki her bir satıra atanmış otomatik bir indeks numarasını göstermektedir.
- **trans_date_trans_time**: Bu sütun, işlemin gerçekleştiği tarih ve zamanı belirtir.
- **cc_num**: Bu sütun, kredi kartı numarasını (gizlenmiş veya kısaltılmış) temsil eder.
- **merchant**: Bu sütun, işlemin gerçekleştirildiği satıcı veya iş yeri adını belirtir.
- **category**: Bu sütun, işlemin yapıldığı satıcı veya iş yerinin kategorisini (örneğin market, restoran) gösterir.
- **amt**: Bu sütun, yapılan işlemin tutarını (miktarını) gösterir.
- **first**: Bu sütun, kart sahibinin adını temsil eder.
- **last**: Bu sütun, kart sahibinin soyadını temsil eder.
- **gender**: Bu sütun, kart sahibinin cinsiyetini belirtir.
- **street**: Bu sütun, kart sahibinin yaşadığı sokak adresini temsil eder.
- **city**: Bu sütun, kart sahibinin yaşadığı şehri belirtir.
- **state**: Bu sütun, kart sahibinin yaşadığı eyalet veya bölgeyi belirtir.
- **zip**: Bu sütun, kart sahibinin yaşadığı posta kodunu temsil eder.
- **lat**: Bu sütun, kart sahibinin yaşadığı yerin enlem bilgisini gösterir.
- **long**: Bu sütun, kart sahibinin yaşadığı yerin boylam bilgisini gösterir.
- **city_pop**: Bu sütun, kart sahibinin yaşadığı şehrin nüfusunu belirtir.
- **job**: Bu sütun, kart sahibinin mesleğini gösterir.
- **dob**: Bu sütun, kart sahibinin doğum tarihini temsil eder.
- **trans_num**: Bu sütun, işleme ait benzersiz işlem numarasını belirtir.
- **unix_time**: Bu sütun, işlemin UNIX zaman damgasını (epoch time) içerir.
- **merch_lat**: Bu sütun, işlemin yapıldığı satıcının konumunun enlem bilgisini gösterir.
- **merch_long**: Bu sütun, işlemin yapıldığı satıcının konumunun boylam bilgisini gösterir.
- **is_fraud**: Bu sütun, işlemin sahtecilik olup olmadığını gösterir (1: sahte, 0: sahte değil).
- **merch_zipcode**: Bu sütun, işlemin yapıldığı satıcının bulunduğu posta kodunu gösterir.

# Yöntem
Veri önişleme adımlarında aşağıdaki adımlar izlenmiştir:
- **Gereksiz sütunları kaldırma (drop)**: Model için anlamlı veya etkili olmayan, analize katkı sağlamayan sütunları veri setinden çıkardım. Bu, hem veri temizliğini hem de işlem süresini optimize etmeye yardımcı oldu.

- **Null değerlerin kontrolü**: Veri setinde eksik (null) değerler olup olmadığını kontrol ettim ve bu değerlerin modellenmeyi olumsuz etkilememesi için gerekli işlemleri uyguladım (örneğin, eksik değerleri doldurma veya ilgili satırları silme).

- **Normalizasyon**: Modelin daha tutarlı sonuçlar verebilmesi için sayısal değerleri normalizasyon işleminden geçirdim. Bu, verilerdeki farklı ölçüm birimlerini ortak bir ölçekte değerlendirerek modelin performansını iyileştirdi.

- **One hot encoding + PCA**: Kategorik verileri sayısal verilere çevirmek için one-hot encoding yöntemini uyguladım. Daha sonra, veri boyutunu azaltmak ve işlem süresini optimize etmek amacıyla Ana Bileşen Analizi (PCA) uyguladım. Ancak bu yöntem istediğim sonuçları vermedi.
  
- **Label encoding**: One-hot encoding + PCA işe yaramadığı için, kategorik verileri sayısal verilere dönüştürmek için label encoding yöntemini kullandım. Bu, kategorik değerleri sıralı bir şekilde kodlayarak veri setinde daha az yer kaplamalarını sağladı.

# Model Seçimi ve Eğitim 
Eğitim kısmını şu şekilde açıklayabiliriz:

- **Model seçiminde voting kullanımı**: Modelin performansını artırmak amacıyla oylama (voting) yöntemi kullanılmıştır. Bu yöntemde birden fazla model bir araya getirilerek daha güçlü bir tahmin elde edilmeye çalışılmıştır. Voting içerisinde **Decision Trees**, **Hist Gradient Boosting** ve **Naive Bayes** algoritmaları kullanılmıştır.

- **Eğitilen modelin cross_val_score ile değerlendirilmesi**: Modelin genelleme yeteneğini test etmek ve aşırı öğrenmenin (overfitting) önüne geçmek amacıyla, eğitilen model **cross_val_score** fonksiyonu ile çapraz doğrulama (cross-validation) kullanılarak değerlendirilmiştir. Bu yöntemde, veri seti farklı k alt kümelere bölünür ve model her bir alt küme üzerinde eğitilip test edilir. Böylece, modelin performansı daha tutarlı bir şekilde ölçülür ve farklı veri kümeleri üzerinde nasıl çalıştığına dair bir fikir elde edilir.

- **Recall metriğinin öncelikli olması ve confusion matrix ile değerlendirme**: Seçilen proje gereği **recall** metriği (duyarlılık) başarım ölçümünde önceliklendirilmiştir. Recall, modelin sahtecilik gibi nadir durumları ne kadar iyi yakaladığını gösterdiği için bu projede daha önemli kabul edilmiştir. Başarım ölçümü, bir karışıklık matrisi (confusion matrix) kullanılarak yapılmıştır. Bu matris, modelin doğru ve yanlış sınıflandırmalarını ayrıntılı olarak gösterir ve recall gibi metriklerin daha net anlaşılmasını sağlar. 
