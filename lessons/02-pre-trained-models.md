<div dir="rtl" align="right">

<h1 dir="rtl" align="right">روز ۲ — مدل‌های از پیش‌آموزش‌دیده (Pre-trained Models)</h1>

<h2 dir="rtl" align="right">هدف درس</h2>
<p dir="rtl" align="right">در پایان این درس باید بتوانید توضیح دهید مدل از پیش‌آموزش‌دیده چیست، چرا اغلب به‌جای ساخت مدل از صفر از آن استفاده می‌کنیم، تفاوت <span dir="ltr">pre-training</span>، <span dir="ltr">inference</span>، <span dir="ltr">prompting</span>، <span dir="ltr">RAG</span> و <span dir="ltr">fine-tuning</span> چیست، چگونه یک مدل را برای محصول انتخاب کنیم و محدودیت‌های مهمی مثل <span dir="ltr">context window</span>، تاریخ قطع دانش، هزینه، latency، حریم خصوصی و وابستگی به provider را بسنجیم.</p>

<h2 dir="rtl" align="right">۱. مدل از پیش‌آموزش‌دیده چیست؟</h2>
<p dir="rtl" align="right">یک <strong>Pre-trained Model</strong> مدلی است که قبل از رسیدن درخواست محصول شما، روی حجم بزرگی از داده آموزش دیده و پارامترهایش الگوهای آماری و ساختارهای مفیدی از داده را یاد گرفته‌اند. بنابراین برای ساخت یک قابلیت AI معمولاً لازم نیست میلیاردها پارامتر را از صفر آموزش دهیم؛ مدل پایه را انتخاب می‌کنیم و آن را از طریق prompt، context، ابزار، RAG یا در صورت نیاز fine-tuning برای مسئله‌ی خودمان به‌کار می‌گیریم.</p>

<pre dir="ltr" align="left"><code>Large training corpus
        ↓
    Pre-training
        ↓
   Base / Foundation Model
        ↓
 ┌──────┼─────────┬───────────┐
Prompt  RAG    Fine-tuning   Tools
 └──────┼─────────┴───────────┘
        ↓
 Product / Application</code></pre>

<div dir="rtl" align="right"><strong>نکته:</strong> «از پیش‌آموزش‌دیده» به معنی «دانای همه‌چیز» یا «مناسب برای هر مسئله» نیست. مدل هنوز محدودیت دانش، خطا، hallucination و محدودیت context دارد.</div>

<h2 dir="rtl" align="right">۲. Pre-training دقیقاً چه اتفاقی است؟</h2>
<p dir="rtl" align="right">در یک LLM، متن به token تبدیل می‌شود و مدل طی آموزش بارها مسئله‌ای شبیه پیش‌بینی token بعدی را حل می‌کند. خطای پیش‌بینی محاسبه می‌شود و با الگوریتم‌های بهینه‌سازی وزن‌های شبکه تغییر می‌کنند. این فرایند بسیار پرهزینه است و به dataset، GPU/accelerator، زیرساخت توزیع‌شده و زمان زیادی نیاز دارد.</p>

<pre dir="ltr" align="left"><code>Text → Tokenizer → Tokens → Transformer → Prediction
                                      ↓
                                  Loss/Error
                                      ↓
                             Update model weights</code></pre>

<p dir="rtl" align="right">بعد از پایان آموزش، در زمان <strong>Inference</strong> معمولاً وزن‌های مدل تغییر نمی‌کنند. برنامه‌ی شما ورودی را ارسال می‌کند و مدل با پارامترهای فعلی خروجی تولید می‌کند. پس <span dir="ltr">Inference ≠ Training</span>.</p>

<h2 dir="rtl" align="right">۳. Foundation Model، Base Model و Instruction-tuned Model</h2>
<p dir="rtl" align="right"><strong>Foundation Model</strong> اصطلاح گسترده‌ای برای مدل بزرگی است که قابلیت استفاده در چندین مسئله را دارد. <strong>Base Model</strong> معمولاً خروجی مستقیم‌تر pre-training است و عمدتاً ادامه‌ی متن را مدل می‌کند. مدل‌های <strong>Instruction-tuned</strong> بعداً برای دنبال‌کردن دستورهای انسانی و رفتار مکالمه‌ای بهتر تنظیم می‌شوند. مدل chat که از API استفاده می‌کنیم معمولاً صرفاً یک base model خام نیست.</p>

