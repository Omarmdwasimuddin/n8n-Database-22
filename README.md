# 🗄️ n8n — Database (Supabase) Integration Guide

> n8n এ Supabase Database সংযুক্ত করে Data Insert করার ধাপে ধাপে গাইড।

---

## 📊 Workflow Overview

```
Manual Trigger
      │
      ▼
Edit Fields (Set)
[Name = "Wasim"]
      │
      ▼
Supabase: Create a row
[Employee Table এ Data Insert]
      │
      ▼
Supabase Dashboard এ Data দেখো ✅
```

---

## 🌐 Supabase সেটআপ

### ✅ ধাপ ১ — Supabase Account ও Project তৈরি করো

- 🔗 [supabase.com](https://supabase.com) ভিজিট করো
- **Sign In** করো
- Dashboard এ যাও
- **"New project"** এ ক্লিক করো
- নিচের তথ্য দাও:

| Field | উদাহরণ |
|-------|---------|
| **Project Name** | `n8n-project` |
| **Database Password** | `DkDdWl9sTYFwmCKI` |

> ⚠️ Password টি নিরাপদ জায়গায় রেখে দাও — পরে দরকার হবে।

- **"Create new project"** বাটনে ক্লিক করো

---

### ✅ ধাপ ২ — Table তৈরি করো

- Left Sidebar থেকে **"Table Editor"** এ ক্লিক করো
- **"Create a table"** এ ক্লিক করো
- **Name** দাও: `Employee`
- **Save** বাটনে ক্লিক করো

---

### ✅ ধাপ ৩ — Column যোগ করো

Table এ Column যোগ করতে **`+`** বাটনে ক্লিক করো:

| Field | উদাহরণ |
|-------|---------|
| **Name** | `Name` |
| **Type** | `text` |

- **Save** বাটনে ক্লিক করো

> ✔️ Supabase এ `Employee` Table প্রস্তুত — এখন n8n এ কাজ শুরু করো।

---

## ⚙️ n8n Workflow সেটআপ

### ✅ ধাপ ৪ — Manual Trigger ও Edit Fields যোগ করো

- **n8n** ওপেন করো
- **"Add first step"** এ ক্লিক করো
- **"Trigger Manually"** সিলেক্ট করো
- **Nodes Panel** ওপেন করো
- **"Edit Fields"** সার্চ করো এবং ক্লিক করো
- **"Add Field"** এ ক্লিক করো
- নিচের Value দাও:

| Field Name | Value |
|------------|-------|
| `Name` | `Wasim` |

- **"Execute step"** এ ক্লিক করো

---

### ✅ ধাপ ৫ — Supabase Node যোগ করো

- **Edit Fields** এর **`+`** বাটনে ক্লিক করো
- **"Supabase"** সার্চ করো এবং ক্লিক করো
- **"Create a row"** সিলেক্ট করো
- **"Set up credential"** এ ক্লিক করো

---

## 🔑 Supabase Credential সেটআপ

### ✅ ধাপ ৬ — Project URL কপি করো

- Supabase Dashboard এ যাও
- **Project Overview** Tab এ ক্লিক করো
- **Project URL** কপি করো
- n8n এর **Host** Field এ Paste করো

---

### ✅ ধাপ ৭ — Service Role Secret কপি করো

নিচের ধাপ অনুসরণ করো:

```
Project Settings
      │
      ▼
API Keys
      │
      ▼
Legacy anon, service_role API keys
      │
      ▼
service_role → secret → Reveal বাটনে ক্লিক করো
      │
      ▼
Copy বাটনে ক্লিক করো
```

- কপি করা Secret টি n8n এর **Service Role Secret** Field এ Paste করো
- **Save** বাটনে ক্লিক করো

---

### ✅ ধাপ ৮ — Supabase Node Value সেট করো

Credential সেটআপ শেষে নিচের Value দাও:

| Field | Value |
|-------|-------|
| **Table Name or ID** | `Employee` *(ক্লিক করলে Supabase থেকে Auto দেখাবে)* |
| **Field Name or ID** | `Name` |
| **Field Value** | Edit Fields থেকে `Name` টেনে এনে দাও |

> 💡 **Field Value কীভাবে দেবে?**
> Field Value এর পাশ থেকে Edit Fields এর `Name` Variable টি **Drag করে** এনে Drop করো।

---

## ▶️ Workflow Execute করো

### ✅ ধাপ ৯ — Execute ও Verify করো

- **Execute Workflow** বাটনে ক্লিক করো
- Supabase Dashboard এ গিয়ে **Table Editor → Employee** Table চেক করো

> ✔️ সফল হলে `Employee` Table এ নতুন Row দেখা যাবে:

| id | Name |
|----|------|
| 1 | Wasim |

---

## 📋 Quick Reference

| ধাপ | কাজ | কোথায় |
|-----|-----|--------|
| ১ | New Project তৈরি | Supabase |
| ২ | Employee Table তৈরি | Supabase |
| ৩ | Name Column যোগ | Supabase |
| ৪ | Manual Trigger ও Edit Fields সেটআপ | n8n |
| ৫ | Supabase Node যোগ | n8n |
| ৬ | Project URL কপি ও Host এ দাও | Supabase → n8n |
| ৭ | Service Role Secret কপি ও দাও | Supabase → n8n |
| ৮ | Table ও Field Value সেট | n8n |
| ৯ | Execute ও Supabase এ Data যাচাই | n8n + Supabase |

---

## 💡 Supabase Credential কোথায় পাবে?

```
supabase.com → Dashboard → তোমার Project
        │
        ├── Project Overview → Project URL (Host এর জন্য)
        │
        └── Project Settings → API Keys
                    └── service_role → secret (Password এর জন্য)
```

---

*Supabase একটি Open Source Firebase Alternative। n8n এর সাথে সংযুক্ত করলে যেকোনো Automation এর Data সহজে Database এ সংরক্ষণ করা যায়।*
