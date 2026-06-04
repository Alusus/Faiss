# فـيس Faiss

[[English]](README.md)

روابط لغة الأسس لمكتبة [FAISS](https://github.com/facebookresearch/faiss) - مكتبة للبحث الفعّال عن التشابه وتجميع المتجهات الكثيفة.

## نظرة عامة

توفر هذه المكتبة روابط لغة الأسس لمكتبة FAISS، مما يتيح عمليات البحث عن التشابه في المتجهات والتجميع عالية الأداء في لغة الأسس.

## التثبيت

<div dir=rtl>

```
اشمل "مـحا"؛
مـحا.اشمل_حزمة("Alusus/Faiss@0.1"، "فـيس.أسس")؛
استخدم فـيس؛
```

</div>

أو بالإنجليزية:

```
import "Apm";
Apm.importPackage("Alusus/Faiss@0.1");
use Faiss;
```

## البدء السريع

### مثال بالعربية

<div dir=rtl>

```
اشمل "مـتم/طـرفية"؛
اشمل "مـتم/مـصفوفة"؛
اشمل "مـحا"؛
مـحا.اشمل_حزمة("Alusus/Faiss@0.1"، "فـيس.أسس")؛
استخدم مـتم؛
استخدم فـيس؛

// إنشاء فهرس مسطح بمتجهات رباعية الأبعاد
عرف الفهرس: سند[فـهرس]؛
فـهرس.أنشئ(الفهرس، 4، "Flat"، نـوع_قياس._نتاج_داخلي_)؛

// إضافة متجهات إلى الفهرس
عرف سب: مـصفوفة[عـائم]({1.0، 2.0، 3.0، 4.0، 2.0، 3.0، 4.0، 5.0})؛
الفهرس.أضف(2، سب.صوان)؛  // متجهان

// البحث عن أقرب الجيران
عرف سس: مـصفوفة[عـائم]({1.5، 2.5، 3.5، 4.5})؛
عرف الوسوم: مصفوفة[صحيح[64]، 3]؛
عرف المسافات: مصفوفة[عـائم، 3]؛
الفهرس.ابحث(1، سس.صوان، 3، المسافات، الوسوم)؛  // البحث عن أقرب 3 جيران

// التنظيف
فـهرس.حرر(الفهرس)؛
```

</div>

### مثال بالإنجليزية

```
import "Srl/Console";
import "Srl/Array";
import "Apm";
Apm.importPackage("Alusus/Faiss@0.1");
use Srl;
use Faiss;

// Create a flat index with 4-dimensional vectors
def index: ref[Index];
Index.new(index, 4, "Flat", MetricType.METRIC_INNER_PRODUCT);

// Add vectors to the index
def xb: Array[Float]({1.0, 2.0, 3.0, 4.0, 2.0, 3.0, 4.0, 5.0});
index.add(2, xb.buf);  // 2 vectors

// Search for nearest neighbors
def xq: Array[Float]({1.5, 2.5, 3.5, 4.5});
def labels: array[Int[64], 3];
def distances: array[Float, 3];
index.search(1, xq.buf, 3, distances, labels);  // Find 3 nearest neighbors

// Clean up
Index.free(index);
```

انظر الأمثلة الكاملة في مجلد `Examples/`.

## التوثيق

تلتف هذه المكتبة حول واجهة FAISS البرمجية بلغة C. للحصول على توثيق مفصل حول المفاهيم والخوارزميات وأفضل الممارسات، يرجى الرجوع إلى التوثيق الرسمي لـ FAISS:

* **التوثيق الرئيسي**: https://github.com/facebookresearch/faiss/wiki
* **مرجع واجهة C البرمجية**: https://github.com/facebookresearch/faiss/blob/main/c_api/
* **دليل البدء**: https://github.com/facebookresearch/faiss/wiki/Getting-started
* **دليل اختيار الفهرس**: https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index

## مرجع الواجهة البرمجية

### فـهرس / Index

الصنف الرئيسي للبحث عن التشابه. [توثيق واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الأصناف الأساسية:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(الكائن: سند[سند[فـهرس]]، ب: صـحيح، وصف: مـؤشر_محارف، نوع_القياس: صـحيح): صـحيح
```

</div>

```
func new(obj: ref[ref[Index]], d: Int, description: CharsPtr, metric: Int): Int
```

إنشاء فهرس باستخدام نص المصنع.

#### حمل / load

<div dir=rtl>

```
دالة حمل(اسم_الملف: مـؤشر_محارف، خيارات: صـحيح، الكائن: سند[سند[فـهرس]]): صـحيح
```

</div>

```
func load(fname: CharsPtr, flags: Int, obj: ref[ref[Index]]): Int
```

تحميل فهرس من ملف.

#### احفظ / save

<div dir=rtl>

```
دالة احفظ(الكائن: سند[فـهرس]، اسم_الملف: مـؤشر_محارف): صـحيح
```

</div>

```
func save(obj: ref[Index], fname: CharsPtr): Int
```

حفظ الفهرس إلى ملف.

#### حرر / free

<div dir=rtl>

```
دالة حرر(obj: سند[فـهرس])
```

</div>

```
func free(obj: ref[Index])
```

تحرير ذاكرة الفهرس.

**الدوال الرئيسية:**

#### درب / train

<div dir=rtl>

```
عملية هذا.درب(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]): صـحيح
```

</div>

```
handler this.train(n: Int[64], x: ref[array[Float]]): Int
```

تدريب الفهرس على البيانات.

#### أضف / add

<div dir=rtl>

```
عملية هذا.أضف(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]): صـحيح
```

</div>

```
handler this.add(n: Int[64], x: ref[array[Float]]): Int
```

إضافة متجهات إلى الفهرس.

#### ابحث / search

<div dir=rtl>

```
عملية هذا.ابحث(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، k: صـحيح[64]،
   مسافات: سند[مصفوفة[عـائم]]، labels: سند[مصفوفة[صـحيح[64]]]
 ): صـحيح
