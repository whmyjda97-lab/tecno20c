# TECNO BG7n — SUSFS v2.2.0 + KernelSU-Next

حزمة GitHub Actions لبناء KernelSU-Next + SUSFS فوق Android common
المطابق لنواة TECNO BG7n الأصلية.

## قبل البناء

هذه الحزمة **لا تحتوي boot.img** بسبب حدود حجم ملفات GitHub.

يجب رفع `boot.img` الأصلي مرة واحدة إلى GitHub Release في نفس المستودع:

- Tag: `stock-boot`
- اسم الملف: `boot.img`

بعد ذلك يقوم الـWorkflow بتنزيله تلقائيًا وإعادة تركيب Image الجديد داخله.

## التشغيل

1. أنشئ Repository جديدًا.
2. ارفع كل محتويات هذه الحزمة.
3. أنشئ Release بالـtag `stock-boot`.
4. أرفق `boot.img` الأصلي.
5. افتح Actions.
6. اختر `Build BG7n SUSFS + KernelSU-Next`.
7. اضغط Run workflow.
8. بعد نجاح البناء حمّل Artifact:
   `BG7n-SUSFS-KSU-build`

الناتج الرئيسي:
`boot-BG7n-SUSFS-KSU.img`

لا تفلش الناتج قبل التحقق من نجاح الـworkflow بالكامل.
احتفظ دائمًا بنسخة boot.img الأصلية.

`dtbo.img` و`vendor_a.img` لا يتم تعديلهما.
