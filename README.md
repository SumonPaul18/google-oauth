# Using Google OAuth for Sign UP / Sign In using users Google Account

#### 1. Google OAuth Credentials কিভাবে পাবেন:
Google OAuth Credentials পেতে নিচের ধাপগুলো অনুসরণ করুন:

1. **Google Cloud Console এ যান**: Google Cloud Console এ যান এবং আপনার Google অ্যাকাউন্ট দিয়ে লগইন করুন।

2. **প্রজেক্ট তৈরি করুন**: একটি নতুন প্রজেক্ট তৈরি করুন বা একটি বিদ্যমান প্রজেক্ট নির্বাচন করুন।

3. **OAuth Consent Screen সেটআপ করুন**:
    - **Navigation Menu** থেকে **APIs & Services** > **OAuth consent screen** এ যান।
    - **User Type** নির্বাচন করুন (যেমন, External) এবং **Create** এ ক্লিক করুন।
    - প্রয়োজনীয় তথ্য পূরণ করুন এবং **Save and Continue** করুন।

4. **Credentials তৈরি করুন**:
    - **Navigation Menu** থেকে **APIs & Services** > **Credentials** এ যান।
    - **Create Credentials** এ ক্লিক করুন এবং **OAuth 2.0 Client IDs** নির্বাচন করুন।
    - **Application type** হিসেবে **Web application** নির্বাচন করুন।
    - **Authorized redirect URIs** এ আপনার অ্যাপের রিডাইরেক্ট URI যোগ করুন (যেমন, `http://localhost:5000/authorize`).
    - **Create** এ ক্লিক করুন।

5. **Credentials ডাউনলোড করুন**:
    - আপনার ক্লায়েন্ট আইডি এবং ক্লায়েন্ট সিক্রেট দেখতে পাবেন। এগুলো ডাউনলোড করুন এবং `.env` ফাইলে যোগ করুন।

#### ৩. .env ফাইল তৈরি করুন:
আপনার প্রজেক্ট ডিরেক্টরিতে একটি `.env` ফাইল তৈরি করুন এবং নিচের মতো করে সেট করুন:
```
SECRET_KEY=your_generated_secret_key
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
```

### উদাহরণ:
```plaintext
SECRET_KEY=b'\x9a\x1d\x8b\x1e\x8f\x1d\x8b\x1e\x8f\x1d\x8b\x1e\x8f\x1d\x8b\x1e\x8f\x1d\x8b\x1e\x8f'
GOOGLE_CLIENT_ID=170052710339-jc3r30g31cso6kenoqp8dasvnooagpdn.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=w5_yb4k9jWGOqS5joHiShOz4
```

এখন আপনার অ্যাপ্লিকেশনটি চালু করুন এবং Google OAuth ব্যবহার করে লগইন করতে পারবেন। যদি কোনো প্রশ্ন থাকে বা কোনো অংশে সাহায্য প্রয়োজন হয়, আমাকে জানাতে পারেন!

---

#### Google OAuth Credentials এর জন্য কি কোনো টাকা লাগবে

Google OAuth Credentials সাধারণত বিনামূল্যে পাওয়া যায়। আপনি Google API Console থেকে OAuth 2.0 credentials (যেমন, client ID এবং client secret) তৈরি করতে পারেন বিনামূল্যে। তবে, যদি আপনার অ্যাপ্লিকেশনটি অনেক বেশি ব্যবহারকারী বা জটিল ফিচার ব্যবহার করে, তাহলে কিছু খরচ হতে পারে।

### বিনামূল্যে ব্যবহারের সীমা:
- **বিনামূল্যে ব্যবহার**: বেশিরভাগ সাধারণ ব্যবহারের জন্য, যেমন লগইন এবং প্রাথমিক ডেটা অ্যাক্সেস, Google OAuth বিনামূল্যে।
- **প্রিমিয়াম ফিচার**: যদি আপনি Google Identity Platform এর প্রিমিয়াম ফিচার ব্যবহার করেন, যেমন ফোন বা মাল্টি-ফ্যাক্টর অথেন্টিকেশন, তাহলে কিছু খরচ হতে পারে¹(https://cloud.google.com/identity-platform/pricing).

### খরচের বিবরণ:
- [Google Identity Platform Pricing](https://cloud.google.com/identity-platform/pricing)
আপনার যদি আরও বিস্তারিত তথ্য বা নির্দিষ্ট প্রশ্ন থাকে, আমাকে জানাতে পারেন!