```

</div>

```
handler this.search(n: Int[64], x: ref[array[Float]], k: Int[64], distances: ref[array[Float]], labels: ref[array[Int[64]]]): Int
```

البحث عن k من أقرب الجيران.

#### بحث_المدى / rangeSearch

<div dir=rtl>

```
عملية هذا.بحث_المدى(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، radius: عـائم، result: سند[نـتيجة_بحث_مدى]): صـحيح
```

</div>

```
handler this.rangeSearch(n: Int[64], x: ref[array[Float]], radius: Float, result: ref[RangeSearchResult]): Int
```

البحث بنطاق.

#### أعد_الضبط / reset

<div dir=rtl>

```
عملية هذا.أعد_الضبط(): صـحيح
```

</div>

```
handler this.reset(): Int
```

إزالة جميع المتجهات من الفهرس.

#### احذف_المعرفات / removeIds

<div dir=rtl>

```
عملية هذا.احذف_المعرفات(sel: سند[مـنتقي_معرف]، nRemoved: سند[طـبيعي_متكيف]): صـحيح
```

</div>

```
handler this.removeIds(sel: ref[IdSelector], nRemoved: ref[ArchWord]): Int
```

إزالة متجهات محددة.

**الخصائص:**

#### البعد / d

<div dir=rtl>

```
البعد: صحيح[64]
```

</div>

```
d: Int[64]
```

بُعد المتجه.

#### العدد_الكلي / nTotal

<div dir=rtl>

```
العدد_الكلي: صحيح[64]
```

</div>

```
nTotal: Int[64]
```

العدد الإجمالي للمتجهات المفهرسة.

#### مدرب / isTrained

<div dir=rtl>

```
مدرب: صحيح
```

</div>

```
isTrained: Int
```

ما إذا كان الفهرس مدرباً (0 أو 1).

#### نوع_القياس / metricType

<div dir=rtl>

```
نوع_القياس: نـوع_قياس
```

</div>

```
metricType: MetricType
```

مقياس المسافة المستخدم.

#### إطناب / verbose

<div dir=rtl>

```
إطناب: صحيح
```

</div>

```
verbose: Int
```

مستوى الإسهاب.

### فـهرس_مسطح / IndexFlat

فهرس القوة الغاشمة الذي يقوم بالبحث الدقيق. [دليل](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#flat-indexes)

**الإنشاء:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[فـهرس_مسطح]]): صـحيح
دالة أنشئ(obj: سند[سند[فـهرس_مسطح]]، d: صـحيح[64]، metric: نـوع_قياس): صـحيح
```

