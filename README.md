
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/PersianSwift.svg)](https://img.shields.io/cocoapods/v/PersianSwift.svg)
[![Platform](https://img.shields.io/cocoapods/p/PersianSwift.svg?style=flat)](http://cocoadocs.org/docsets/PersianSwift)


<h1 dir='rtl'>پارسی‌سوییفت</h1>

<p dir="rtl">
کتابخانه PersianSwift یک کتابخانه نوشته شده برای زبان برنامه‌نویسی Swift هستش که استفاده از این زبان برنامه‌نویسی رو برای زبان فارسی راحت‌تر و شیرین‌تر می‌کنه.
</p>

<p dir="rtl">
برای راحتی بیشتر موقع استفاده، بیشتر امکانات این کتابخونه از طریق Extensionهای تعریف شده برای انواع داده در Swift در دسترس هست.
</p>

<p dir="rtl">
مثلا با استفاده از ابزار زیر، مقدار عددی 12345 به مقدار متنی متناظر باهاش و همراه با اعداد فارسی در دسترس هست:
</p>

```swift
let int = 12345
let persianString = int.ps.stringWithPersianDigits // ۱۲۳۴۵
```

## <p dir="rtl">نحوه نصب</p>

<p dir="rtl">
با استفاده از 
<a href="http://cocoapods.org">CocoaPod</a>
 خیلی راحت می‌تونین این کتابخونه رو به پروژه خودتون اضافه‌اش کنین.
</p>

```bash
pod 'PersianSwift', '~> 1.5' // Swift 3.0
pod 'PersianSwift', '~> 1.7' // Swift 4.0
```

<p dir="rtl">
بعد از نصب می‌تونین هرجایی که خواستین اون رو `import` کنین و از امکاناتش استفاده کنین.
</p>

```swift
import PersianSwift
```

<p dir="rtl">
در ادامه توضیحات مفصل قسمت‌های پیاده‌سازی شده رو نشون میدیم.
</p>

---
<h2 dir='rtl'>استفاده از دستورات آماده شده</h2>

<h3 dir='rtl'>متون یا همون <code>String</code></h3>

<p dir="rtl">
  <ul dir="rtl"><li>چک کردن اینکه متن مورد نظر شماره تلفن موبایل باشه</li></ul>
</p>

```swift
String.ps.isPersianPhoneNumber -> Bool
```

<p dir="rtl">
  <ul dir="rtl"><li>تبدیل شده متن موجود، بهمراه تبدیل اعداد از به فارسی و یا لاتین</li></ul>
</p>

```swift
String.ps.withPersianDigits -> String
String.ps.withEasternDigits -> String

String.ps.toPersianDigits() -> Void
String.ps.toEnglishDigits() -> Void
```

<p dir="rtl">
  <ul dir="rtl"><li>تبدیل کاراکترهای خاص در متن فارسی (حروف ک عربی و ی عربی)</li></ul>
</p>

```swift
String.ps.withFixedPersianCharacters -> String
String.ps.fixPersianCharacters() -> Void
```

<p dir="rtl">
  <ul dir="rtl"><li>
    تبدیل شده متن موجود، بهمراه ظاهر قیمت
    <p>اگه متن ما ساختار عددی مثل "12345" نداشته باشه، خروجی nil میشه.</p>
  </li></ul>
</p>


```swift
String.ps.withIranRialStyle -> String?
String.ps.withIranTomanStyle -> String?
String.ps.withCurrencyStyle -> String?
```

<p dir="rtl">
  <ul dir="rtl"><li>
    تبدیل متن با ساختار تاریخ، به تاریخ شمسی متناظر با اون
    <p>
    اگه متن ما ساختار تاریخ مثل "2017-06-03 17:23:41" رو نداشته باشه، خروجی `nil` میشه. البته فرمت ورودی رو میتونین موقع استفاده از این متد تنظیم کنین.
    </p>
  </li></ul>
</p>


```swift
String.ps.asPersianDate(fromGregorianFormat: String) -> String?
```

---

<h3 dir="rtl">اعداد مثل <code>Int Double Float</code></h3>

<p dir="rtl">
برای این نوع داده‌ها، اول یه <code>protocol</code> به اسم <code>Numeric</code> تعریف شده و بعد نوع‌های <code>Int, Double, Float</code> این پروتکل رو استفاده کردن.
</p>

```swift
public protocol Numeric {}

extension Int    : Numeric {}
extension Double : Numeric {}
extension Float  : Numeric {}
```

<p dir="rtl">
بعد به اون پروتکل تعریف شده، موارد زیر اضافه شدن.
</p>

<p dir="rtl">
  <ul dir="rtl"><li>دریافت عدد بصورت متن</li></ul>
</p>


```swift
Numeric.ps.string -> String
```


<p dir="rtl">
  <ul dir="rtl"><li>دریافت عدد بصورت متن بهمراه اعداد فارسی</li></ul>
</p>

```swift
Numeric.ps.stringWithPersianDigits -> String
```

<p dir="rtl">
  <ul dir="rtl"><li>دریافت عدد بصورت متن و با ظاهر قیمت</li></ul>
</p>

```swift
Numeric.ps.stringWithCurrencyStyle -> String
```

---

<h3 dir="rtl">موارد مربوط به تاریخ یا همون Date</h3>

<p dir="rtl">
با استفاده از موارد آماده شده، میتونین خیلی راحت یه تاریخ رو به شمسی تبدیل کنین. به عنوان مثال با استفاده از `timeinterval` دریافتی از وب‌سرویس، یه تاریخ بسازین. و بعد خیلی راحت اون رو به تاریخ شمسی تبدیل کنین.
</p>

<p dir="rtl">
نام موارد آماده شده و نمونه خروجی‌شون توی مثال زیر آورده شده:
</p>

```swift
let date = Date(timeIntervalSince1970: TimeInterval(exactly: 629152200)!)
_ = date.ps.asPersianDate // شنبه ۱۸ آذر ۱۳۶۸
_ = date.ps.asFullPersianDateTime // شنبه ۱۸ آذر ماه ۱۳۶۸ ساعت ۱۲:۰۰:۰۰ قبل از ظهر
```

---

<h2 dir="rtl">آرایه‌ها</h2>

<h3 dir="rtl">آرایه‌های متنی یا همون [String]</h3>

<p dir="rtl">
  <ul dir="rtl">
    <li>
      به ترتیب کردن آرایه‌ای از Stringها و دریافت خروجی
      <p>
      این دستور روی آرایه‌ای از String اعمال میشه و اون رو بطور صعودی به ترتیب میکنه و بعنوان خروجی برمیگردونه.
      </p>
    </li>
  </ul>
</p>


```swift
[String].ps.sortedPersianStrings
```

<p dir="rtl">
  <ul dir="rtl">
    <li>
      به ترتیب کردن درجای آرایه‌ای از Stringها
      <p>
      این دستور هم روی آرایه‌ای از String اعمال میشه و خود اون آرایه رو درجا به ترتیب میکنه. موقع استفاده از این دستور میتونین صعودی یا نزولی بودن ترتیب رو انتخاب کنین.
      </p>
    </li>
  </ul>
</p>


```swift
[String].ps.sortPersianStrings(desc: Bool)
```

---

<h2 dir='rtl'>همکاری</h2>

<p dir="rtl">
هرگونه همکاری و همفکری به شدت و با آغوش باز پذیرفته میشه. پس بیاین همدیگه رو در آغوش بگیریم!!! 😆😂😋
</p>





