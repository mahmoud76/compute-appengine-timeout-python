![status: inactive](https://img.shields.io/badge/status-inactive-red.svg)

This project is no longer actively developed or maintained.  

For more information about Compute Engine, refer to our [documentation](https://cloud.google.com/compute).
For more information about App Engine, refer to our [documentation](https://cloud.google.com/appengine).

Instance timeout helper
================================

This App Engine application monitors your Google Compute Engine instances and deletes any non-production instances once they're 8 hours old. This helps avoid accidentally running instances for a long time. Any instances tagged "production" will be left running.

> WARNING: When instances are stopped, all data on ephemeral disks is destroyed. This application looks at ALL instances in a project and will delete any instances which aren't tagged "production". For extra safety, the application defaults to running in DRY_RUN mode, where deletes are logged, but not applied. 

This sample application demonstrates the [Compute Engine API](https://developers.google.com/compute/docs/reference/v1beta13/) from App Engine, specifically: listing instances and deleting instances. The same pattern can be used for other GCE API calls.

You can configure how often the application checks the instances, which tags will be left alone and how long instances are allowed to run before deleting them.


## Run Locally

1. Install the [Google Cloud SDK](https://cloud.google.com/sdk/), including the [gcloud tool](https://cloud.google.com/sdk/gcloud/), and [gcloud app component](https://cloud.google.com/sdk/gcloud-app).
2. Setup the gcloud tool.

   ```
   gcloud components update app
   gcloud auth login
   gcloud config set project <your-app-id>
   ```
   You don't need a valid app-id to run locally, but will need a valid id to deploy below.
   
1. Clone this repo.

   ```
   git clone https://github.com/GoogleCloudPlatform/compute-appengine-timeout-python.git
   ```
1. Install the required libraries

   ```
   pip install -t lib/ -r requirements.txt
   ```
(Note this requires at least `pip` version 6.0

1. Run this project locally from the command line.

   ```
   gcloud preview app run <REPO NAME>/
   ```

1. Visit the application at [http://localhost:8080](http://localhost:8080).

## Deploying

1. Use the [Cloud Developer Console](https://console.developer.google.com)  to create a project/app id. (App id and project id are identical)
2. Configure gcloud with your app id.

   ```
   gcloud config set project <your-app-id>
   ```
1. Use the [Admin Console](https://appengine.google.com) to view data, queues, and other App Engine specific administration tasks.
1. Use gcloud to deploy your app.

   ```
   gcloud preview app deploy <REPO NAME>/
   ```

1. Congratulations!  Your application is now live at your-app-id.appspot.com

> As long as DRY_RUN is set to `True` (the default) in `main.py`, the application will only log deletes.

View the index at the root of the application, at `http://YOUR-APP-ID.appspot.com`.
Check that production instances are being excluded and older instances would be deleted. 

To create instances tagged "production", add the instance using the GCE Console and include "production" in the tags field. Or add it using gcloud

    $ gcloud compute instances create test --tags production

You can optionally run the cron task manually and check the logs to verify that the correct instances will be deleted. 

Visit `http://YOUR-APP-ID.appspot.com/cron/delete` to run deletes immediately. Then check the AppEngine logs. You should see "DRY_RUN, not deleted" if any instances are old enough to be deleted.

Once everything looks good, edit `main.py` and change `DRY_RUN` to `False`.

Happy Computing!



"8210","بوبا العربية"
"8310","أمانة للتأمين"
"1302","بوان"
"1301","أسلاك"
"4040","سابتكو"
"8140","الأهلية"
"4007","الحمادي"
"8010","التعاونية"
"2270","سدافكو"
"4240","الحكير"
"2330","المتقدمة"
"2310","سبكيم العالمية"
"1212","أسترا الصناعية"
"2220","معدنية"
"6001","حلواني إخوان"
"4002","المواساة"
"2320","البابطين"
"2070","سبيماكو الدوائية"
"8311","عناية"
"4230","البحر الأحمر"
"2040","الخزف السعودي"
"8290","سوليدرتي"
"4110","مبرد"
"2290","ينساب"
"2300","صناعة الورق"
"1303","صناعات كهربائية"
"6020","جاكو"
"8120","إتحاد الخليج"
"3003","أسمنت المدينة"
"8070","الدرع العربي"
"4061","أنعام القابضة"
"2200","أنابيب"
"8280","العالمية"
"2150","زجاج"
"4003","إكسترا"
"1214","شاكر"
"2240","الزامل للصناعة"
"3004","أسمنت الشمالية"
"8012","جزيرة تكافل"
"8020","ملاذ للتأمين"
"4050","ساسكو"
"4200","الدريس"
"2090","جبسكو"
"8130","الأهلي للتكافل"
"1330","الخضري"
"8011","متلايف إيه أي جي العربي"
"2130","صدق"
"8312","الانماء طوكيو مارين"
"2340","العبداللطيف"
"3020","اسمنت اليمامة"
"8190","المتحدة للتأمين"
"8100","سايكو"
"4001","أسواق ع العثيم"
"2050","صافولا"
"1320","أنابيب السعودية"
"4100","مكة للإنشاء"
"1820","مجموعة الحكير"
"8160","التأمين العربية"
"2360","الفخارية"
"5110","السعودية للكهرباء"
"4260","بدجت السعودية"
"4020","العقارية"
"4320","الأندلس"
"3005","أسمنت أم القرى"
"9400","نوفا للإستثمارات"
"3040","أسمنت القصيم"
"2080","غازكو"
"8200","الاعادة السعودية"
"7040","جو"
"1202","ميبكو"
"1150","مصرف الإنماء"
"2010","سابك"
"1120","مصرف الراجحي"
"4190","جرير"
"2280","المراعي"
"4070","تهامة"
"2250","مجموعة السعودية"
"7010","الاتصالات السعودية"
"8050","سلامة"
"2160","أميانتيت"
"4150","الرياض للتعمير"
"8040","أليانز إس إف"
"2002","بتروكيم"
"1810","الطيار"
"1050","البنك السعودي الفرنسي"
"4004","دله الصحية"
"3002","أسمنت نجران"
"4140","الصادرات"
"3091","أسمنت الجوف"
"4250","جبل عمر"
"1211","معادن"
"3001","أسمنت حائل"
"1090","سامبا"
"1080","العربي الوطني"
"4280","المملكة القابضة"
"1010","بنك الرياض"
"4009","ميكو"
"4010","دور"
"1180","الأهلي"
"4090","طيبة"
"2180","فيبكو"
"2060","التصنيع"
"8150","أسيج"
"3080","أسمنت الشرقية"
"2370","مسك"
"1030","الاستثمار"
"2020","سافكو"
"3030","الأسمنت السعودية"
"4006","اسواق المزرعة"
"3060","أسمنت ينبع"
"4180","فتيحي"
"4030","البحري"
"2140","الأحساء للتنمية"
"3050","اسمنت الجنوب"
"6002","هرفي للأغذية"
"4220","إعمار المدينة الاقتصادية"
"4008","ساكو"
"6040","تبوك الزراعية"
"2120","المتطورة"
"2030","ساركو"
"8030","ميدغلف"
"1213","السريع"
"4080","عسير"
"8110","وفا للتأمين"
"8180","الصقر للتأمين"
"4290","الخليج للتدريب"
"4170","شمس"
"1060","ساب"
"6010","نادك"
"8240","أيس"
"1140","بنك البلاد"
"2210","نماء للكيماويات"
"2230","الكيميائية"
"2350","كيان السعودية"
"8080","ساب تكافل"
"1201","تكوين"
"2001","كيمانول"
"8170","الاتحاد التجاري"
"6004","الخطوط السعودية للتموين"
"1210","بي سي اي"
"3090","أسمنت تبوك"
"6050","الأسماك"
"8260","الخليجية العامة"
"2190","سيسكو"
"1020","بنك الجزيرة"
"4310","مدينة المعرفة"
"6070","الجوف الزراعية"
"2380","بترو رابغ"
"7030","زين السعودية"
"8060","ولاء"
"4160","ثمار"
"4005","رعاية"
"1040","سعودي هولندي"
"8270","بروج للتأمين التعاوني"
"6090","جازادكو"
"4300","دار الأركان"
"8230","تكافل الراجحي"
"8300","الوطنية للتأمين"
"4031","الخدمات الأرضية"
"2100","وفرة"
"4210","الأبحاث والتسويق"
"2170","اللجين"
"3010","أسمنت العربية"
"2110","الكابلات"
"2260","الصحراء"
"7020","موبايلي"
"6060","الشرقية للتنمية"
"4270","طباعة وتغليف"
"8250","أكسا التعاونية"