<h2 dir="rtl" align="right">۴. چرا به‌جای Training از صفر از مدل آماده استفاده کنیم؟</h2>
<ul dir="rtl" align="right">
<li><strong>هزینه و زمان:</strong> قابلیت محصول را بسیار سریع‌تر می‌توان ساخت.</li>
<li><strong>کیفیت پایه:</strong> مدل از قبل زبان، کدنویسی، استدلال و الگوهای عمومی زیادی آموخته است.</li>
<li><strong>زیرساخت کمتر:</strong> در مدل‌های hosted، مدیریت GPU و serving عمدتاً بر عهده provider است.</li>
<li><strong>تکرار سریع:</strong> می‌توان مدل و prompt را سریع عوض و با eval مقایسه کرد.</li>
<li><strong>تمرکز مهندسی روی محصول:</strong> تیم می‌تواند روی retrieval، امنیت، workflow، observability و تجربه‌ی کاربر تمرکز کند.</li>
</ul>

<h2 dir="rtl" align="right">۵. چهار سطح مهم تطبیق مدل با محصول</h2>
<p dir="rtl" align="right"><strong>Prompting:</strong> رفتار مورد انتظار را در ورودی تعریف می‌کنیم؛ دانش مدل عوض نمی‌شود. <strong>RAG:</strong> اطلاعات اختصاصی یا جدید را هنگام درخواست بازیابی و وارد context می‌کنیم. <strong>Tools:</strong> مدل اجازه پیدا می‌کند از سرویس‌های خارجی برای گرفتن داده یا انجام action استفاده کند. <strong>Fine-tuning:</strong> با نمونه‌های آموزشی، رفتار/وزن‌های مدل را برای الگوی خاصی تنظیم می‌کنیم. این چهار مورد جای یکدیگر نیستند و ممکن است ترکیب شوند.</p>

<pre dir="ltr" align="left"><code>User Request
     ↓
ASP.NET Core API
     ↓
Retrieve company data ──→ Vector DB / Search
     ↓
Prompt + Retrieved Context
     ↓
Pre-trained LLM ──→ Tool Call (optional)
     ↓
Validation / Guardrails
     ↓
Response</code></pre>

<h2 dir="rtl" align="right">۶. Context Window چیست؟</h2>
<p dir="rtl" align="right"><span dir="ltr">Context Window</span> ظرفیت اطلاعاتی است که مدل در یک درخواست/تعامل می‌تواند در context فعال خود پردازش کند و معمولاً با token بیان می‌شود. دستور سیستم، پیام‌های گفتگو، اسناد RAG، tool results و خروجی مورد انتظار همگی می‌توانند بخشی از بودجه‌ی context را مصرف کنند.</p>
<p dir="rtl" align="right">Context بزرگ‌تر مفید است، اما به معنی حافظه‌ی دائمی یا کیفیت تضمین‌شده نیست. فرستادن داده‌ی بیشتر می‌تواند هزینه و latency را بالا ببرد و حتی نویز ایجاد کند. طراحی درست یعنی فقط context مرتبط را وارد کنیم.</p>

<h2 dir="rtl" align="right">۷. Knowledge Cut-off با Context Window فرق دارد</h2>
<p dir="rtl" align="right"><strong>Knowledge cut-off</strong> به مرز زمانی دانش حاصل از آموزش مدل اشاره دارد؛ <strong>context window</strong> ظرفیت اطلاعاتی است که همین حالا به مدل داده‌ایم. اگر قیمت لحظه‌ای سهم یا وضعیت سفارش لازم باشد، حتی مدلی با context بسیار بزرگ نمی‌تواند آن را از دانش آموزشی تضمین کند؛ باید داده‌ی زنده از API/DB/tool دریافت شود.</p>

<h2 dir="rtl" align="right">۸. Hosted/Closed در برابر Open-weight</h2>
<p dir="rtl" align="right">مدل‌های hosted معمولاً از طریق API مصرف می‌شوند و provider عملیات serving را مدیریت می‌کند. در مدل‌های open-weight وزن مدل برای اجرا/استقرار در اختیار مصرف‌کننده قرار می‌گیرد (شرایط مجوز هر مدل متفاوت است). Self-hosting می‌تواند کنترل داده و deployment بیشتری بدهد، اما GPU، scaling، batching، monitoring، upgrades و امنیت serving را نیز به مسئولیت شما تبدیل می‌کند.</p>

