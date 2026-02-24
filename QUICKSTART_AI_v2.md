# AI Interview Assistant - v2.0 Quick Start Guide

## ✨ New Features (AI-Powered)

✅ **Dynamic Question Generation**: Questions generated in real-time by Gemini AI
✅ **Intelligent Answer Analysis**: Deep analysis of sentence formation, technical accuracy, keywords, and examples
✅ **Answer Validation**: Rejects vague/short/invalid answers automatically
✅ **Real-time Feedback**: "Thank you" message + AI analysis after each answer
✅ **Database Persistence**: All data saved to MongoDB (ai_interviews)
✅ **Gemini Integration**: Uses Google Gemini Pro for best accuracy

---

## 🚀 Setup Steps

### 1. **Backend Setup** (one time only)

```bash
cd backend

# Install dependencies with Gemini API
pip install -r requirements.txt

# Verify installation
python -c "import google.generativeai; print('✓ Gemini installed')"
```

### 2. **MongoDB Setup** (verify running)

```bash
# Verify MongoDB is running
mongosh
> show databases
> use ai_interviews
> show collections
```

### 3. **Start Backend Server**

```bash
cd backend
uvicorn main_v2:app --reload --port 8000
```

✓ API Docs: http://localhost:8000/docs

### 4. **Start Frontend** (in new terminal)

```bash
cd c:\Users\ABHIRAM\Documents\ai-interview-assistant
pnpm install
pnpm dev
```

✓ Frontend: http://localhost:3000

---

## 🎯 How It Works Now

### Interview Flow:

```
1. Setup Page
   ↓
2. Interview Page (IMPROVED)
   → AI generates dynamic question based on role/skills
   → User answers question
   → Submit answer
   ↓
3. INSTANT AI ANALYSIS (NEW!)
   → Answer validation (rejects vague answers)
   → Gemini analyzes:
     • Sentence formation
     • Technical accuracy
     • Keyword usage
     • Examples/scenarios
     • Depth of understanding
   → Returns marks (0-10) + detailed feedback
   ↓
4. "Thank you for response!" message
   ↓
5. Next question fetched automatically
   ↓
6. Repeat until 8 questions complete
   ↓
7. Results Page
   → Overall score & percentage
   → Detailed analysis per question
   → Recommendation (Hire / Maybe / No Hire)
   → Data saved to ai_interviews database ✓
```

---

## 🔑 Configuration

### Backend .env (`backend/.env`)

```env
# Already configured:
MONGODB_URL=mongodb://localhost:27017
DATABASE_NAME=ai_interviews
GEMINI_API_KEY=YOUR_GEMINI_API_KEY_HERE
PORT=8000
```

### Frontend .env (`.env.local`)

```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_USE_MOCK_DATA=false
```

---

## 📊 AI Analysis Details

### Answer Validation (Rejects):
- ❌ Less than 30 characters
- ❌ Vague answers: "yes", "no", "maybe", "idk"
- ❌ Gibberish/invalid content
- ❌ Excessive repetition (< 30% unique words)

### Scoring (1-10 marks per answer):
- **Sentence Formation**: Structure and clarity
- **Technical Accuracy**: Correctness of content
- **Keyword Usage**: Technical terminology
- **Examples/Scenarios**: Real-world applications
- **Depth**: Understanding level
- **Completeness**: Fully addresses question

### Overall Recommendation:
- ✅ **≥ 85%**: Strong Hire
- ✅ **70-84%**: Hire
- ⚠️ **55-69%**: Maybe
- ❌ **< 55%**: No Hire

---

## 📁 Database Schema

### `ai_interviews.reports` Collection

```json
{
  "_id": ObjectId,
  "interview_id": "string",
  "candidate_name": "string",
  "candidate_email": "string",
  "role": "string",
  "experience_level": "string",
  "skills": ["array"],
  "total_questions": 8,
  "answered_questions": 8,
  "overall_score": 7.5,
  "overall_percentage": 75.0,
  "recommendation": "Hire",
  "strengths": ["array"],
  "improvements": ["array"],
  "responses_summary": [
    {
      "question_id": "string",
      "marks": 8,
      "percentage": 80,
      "correctness": "good",
      "is_valid": true
    }
  ],
  "generated_at": ISODate()
}
```

---

## 🐛 Troubleshooting

### Issue: "Gemini API key not configured"
**Fix**: Verify `GEMINI_API_KEY` in `backend/.env`

### Issue: "MongoDB connection failed"
**Fix**: Ensure MongoDB is running: `mongosh`

### Issue: Frontend shows "Exit Code: 1"
**Fix**: 
```bash
cd c:\Users\ABHIRAM\Documents\ai-interview-assistant
pnpm install
rm -r .next
pnpm dev
```

### Issue: "Answer rejected as invalid"
**Solution**: Provide detailed answers (>30 characters) with specific examples

---

## ✅ Test Checklist

- [ ] Backend starts without errors (http://localhost:8000/docs)
- [ ] MongoDB has `ai_interviews` database
- [ ] Frontend loads (http://localhost:3000)
- [ ] Can create interview with setup page
- [ ] AI generates first question dynamically
- [ ] Can submit answer and see "Thank you" message
- [ ] AI analysis feedback appears after answer
- [ ] Next question loads automatically
- [ ] All 8 questions complete
- [ ] Results show overall percentage & recommendation
- [ ] Data appears in `ai_interviews.reports` collection

---

## 📚 API Endpoints

### Core Endpoints:
- `POST /api/interviews` - Create interview
- `GET /api/interviews/{id}/question` - Get next AI-generated question
- `POST /api/interviews/{id}/response` - Submit answer + AI analysis
- `POST /api/interviews/{id}/complete` - Finalize interview
- `GET /api/interviews/{id}/report` - Get detailed report

### Report Endpoints:
- `GET /api/reports` - List all reports
- `GET /api/interviews/{id}/report` - Get specific report

---

## 🎓 Example Interview

**Question (AI-Generated for Backend role):**
> "Design a scalable API for handling real-time data streams. Describe your architecture, database choices, and caching strategy."

**Good Answer (8-10 marks):**
> "I would design a microservices architecture using event-driven systems. For the database, I'd use a time-series database like InfluxDB for metrics and PostgreSQL for relational data. I'd implement Redis caching for frequently accessed data and use message queues like Kafka for handling data streams. This approach ensures scalability, fault tolerance, and optimal performance. I've implemented this in my previous project where we handled 100K+ requests per second."

**Poor Answer (0-3 marks):**
> "Use a database. Cache things. Make it fast."

---

## 🚀 Next Steps

1. **Test Interview Flow**: Create interview → Answer all questions → Check results
2. **Verify Database**: Check `mongosh` for saved reports
3. **Monitor Logs**: Check console output for AI analysis details
4. **Iterate**: Refine questions/scoring based on interview results

---

## 📞 Support

For issues or questions:
1. Check MongoDB is running: `mongosh`
2. Check backend logs for errors
3. Verify Gemini API key in `.env`
4. Check browser console for frontend errors

---

**Version**: 2.0.0 (AI-Powered)
**Last Updated**: December 18, 2025
