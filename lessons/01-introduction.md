<div dir="rtl" align="right">

<h1 dir="rtl" align="right">روز ۱ — Introduction</h1>

<h2 dir="rtl" align="right">هدف درس</h2>

<p dir="rtl" align="right">در پایان این بخش باید بتوانیم جایگاه مفاهیم اصلی <span dir="ltr">AI Engineering</span> را در یک سیستم واقعی تشخیص دهیم و تفاوت میان <span dir="ltr">AI Engineer</span> و <span dir="ltr">ML Engineer</span> را توضیح دهیم.</p>

<h2 dir="rtl" align="right"><span dir="ltr">AI Engineer</span> چیست؟</h2>

<p dir="rtl" align="right"><span dir="ltr">AI Engineer</span> معمولاً مهندسی است که قابلیت‌های مدل‌های هوش مصنوعی، به‌خصوص مدل‌های از پیش‌آموزش‌دیده، را به یک قابلیت واقعی و قابل‌اعتماد در محصول نرم‌افزاری تبدیل می‌کند.</p>

<p dir="rtl" align="right">تمرکز این نقش معمولاً شامل موارد زیر است:</p>

<ul dir="rtl" align="right">
  <li>Integration</li>
  <li>Orchestration</li>
  <li>Data Flow</li>
  <li>Reliability</li>
  <li>Evaluation</li>
  <li>Security</li>
  <li>Monitoring</li>
  <li>Cost Control</li>
  <li>Productization</li>
</ul>

<p dir="rtl" align="right">مدل هوش مصنوعی فقط یکی از اجزای سیستم است.</p>

<p dir="rtl" align="right">نمونه‌ی معماری:</p>

<pre dir="ltr" align="left"><code>Client
  ↓
Backend API
  ↓
Retrieval / Tools
  ↓
LLM
  ↓
Validation
  ↓
Response</code></pre>

<h2 dir="rtl" align="right"><span dir="ltr">AI Engineer</span> در برابر <span dir="ltr">ML Engineer</span></h2>

<h3 dir="rtl" align="right"><span dir="ltr">AI Engineer</span></h3>

<p dir="rtl" align="right">بیشتر روی استفاده از مدل‌های آماده و تبدیل آن‌ها به قابلیت محصول تمرکز دارد:</p>

<ul dir="rtl" align="right">
  <li>استفاده از <span dir="ltr">API</span> و <span dir="ltr">SDK</span> مدل‌ها</li>
  <li>ساخت <span dir="ltr">RAG</span></li>
  <li>ساخت <span dir="ltr">Agent</span></li>
  <li><span dir="ltr">Prompt Engineering</span></li>
  <li><span dir="ltr">Evaluation</span></li>
  <li><span dir="ltr">Monitoring</span></li>
  <li><span dir="ltr">Integration</span> با <span dir="ltr">Backend</span></li>
</ul>

<h3 dir="rtl" align="right"><span dir="ltr">ML Engineer</span></h3>

<p dir="rtl" align="right">معمولاً به چرخه‌ی ساخت و اجرای مدل نزدیک‌تر است:</p>

<ul dir="rtl" align="right">
  <li>Data Pipeline</li>
  <li>Training</li>
  <li>Experimentation</li>
  <li>Feature Engineering</li>
  <li>Model Evaluation</li>
  <li>Model Serving</li>
  <li>Optimization</li>
</ul>

<p dir="rtl" align="right">مرز این دو نقش کاملاً صلب نیست و در بعضی تیم‌ها هم‌پوشانی زیادی دارند.</p>

<h2 dir="rtl" align="right"><span dir="ltr">AI</span> در برابر <span dir="ltr">AGI</span></h2>

<h3 dir="rtl" align="right"><span dir="ltr">AI</span></h3>

<p dir="rtl" align="right">سامانه‌هایی که وظایف مشخصی مانند تولید متن، ترجمه، تشخیص تصویر یا <span dir="ltr">recommendation</span> را انجام می‌دهند.</p>

<h3 dir="rtl" align="right"><span dir="ltr">AGI</span></h3>

<p dir="rtl" align="right"><span dir="ltr">Artificial General Intelligence</span> مفهومی برای هوش عمومی با توانایی قابل‌انتقال میان حوزه‌های مختلف است.</p>

<p dir="rtl" align="right">در این رودمپ <span dir="ltr">AGI</span> بیشتر یک مفهوم زمینه‌ای است.</p>

<h2 dir="rtl" align="right"><span dir="ltr">LLM</span> چیست؟</h2>

<p dir="rtl" align="right"><span dir="ltr">LLM</span> مخفف <span dir="ltr">Large Language Model</span> است.</p>