</div>

```
func new(obj: ref[ref[IndexFlat]]): Int
func new(obj: ref[ref[IndexFlat]], d: Int[64], metric: MetricType): Int
```

**دوال إضافية:**

#### هات_البيانات / getXb

<div dir=rtl>

```
عملية هذا.هات_البيانات(outXb: سند[سند[مصفوفة[عـائم]]]، outSize: سند[طـبيعي_متكيف])
```

</div>

```
handler this.getXb(outXb: ref[ref[array[Float]]], outSize: ref[ArchWord])
```

الحصول على المتجهات المخزنة.

#### احسب_مسافة_مجموعة_جزئية / computeDistanceSubset

<div dir=rtl>

```
عملية هذا.احسب_مسافة_مجموعة_جزئية(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، k: صـحيح[64]، outDistances: سند[مصفوفة[عـائم]]، labels: سند[مصفوفة[صـحيح[64]]]): صـحيح
```

</div>

```
handler this.computeDistanceSubset(n: Int[64], x: ref[array[Float]], k: Int[64], outDistances: ref[array[Float]], labels: ref[array[Int[64]]]): Int
```

حساب المسافات إلى مجموعة جزئية.

يرث جميع دوال فـهرس / Index.

### فـهرس_مسطح_آيبي / IndexFlatIp

فهرس مسطح متخصص لمقياس الجداء الداخلي. [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**الإنشاء:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[فـهرس_مسطح_آيبي]]): صـحيح
دالة أنشئ(obj: سند[سند[فـهرس_مسطح_آيبي]]، d: صـحيح[64]): صـحيح
```

</div>

```
func IndexFlatIp.new(obj: ref[ref[IndexFlatIp]]): Int
func IndexFlatIp.new(obj: ref[ref[IndexFlatIp]], d: Int[64]): Int
```

### فـهرس_مسطح_ل2 / IndexFlatL2

فهرس مسطح متخصص لمسافة L2 (إقليدس). [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**الإنشاء:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[فـهرس_مسطح_ل2]]): صـحيح
دالة أنشئ(obj: سند[سند[فـهرس_مسطح_ل2]]، d: صـحيح[64]): صـحيح
```

</div>

```
func new(obj: ref[ref[IndexFlatL2]]): Int
func new(obj: ref[ref[IndexFlatL2]], d: Int[64]): Int
```

### فـهرس_ملف_معكوس / IndexIvf

