# **Case Brief: Inefficient Handling of Supplier Advertisements**

## **Problem Definition**

The company receives approximately **100 supplier advertisements per workday** by **email**. Each advertisement is forwarded to about **5 employees in the Purchasing Department**. The selection of employees is **almost random**, but with a **higher probability of emails being sent to senior decision makers**.

The department consists of:

- **5 senior decision makers**, with an average cost of **\$80 per hour**

- **35 other staff**, with an average cost of **\$50 per hour**

For each email advertisement:

- **99% are irrelevant**, requiring about **2 minutes** to review and discard.

- **1% may be relevant**, requiring further evaluation (not detailed here).

### **Current Cost of Irrelevant Emails**

- Total employee time wasted per day:\
  100 emails × 99% irrelevant × 5 employees × 2 minutes = **990 minutes (16.5 hours)**

- Distribution of wasted time (based on probability of assignment):

  - Senior decision makers (40% share): **6.6 hours/day** → **\$528/day**

  - Other staff (60% share): **9.9 hours/day** → **\$495/day**

- Total cost of wasted time = **\$1,023 per day**

- Annualized (250 workdays) = **\$255,750 per year**

This process wastes significant employee time, particularly that of senior decision makers whose work is more valuable. The company wants to minimize the cost caused by irrelevant emails.



## **Expected Outcome**

**Key Properties of the Solution:**

1.  **Local AI model operation: The AI system classifies incoming supplier emails and decides whether to forward them to an employee or trash them. It runs continuously (24/7) and handles all 100 daily emails, reducing the need for employees to review irrelevant messages.**

2.  **Automatic filtering of irrelevant emails: Out of 99 daily irrelevant emails, 79 are discarded automatically; only 20 are forwarded to employees.**

3.  **Targeted routing of relevant emails: Each relevant email (1% of total) is sent to a single employee.**

    - **70% reach the correct decision maker directly (no wasted time)**

    - **20% initially reach the wrong person but are forwarded correctly, consuming 5 minutes of employee time**

    - **10% reach the wrong person and are discarded, consuming 2 minutes of employee time**

4.  **System maintenance: A senior IT staff member works 1 hour/day to maintain and monitor the AI system.**

**Expected Reduction in Work Hours:**

- **Time spent handling irrelevant emails by employees: reduced from \~16 hours/day to \~0.667 hours/day**

- **Time spent handling misrouted relevant emails: \~1.2 minutes/day**

- **Total reduction in employee work hours: \~15.3 hours/day**

**Expected Cost Reduction:**

- **Cost with AI-assisted routing (employees + IT + AI model): \~\$30,841/year**

- **Annual savings: \~\$224,909/year**

## Solution proposal (Chat Based, e.g. ChatGPT through a web browser)

### **Workflow:**

1.  **At the start of each session, the employee inputs each person's role and product responsibilities into the LLM.**

2.  **The employee copies the email text into the LLM chat interface.**

3.  **The LLM indicates whether the email is relevant or irrelevant. If it no longer remembers each person's roles, the employee re-enters the roles and responsibilities.**

4.  **The employee manually forwards relevant emails or discards irrelevant ones.**

5.  **Repeat for all emails received during the day.**

### **Observed Limitation:**

- **Repetitive effort: Copying text one by one into the chat window was slow and frustrating.**

- **Forgetting context: The LLM often "lost track" of the roles and responsibilities after a few emails, forcing us to re-enter the same information multiple times.**

- **No real time savings: Even when the LLM gave correct judgments, we still had to manually forward or delete each email ourselves.**

- **Doesn't scale: Processing a full day's worth (100 emails) this way was unrealistic --- it took almost as long as just reading the emails directly.**

## Solution proposal (Agentic)

### **Workflow:**

1.  **Email Arrival → Email Ingestion Module**

    - **Extract text → Clean → Tokenize**

2.  **Processed Email → RAG Classification Module**

    - **Query internal database (product categories, employee responsibilities)**

    - **Combine email + retrieved context → LLM → Classification**

3.  **Classification Output → Routing Module**

    - **Relevant → Forward to designated employee**

    - **Irrelevant → Trash folder**

4.  **Logging & Monitoring → IT Maintenance**

    - **Track misrouted emails**

    - **Update retrieval knowledge base**

    - **Adjust model thresholds if needed**
