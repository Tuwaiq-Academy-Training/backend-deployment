# API Deployment using Render



> ملاحظة: تأكد قبل القيام بالخطوات ادناه بتواجد الأمرين التاليين في المشروع الخاص بك. 

```
        "build": "npx tsc",
        "start": "node dist/app.js",
```

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1678261822945_Screen+Shot+1444-08-16+at+10.50.15+AM.png)




### الخطوات

١. الدخول على موقع render من خلال الرابط التالي https://render.com/

٢. تسجيل حساب جديد باستخدام الخيارات المتاحة في render.

٣. اتباع الخطوات التالية من خلال اتباع خطوات رفع web services.

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345496582_Screen+Shot+1444-07-11+at+1.09.44+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345504992_Screen+Shot+1444-07-11+at+1.09.51+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345513300_Screen+Shot+1444-07-11+at+1.09.56+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345522939_Screen+Shot+1444-07-11+at+1.10.16+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345525980_Screen+Shot+1444-07-11+at+1.11.07+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345530501_Screen+Shot+1444-07-11+at+1.11.52+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345534234_Screen+Shot+1444-07-11+at+1.12.25+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345556711_Screen+Shot+1444-07-11+at+1.13.28+PM.png)


بعد الربط في todo repository سنقوم بالدخول على web services لتظهر لنا الصورة التالية

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345564709_Screen+Shot+1444-07-11+at+1.13.33+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345603722_Screen+Shot+1444-07-11+at+1.45.40+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345610201_Screen+Shot+1444-07-11+at+1.45.59+PM.png)


بعد ان قمنا بالضغط على create web service لم تتم العمليّة بنجاح بسبب فشل عمليّة build لذلك سنقوم بالدخول على اعدادات deploy من ثمّ التحديث على build command ليقوم بتنزيل المكتبات المطلوبة اولاً من ثمّ عمل build للبرنامج. 

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345615005_Screen+Shot+1444-07-11+at+1.49.04+PM.png)


بعد عمل save changes سيقوم render بعمليّة deploy مرّة أخرى. بعد ذلك سيظهر لنا رابط deployed api لنقوم بنسخه واختبار. 

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345944377_Screen+Shot+1444-07-11+at+4.52.17+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345628660_Screen+Shot+1444-07-11+at+2.18.39+PM.png)


نلاحظ أعلاه انه توجد اشكاليّة في الربط مع قاعدة البيانات في planetscale. لحل هذه المشكله قمنا باختبار عدّة حلول نتج عنها ان قيمة sslcert في connection string يجب تحديثها. لذلك بعد تحديثها للقيمة  `sslcert=/etc/ssl/certs/ca-certificates.crt`  بناءً على ( الرابط التالي) [https://planetscale.com/docs/concepts/secure-connections#debian--ubuntu--gentoo--arch--slackware]  اصبح connection string بهذا الشكل.

    mysql://*************@us-east.connect.psdb.cloud/todo?ssl={"rejectUnauthorized":true}&sslcert=/etc/ssl/certs/ca-certificates.crt
![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345641083_Screen+Shot+1444-07-11+at+4.39.21+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_45B7735E684D609FAF1E67BAFAC8B529767473809AAEA0BD1A54A66C859C0318_1675345645715_Screen+Shot+1444-07-11+at+4.40.31+PM.png)







- مصدر عن sslcert
https://www.kaspersky.com/resource-center/definitions/what-is-a-ssl-certificate

