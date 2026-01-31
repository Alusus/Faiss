<div dir=rtl>

# فـيس Faiss
[[English]](readme.md)

روابط لغة الأسس لمكتبة [FAISS](https://github.com/facebookresearch/faiss) - مكتبة للبحث الفعّال عن التشابه وتجميع المتجهات الكثيفة.

## نظرة عامة

توفر هذه المكتبة روابط لغة الأسس لمكتبة FAISS، مما يتيح عمليات البحث عن التشابه في المتجهات والتجميع عالية الأداء في لغة الأسس.

## التثبيت

```alusus
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Faiss"، "فـيس.أسس")؛
استخدم فـيس؛
```

أو بالإنجليزية:

<div dir=ltr>

```alusus
import "Apm";
Apm.importFile("Alusus/Faiss");
use Faiss;
```

</div>

## البدء السريع

### مثال بالعربية

```alusus
اشمل "مـتم/طـرفية"؛
اشمل "مـتم/مـصفوفة"؛
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Faiss"، "فـيس.أسس")؛
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

### مثال بالإنجليزية

<div dir=ltr>

```alusus
import "Srl/Console";
import "Srl/Array";
import "Apm";
Apm.importFile("Alusus/Faiss");
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

</div>

انظر الأمثلة الكاملة في مجلد `Examples/`.

## التوثيق

تلتف هذه المكتبة حول واجهة FAISS البرمجية بلغة C. للحصول على توثيق مفصل حول المفاهيم والخوارزميات وأفضل الممارسات، يرجى الرجوع إلى التوثيق الرسمي لـ FAISS:

- **التوثيق الرئيسي**: https://github.com/facebookresearch/faiss/wiki
- **مرجع واجهة C البرمجية**: https://github.com/facebookresearch/faiss/blob/main/c_api/
- **دليل البدء**: https://github.com/facebookresearch/faiss/wiki/Getting-started
- **دليل اختيار الفهرس**: https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index

## مرجع الواجهة البرمجية

### الأصناف الأساسية

#### فـهرس / Index
الصنف الرئيسي للبحث عن التشابه. [توثيق واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**دالة المصنع:**
- `أنشئ` / `new`
  ```alusus
  فـهرس.أنشئ(الكائن: سند[سند[فـهرس]]، ب: صـحيح، وصف: مـؤشر_محارف، نوع_القياس: صـحيح): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Index.new(obj: ref[ref[Index]]، d: Int، وصف: CharsPtr، metric: Int): Int
  ```
  
</div>

  إنشاء فهرس باستخدام نص المصنع

**الدوال الرئيسية:**
- `درب` / `train`
  ```alusus
  فـهرس.درب(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]): صـحيح
  ```
  
<div dir=ltr>

  ```alusus
  Index.train(n: Int[64]، x: ref[array[Float]]): Int
  ```

</div>

  تدريب الفهرس على البيانات

- `أضف` / `add`
  ```alusus
  فـهرس.أضف(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]): صـحيح
  ```
 
<div dir=ltr>

  ```alusus
  Index.add(n: Int[64]، x: ref[array[Float]]): Int
  ```

</div>

  إضافة متجهات إلى الفهرس

- `ابحث` / `search`
  ```alusus
  فـهرس.ابحث(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، k: صـحيح[64]،
     مسافات: سند[مصفوفة[عـائم]]، labels: سند[مصفوفة[صـحيح[64]]]
   ): صـحيح
  ```
  
<div dir=ltr>

  ```alusus
  Index.search(n: Int[64]، x: ref[array[Float]]، k: Int[64]،
     distances: ref[array[Float]]، labels: ref[array[Int[64]]]
   ): Int
  ```

</div>

  البحث عن k من أقرب الجيران

- `بحث_المدى` / `rangeSearch`
  ```alusus
  فـهرس.بحث_المدى(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، radius: عـائم،
   result: سند[نـتيجة_بحث_مدى]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Index.rangeSearch(n: Int[64], x: ref[array[Float]], radius: Float,
   result: ref[RangeSearchResult]): Int
  ```

</div>

  البحث بنطاق

- `أعد_الضبط` / `reset`
  ```alusus
  فـهرس.أعد_الضبط(): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Index.reset(): Int
  ```

</div>

  إزالة جميع المتجهات من الفهرس

- `احذف_المعرفات` / `removeIds`
  ```alusus
  فـهرس.احذف_المعرفات(sel: سند[مـنتقي_معرف]، nRemoved: سند[كلمة_معمارية]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Index.removeIds(sel: ref[IdSelector], nRemoved: ref[ArchWord]): Int
  ```

</div>

  إزالة متجهات محددة

**الخصائص:**
- `البعد` / `d`: `صحيح[64]` - بُعد المتجه
- `العدد_الكلي` / `nTotal`: `صحيح[64]` - العدد الإجمالي للمتجهات المفهرسة
- `مدرب` / `isTrained`: `صحيح` - ما إذا كان الفهرس مدرباً (0 أو 1)
- `نوع_القياس` / `metricType`: `نـوع_قياس` - مقياس المسافة المستخدم
- `إطناب` / `verbose`: `صحيح` - مستوى الإسهاب

**التنظيف:**
- `حرر` / `free`
  ```alusus
  فـهرس.حرر(obj: سند[فـهرس])
  ```

<div dir=ltr>

  ```alusus
  Index.free(obj: ref[Index])
  ```

</div>

  تحرير ذاكرة الفهرس

#### فـهرس_مسطح / IndexFlat
فهرس القوة الغاشمة الذي يقوم بالبحث الدقيق. [دليل](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#flat-indexes)

**الإنشاء:**
- `أنشئ` / `new`
  ```alusus
  فـهرس_مسطح.أنشئ(obj: سند[سند[فـهرس_مسطح]]): صـحيح
  فـهرس_مسطح.أنشئ(obj: سند[سند[فـهرس_مسطح]]، d: صـحيح[64]، metric: نـوع_قياس): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexFlat.new(obj: ref[ref[IndexFlat]]): Int
  IndexFlat.new(obj: ref[ref[IndexFlat]], d: Int[64], metric: MetricType): Int
  ```

</div>

**دوال إضافية:**
- `هات_البيانات` / `getXb`
  ```alusus
  فـهرس_مسطح.هات_البيانات(outXb: سند[سند[مصفوفة[عـائم]]]، outSize: سند[كلمة_معمارية])
  ```

<div dir=ltr>

  ```alusus
  IndexFlat.getXb(outXb: ref[ref[array[Float]]], outSize: ref[ArchWord])
  ```

</div>

  الحصول على المتجهات المخزنة

- `احسب_مسافة_مجموعة_جزئية` / `computeDistanceSubset`
  ```alusus
  فـهرس_مسطح.احسب_مسافة_مجموعة_جزئية(n: صـحيح[64]، x: سند[مصفوفة[عـائم]]، k: صـحيح[64]،
   outDistances: سند[مصفوفة[عـائم]]، labels: سند[مصفوفة[صـحيح[64]]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexFlat.computeDistanceSubset(n: Int[64], x: ref[array[Float]], k: Int[64],
   outDistances: ref[array[Float]], labels: ref[array[Int[64]]]): Int
  ```

</div>

  حساب المسافات إلى مجموعة جزئية

يرث جميع دوال فـهرس / Index.

#### فـهرس_مسطح_آيبي / IndexFlatIp
فهرس مسطح متخصص لمقياس الجداء الداخلي. [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**الإنشاء:**
- `أنشئ` / `new`
  ```alusus
  فـهرس_مسطح_آيبي.أنشئ(obj: سند[سند[فـهرس_مسطح_آيبي]]): صـحيح
  فـهرس_مسطح_آيبي.أنشئ(obj: سند[سند[فـهرس_مسطح_آيبي]]، d: صـحيح[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexFlatIp.new(obj: ref[ref[IndexFlatIp]]): Int
  IndexFlatIp.new(obj: ref[ref[IndexFlatIp]], d: Int[64]): Int
  ```

</div>

#### فـهرس_مسطح_ل2 / IndexFlatL2
فهرس مسطح متخصص لمسافة L2 (إقليدس). [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

**الإنشاء:**
- `أنشئ` / `new`
  ```alusus
  فـهرس_مسطح_ل2.أنشئ(obj: سند[سند[فـهرس_مسطح_ل2]]): صـحيح
  فـهرس_مسطح_ل2.أنشئ(obj: سند[سند[فـهرس_مسطح_ل2]]، d: صـحيح[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexFlatL2.new(obj: ref[ref[IndexFlatL2]]): Int
  IndexFlatL2.new(obj: ref[ref[IndexFlatL2]], d: Int[64]): Int
  ```

</div>

#### فـهرس_ملف_معكوس / IndexIvf
فهرس الملفات المعكوسة للبحث التقريبي الأسرع. [دليل](https://github.com/facebookresearch/faiss/wiki/Faiss-indexes#cell-probe-methods-indexivf-indexes)

**خصائص إضافية:**
- `عدد_القوائم` / `nList`: `كلمة_معمارية` - عدد القوائم المعكوسة (العناقيد)
- `عدد_الاستقصاءات` / `nProbe`: `كلمة_معمارية` - عدد العناقيد المراد زيارتها أثناء البحث (قابل للضبط)
- `المكمم` / `quantizer`: `سند[فـهرس]` - فهرس المكمم
- `يمتلك_الحقول` / `ownFields`: `صحيح` - ما إذا كان الفهرس يمتلك حقوله

**دوال إضافية:**
- `ادمج_من` / `mergeFrom`
  ```alusus
  فـهرس_ملف_معكوس.ادمج_من(other: سند[فـهرس_ملف_معكوس]، addId: صـحيح[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexIvf.mergeFrom(other: ref[IndexIvf], addId: Int[64]): Int
  ```

</div>

  دمج فهرس IVF آخر

- `انسخ_مجموعة_جزئية_إلى` / `copySubsetTo`
  ```alusus
  فـهرس_ملف_معكوس.انسخ_مجموعة_جزئية_إلى(other: سند[فـهرس_ملف_معكوس]، subsetType: صـحيح، a1: صـحيح[64]، a2: صـحيح[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexIvf.copySubsetTo(other: ref[IndexIvf], subsetType: Int, a1: Int[64], a2: Int[64]): Int
  ```

</div>

  نسخ مجموعة جزئية من المتجهات

- `هات_حجم_القائمة` / `getListSize`
  ```alusus
  فـهرس_ملف_معكوس.هات_حجم_القائمة(listNo: كلمة_معمارية): كلمة_معمارية
  ```

<div dir=ltr>

  ```alusus
  IndexIvf.getListSize(listNo: ArchWord): ArchWord
  ```

</div>

  الحصول على حجم القائمة المعكوسة

- `اصنع_تعيينا_مباشرا` / `makeDirectMap`
  ```alusus
  فـهرس_ملف_معكوس.اصنع_تعيينا_مباشرا(newMaintainDirectMap: صـحيح): صـحيح
  ```

<div dir=ltr>

  ```alusus
  IndexIvf.makeDirectMap(newMaintainDirectMap: Int): Int
  ```

</div>

  إنشاء خريطة مباشرة لإعادة البناء

- `عامل_عدم_التوازن` / `imbalanceFactor`: `عـائم[64]` - الحصول على عامل عدم توازن العناقيد
- `اطبع_الإحصائيات` / `printStats`: `()` - طباعة إحصائيات الفهرس

#### فـهرس_ثنائي / IndexBinary
فهرس للمتجهات الثنائية (هامينغ). [دليل](https://github.com/facebookresearch/faiss/wiki/Binary-indexes)

مشابه لـ فـهرس / Index ولكنه يعمل على المتجهات الثنائية (مصفوفات Word[8] بدلاً من Float).

### الأصناف الداعمة

#### فـضاء_وسيط / ParameterSpace
إدارة معاملات الفهرس للبحث الشبكي والضبط. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/ParameterSpace_c.h)

**الدوال:**
- `أنشئ` / `new`
  ```alusus
  فـضاء_وسيط.أنشئ(parameterSpace: سند[سند[فـضاء_وسيط]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  ParameterSpace.new(parameterSpace: ref[ref[ParameterSpace]]): Int
  ```

</div>

- `حدد_وسيط_فهرس` / `setIndexParameter`
  ```alusus
  فـضاء_وسيط.حدد_وسيط_فهرس(index: سند[فـهرس]، paramName: مـؤشر_محارف، val: عـائم[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  ParameterSpace.setIndexParameter(index: ref[Index], paramName: CharsPtr, val: Float[64]): Int
  ```

</div>

  تعيين معامل واحد

- `حدد_وسطاء_فهرس` / `setIndexParameters`
  ```alusus
  فـضاء_وسيط.حدد_وسطاء_فهرس(index: سند[فـهرس]، params: مـؤشر_محارف): صـحيح
  ```

<div dir=ltr>

  ```alusus
  ParameterSpace.setIndexParameters(index: ref[Index], params: CharsPtr): Int
  ```

</div>

  تعيين معاملات متعددة

- `أضف_مدى` / `addRange`
  ```alusus
  فـضاء_وسيط.أضف_مدى(name: مـؤشر_محارف، outRange: سند[سند[مـدى_وسيط]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  ParameterSpace.addRange(name: CharsPtr, outRange: ref[ref[ParameterRange]]): Int
  ```

</div>

  إضافة نطاق معامل

#### وسـطاء_بحث / SearchParameters
معاملات البحث في وقت التشغيل. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**
- `أنشئ` / `new`
  ```alusus
  وسـطاء_بحث.أنشئ(obj: سند[سند[وسـطاء_بحث]]، sel: سند[مـنتقي_معرف]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  SearchParameters.new(obj: ref[ref[SearchParameters]], sel: ref[IdSelector]): Int
  ```

</div>

- `عدد_الاستقصاءات` / `nProbe`: `صحيح` - عدد العناقيد المراد استقصاءها (لفهارس IVF)

#### وسـطاء_بحث_ملف_معكوس / SearchParametersIvf
معاملات بحث موسعة لفهارس IVF.

**الدوال:**
- `أنشئ` / `new`
  ```alusus
  وسـطاء_بحث_ملف_معكوس.أنشئ(obj: سند[سند[وسـطاء_بحث_ملف_معكوس]]): صـحيح
  وسـطاء_بحث_ملف_معكوس.أنشئ(obj: سند[سند[وسـطاء_بحث_ملف_معكوس]]، sel: سند[مـنتقي_معرف]،
   nprobe: كلمة_معمارية، maxCodes: كلمة_معمارية): صـحيح
  ```

<div dir=ltr>

  ```alusus
  SearchParametersIvf.new(obj: ref[ref[SearchParametersIvf]]): Int
  SearchParametersIvf.new(obj: ref[ref[SearchParametersIvf]], sel: ref[IdSelector],
   nprobe: ArchWord, maxCodes: ArchWord): Int
  ```

</div>

**الخصائص:**
- `المنتقي` / `sel`: `سند[مـنتقي_معرف]` - منتقي المعرف
- `عدد_الاستقصاءات` / `nProbe`: `كلمة_معمارية` - عدد العناقيد المراد استقصاءها
- `أقصى_شفرات` / `maxCodes`: `كلمة_معمارية` - الحد الأقصى للشفرات المراد فحصها

#### تـجميع / Clustering
تطبيق تجميع K-means. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Clustering_c.h)

**الإنشاء:**
- `أنشئ` / `new`
  ```alusus
  تـجميع.أنشئ(out: سند[سند[تـجميع]]، d: صـحيح، k: صـحيح): صـحيح
  تـجميع.أنشئ(out: سند[سند[تـجميع]]، d: صـحيح، k: صـحيح، params: مؤشر[وسـطاء_تجميع]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Clustering.new(out: ref[ref[Clustering]], d: Int, k: Int): Int
  Clustering.new(out: ref[ref[Clustering]], d: Int, k: Int, params: ptr[ClusteringParameters]): Int
  ```

</div>

**الدوال:**
- `درب` / `train`
  ```alusus
  تـجميع.درب(n: صـحيح[64]، x: سند[عـائم]، index: سند[فـهرس]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Clustering.train(n: Int[64], x: ref[Float], index: ref[Index]): Int
  ```

</div>

  تشغيل k-means

- `هات_المراكز` / `getCentroids`
  ```alusus
  تـجميع.هات_المراكز(centroids: سند[سند[مصفوفة[عـائم]]]، size: سند[كلمة_معمارية])
  ```

<div dir=ltr>

  ```alusus
  Clustering.getCentroids(centroids: ref[ref[array[Float]]], size: ref[ArchWord])
  ```

</div>

  الحصول على مراكز العناقيد

- `هات_إحصائيات_الدورة` / `getIterationStats`
  ```alusus
  تـجميع.هات_إحصائيات_الدورة(stats_out: سند[سند[إحـصائيات_دورة_تجميع]]، size: سند[كلمة_معمارية])
  ```

<div dir=ltr>

  ```alusus
  Clustering.getIterationStats(stats_out: ref[ref[ClusteringIterationStats]], size: ref[ArchWord])
  ```

</div>

  الحصول على إحصائيات التكرار

**الخصائص:**
- `عدد_الدورات` / `niter`: `صحيح` - عدد التكرارات
- `عدد_الإعادات` / `nredo`: `صحيح` - عدد إعادات k-means
- `عدد_المراكز` / `k`: `كلمة_معمارية` - عدد العناقيد
- `البعد` / `d`: `كلمة_معمارية` - بُعد المتجه

#### مـنتقي_معرف / IdSelector
اختيار مجموعات فرعية من المتجهات حسب المعرف. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الأنواع:**
- `مـنتقي_معرف_حزمة` / `IdSelectorBatch` - اختيار معرفات محددة من قائمة
- `مـنتقي_معرف_مدى` / `IdSelectorRange` - اختيار المعرفات في نطاق
- `مـنتقي_معرف_بتماب` / `IdSelectorBitmap` - الاختيار باستخدام خريطة بت
- `مـنتقي_معرف_نفي` / `IdSelectorNot` - عكس منتقي
- `مـنتقي_معرف_و` / `IdSelectorAnd` - دمج المنتقيات بـ AND
- `مـنتقي_معرف_أو` / `IdSelectorOr` - دمج المنتقيات بـ OR
- `مـنتقي_معرف_أو_حصري` / `IdSelectorXor` - دمج المنتقيات بـ XOR

#### نـتيجة_بحث_مدى / RangeSearchResult
نتائج استعلامات البحث بنطاق. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**
- `أنشئ` / `new`
  ```alusus
  نـتيجة_بحث_مدى.أنشئ(obj: سند[سند[نـتيجة_بحث_مدى]]، nq: صـحيح[64]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  RangeSearchResult.new(obj: ref[ref[RangeSearchResult]], nq: Int[64]): Int
  ```

</div>

- `نفذ_التخصيص` / `doAllocation`
  ```alusus
  نـتيجة_بحث_مدى.نفذ_التخصيص(): صـحيح
  ```

<div dir=ltr>

  ```alusus
  RangeSearchResult.doAllocation(): Int
  ```

</div>

  تخصيص صوانات النتائج

- `حجم_الصوان` / `bufferSize`
  ```alusus
  نـتيجة_بحث_مدى.حجم_الصوان(): كلمة_معمارية
  ```

<div dir=ltr>

  ```alusus
  RangeSearchResult.bufferSize(): ArchWord
  ```

</div>

  الحصول على حجم الصوان

- `هات_الحدود` / `getLims`
  ```alusus
  نـتيجة_بحث_مدى.هات_الحدود(outLims: سند[سند[مصفوفة[كلمة_معمارية]]])
  ```

<div dir=ltr>

  ```alusus
  RangeSearchResult.getLims(outLims: ref[ref[array[ArchWord]]])
  ```

</div>

  الحصول على مصفوفة حدود النتائج

- `هات_الوسوم` / `getLabels`
  ```alusus
  نـتيجة_بحث_مدى.هات_الوسوم(outLabels: سند[سند[مصفوفة[صـحيح[64]]]]، outDistances: سند[سند[سند[عـائم]]])
  ```

<div dir=ltr>

  ```alusus
  RangeSearchResult.getLabels(outLabels: ref[ref[array[Int[64]]]], outDistances: ref[ref[ref[Float]]])
  ```

</div>

  الحصول على الوسوم والمسافات

#### حـاسب_مسافة / DistanceComputer
حساب المسافات إلى المتجهات. [واجهة C البرمجية](https://github.com/facebookresearch/faiss/blob/main/c_api/Index_c.h)

**الدوال:**
- `حدد_الاستعلام` / `setQuery`
  ```alusus
  حـاسب_مسافة.حدد_الاستعلام(x: سند[مصفوفة[عـائم]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  DistanceComputer.setQuery(x: ref[array[Float]]): Int
  ```

</div>

  تعيين متجه الاستعلام

- `مسافة_متجه_للاستعلام` / `vectorToQueryDis`
  ```alusus
  حـاسب_مسافة.مسافة_متجه_للاستعلام(i: صـحيح[64]، qd: سند[مصفوفة[عـائم]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  DistanceComputer.vectorToQueryDis(i: Int[64], qd: ref[array[Float]]): Int
  ```

</div>

  المسافة إلى الاستعلام

- `مسافة_متماثلة` / `symmetricDis`
  ```alusus
  حـاسب_مسافة.مسافة_متماثلة(i: صـحيح[64]، j: صـحيح[64]، vd: سند[مصفوفة[عـائم]]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  DistanceComputer.symmetricDis(i: Int[64], j: Int[64], vd: ref[array[Float]]): Int
  ```

</div>

  المسافة المتماثلة

### الثوابت

#### نـوع_قياس / MetricType
مقاييس المسافة. [توثيق](https://github.com/facebookresearch/faiss/wiki/MetricType-and-distances)

- `_نتاج_داخلي_` / `METRIC_INNER_PRODUCT`: `0` - الجداء الداخلي (أقصى تشابه)
- `_ل2_` / `METRIC_L2`: `1` - المسافة الإقليدية (معيار L2)
- `_ل1_` / `METRIC_L1`: `2` - مسافة مانهاتن (معيار L1)
- `_ل8_` / `METRIC_LINF`: `3` - معيار اللانهاية (مسافة تشيبيشيف)
- `_لس_` / `METRIC_LP`: `4` - معيار Lp
- `_كانبيرا_` / `METRIC_CANBERRA`: `20` - مسافة كانبيرا
- `_براي_كرتس_` / `METRIC_BRAY_CURTIS`: `21` - تباين براي-كورتس
- `_جنسن_شانون_` / `METRIC_JENSEN_SHANNON`: `22` - تباعد جينسن-شانون

#### رمـز_خطأ / ErrorCode
رموز الإرجاع من دوال واجهة C البرمجية.

- `_نجاح_` / `OK`: `0` - نجاح
- `_استثناء_مجهول_` / `UNKNOWN_EXCEPT`: `-1` - استثناء غير معروف
- `_استثناء_فيس_` / `FAISS_EXCEPT`: `-2` - استثناء FAISS
- `_استثناء_قياسي_` / `STD_EXCEPT`: `-4` - استثناء المكتبة القياسية

### الدوال

- `هات_آخر_خطأ` / `getLastError`
  ```alusus
  فـيس.هات_آخر_خطأ(): مـؤشر_محارف
  ```

<div dir=ltr>

  ```alusus
  Faiss.getLastError(): CharsPtr
  ```

</div>

  الحصول على رسالة الخطأ الأخيرة

- `تجميع_كيمينز` / `kmeansClustering`
  ```alusus
  فـيس.تجميع_كيمينز(d: كلمة_معمارية، n: كلمة_معمارية، k: كلمة_معمارية،
   x: سند[مصفوفة[عـائم]]، centroids: سند[مصفوفة[عـائم]]، q_error: سند[عـائم]): صـحيح
  ```

<div dir=ltr>

  ```alusus
  Faiss.kmeansClustering(d: ArchWord, n: ArchWord, k: ArchWord,
   x: ref[array[Float]], centroids: ref[array[Float]], q_error: ref[Float]): Int
  ```

</div>

  k-means مستقل

## دعم GPU

لتفعيل تسريع GPU، قم بتعيين متغير البيئة قبل التشغيل:
```bash
export FAISS_USE_GPU=1
```

ستقوم المكتبة تلقائياً بتحميل الملفات الثنائية المفعّلة لـ GPU عند توفرها. راجع [توثيق FAISS GPU](https://github.com/facebookresearch/faiss/wiki/Faiss-on-the-GPU) للتفاصيل.

## نصوص مصنع الفهرس

تقبل دالة المصنع `أنشئ` / `new` نصوصاً لإنشاء أنواع فهرس مختلفة:

- `"Flat"` - بحث دقيق (قوة غاشمة)
- `"IVFn,Flat"` - IVF مع n مركز، ترميز مسطح
- `"IVFn,PQm"` - IVF مع n مركز، PQ مع m مكمّم فرعي
- `"HNSW32"` - عالم صغير قابل للتنقل الهرمي مع 32 جار
- `"IVFn,HNSW32"` - IVF و HNSW مدمجان

راجع [توثيق مصنع الفهرس](https://github.com/facebookresearch/faiss/wiki/The-index-factory) لجميع الخيارات والتوليفات المتاحة.

## الأمثلة

أمثلة عمل كاملة في مجلد `Examples/`:

- **مثال.أسس** - فهرس مسطح أساسي مع بحث الجداء الداخلي (عربي)
- **مثال٢.أسس** - فهرس IVF مع ضبط المعاملات (عربي)
- **example.alusus** - فهرس مسطح أساسي مع بحث الجداء الداخلي (إنجليزي)
- **example2.alusus** - فهرس IVF مع ضبط المعاملات (إنجليزي)

## نصائح الأداء

1. **اختيار الفهرس**:
   - استخدم `فـهرس_مسطح` / `IndexFlat` للبحث الدقيق في مجموعات البيانات <1 مليون متجه
   - استخدم `فـهرس_ملف_معكوس` / `IndexIVF` للبحث التقريبي في مجموعات البيانات الأكبر
   - راجع [دليل اختيار الفهرس](https://github.com/facebookresearch/faiss/wiki/Guidelines-to-choose-an-index)

2. **التدريب**: تتطلب فهارس IVF والفهارس التقريبية الأخرى التدريب قبل إضافة المتجهات

3. **معامل nprobe**: بالنسبة لفهارس IVF، nprobe أعلى = دقة أفضل ولكن بحث أبطأ

4. **تسريع GPU**: فعّل GPU للعمليات على >10 مليون متجه

5. **الذاكرة**: تخزّن الفهارس المسطحة جميع المتجهات في الذاكرة؛ استخدم الضغط لمجموعات البيانات الكبيرة

راجع [إرشادات أداء FAISS](https://github.com/facebookresearch/faiss/wiki/Lower-memory-footprint) للتوصيات التفصيلية.

## موارد إضافية

- **FAISS على GitHub**: https://github.com/facebookresearch/faiss
- **ويكي FAISS**: https://github.com/facebookresearch/faiss/wiki
- **ورقة بحثية**: [البحث عن التشابه بمليارات المقاييس مع GPUs](https://arxiv.org/abs/1702.08734)
- **لغة الأسس**: https://alusus.org

## الترخيص

تتبع هذه الروابط ترخيص FAISS (MIT). راجع ملف `LICENSE` للتفاصيل.

</div>

