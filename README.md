الهدف

تطبيق “رسالة” لإدارة خدمة الشباب داخل الكنيسة، بأدوار (أدمن – خادم – مخدوم) مع صلاحيات واضحة، تسجيل مبني على “كود كنيسة”، وصفحة رئيسية مطابقة للتصميم اللي اتفقنا عليه (هيدر أحمر + بادج مستوى + ترحيب + CTA + شبكة 3×3).

2) الأدوار والصلاحيات (مختصر)

الصلاحية	أدمن	خادم	مخدوم

إنشاء/توزيع أكواد الكنيسة	✅	❌	❌
قبول/رفض طلبات الانضمام	✅	❌	❌
إدارة الرسالة اليومية	✅	✅	عرض فقط
النوتة الروحية	إدارة/عرض	إدارة/عرض	إدارة بياناته فقط
الاجتماعات	إدارة/عرض	إدارة/عرض	عرض فقط
المسابقات/المحاضرات	إدارة/عرض	إدارة/عرض	عرض فقط
الشات	إدارة الغرف/المحتوى	إدارة/مشاركة	مشاركة
الأعضاء	عرض/إدارة	عرض فقط	—
الملف الشخصي	إدارة	إدارة	إدارة
صفحة إنشاء الأكواد بالرئيسية	تظهر للأدمن فقط	—	—


> ملاحظة: “إدارة” = إنشاء/تعديل/حذف. “عرض فقط” = قراءة.



3) تدفّقات التسجيل/الدخول

الأدمن: يسجّل أولًا بكود كنيسة يقوم هو بإنشائه (من التسجيل أو من صفحة رئيسية للأدمن). بعد أول أدمن، أي محاولة إنشاء كود من غير أدمن تُمنع.

الخادم/المخدوم: يسجّل بكود أرسله الأدمن + كلمة سر. تظهر لهما حقول الملف الشخصي.

الكودين: للأدمن ممكن يولّد كودين مستقلين: واحد للخدام، واحد للمخدومين. يتم تعيين دور المتسجل حسب الكود المستخدم.

الدخول: (كود الكنيسة + كلمة السر) أو (هاتف/إيميل + كلمة السر) حسب ما اخترناه، المعيار النهائي: كود الكنيسة + كلمة المرور كما طلبت.


4) الشاشات (UI)

مشتركة لكن تختلف بالألوان والصلاحيات:

1. شاشة البداية/الدخول LoginActivity


2. شاشة التسجيل RegisterActivity (بحقولك كاملة، مع إظهار زر “إنشاء كود” للأدمن فقط)


3. الصفحة الرئيسية:

HomeAdminActivity (أحمر/بنفسجي – فيها بطاقة “إنشاء كود الكنيسة” + كل البلاطات)

HomeServantActivity (نفس الألوان الإدارية – بلاطة إنشاء الكود غير موجودة)

HomeMemberActivity (لون مختلف – بلاطة إنشاء الكود غير موجودة)

كل الصفحات بنفس شبكة 3 أعمدة × 3، وبلاطات بصورك بدل الألوان (زي ما عملنا).



4. إنشاء كود الكنيسة CreateChurchCodeActivity (للأدمن فقط – وتوليد كود خادم وكود مخدوم)


5. طلبات الانضمام RequestsActivity (للأدمن فقط)


6. الأعضاء MembersActivity (للأدمن عرض/إدارة – للخادم عرض فقط)


7. الرسالة اليومية DailyMessageActivity


8. النوتة الروحية SpiritualNoteActivity (المخدوم يعدّل نوتته هو فقط)


9. الاجتماعات MeetingsActivity


10. المحاضرات والفقرات LecturesActivity


11. المسابقات CompetitionsActivity


12. النقاط/الإنجازات RewardsActivity


13. الشات ChatActivity


14. الملف الشخصي ProfileActivity



عناصر ثابتة في الرئيسية (مطابقة للتصميم):

هيدر أحمر كبسولة بها (أيقونة النجمة – عنوان “رسالة” – أيقونة القائمة).

بادج “المستوى”.

قسم الترحيب: “مرحباً” + اسم المستخدم (يتغيّر حسب المسجل) + جملة ترحيب قابلة للتعديل من الأدمن/الخادم.

زر CTA: “اعرض الرسالة اليومية”.

شبكة 3×3 (صور البلاطات من مواردك).

نقاط ديكورية أسفل.


5) الثيم والألوان

Admin/Servant Theme: اللون الأساسي (أحمر/بنفسجي) للهيدر والـCTA.

Member Theme: لون آخر مميز للأعضاء.

تفعيل RTL وخط عربي مناسب، ودعم android:supportsRtl="true".


6) هيكلة المشروع (Packages)