<p dir="rtl" align="right">مدل زبانی بزرگ روی حجم بزرگی از داده آموزش می‌بیند و هنگام تولید متن، با توجه به <span dir="ltr">context</span> موجود، توکن‌های بعدی را مدل‌سازی و تولید می‌کند.</p>

<p dir="rtl" align="right">یک <span dir="ltr">LLM</span> را نباید مانند یک <span dir="ltr">Database</span> در نظر گرفت. خروجی آن تولید می‌شود و همین موضوع یکی از دلایل امکان <span dir="ltr">Hallucination</span> است.</p>

<h2 dir="rtl" align="right"><span dir="ltr">Training</span> و <span dir="ltr">Inference</span></h2>

<h3 dir="rtl" align="right"><span dir="ltr">Training</span></h3>

<p dir="rtl" align="right">مرحله‌ای که پارامترهای مدل با استفاده از داده و فرایند بهینه‌سازی یاد گرفته یا تنظیم می‌شوند.</p>

<pre dir="ltr" align="left"><code>Data → Training → Model</code></pre>

<h3 dir="rtl" align="right"><span dir="ltr">Inference</span></h3>

<p dir="rtl" align="right">مرحله‌ی استفاده از مدل آموزش‌دیده برای تولید خروجی روی ورودی جدید.</p>

<pre dir="ltr" align="left"><code>Prompt → Trained Model → Response</code></pre>

<p dir="rtl" align="right">هنگام استفاده از یک <span dir="ltr">API</span> مدل، معمولاً در حال انجام <span dir="ltr">Inference</span> هستیم.</p>

<h2 dir="rtl" align="right"><span dir="ltr">Embedding</span> چیست؟</h2>

<p dir="rtl" align="right"><span dir="ltr">Embedding</span> یک نمایش عددی برداری از محتوا است.</p>

<pre dir="ltr" align="left"><code>Text → [0.12, -0.42, 0.91, ...]</code></pre>

<p dir="rtl" align="right"><span dir="ltr">Embedding</span> کمک می‌کند شباهت معنایی میان محتواها قابل محاسبه شود.</p>

<p dir="rtl" align="right">از این قابلیت برای مواردی مانند <span dir="ltr">Semantic Search</span> استفاده می‌شود.</p>

<h2 dir="rtl" align="right"><span dir="ltr">Vector Database</span> چیست؟</h2>

<p dir="rtl" align="right"><span dir="ltr">Vector Database</span> برای ذخیره، <span dir="ltr">index</span> و جست‌وجوی <span dir="ltr">embedding</span>ها بهینه شده است.</p>

<p dir="rtl" align="right">الگوی ساده:</p>

<pre dir="ltr" align="left"><code>Document
   ↓
Embedding
   ↓
Vector Database</code></pre>

<p dir="rtl" align="right">و هنگام جست‌وجو:</p>

<pre dir="ltr" align="left"><code>Question
   ↓
Embedding
   ↓
Similarity Search
   ↓
Relevant Documents</code></pre>

<h2 dir="rtl" align="right"><span dir="ltr">RAG</span> چیست؟</h2>

<p dir="rtl" align="right"><span dir="ltr">RAG</span> مخفف <span dir="ltr">Retrieval-Augmented Generation</span> است.</p>

<p dir="rtl" align="right">در <span dir="ltr">RAG</span> قبل از تولید پاسخ، اطلاعات مرتبط از یک منبع بیرونی بازیابی می‌شوند و همراه سؤال در اختیار مدل قرار می‌گیرند.</p>

<pre dir="ltr" align="left"><code>User Question
      ↓
Embedding
      ↓
Vector Search
      ↓
Relevant Documents
      ↓
Prompt + Context
      ↓
LLM
      ↓
Answer</code></pre>

<p dir="rtl" align="right"><span dir="ltr">RAG</span> یکی از روش‌های اصلی اتصال <span dir="ltr">LLM</span> به دانش اختصاصی یا به‌روز یک سازمان است.</p>

<h2 dir="rtl" align="right"><span dir="ltr">AI Agent</span> چیست؟</h2>

<p dir="rtl" align="right">یک <span dir="ltr">Chatbot</span> ساده معمولاً چنین مسیری دارد:</p>

<pre dir="ltr" align="left"><code>Input → LLM → Text</code></pre>

<p dir="rtl" align="right">اما <span dir="ltr">Agent</span> می‌تواند برای رسیدن به هدف از <span dir="ltr">Tool</span> یا <span dir="ltr">Function</span> استفاده کند.</p>

<pre dir="ltr" align="left"><code>User
 ↓
LLM
 ↓
Tool Call
 ↓
Backend API
 ↓
Tool Result
 ↓