<h2 dir="rtl" align="right">۹. اکوسیستم‌هایی که باید بشناسید</h2>
<p dir="rtl" align="right">در این مرحله هدف حفظ‌کردن یک «بهترین مدل» نیست؛ بازار سریع تغییر می‌کند. باید خانواده‌های مهم و روش ارزیابی را بشناسید: مدل‌ها و APIهای OpenAI، Claude از Anthropic، Gemini از Google، سرویس‌های Azure AI و AWS SageMaker، مدل‌های موجود در Hugging Face، خانواده‌های Mistral و سرویس‌های Cohere و Replicate. انتخاب نهایی باید با نیاز و eval واقعی پروژه انجام شود.</p>

<h2 dir="rtl" align="right">۱۰. معیارهای انتخاب مدل برای یک Backend واقعی</h2>
<ul dir="rtl" align="right">
<li><strong>Capability:</strong> آیا مدل در task واقعی ما کیفیت کافی دارد؟ متن، کد، vision، structured output یا tool calling؟</li>
<li><strong>Quality/Evaluation:</strong> روی dataset و سناریوهای واقعی خودمان چقدر درست عمل می‌کند؟</li>
<li><strong>Latency:</strong> p50/p95 زمان پاسخ برای UX قابل قبول است؟</li>
<li><strong>Cost:</strong> هزینه‌ی ورودی، خروجی، retrieval و تعداد درخواست‌ها در مقیاس واقعی چقدر می‌شود؟</li>
<li><strong>Context:</strong> ظرفیت context برای اسناد و conversation ما مناسب است؟</li>
<li><strong>Freshness:</strong> آیا داده‌ی تازه لازم است و باید RAG/tool اضافه شود؟</li>
<li><strong>Privacy/Compliance:</strong> چه داده‌ای به provider می‌رود و سیاست نگهداری/منطقه‌ی داده چیست؟</li>
<li><strong>Reliability:</strong> rate limit، timeout، retry، SLA و fallback چگونه مدیریت می‌شوند؟</li>
<li><strong>Portability:</strong> وابستگی به API و featureهای اختصاصی provider چقدر است؟</li>
</ul>

<h2 dir="rtl" align="right">۱۱. مثال معماری در .NET</h2>
<p dir="rtl" align="right">بهتر است Controller مستقیماً به SDK یک provider قفل نشود. یک abstraction در لایه‌ی application تعریف کنید و adapterهای provider را در infrastructure قرار دهید. این کار تست، fallback و تغییر مدل را ساده‌تر می‌کند.</p>

<pre dir="ltr" align="left"><code>public interface IChatModel
{
    Task&lt;ModelResponse&gt; GenerateAsync(
        ModelRequest request,
        CancellationToken cancellationToken);
}

// Infrastructure
OpenAiChatModel : IChatModel
OtherProviderChatModel : IChatModel

// Application
AnswerQuestionHandler → IChatModel</code></pre>

<p dir="rtl" align="right">در production فقط abstraction کافی نیست؛ timeout، cancellation، retry کنترل‌شده، circuit breaker، rate limiting، telemetry، token/cost metrics، prompt/model version و evaluation نیز باید دیده شوند.</p>

<h2 dir="rtl" align="right">۱۲. محدودیت‌ها و ریسک‌ها</h2>
<ul dir="rtl" align="right">
<li><strong>Hallucination:</strong> پاسخ روان الزاماً پاسخ صحیح نیست.</li>
<li><strong>Stale knowledge:</strong> دانش آموزشی ممکن است قدیمی باشد.</li>
<li><strong>Non-determinism:</strong> یک ورودی می‌تواند خروجی‌های متفاوتی ایجاد کند.</li>
<li><strong>Prompt injection:</strong> متن خارجی ممکن است تلاش کند دستورهای سیستم را منحرف کند.</li>
<li><strong>Data leakage:</strong> ارسال اطلاعات حساس بدون طراحی privacy خطرناک است.</li>
<li><strong>Cost/latency:</strong> context و output بزرگ رایگان نیستند.</li>
<li><strong>Vendor/model drift:</strong> رفتار مدل یا سرویس می‌تواند با نسخه‌ها تغییر کند؛ regression eval لازم است.</li>
</ul>

<h2 dir="rtl" align="right">۱۳. اشتباه رایج: مدل بزرگ‌تر همیشه بهتر نیست</h2>
<p dir="rtl" align="right">برای classification ساده یا extraction ساختاریافته ممکن است یک مدل کوچک‌تر سریع‌تر و ارزان‌تر با کیفیت کافی باشد. معماری حرفه‌ای مدل را بر اساس <strong>quality × latency × cost × risk</strong> انتخاب می‌کند، نه صرفاً نام یا اندازه‌ی مدل.</p>