com.example.risala/
  data/
    local/ (SessionManager, Room لو لزم)
    remote/ (Firestore, Auth, Storage)
    repo/ (ChurchRepo, UserRepo, RequestsRepo, ChatRepo ...)
    models/ (UserProfile, Church, JoinRequest, Note, Message, Meeting, Lecture, Competition, Reward ...)
  ui/
    auth/ (LoginActivity, RegisterActivity)
    home/ (HomeAdminActivity, HomeServantActivity, HomeMemberActivity)
    church/ (CreateChurchCodeActivity, RequestsActivity, MembersActivity)
    features/ (DailyMessageActivity, SpiritualNoteActivity, MeetingsActivity, LecturesActivity,
               CompetitionsActivity, RewardsActivity, ChatActivity, ProfileActivity)
    common/ (BaseActivity, BaseDrawerActivity, adapters, viewholders)
  util/ (Role enum, Extensions, Validators)

7) نموذج البيانات (Firestore – مقترح)

churches/{churchId}

name, codeServant, codeMember, maxMembers, validUntil, createdByUid


users/{uid}

fullName, role (admin/servant/member), churchId, phone, email, gender, dob,
address, country, city, education, photoUrl, greetingText (للعبارة تحت “مرحباً”)


joinRequests/{id}

churchId, applicantUid, roleRequested, status (pending/approved/rejected), timestamps


dailyMessages/{churchId}/{date}

title, content, createdByUid


notes/{uid}/{noteId}

title, content, date


meetings/{churchId}/{meetingId}

title, date, location, description


lectures/{churchId}/{lectureId}

title, speaker, date, attachments


competitions/{churchId}/{compId}

title, rules, deadline, results


rewards/{churchId}/users/{uid}

points, levels, history[]


chats/{churchId}/rooms/{roomId}/messages/{messageId}

senderUid, text, createdAt



8) قواعد الأمان (Firestore Rules – فكرة)

// يُفترض وجود وثيقة user لكل مستخدم تُحدِّد دوره وكنيسته
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    function userDoc() { return get(/databases/$(db)/documents/users/$(request.auth.uid)); }
    function role() { return userDoc().data.role; }
    function churchId() { return userDoc().data.churchId; }

    // users: كل مستخدم يشوف ويحدث حسابه فقط (عدا الدور يحدّثه الأدمن)
    match /users/{uid} {
      allow read: if request.auth != null && (uid == request.auth.uid || role() in ['admin','servant']);
      allow update: if request.auth != null && uid == request.auth.uid
                    && !(request.resource.data.role in ['admin','servant','member']); // منع تعديل الدور
      allow update: if role() == 'admin'; // الأدمن يقدر يعدّل أي بروفايل
      allow create: if request.auth != null;
    }

    // الكنائس: أدمن الكنيسة فقط يعدّل الأكواد
    match /churches/{cid} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && role() == 'admin' && churchId() == cid;
    }

    // طلبات الانضمام: الأدمن يقرأ/يقبل/يرفض؛ المستخدم يشوف طلبه
    match /joinRequests/{id} {
      allow create: if request.auth != null;
      allow read: if request.auth != null && (
          role() == 'admin' || resource.data.applicantUid == request.auth.uid
      );
      allow update, delete: if request.auth != null && role() == 'admin';
    }

    // الرسالة اليومية/الاجتماعات/المحاضرات/المسابقات: أدمن/خادم يكتبون؛ الكل يقرأ
    match /dailyMessages/{cid}/{doc=**} {
      allow read: if request.auth != null && churchId() == cid;
      allow write: if request.auth != null && churchId() == cid && role() in ['admin','servant'];
    }
    match /meetings/{cid}/{doc=**} { allow read: if request.auth != null && churchId() == cid;
      allow write: if request.auth != null && churchId() == cid && role() in ['admin','servant']; }
    match /lectures/{cid}/{doc=**} { allow read: if request.auth != null && churchId() == cid;
      allow write: if request.auth != null && churchId() == cid && role() in ['admin','servant']; }
    match /competitions/{cid}/{doc=**} { allow read: if request.auth != null && churchId() == cid;
      allow write: if request.auth != null && churchId() == cid && role() in ['admin','servant']; }

    // النوتة الروحية: صاحبها فقط
    match /notes/{uid}/{noteId} {
      allow read, write: if request.auth != null && uid == request.auth.uid;
    }

    // النقاط/الإنجازات: الأدمن/الخادم يكتبون، صاحب الحساب يقرأ
    match /rewards/{cid}/users/{uid} {
      allow read: if request.auth != null && churchId() == cid && (uid == request.auth.uid || role() in ['admin','servant']);
      allow write: if request.auth != null && churchId() == cid && role() in ['admin','servant'];
    }

    // الشات: أعضاء نفس الكنيسة يقرأون/يكتبون
    match /chats/{cid}/{doc=**} {
      allow read, write: if request.auth != null && churchId() == cid;
    }
  }
}

9) منطق الوصول داخل التطبيق (Gatekeeping)

في كل Activity نقرأ الدور من SessionManager أو من Firestore بعد الدخول:

لو admin → افتح HomeAdminActivity

لو servant → HomeServantActivity

لو member → HomeMemberActivity


