## ۱
استفاده از چندریختی به جای شرط
در بخش Address یک enum داریم که مشخص میکند چه نوع آدرسدهی باید انجام شود. همچنین هنگامی که میخواهیم آدرس را چاپ کنیم یک شرط داریم که به ازای هر مورد در enum یک چیزی را چاپ میکند. با استفاده از چندریختی میتوانیم به ازای هر نوع یک کلاس بسازیم که همگی از یک اینترفیس تبعیت میکنند. پس از آن در هر کدام از کلاس‌ها، نحوه چاپ آن کلاس را مشخص میکنیم. تکه کدهای زیر مربوط به هریک از کلاس‌ها هستند.  
```java
public interface TypeAddress {
    public String toString(int num);
}
```

```java
public class IndirectAccess extends TypeAddress {


    public String toString(int num){
        return "@" + num;
    }
}

public class ImidiateAddress extends TypeAddress {

    public String toString(int num){
        return "#" + num;
    }

}
public class DirectAccess extends TypeAddress {

    public String toString(int num){
        return num + "";
    }
}
```
همچنین تغییراتی در بخش‌های دیگر نیز بسته به این تغییر داشتیم. برای مثال در بخش آدرس داریم:
```java
public class Address {
    public int num;
    public TypeAddress typeAddress;
    public varType varType;

    public Address(int num, varType varType, TypeAddress typeAddress) {
        this.num = num;
        this.typeAddress = typeAddress;
        this.varType = varType;
    }

    public Address(int num, varType varType) {
        this.num = num;
        this.typeAddress = new DirectAddress();
        this.varType = varType;
    }

    public String toString() {
        return typeAddress.toString(num);
    }
```




## پرسش‌ها


1. هر یک از مفاهیم زیر را در حد یک خط توضیح دهید.
    - کد تمیز: کد تمیز به کدهای برنامه نویسی‌ای اشاره دارد که ساختار مناسب و تمیزی دارند، به راحتی قابل درکند و نگه‌داری از آن‌ها آسان است. این کدها از قراردادها و بهترین شیوه‌ها (best practices) پیروی می‌کنند. کد تمیز بر سادگی، خوانایی و حداقل پیچیدگی، افزایش همکاری و کاهش خطاها در توسعه نرم‌افزار تاکید دارد.
    - بدهی فنی: بدهی فنی در برنامه نویسی مانند استفاده از میانبرها یا استفاده از راه حل‌های سریع هنگام نوشتن کد است که می‌تواند در کوتاه مدت، کارها را سریع‌تر کند اما منجر به افزایش پیچیدگی، مشکلات نگهداری و کاهش کارایی در درازمدت می شود. این مورد مانند قرض گرفتن زمان از آینده برای اتمام سریع کاری در حال حاضر است، اما باید بعداً با صرف زمان بیشتر برای اصلاح یا بهبود کد، آن را بازپرداخت کنیم.
    - بوی بد: بوی بد در برنامه نویسی به بخشی از کد اشاره دارد که درست به نظر نمی‌رسد. ممکن است یک باگ نباشد، اما نشانه‌ی آن است که کد می تواند بهبود یابد. درست مانند اینکه بوی بد در زندگی واقعی به ما می‌گوید چیزی مشکل دارد، بوی بد در کد نشان می‌دهد که راه بهتری برای نوشتن آن برای وضوح، کارایی یا قابلیت نگهداری وجود دارد. مثال‌های آن، کدهای با ساختاری ضعیف، کدهای تکراری و یا ناکارآمد، که نگهداری و اشکال‌زدابیشان دشوارتر است، می‌باشند.
---