فهرس الملفات المعكوسة للبحث التقريبي الأسرع. [دليل](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#cell-probe-methods-indexivf-indexes)

#### عدد_القوائم / nList

<div dir=rtl>

```
عدد_القوائم: طـبيعي_متكيف
```

</div>

عدد القوائم المعكوسة (العناقيد).

#### عدد_الاستقصاءات / nProbe

<div dir=rtl>

```
عدد_الاستقصاءات: طـبيعي_متكيف
```

</div>

عدد العناقيد المراد زيارتها أثناء البحث (قابل للضبط).

#### المكمم / quantizer

<div dir=rtl>

```
المكمم: سند[فـهرس]
```

</div>

فهرس المكمم.

#### يمتلك_الحقول / ownFields

<div dir=rtl>

```
يمتلك_الحقول: صحيح
```

</div>

ما إذا كان الفهرس يمتلك حقوله.

**دوال إضافية:**

#### ادمج_من / mergeFrom

<div dir=rtl>

```
عملية هذا.ادمج_من(other: سند[فـهرس_ملف_معكوس]، addId: صـحيح[64]): صـحيح
```

</div>

```
handler this.mergeFrom(other: ref[IndexIvf], addId: Int[64]): Int
```

دمج فهرس IVF آخر.

#### انسخ_مجموعة_جزئية_إلى / copySubsetTo

<div dir=rtl>

```
عملية هذا.انسخ_مجموعة_جزئية_إلى(other: سند[فـهرس_ملف_معكوس]، subsetType: صـحيح، a1: صـحيح[64]، a2: صـحيح[64]): صـحيح
```

</div>

```
handler this.copySubsetTo(other: ref[IndexIvf], subsetType: Int, a1: Int[64], a2: Int[64]): Int
```

نسخ مجموعة جزئية من المتجهات.

#### هات_حجم_القائمة / getListSize

<div dir=rtl>

```
عملية هذا.هات_حجم_القائمة(listNo: طـبيعي_متكيف): طـبيعي_متكيف
```

</div>

```
handler this.getListSize(listNo: ArchWord): ArchWord
```

الحصول على حجم القائمة المعكوسة.

#### اصنع_تعيينا_مباشرا / makeDirectMap

<div dir=rtl>

```
عملية هذا.اصنع_تعيينا_مباشرا(newMaintainDirectMap: صـحيح): صـحيح
```

</div>

```
handler this.makeDirectMap(newMaintainDirectMap: Int): Int
```

إنشاء خريطة مباشرة لإعادة البناء.

#### عامل_عدم_التوازن / imbalanceFactor

<div dir=rtl>

```
عملية هذا.عامل_عدم_التوازن: عـائم[64]
```

</div>

```
handler this.imbalanceFactor: Float[64]
```

الحصول على عامل عدم توازن العناقيد.

#### اطبع_الإحصائيات / printStats

<div dir=rtl>

```
عملية هذا.اطبع_الإحصائيات()
```

</div>

```
handler this.printStats()
```

طباعة إحصائيات الفهرس.

### فـهرس_ثنائي / IndexBinary

فهرس للمتجهات الثنائية (هامينغ). [دليل](https://github.com/facebookresearch/faiss/wiki/Binary-indexes)

مشابه لـ فـهرس / Index ولكنه يعمل على المتجهات الثنائية (مصفوفات Word[8] بدلاً من Float).

**الأصناف الداعمة**

### فـضاء_وسيط / ParameterSpace

إدارة معاملات الفهرس للبحث الشبكي والضبط. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/ParameterSpace_c.h)

**الدوال:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(parameterSpace: سند[سند[فـضاء_وسيط]]): صـحيح
```

</div>

```
func new(parameterSpace: ref[ref[ParameterSpace]]): Int
```

#### حدد_وسيط_فهرس / setIndexParameter

<div dir=rtl>

```
عملية هذا.حدد_وسيط_فهرس(index: سند[فـهرس]، paramName: مـؤشر_محارف، val: عـائم[64]): صـحيح
```

</div>

```
handler this.setIndexParameter(index: ref[Index], paramName: CharsPtr, val: Float[64]): Int
```

تعيين معامل واحد.

#### حدد_وسطاء_فهرس / setIndexParameters

<div dir=rtl>

```
عملية هذا.حدد_وسطاء_فهرس(index: سند[فـهرس]، params: مـؤشر_محارف): صـحيح
```

</div>

```
handler this.setIndexParameters(index: ref[Index], params: CharsPtr): Int
```

تعيين معاملات متعددة.

#### أضف_مدى / addRange

<div dir=rtl>

```
عملية هذا.أضف_مدى(name: مـؤشر_محارف، outRange: سند[سند[مـدى_وسيط]]): صـحيح
```

</div>

```
handler this.addRange(name: CharsPtr, outRange: ref[ref[ParameterRange]]): Int
```

إضافة نطاق معامل.

### وسـطاء_بحث / SearchParameters

معاملات البحث في وقت التشغيل. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[وسـطاء_بحث]]، sel: سند[مـنتقي_معرف]): صـحيح
```

</div>

```
func new(obj: ref[ref[SearchParameters]], sel: ref[IdSelector]): Int
```

**الخصائص:**

#### عدد_الاستقصاءات / nProbe

<div dir=rtl>

```
عدد_الاستقصاءات: صحيح
```

</div>

عدد العناقيد المراد استقصاءها (لفهارس IVF).

### وسـطاء_بحث_ملف_معكوس / SearchParametersIvf

معاملات بحث موسعة لفهارس IVF.

**الدوال:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[وسـطاء_بحث_ملف_معكوس]]): صـحيح
دالة أنشئ(obj: سند[سند[وسـطاء_بحث_ملف_معكوس]]، sel: سند[مـنتقي_معرف]،nprobe: طـبيعي_متكيف، maxCodes: طـبيعي_متكيف): صـحيح
```

</div>

```
func new(obj: ref[ref[SearchParametersIvf]]): Int
func new(obj: ref[ref[SearchParametersIvf]], sel: ref[IdSelector], nprobe: ArchWord, maxCodes: ArchWord): Int
```

**الخصائص:**

#### المنتقي / sel

<div dir=rtl>

```
المنتقي: سند[مـنتقي_معرف]
```

</div>

منتقي المعرف.

#### عدد_الاستقصاءات / nProbe

<div dir=rtl>

```
عدد_الاستقصاءات: طـبيعي_متكيف
```

</div>

عدد العناقيد المراد استقصاءها.

#### أقصى_شفرات / maxCodes

<div dir=rtl>

```
أقصى_شفرات: طـبيعي_متكيف
```

</div>

الحد الأقصى للشفرات المراد فحصها.

### تـجميع / Clustering

تطبيق تجميع K-means. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Clustering_c.h)

**الإنشاء:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(out: سند[سند[تـجميع]]، d: صـحيح، k: صـحيح): صـحيح
دالة أنشئ(out: سند[سند[تـجميع]]، d: صـحيح، k: صـحيح، params: مؤشر[وسـطاء_تجميع]): صـحيح
```