LLM
 ↓
Final Answer</code></pre>

<p dir="rtl" align="right">نمونه:</p>

<p dir="rtl" align="right">کاربر می‌گوید:</p>

<blockquote dir="rtl" align="right">وضعیت سفارش 12532 را بررسی کن.</blockquote>

<p dir="rtl" align="right"><span dir="ltr">Agent</span> می‌تواند تصمیم بگیرد تابع زیر را اجرا کند:</p>

<pre dir="ltr" align="left"><code>GetOrderStatus(12532)</code></pre>

<h2 dir="rtl" align="right"><span dir="ltr">Prompt Engineering</span></h2>

<p dir="rtl" align="right"><span dir="ltr">Prompt Engineering</span> یعنی طراحی ورودی مدل به‌گونه‌ای که موارد زیر مشخص باشند:</p>

<ul dir="rtl" align="right">
  <li>Role</li>
  <li>Goal</li>
  <li>Context</li>
  <li>Constraints</li>
  <li>Output Format</li>
</ul>

<p dir="rtl" align="right"><span dir="ltr">Prompt</span> خوب مهم است، اما جای موارد زیر را نمی‌گیرد:</p>

<ul dir="rtl" align="right">
  <li>Architecture</li>
  <li>Validation</li>
  <li>Security</li>
  <li>Data Quality</li>
  <li>Observability</li>
</ul>

<h2 dir="rtl" align="right">تصویر کلی</h2>

<p dir="rtl" align="right">یک سیستم <span dir="ltr">AI</span> واقعی می‌تواند چنین ساختاری داشته باشد:</p>

<pre dir="ltr" align="left"><code>User
 ↓
ASP.NET Core API
 ↓
Embedding Model
 ↓
Vector Database
 ↓
Relevant Documents
 ↓
Prompt + Retrieved Context
 ↓
LLM
 ↓
Tool Call / Agent
 ↓
Validation
 ↓
Response</code></pre>

<h2 dir="rtl" align="right">نکات کلیدی مرور</h2>

<ul dir="rtl" align="right">
  <li><span dir="ltr">Training</span> یعنی یادگیری مدل؛ <span dir="ltr">Inference</span> یعنی استفاده از مدل آماده.</li>
  <li><span dir="ltr">Embedding</span> محتوا را به <span dir="ltr">Vector</span> تبدیل می‌کند.</li>
  <li><span dir="ltr">Vector Database</span> امکان <span dir="ltr">Similarity Search</span> سریع را فراهم می‌کند.</li>
  <li><span dir="ltr">RAG</span> دانش بیرونی را قبل از <span dir="ltr">Generation</span> وارد <span dir="ltr">Context</span> می‌کند.</li>
  <li><span dir="ltr">Agent</span> می‌تواند <span dir="ltr">Tool</span> یا <span dir="ltr">Function</span> اجرا کند.</li>
  <li><span dir="ltr">Prompt Engineering</span> فقط یکی از اجزای سیستم <span dir="ltr">AI production</span> است.</li>
  <li><span dir="ltr">AI Engineer</span> بیش از خود مدل، با تبدیل قابلیت مدل به محصول واقعی سروکار دارد.</li>
</ul>

<h2 dir="rtl" align="right">فلش‌کارت‌ها</h2>

<h3 dir="rtl" align="right"><span dir="ltr">Training</span> در برابر <span dir="ltr">Inference</span>؟</h3>

<p dir="rtl" align="right"><strong>Training:</strong> یادگیری یا تنظیم پارامترهای مدل.</p>
<p dir="rtl" align="right"><strong>Inference:</strong> استفاده از مدل آموزش‌دیده روی ورودی جدید.</p>

<h3 dir="rtl" align="right"><span dir="ltr">Embedding</span> چه می‌کند؟</h3>

<p dir="rtl" align="right">محتوا را به نمایش عددی برداری تبدیل می‌کند تا شباهت معنایی قابل محاسبه باشد.</p>

<h3 dir="rtl" align="right"><span dir="ltr">RAG</span> چه کاری انجام می‌دهد؟</h3>

<p dir="rtl" align="right">اطلاعات مرتبط را از منبع خارجی بازیابی کرده و پیش از <span dir="ltr">Generation</span> به <span dir="ltr">Context</span> مدل اضافه می‌کند.</p>

<h3 dir="rtl" align="right"><span dir="ltr">Agent</span> چه چیزی فراتر از <span dir="ltr">Chatbot</span> دارد؟</h3>

<p dir="rtl" align="right">توانایی فراخوانی <span dir="ltr">Tool</span> یا <span dir="ltr">Function</span> و انجام چند مرحله برای رسیدن به یک هدف.</p>

</div>