2. طبق دسته‌بندی وب‌سایت refactoring.guru، بوهای بد کد به پنج دسته تقسیم می‌شوند. در مورد هر کدام از این پنج دسته توضیح مختصری دهید.
    - دسته‌ی اول، bloaters است که کدهای بسیار بزرگ یا پیچیده هستند که می‌توانند ساده شوند. bloaters درک، نگهداری و اصلاح کد را سخت تر می‌کنند. مثال‌ها شامل روش‌ها یا کلاس‌های طولانی است که بیش از حد کارهای مختلف انجام می‌دهند، یا ساختارهای داده‌ای که به‌طور غیرضروری بزرگ شده‌اند.
    - دسته‌ی دوم، Object-Orientation Abusers است که زمانی رخ می دهد که اصول شی گرا به درستی رعایت نشود و منجر به کدهایی می شود که از مزایای برنامه نویسی شی گرا به طور کامل استفاده نمی کند. مشکلات رایج آن عبارتند از استفاده نامناسب از وراثت، کلاس هایی با مسئولیت های بیش از حد، یا متدهایی که باید در یک کلاس متفاوت باشند.
    - دسته‌ی سوم، Change Preventers است که تغییر یا گسترش کد را در هنگام تغییر نیازها دشوار می‌کند. آنها اغلب ناشی از وابستگی های فشرده، ساختارهای سفت و سخت یا انتزاع ضعیف هستند. به عنوان مثال می توان به مقادیر hard-coded، فقدان رابط‌های مناسب، یا اجزای محکم‌جفت‌شده اشاره کرد.
    - دسته‌ی چهارم، Dispensables است که به قسمت‌هایی از کد اشاره می‌کنند که می توان بدون تأثیرگذاری بر عملکرد، با خیال راحت حذف شوند. آنها باعث پیچیدگی غیر ضروری می‌شوند و می‌توانند توسعه دهندگان را گیج کنند. به عنوان مثال می توان به کدهای کامنت شده، متغیرهای استفاده نشده یا کدهای مرده اشاره کرد که هرگز اجرا نمی شوند.
    - دسته‌ی پنجم، Couplers است که نشان‌دهنده ارتباط بیش از حد بین بخش‌های مختلف کد است که تغییر یک قسمت را بدون تأثیر بر روی قسمت‌های دیگر دشوار می‌کند. اتصال محکم انعطاف پذیری را کاهش می دهد و کد را شکننده تر می کند. به عنوان مثال می توان به کلاس هایی اشاره کرد که به شدت به یکدیگر متکی هستند یا پارامترهای زیادی را بین توابع ارسال می کنند.

---

3.  یکی از انواع بوهای بد، Lazy Class است.
    - این بوی بد در کدام یک از دسته‌بندی‌های پنج‌گانه قرار می‌گیرد؟ یک lazy class معمولاً در زمینه بوی کد تحت دسته Dispensables قرار می گیرد. کلاس تنبل به کلاسی اطلاق می‌شود که value  زیادی به پایگاه کد مبادله نمی‌کند و می‌توان با خیال راحت بدون تأثیر بر عملکرد یا طراحی کلی سیستم، آن را حذف کرد. حذف چنین کلاس هایی می تواند وضوح کد را بهبود بخشد و پیچیدگی غیر ضروری را کاهش دهد.
    - برای برطرف‌کردن این بو، استفاده از کدام بازآرایی‌ها پیشنهاد می‌شود؟ راه اول، Remove Unused Code است. اگر کلاس تنبل حاوی متدها یا فیلدهای استفاده نشده باشد، حذف آنها باعث کاهش شلوغی می شود. راه دوم، Merge Classes است. اگر چندین کلاس کوچک با حداقل عملکرد وجود داشته باشد، ادغام آنها می تواند پایگاه کد را ساده کند. راه سوم، Inline Class است. اگر کلاس تنبل رفتار قابل توجهی ارائه نمی دهد و متدهای آن را می توان به راحتی به جای دیگری منتقل کرد، آن را inline می‌کنیم.
    - در چه مواقعی باید این بو را نادیده گرفت؟
      می‌توان زمانی که lazy class برای توسعه آینده، سازگاری خارجی، ارائه اسناد یا برای اهداف debugging موقت مورد نیاز است، آن را نادیده بگیریم.

---