</div>

```
func new(out: ref[ref[Clustering]], d: Int, k: Int): Int
func new(out: ref[ref[Clustering]], d: Int, k: Int, params: ptr[ClusteringParameters]): Int
```

إنشاء بالبُعد وعدد العناقيد k. الصيغة الثانية تنشئ بمعاملات.

**الدوال:**

#### درب / train

<div dir=rtl>

```
عملية هذا.درب(n: صـحيح[64]، x: سند[عـائم]، index: سند[فـهرس]): صـحيح
```

</div>

```
handler this.train(n: Int[64], x: ref[Float], index: ref[Index]): Int
```

تشغيل k-means.

#### هات_المراكز / getCentroids

<div dir=rtl>

```
عملية هذا.هات_المراكز(centroids: سند[سند[مصفوفة[عـائم]]]، size: سند[طـبيعي_متكيف])
```

</div>

```
handler this.getCentroids(centroids: ref[ref[array[Float]]], size: ref[ArchWord])
```

الحصول على مراكز العناقيد.

#### هات_إحصائيات_الدورة / getIterationStats

<div dir=rtl>

```
عملية هذا.هات_إحصائيات_الدورة(stats_out: سند[سند[إحـصائيات_دورة_تجميع]]، size: سند[طـبيعي_متكيف])
```

</div>

```
handler this.getIterationStats(stats_out: ref[ref[ClusteringIterationStats]], size: ref[ArchWord])
```

الحصول على إحصائيات التكرار.

**الخصائص:**

#### عدد_الدورات / niter

<div dir=rtl>

```
عدد_الدورات: صحيح
```

</div>

عدد التكرارات.

#### عدد_الإعادات / nredo

<div dir=rtl>

```
عدد_الإعادات: صحيح
```

</div>

عدد إعادات k-means.

#### عدد_المراكز / k

<div dir=rtl>

```
عدد_المراكز: طـبيعي_متكيف
```

</div>

عدد العناقيد.

#### البعد / d

<div dir=rtl>

```
البعد: طـبيعي_متكيف
```

</div>

بُعد المتجه.

### مـنتقي_معرف / IdSelector

اختيار مجموعات فرعية من المتجهات حسب المعرف. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الأنواع:**
* `مـنتقي_معرف_حزمة` / `IdSelectorBatch`: اختيار معرفات محددة من قائمة
* `مـنتقي_معرف_مدى` / `IdSelectorRange`: اختيار المعرفات في نطاق
* `مـنتقي_معرف_بتماب` / `IdSelectorBitmap`: الاختيار باستخدام خريطة بت
* `مـنتقي_معرف_نفي` / `IdSelectorNot`: عكس منتقي
* `مـنتقي_معرف_و` / `IdSelectorAnd`: دمج المنتقيات بـ AND
* `مـنتقي_معرف_أو` / `IdSelectorOr`: دمج المنتقيات بـ OR
* `مـنتقي_معرف_أو_حصري` / `IdSelectorXor`: دمج المنتقيات بـ XOR

### نـتيجة_بحث_مدى / RangeSearchResult

نتائج استعلامات البحث بنطاق. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**