زر “إنشاء كود الكنيسة”:

يظهر في الرئيسية للأدمن فقط

يظهر في التسجيل فقط عندما يكون اختيار الدور = أدمن (أو زر خاص للأدمن قبل أول أدمن)


العبارة تحت “مرحباً”: حقل نصي محفوظ في users/{uid}.greetingText:

الأدمن/الخادم يقدروا يغيروا “عبارة عامة للكنيسة” (churches/{churchId}.greetingDefault)

المخدوم يرى العامة إلا إذا ضبط لنفسه عبارة شخصية (اختياري).



10) الخلفية/التصميم (تطابق الصورة)

خلفية home_bg بقياس 1080×2400 (أو أعلى) وscaleType="centerCrop" + طبقة تدرّج خفيفة (اختياري) لرفع المقروئية.

شبكة البلاطات 3×3، كل بلاطة صورة PNG/JPG جاهزة من عندك، داخل MaterialCardView بحواف 18dp.

الصور الصغيرة للأيقونات (المينيو/النجمة/الأفاتار) موحدة الأسلوب.

زر + (FloatActionButton) بالأسفل يمين:

لو له هدف (فتح إنشاء اجتماع/رسالة يومية للأدمن والخادم) نفعّله حسب الدور؛ لو ملوش، نشيله.



11) تجربة المستخدم

اللغة الافتراضية: العربية – RTL.

الاسم المعروض “مرحباً {الاسم}” يتسحب من البروفايل (الاسم اللي اتسجل بيه).

في التسجيل: تُحفظ كل البيانات فور الإنشاء في users/{uid}، وتظهر فورًا في “الملف الشخصي”.


12) الأمان

كل عمليات CRUD تمر عبر الـRepos، لا وصول مباشر للداتابيز من الـUI.

مصادقة Firebase Auth (Email+Password أو Phone لاحقًا).

قواعد Firestore (أعلاه) تعكس صلاحياتك.


13) الأداء/الأوفلاين

تفعيل Firestore Offline Persistence.

كاش بسيط في SessionManager/Room لو لزم للمحتوى المقروء مثل الاجتماعات والرسالة اليومية.


14) التحليلات والتنبيهات (اختياري)

Firebase Analytics للأحداث المهمة (تسجيل/فتح موديول/نجاح مشاركة).

FCM لإرسال الرسالة اليومية والإشعارات بالمواعيد.


15) الأصول (Assets)

الخلفيات: 1080×2400 على الأقل.

البلاطات: 600×600 px (أو 512×512) PNG/WebP.

الأيقونات: 24dp/48dp مع نسخ @2x/@3x (أو Vector Drawable).


16) أسماء الموارد (اقتراح)

صور البلاطات: tile_daily.png, tile_note.png, tile_message.png, tile_members.png, tile_meetings.png, tile_rewards.png, tile_competitions.png, tile_chat.png, tile_profile.png

أيقونات الهيدر: ic_star.png, ic_menu.png, ic_person.png

الخلفية: home_bg.jpg


17) تقسيم الألوان حسب الدور

Admin/Servant: colorPrimary = #C62828 (أحمر) أو بنفسجيك الحالي، cta = نفس الأساسي

Member: colorPrimary = #00897B (أخضر مزرّق) أو لونك المقترح


18) خطوات التنفيذ (Checklist)

1. ضبط الثيمات (دورين: Admin/Servant + Member) وتفعيل RTL.


2. بناء SessionManager + Role enum + BaseActivity.


3. تنفيذ شاشات Auth (دخول/تسجيل) كما طلبت:

التسجيل فقط بكود الكنيسة + كلمة السر؛ زر إنشاء الكود يظهر للأدمن فقط.



4. بناء ثلاث صفحات رئيسية منفصلة، مع نفس التصميم والبلاطات.


5. إظهار/إخفاء بلاطة “إنشاء كود الكنيسة” للأدمن فقط.


6. ربط Firestore (الموديلات/الريبو/القواعد).


7. تنفيذ الميزات (طلبات – أعضاء – رسالة يومية – …) تدريجيًا.


8. اختبار صلاحيات القراءة/الكتابة لكل دور.


9. رفع الصور والأصول النهائية.


10. إعداد توقيع وإصدار APK/AAB.



19) معايير القبول (Acceptance)

الصفحة الرئيسية مطابقة تمامًا للتصميم (الهيدر/البادج/الترحيب/CTA/شبكة 3×3/نقاط).

زر إنشاء الكود يظهر ويشتغل للأدمن فقط (في الرئيسية وأثناء التسجيل).

المخدوم لا يمكنه تعديل بيانات غيره ولا يرى غير بياناته بالنوتة والإنجازات.

صلاحيات الشاشات كما في الجدول.

الجملة تحت “مرحباً” قابلة للتعديل للأدمن/الخادم، وتُعرض ديناميكيًا.

التسجيل يحفظ البيانات كاملة ويملأ الملف الشخصي فورًا.
