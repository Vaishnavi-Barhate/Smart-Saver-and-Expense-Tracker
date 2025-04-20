
#  SystemDesign.md

##  Project Name: SmartSave – AI-Powered Micro-Saving & Budgeting Assistant

---

##  Overview

**SmartSave** is a modular financial wellness engine designed to be integrated into digital wallets like PhonePe, GPay, or Paytm. It automatically rounds up users’ daily UPI transactions and stores the difference in customizable virtual savings jars. Alongside, an AI engine tracks user spending behavior and provides smart alerts, suggestions, and financial nudges to build saving habits, prevent overspending, and boost financial literacy.

---

## 🧩 Key Features

1. **Micro-Rounding Engine**  
   - Rounds up every transaction to nearest ₹1 / ₹10 / ₹50 (user-configurable).  
   - Difference is stored in a virtual savings jar linked to UPI or wallet balance.

2. **Goal-Driven Savings Jars**  
   - Users can create multiple jars for different goals (e.g., vacation, gadgets).  
   - Set target amount, deadline, and add images for emotional engagement.

3. **AI Budget Tracker**  
   - Categorizes spends (food, travel, shopping, etc.)  
   - Predicts spending trends & detects anomalies  
   - Sends alerts when close to budget limits

4. **Gamified Financial Nudges**  
   - Streak rewards, saving challenges, group jars  
   - Weekly performance summaries & motivational badges

5. **UPI/Wallet Integration**  
   - Seamless connection with user’s PhonePe/GPay/Paytm account  
   - Option to withdraw or lock funds with two-factor verification

---

## 🏗️ Architecture Overview

```
Frontend (Mobile App / SDK)
   |
   |---> Auth & Wallet Connection (Firebase / UPI Token)
   |
   |---> Transaction Layer (UPI API / Mocked DB)
   |
   |---> Micro-Saving Engine
   |         |---> Rounding Rules (Configurable)
   |         |---> Goal Jar Allocator
   |
   |---> AI & Budget Module
   |         |---> Expense Categorizer (NLP + ML)
   |         |---> Overspending Predictor
   |         |---> Recommendation Engine
   |
   |---> Notification Engine (FCM / OneSignal)
   |
Backend (Node.js or Flask API)
   |
   |---> MongoDB / Firestore
   |---> Auth Layer (JWT + Firebase Auth)
   |---> Webhook Handler for Transactions
```

---

## 🗃️ Database Schema (MongoDB / Firebase Firestore)

### `users`
```json
{
  "user_id": "UID123",
  "name": "Ankit",
  "email": "ankit@email.com",
  "linked_wallet": "PhonePe",
  "default_rounding": 10,
  "monthly_budget": 12000,
  "preferences": {
    "notifications": true,
    "auto_saving_enabled": true
  }
}
```

### `transactions`
```json
{
  "txn_id": "TXN98345",
  "user_id": "UID123",
  "amount": 197.25,
  "rounded_to": 200,
  "saved_amount": 2.75,
  "category": "Food",
  "timestamp": "2025-04-20T12:30:00Z"
}
```

### `goal_jars`
```json
{
  "jar_id": "JAR456",
  "user_id": "UID123",
  "name": "Goa Trip",
  "target_amount": 15000,
  "saved_so_far": 3150,
  "deadline": "2025-06-01",
  "image_url": "goal_jar_goa.png"
}
```

### `budget_alerts`
```json
{
  "alert_id": "ALT321",
  "user_id": "UID123",
  "type": "overspend_warning",
  "category": "Entertainment",
  "threshold": 90,
  "triggered_on": "2025-04-18"
}
```

---

## 🤖 AI/ML Component

| Module | Function |
|--------|----------|
| `Expense Categorizer` | NLP-based classification of transaction descriptions |
| `Overspend Predictor` | Uses time-series + rule-based model to forecast spikes |
| `Recommendation Engine` | Suggests weekly save targets, jar boosts, & budget rebalance |

Model Training:  
- Use dummy or synthetic data (₹ values, categories, timestamps)  
- Libraries: `Scikit-learn`, `Pandas`, `TensorFlow Lite (optional for mobile)`

---

## 🔐 Security Considerations

- 🔑 JWT-based secure APIs for user sessions  
- 🔒 Encrypted UPI token handling (no storing of credentials)  
- ✅ Two-factor OTP for jar withdrawal  
- 📊 Role-based access for admin insights and audit logging

---

## 📲 Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | Flutter / React Native |
| Backend | Node.js (Express) or Python (Flask) |
| Database | MongoDB Atlas / Firebase Firestore |
| AI/ML | Python (Scikit-learn, Pandas) |
| Auth | Firebase Auth + JWT |
| Notifications | Firebase Cloud Messaging / OneSignal |
| Integration | RazorpayX, UPI APIs, Paytm SDK (optional) |

---

## 🚀 Scalability

- Event-based microservices for saving actions  
- Webhooks for real-time transaction tracking  
- Redis caching for recent transactions  
- Load balancing with containerized services (Docker + Kubernetes)