#### أنشئ / new

<div dir=rtl>

```
دالة أنشئ(obj: سند[سند[نـتيجة_بحث_مدى]]، nq: صـحيح[64]): صـحيح
```

</div>

```
func new(obj: ref[ref[RangeSearchResult]], nq: Int[64]): Int
```

#### نفذ_التخصيص / doAllocation

<div dir=rtl>

```
عملية هذا.نفذ_التخصيص(): صـحيح
```

</div>

```
handler this.doAllocation(): Int
```

تخصيص صوانات النتائج.

#### حجم_الصوان / bufferSize

<div dir=rtl>

```
عملية هذا.حجم_الصوان(): طـبيعي_متكيف
```

</div>

```
handler this.bufferSize(): ArchWord
```

الحصول على حجم الصوان.

#### هات_الحدود / getLims

<div dir=rtl>

```
عملية هذا.هات_الحدود(outLims: سند[سند[مصفوفة[طـبيعي_متكيف]]])
```

</div>

```
handler this.getLims(outLims: ref[ref[array[ArchWord]]])
```

الحصول على مصفوفة حدود النتائج.

#### هات_الوسوم / getLabels

<div dir=rtl>

```
عملية هذا.هات_الوسوم(outLabels: سند[سند[مصفوفة[صـحيح[64]]]]، outDistances: سند[سند[سند[عـائم]]])
```

</div>

```
handler this.getLabels(outLabels: ref[ref[array[Int[64]]]], outDistances: ref[ref[ref[Float]]])
```

الحصول على الوسوم والمسافات.

### حـاسب_مسافة / DistanceComputer

حساب المسافات إلى المتجهات. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**

#### حدد_الاستعلام / setQuery

<div dir=rtl>

```
عملية هذا.حدد_الاستعلام(x: سند[مصفوفة[عـائم]]): صـحيح
```

</div>

```
handler this.setQuery(x: ref[array[Float]]): Int
```

تعيين متجه الاستعلام.

#### مسافة_متجه_للاستعلام / vectorToQueryDis

<div dir=rtl>

```
عملية هذا.مسافة_متجه_للاستعلام(i: صـحيح[64]، qd: سند[مصفوفة[عـائم]]): صـحيح
```

</div>

```
handler this.vectorToQueryDis(i: Int[64], qd: ref[array[Float]]): Int
```

المسافة إلى الاستعلام.

#### مسافة_متماثلة / symmetricDis

<div dir=rtl>

```
عملية هذا.مسافة_متماثلة(i: صـحيح[64]، j: صـحيح[64]، vd: سند[مصفوفة[عـائم]]): صـحيح
```

</div>

```
handler this.symmetricDis(i: Int[64], j: Int[64], vd: ref[array[Float]]): Int
```

المسافة المتماثلة.

### الثوابت

#### نـوع_قياس / MetricType

