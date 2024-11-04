# جزوه: ایجاد چت بات با استفاده از مدل‌های OpenAI

## بخش اول: چت بات بدون طبقه‌بندی نیت

در این بخش، یک کد ساده برای ایجاد یک چت بات با استفاده از کتابخانه OpenAI ارائه می‌شود. این کد به شما امکان می‌دهد به راحتی با مدل‌های OpenAI چت کنید.

### کد:

```python
import openai

# تنظیم کلید API خود
openai.api_key = 'YOUR_API_KEY'

# حلقه چت ساده
while True:
    user_input = input("شما: ")
    
    # اگر کاربر "خروج" وارد کند، برنامه پایان می‌یابد
    if user_input.lower() == "خروج":
        print("چت پایان یافت.")
        break
    
    # درخواست به مدل OpenAI
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": user_input}]
    )
    
    # استخراج پاسخ از مدل
    answer = response['choices'][0]['message']['content'].strip()
    
    # نمایش پاسخ
    print("هوش مصنوعی:", answer)
```

### توضیحات کد:

1. **وارد کردن کتابخانه**: 
   - `import openai` - این خط کتابخانه OpenAI را وارد می‌کند تا بتوانیم از امکانات آن استفاده کنیم.

2. **تنظیم کلید API**: 
   - `openai.api_key = 'YOUR_API_KEY'` - این خط کلید API شما را تنظیم می‌کند که برای احراز هویت با OpenAI ضروری است.

3. **حلقه چت**: 
   - `while True:` - ایجاد یک حلقه بی‌پایان که تا زمانی که کاربر تصمیم به خروج نگیرد ادامه دارد.

4. **بررسی خروج**: 
   - `if user_input.lower() == "خروج":` - اگر کاربر کلمه "خروج" را وارد کند، برنامه به پایان می‌رسد.

5. **درخواست به مدل**: 
   - `response = openai.ChatCompletion.create(...)` - این خط ورودی کاربر را به مدل gpt-3.5-turbo ارسال می‌کند و پاسخ را دریافت می‌کند.

6. **نمایش پاسخ**: 
   - `print("هوش مصنوعی:", answer)` - این خط پاسخ مدل را چاپ می‌کند.

### نحوه استفاده:

- کافیست کد را اجرا کنید و با هوش مصنوعی چت کنید.
- برای پایان دادن به چت، کافیست "خروج" را وارد کنید.

---

## بخش دوم: چت بات با طبقه بندی به روش غیرمستقیم برای نسخه‌های قدیمی‌تر

در این بخش، کدی برای یک دستیار هوش مصنوعی ارائه می‌شود که به صورت خودکار ورودی‌های مختلف را تجزیه و تحلیل می‌کند.

### 1. نصب کتابخانه‌های مورد نیاز

قبل از اجرای کد، مطمئن شوید که کتابخانه‌های OpenAI و pandas نصب شده‌اند:

```bash
pip install openai pandas
```

### 2. کد کامل برای دستیار هوش مصنوعی

```python
import openai
import pandas as pd

# تنظیم کلید API خود
openai.api_key = 'YOUR_API_KEY'

# تابعی برای پردازش ورودی کاربر و ارائه پاسخ
def process_user_input(user_input):
    # پرامپت برای مدل
    prompt = f"You are a helpful assistant for workplace tasks. Please analyze the following request and provide a suitable response:nnUser request: '{user_input}'nResponse:"
    
    # درخواست به مدل OpenAI
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[{"role": "user", "content": prompt}]
    )
    
    # استخراج پاسخ از مدل
    answer = response['choices'][0]['message']['content'].strip()
    return answer

# ورودی‌های آزمایشی
user_inputs = [
    "لطفا یک یادآوری برای جلسه فردا ساعت 10 صبح تنظیم کن.",
    "چطور می‌توانم یک گزارش ماهانه تهیه کنم؟",
    "می‌خواهم به تیمم درباره پروژه جدید اطلاع دهم.",
    "لطفا اطلاعات بیشتری درباره مزایای کار در این شرکت بده.",
    "چگونه می‌توانم با مشتریان ارتباط برقرار کنم؟"
]

# ایجاد DataFrame برای ذخیره نتایج
results = pd.DataFrame(columns=["User Input", "Response"])

# پردازش ورودی‌ها و دریافت پاسخ
for input_text in user_inputs:
    response = process_user_input(input_text)
    results = results.append({"User Input": input_text, "Response": response}, ignore_index=True)

# نمایش نتایج
print(results)
```

