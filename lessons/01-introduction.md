<div dir="rtl">

# روز ۱ — Introduction

## هدف درس

در پایان این بخش باید بتوانیم جایگاه مفاهیم اصلی AI Engineering را در یک سیستم واقعی تشخیص دهیم و تفاوت میان AI Engineer و ML Engineer را توضیح دهیم.

## AI Engineer چیست؟

AI Engineer معمولاً مهندسی است که قابلیت‌های مدل‌های هوش مصنوعی، به‌خصوص مدل‌های از پیش‌آموزش‌دیده، را به یک قابلیت واقعی و قابل‌اعتماد در محصول نرم‌افزاری تبدیل می‌کند.

تمرکز این نقش معمولاً شامل موارد زیر است:

- Integration
- Orchestration
- Data Flow
- Reliability
- Evaluation
- Security
- Monitoring
- Cost Control
- Productization

مدل هوش مصنوعی فقط یکی از اجزای سیستم است.

نمونه‌ی معماری:

```text
Client
  ↓
Backend API
  ↓
Retrieval / Tools
  ↓
LLM
  ↓
Validation
  ↓
Response
```

## AI Engineer در برابر ML Engineer

### AI Engineer

بیشتر روی استفاده از مدل‌های آماده و تبدیل آن‌ها به قابلیت محصول تمرکز دارد:

- استفاده از API و SDK مدل‌ها
- ساخت RAG
- ساخت Agent
- Prompt Engineering
- Evaluation
- Monitoring
- Integration با Backend

### ML Engineer

معمولاً به چرخه‌ی ساخت و اجرای مدل نزدیک‌تر است:

- Data Pipeline
- Training
- Experimentation
- Feature Engineering
- Model Evaluation
- Model Serving
- Optimization

مرز این دو نقش کاملاً صلب نیست و در بعضی تیم‌ها هم‌پوشانی زیادی دارند.

## AI در برابر AGI

### AI

سامانه‌هایی که وظایف مشخصی مانند تولید متن، ترجمه، تشخیص تصویر یا recommendation را انجام می‌دهند.

### AGI

Artificial General Intelligence مفهومی برای هوش عمومی با توانایی قابل‌انتقال میان حوزه‌های مختلف است.

در این رودمپ AGI بیشتر یک مفهوم زمینه‌ای است.

## LLM چیست؟

LLM مخفف Large Language Model است.

مدل زبانی بزرگ روی حجم بزرگی از داده آموزش می‌بیند و هنگام تولید متن، با توجه به context موجود، توکن‌های بعدی را مدل‌سازی و تولید می‌کند.

یک LLM را نباید مانند یک Database در نظر گرفت. خروجی آن تولید می‌شود و همین موضوع یکی از دلایل امکان Hallucination است.

## Training و Inference

### Training

مرحله‌ای که پارامترهای مدل با استفاده از داده و فرایند بهینه‌سازی یاد گرفته یا تنظیم می‌شوند.

```text
Data → Training → Model
```

### Inference

مرحله‌ی استفاده از مدل آموزش‌دیده برای تولید خروجی روی ورودی جدید.

```text
Prompt → Trained Model → Response
```

هنگام استفاده از یک API مدل، معمولاً در حال انجام Inference هستیم.

## Embedding چیست؟

Embedding یک نمایش عددی برداری از محتوا است.

مثلاً:

```text
Text → [0.12, -0.42, 0.91, ...]
```

Embedding کمک می‌کند شباهت معنایی میان محتواها قابل محاسبه شود.

از این قابلیت برای مواردی مانند Semantic Search استفاده می‌شود.

## Vector Database چیست؟

Vector Database برای ذخیره، index و جست‌وجوی embeddingها بهینه شده است.

الگوی ساده:

```text
Document
   ↓
Embedding
   ↓
Vector Database
```

و هنگام جست‌وجو:

```text
Question
   ↓
Embedding
   ↓
Similarity Search
   ↓
Relevant Documents
```

## RAG چیست؟

RAG مخفف Retrieval-Augmented Generation است.

در RAG قبل از تولید پاسخ، اطلاعات مرتبط از یک منبع بیرونی بازیابی می‌شوند و همراه سؤال در اختیار مدل قرار می‌گیرند.

```text
User Question
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
Answer
```

RAG یکی از روش‌های اصلی اتصال LLM به دانش اختصاصی یا به‌روز یک سازمان است.

## AI Agent چیست؟

یک Chatbot ساده معمولاً چنین مسیری دارد:

```text
Input → LLM → Text
```

اما Agent می‌تواند برای رسیدن به هدف از Tool یا Function استفاده کند.

مثلاً:

```text
User
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
Final Answer
```

نمونه:

کاربر می‌گوید:

> وضعیت سفارش 12532 را بررسی کن.

Agent می‌تواند تصمیم بگیرد تابع زیر را اجرا کند:

```text
GetOrderStatus(12532)
```

## Prompt Engineering

Prompt Engineering یعنی طراحی ورودی مدل به‌گونه‌ای که موارد زیر مشخص باشند:

- Role
- Goal
- Context
- Constraints
- Output Format

Prompt خوب مهم است، اما جای موارد زیر را نمی‌گیرد:

- Architecture
- Validation
- Security
- Data Quality
- Observability

## تصویر کلی

یک سیستم AI واقعی می‌تواند چنین ساختاری داشته باشد:

```text
User
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
Response
```

## نکات کلیدی مرور

- Training یعنی یادگیری مدل؛ Inference یعنی استفاده از مدل آماده.
- Embedding محتوا را به Vector تبدیل می‌کند.
- Vector Database امکان Similarity Search سریع را فراهم می‌کند.
- RAG دانش بیرونی را قبل از Generation وارد Context می‌کند.
- Agent می‌تواند Tool یا Function اجرا کند.
- Prompt Engineering فقط یکی از اجزای سیستم AI production است.
- AI Engineer بیش از خود مدل، با تبدیل قابلیت مدل به محصول واقعی سروکار دارد.

## فلش‌کارت‌ها

### Training vs Inference؟

**Training:** یادگیری یا تنظیم پارامترهای مدل.

**Inference:** استفاده از مدل آموزش‌دیده روی ورودی جدید.

### Embedding چه می‌کند؟

محتوا را به نمایش عددی برداری تبدیل می‌کند تا شباهت معنایی قابل محاسبه باشد.

### RAG چه کاری انجام می‌دهد؟

اطلاعات مرتبط را از منبع خارجی بازیابی کرده و پیش از Generation به Context مدل اضافه می‌کند.

### Agent چه چیزی فراتر از Chatbot دارد؟

توانایی فراخوانی Tool یا Function و انجام چند مرحله برای رسیدن به یک هدف.

</div>
