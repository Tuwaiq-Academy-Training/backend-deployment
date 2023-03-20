# Database Deployment using Planetscale. 

عندما نريد رفع API على cloud يجب علينا ايضاً رفع قاعدة البيانات. لأنها ان كانت محليّة لن يستطيع أحد الوصول اليها، لذلك في هذه المقالة سنقوم باتّباع خطوات معيّنة لرفع قاعدة البيانات باستخدام Planetscale.


### الخطوات.

- تسجيل حساب في Planetscale من خلال الضغط على sign up في الرابط التالي https://app.planetscale.com/ .
- سيصلك بعد تسجيل الحساب بريد الكتروني للتحقق من البريد الالكتروني في عمليّة انشاء حساب جديد.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675165378345_Screen+Shot+1444-07-09+at+2.42.51+PM.png)

- بمجرّد الضغط على confirm email سنتذهب الى مرحلة setup للحساب وقاعدة البيانات.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675168895879_Screen+Shot+1444-07-09+at+1.58.09+PM+2.png)



![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675168937310_Screen+Shot+1444-07-09+at+1.58.14+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164382910_Screen+Shot+1444-07-09+at+1.58.24+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164385478_Screen+Shot+1444-07-09+at+1.58.54+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164391157_Screen+Shot+1444-07-09+at+1.59.22+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164394874_Screen+Shot+1444-07-09+at+2.00.14+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164398986_Screen+Shot+1444-07-09+at+2.00.22+PM.png)

- في نهاية تعريفهم لكل المميزات التي لديهم ستجد زر اضافة قاعدة بيانات جديدة، قم بالضغط عليه واختيار اسم مناسب لقاعدة البيانات الخاصة بك.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164419898_Screen+Shot+1444-07-09+at+2.01.05+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164424535_Screen+Shot+1444-07-09+at+2.01.23+PM.png)

- عند الضغط على زر connection او الاتصال سيتم اعطاؤك رابط بحسب اللغة او التقنية المستخدمة لكي تنسخة وتضيفه على برنامجك حتّى يتم ربط البرنامج في قاعدة البيانات الخاصّة بك.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164435862_Screen+Shot+1444-07-09+at+2.02.16+PM+2.png)

- قم بنسخ الرّابط واضافته في ملف .env
- بمجرّد اضافتك للرابط ستجد اشكالية في prisma المدونه هنا https://github.com/prisma/prisma/issues/11246 ، لذلك سنقوم باستخدام الحل المرفق وهو اضافة sslcert كما هو موجود في الصورة التالية. 
    > ملاحظة: مسار الشهادة certificate المرفق هو خاص في MacOS. لذلك ان كنت تستخدم windows قم باستخدام sslcert=/etc/pki/tls/certs/ca-bundle.crt.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164457280_Screen+Shot+1444-07-09+at+2.10.32+PM+2.png)

- بعد اضافة الرّابط قمنا باستخدام الأمر npx prisma db push حتى نقوم برفع هيكلة الجداول في قاعدة البيانات. لكن نلاحظ مشكلة وهي أن Planetscale لا يقوم بعمل علاقات relationship كما تقوم به prisma أي انه يقوم بحذف foreign keys في الهيكلة. لذلك سنقوم بمحاولة محاكاة emulate العلاقات باستخدام الحل التالي والمرفق من قبل prisma وهو من خلال اضافة index او مؤشر.
![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164448377_Screen+Shot+1444-07-09+at+2.14.18+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164534148_Screen+Shot+1444-07-09+at+2.28.47+PM.png)


مصدر لتفادي مشكلة Foreign Key 

https://www.prisma.io/docs/guides/database/using-prisma-with-planetscale#how-to-create-indexes-on-foreign-keys


schema.prisma

    // This is your Prisma schema file,
    // learn more about it in the docs: https://pris.ly/d/prisma-schema
    generator client {
      provider = "prisma-client-js"
    }
    datasource db {
      provider = "mysql"
      url      = env("DATABASE_URL")
    }
    model User{
      id String @id @default(uuid())
      name String
      email String @unique
      password String
      role Role @default(User)
      tasks Task[]
    }
    model Task{
      id String @id @default(uuid())
      title String 
      isCompleted Boolean @default(false)
      user User @relation(fields: [userId], references: [id])
      userId String
      @@index([userId])
    }
    
    enum Role{
      User
      Admin
    }

بعد ذلك، سنقوم بعمل npx prisma db push. من ثمّ اختبار API كالتالي.


![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164698196_Screen+Shot+1444-07-09+at+2.19.35+PM+2.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164701180_Screen+Shot+1444-07-09+at+2.19.50+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675164705868_Screen+Shot+1444-07-09+at+2.21.08+PM.png)


الآن، حاول اغلاق server واعادة تشغيله لتلاحظ أن البيانات ما زالت مخزّنه ولم يتم حذفها.

لعرض البيانات في Planetscale سنقوم باستخدام console كالتالي.

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675165193298_Screen+Shot+1444-07-09+at+2.23.51+PM+2.png)



![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675165199711_Screen+Shot+1444-07-09+at+2.23.41+PM.png)

![](https://paper-attachments.dropboxusercontent.com/s_FB4B198C59800838CAB787CD31838C669DD130A90F8DA32DB48D7555829F478E_1675165203181_Screen+Shot+1444-07-09+at+2.23.26+PM.png)