مقاييس المسافة. [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

* `_نتاج_داخلي_` / `METRIC_INNER_PRODUCT` (`0`): الجداء الداخلي (أقصى تشابه)
* `_ل2_` / `METRIC_L2` (`1`): المسافة الإقليدية (معيار L2)
* `_ل1_` / `METRIC_L1` (`2`): مسافة مانهاتن (معيار L1)
* `_ل8_` / `METRIC_LINF` (`3`): معيار اللانهاية (مسافة تشيبيشيف)
* `_لس_` / `METRIC_LP` (`4`): معيار Lp
* `_كانبيرا_` / `METRIC_CANBERRA` (`20`): مسافة كانبيرا
* `_براي_كرتس_` / `METRIC_BRAY_CURTIS` (`21`): تباين براي-كورتس
* `_جنسن_شانون_` / `METRIC_JENSEN_SHANNON` (`22`): تباعد جينسن-شانون

#### رمـز_خطأ / ErrorCode

رموز الإرجاع من دوال واجهة C البرمجية.

* `_نجاح_` / `OK` (`0`): نجاح
* `_استثناء_مجهول_` / `UNKNOWN_EXCEPT` (`-1`): استثناء غير معروف
* `_استثناء_فيس_` / `FAISS_EXCEPT` (`-2`): استثناء FAISS
* `_استثناء_قياسي_` / `STD_EXCEPT` (`-4`): استثناء المكتبة القياسية

### الدوال

#### هات_آخر_خطأ / getLastError

<div dir=rtl>

```
دالة هات_آخر_خطأ(): مـؤشر_محارف
```

</div>

```
func getLastError(): CharsPtr
```

الحصول على رسالة الخطأ الأخيرة.

#### تجميع_كيمينز / kmeansClustering

<div dir=rtl>

```
دالة تجميع_كيمينز(d: طـبيعي_متكيف، n: طـبيعي_متكيف، k: طـبيعي_متكيف، x: سند[مصفوفة[عـائم]]، centroids: سند[مصفوفة[عـائم]]، q_error: سند[عـائم]): صـحيح
```

</div>

```
func kmeansClustering(d: ArchWord, n: ArchWord, k: ArchWord, x: ref[array[Float]], centroids: ref[array[Float]], q_error: ref[Float]): Int
```

k-means مستقل.

## دعم GPU

لتفعيل تسريع GPU، قم بتعيين متغير البيئة قبل التشغيل:

```bash
export FAISS_USE_GPU=1
```

ستقوم المكتبة تلقائياً بتحميل الملفات الثنائية المفعّلة لـ GPU عند توفرها. راجع [توثيق FAISS GPU](https://github.com/facebookresearch/faiss/wiki/Faiss-on-the-GPU) للتفاصيل.

## نصوص مصنع الفهرس

تقبل دالة المصنع `فـهرس.أنشئ` / `Index.new` نصوصاً لإنشاء أنواع فهرس مختلفة:

* `"Flat"`: بحث دقيق (قوة غاشمة)
* `"IVFn,Flat"`: IVF مع n مركز، ترميز مسطح
* `"IVFn,PQm"`: IVF مع n مركز، PQ مع m مكمّم فرعي
* `"HNSW32"`: عالم صغير قابل للتنقل الهرمي مع 32 جار
* `"IVFn,HNSW32"`: IVF و HNSW مدمجان

راجع [توثيق مصنع الفهرس](https://github.com/facebookresearch/faiss/wiki/The-index-factory) لجميع الخيارات والتوليفات المتاحة.

## الأمثلة

أمثلة عمل كاملة في مجلد `Examples/`:

* **مثال.أسس**: فهرس مسطح أساسي مع بحث الجداء الداخلي (عربي)
* **مثال٢.أسس**: فهرس IVF مع ضبط المعاملات (عربي)
* **example.alusus**: فهرس مسطح أساسي مع بحث الجداء الداخلي (إنجليزي)
* **example2.alusus**: فهرس IVF مع ضبط المعاملات (إنجليزي)

## نصائح الأداء

1. **اختيار الفهرس**:
   * استخدم `فـهرس_مسطح` / `IndexFlat` للبحث الدقيق في مجموعات البيانات <1 مليون متجه
   * استخدم `فـهرس_ملف_معكوس` / `IndexIVF` للبحث التقريبي في مجموعات البيانات الأكبر
   * راجع [دليل اختيار الفهرس](https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index)

2. **التدريب**: تتطلب فهارس IVF والفهارس التقريبية الأخرى التدريب قبل إضافة المتجهات

3. **معامل nprobe**: بالنسبة لفهارس IVF، nprobe أعلى = دقة أفضل ولكن بحث أبطأ

4. **تسريع GPU**: فعّل GPU للعمليات على >10 مليون متجه

5. **الذاكرة**: تخزّن الفهارس المسطحة جميع المتجهات في الذاكرة؛ استخدم الضغط لمجموعات البيانات الكبيرة

راجع [إرشادات أداء FAISS](https://github.com/facebookresearch/faiss/wiki/Lower-memory-footprint) للتوصيات التفصيلية.

## موارد إضافية

* **FAISS على GitHub**: https://github.com/facebookresearch/faiss
* **ويكي FAISS**: https://github.com/facebookresearch/faiss/wiki
* **ورقة بحثية**: [البحث عن التشابه بمليارات المقاييس مع GPUs](https://arxiv.org/abs/1702.08734)
* **لغة الأسس**: https://alusus.org

## الترخيص

تتبع هذه الروابط ترخيص FAISS (MIT). راجع ملف `LICENSE` للتفاصيل.