### توضیحات کد:

1. **نصب کتابخانه‌ها**: 
   - مطمئن شوید که کتابخانه‌های OpenAI و pandas نصب شده‌اند.

2. **تنظیم کلید API**: 
   - `openai.api_key = 'YOUR_API_KEY'` - مشابه بخش قبلی، کلید API شما تنظیم می‌شود.

3. **تابع process_user_input**: 
   - این تابع ورودی کاربر را دریافت کرده و با استفاده از پرامپت مناسب، درخواست را تجزیه و تحلیل و پاسخ می‌دهد.

4. **ورودی‌های آزمایشی**: 
   - تعدادی ورودی نمونه برای آزمایش دستیار ایجاد شده‌اند.

5. **پردازش ورودی‌ها**: 
   - ورودی‌ها پردازش شده و پاسخ‌ها در یک DataFrame ذخیره می‌شوند.

6. **نمایش نتایج**: 
   - در انتها، نتایج شامل ورودی‌های کاربر و پاسخ‌های مربوطه نمایش داده می‌شوند.

### نکات پایانی:

- اطمینان حاصل کنید که کلید API شما معتبر است و محدودیت‌های مربوط به استفاده از مدل OpenAI را رعایت کنید.
- می‌توانید ورودی‌ها و درخواست‌های بیشتری اضافه کنید تا دستیار شما قابلیت‌های بیشتری داشته باشد.

---

## بخش سوم: چت بات با طبقه بندی مستقیم برای نسخه‌های به‌روز شده

برای استفاده از نسخه ۴.۰ مدل‌های OpenAI، از کدی مشابه کد اول که از `openai.ChatCompletion.create` استفاده می‌کند، بهره ببرید.

### کد:

```python
import openai
import pandas as pd

# تنظیم کلید API خود
openai.api_key = 'YOUR_API_KEY'

# تابعی برای پردازش ورودی کاربر و ارائه پاسخ
def process_user_input(user_input):
    # پرامپت برای مدل
    prompt = f"You are a helpful assistant for workplace tasks. Please analyze the following request and provide a suitable response:nnUser request: '{user_input}'nResponse:"
    
    # درخواست به مدل OpenAI
    response = openai.ChatCompletion.create(
        model="gpt-4",  # تغییر به مدل GPT-4
        messages=[{"role": "user", "content": prompt}]
    )
    
    # استخراج پاسخ از مدل
    answer = response['choices'][0]['message']['content'].strip()
    return answer

# ورودی‌های آزمایشی
user_inputs = [
    "لطفا یک یادآوری برای جلسه فردا ساعت 10 صبح تنظیم کن.",
    "چطور می‌توانم یک گزارش ماهانه تهیه کنم؟",
    "می‌خواهم به تیمم درباره پروژه جدید اطلاع دهم.",
    "لطفا اطلاعات بیشتری درباره مزایای کار در این شرکت بده.",
    "چگونه می‌توانم با مشتریان ارتباط برقرار کنم؟"
]

# ایجاد DataFrame برای ذخیره نتایج
results = pd.DataFrame(columns=["User Input", "Response"])

# پردازش ورودی‌ها و دریافت پاسخ
for input_text in user_inputs:
    response = process_user_input(input_text)
    results = results.append({"User Input": input_text, "Response": response}, ignore_index=True)

# نمایش نتایج
print(results)
```

### نکات:

1. **مدل**: 
   - در این کد، مدل به "gpt-4" تغییر داده شده است.

2. **استفاده از ChatCompletion**: 
   - این روش به شما اجازه می‌دهد تا از قابلیت‌های جدیدتر و تعاملات پیچیده‌تری بهره‌مند شوید.

3. **سازگاری با ورودی‌ها**: 
   - این کد به خوبی با ورودی‌های متنوع کار می‌کند و پاسخ‌های مفیدی ارائه می‌دهد.

---

این جزوه به شما کمک می‌کند تا با استفاده از کدهای ارائه شده، چت بات‌های خود را بسازید و از قابلیت‌های مختلف مدل‌های OpenAI بهره‌مند شوید.