<h2 dir="rtl" align="right">۱۴. مثال تصمیم‌گیری برای سامانه‌ی کارگزاری</h2>
<p dir="rtl" align="right">فرض کنید کاربر می‌پرسد «آخرین وضعیت سفارش من چیست؟». این داده نباید از حافظه‌ی مدل پاسخ داده شود. Backend هویت و مجوز را بررسی می‌کند، Order API را فراخوانی می‌کند و نتیجه را در اختیار مدل می‌گذارد تا در صورت نیاز توضیح انسانی تولید کند. در مقابل، برای «مفهوم سفارش محدود چیست؟» ممکن است دانش عمومی مدل کافی باشد؛ البته پاسخ حساس مالی همچنان به guardrail و منابع معتبر نیاز دارد.</p>

<h2 dir="rtl" align="right">خلاصه‌ی ذهنی</h2>
<pre dir="ltr" align="left"><code>Need AI capability?
      ↓
Choose a pre-trained model
      ↓
Is instruction enough? ── Yes → Prompt
      │ No
      ↓
Need private/fresh knowledge? ── Yes → RAG / Tools
      │
Need consistent specialized behavior? → Consider Fine-tuning
      ↓
Evaluate quality + latency + cost + safety
      ↓
Observe continuously in production</code></pre>

<h2 dir="rtl" align="right">فلش‌کارت‌ها</h2>
<ul dir="rtl" align="right">
<li><strong>Pre-trained Model؟</strong> مدلی که پیش از استفاده‌ی محصول روی داده‌ی گسترده آموزش دیده است.</li>
<li><strong>Training vs Inference؟</strong> Training پارامترها را یاد می‌دهد/تغییر می‌دهد؛ Inference از پارامترهای موجود برای تولید خروجی استفاده می‌کند.</li>
<li><strong>Context Window؟</strong> بودجه‌ی context فعال مدل، معمولاً بر حسب token؛ حافظه‌ی دائمی نیست.</li>
<li><strong>Knowledge Cut-off؟</strong> مرز زمانی تقریبی دانش حاصل از آموزش، نه محدودیت اندازه‌ی prompt.</li>
<li><strong>RAG یا Fine-tuning؟</strong> RAG عمدتاً دانش بیرونی/تازه را هنگام inference می‌آورد؛ fine-tuning عمدتاً رفتار مدل را با نمونه‌های آموزشی تخصصی‌تر می‌کند.</li>
<li><strong>چرا abstraction در Backend؟</strong> کاهش coupling به provider و ساده‌شدن test، fallback و migration.</li>
</ul>

<h2 dir="rtl" align="right">آزمون پایان درس</h2>
<ol dir="rtl" align="right">
<li>تفاوت pre-training و inference چیست؟</li>
<li>چرا context window را نباید با knowledge cut-off یکی دانست؟</li>
<li>برای پاسخ به «وضعیت فعلی سفارش من» مدل به چه چیزی نیاز دارد؟ الف) فقط prompt بهتر ب) API/tool با authorization ج) fine-tuning د) context بزرگ‌تر</li>
<li>اگر مدل دانش اختصاصی شرکت را ندارد، اولین گزینه‌ی معماری معمولاً چیست؟ الف) آموزش از صفر ب) RAG ج) GPU بیشتر د) temperature بالاتر</li>
<li>دو مزیت و دو هزینه‌ی self-hosting یک مدل open-weight را نام ببرید.</li>
<li>چرا بزرگ‌ترین مدل الزاماً بهترین انتخاب production نیست؟</li>
<li>در معماری .NET چرا بهتر است application به interface مدل وابسته باشد؟</li>
<li>سه metric که برای مقایسه‌ی دو مدل در production ثبت می‌کنید چیست؟</li>
</ol>

<details dir="rtl"><summary><strong>پاسخ کوتاه آزمون</strong></summary>
<p>۱) Training وزن‌ها را یاد می‌دهد؛ inference با وزن‌های موجود پاسخ می‌سازد. ۲) اولی ظرفیت context جاری و دومی زمان دانش آموزشی است. ۳) ب. ۴) ب. ۵) کنترل/حریم خصوصی و انعطاف deployment؛ در برابر زیرساخت GPU و عملیات/نگهداری. ۶) trade-off کیفیت، latency، هزینه و ریسک. ۷) کاهش coupling و امکان test/fallback/migration. ۸) مثلاً quality/eval score، p95 latency و cost per request؛ error rate نیز مهم است.</p>
</details>

</div>
