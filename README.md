# Fraud Call Transcript Analyzer

Analyze credit card fraud-related call transcripts to extract call topics and customer friction points. Output results in CSV format with topics, subtopics, friction points, and sentiment analysis.

## When to Use This Skill

Use this skill when:
- Analyzing credit card fraud-related customer service call transcripts
- Extracting common topics from customer calls
- Identifying customer pain points and friction points
- Generating reports on call patterns and sentiment
- Processing multiple call transcripts for trend analysis

## Output Format

The skill outputs structured data in CSV format with the following columns:

| Column | Description |
|--------|-------------|
| call_id | Unique identifier for each call |
| transcript | The call transcript text |
| main_topic | High-level category of the call |
| subtopic | Specific type within the main topic |
| friction_points | Customer pain points or concerns |
| sentiment | Customer sentiment (positive/negative/neutral) |
| sentiment_score | Numeric sentiment score (-1 to 1) |
| timestamp | When the call occurred |

## Analysis Workflow

### Step 1: Parse and Clean Transcripts

For each transcript:
1. Remove duplicate lines and normalize whitespace
2. Extract speaker labels (Customer, Agent, etc.)
3. Preserve conversation structure

### Step 2: Identify Topics

Analyze each transcript to determine:

**High-level categories (main_topic):**
- Transaction Issues (declined, unauthorized charges, pending transactions)
- Account Security (login issues, suspicious activity, card replacement)
- Billing & Disputes (chargebacks, refunds, statement errors)
- Technical Issues (app crashes, login problems, integration errors)
- Process Inquiries (replacement cards, PIN resets, card activation)

**Specific types (subtopic):**
- Repeated transaction declines
- International transaction flags
- Large amount alerts
- Multiple unauthorized charges
- Card lost/stolen
- Card frozen
- Charge reversal requests
- Refund processing delays
- Statement errors
- App login failures
- Biometric verification issues

### Step 3: Identify Friction Points

Extract customer pain points by identifying:
- Frustration indicators (repeated phrases, raised voice indicators)
- Delayed resolutions or unmet expectations
- Technical difficulties causing extended calls
- Confusion about process steps
- Lack of empathy from agents
- Unclear communication

### Step 4: Analyze Sentiment

Determine customer sentiment:
- **Positive**: Resolved quickly, satisfied with resolution
- **Negative**: Frustrated, angry, felt treated unfairly
- **Neutral**: Calm, informational, no strong emotion

Assign sentiment score (-1 to 1):
- Score 1.0: Very positive
- Score 0.5: Slightly positive
- Score 0.0: Neutral
- Score -0.5: Slightly negative
- Score -1.0: Very negative

### Step 5: Generate CSV Output

Produce CSV with all extracted data. Include headers and quote all string fields.

## Main Topics and Subtopics

### Transaction Issues
- **Repeated transaction declines** - Keywords: `declined`, `denied`, `rejected`
- **International transaction flags** - Keywords: `international`, `overseas`, `abroad`, `cross-border`
- **Large amount alerts** - Keywords: `large amount`, `large purchase`, `high-value`
- **Multiple unauthorized charges** - Keywords: `multiple charge`, `several transaction`
- **Pending transaction issues** - Keywords: `pending`, `hold`, `authorization`

### Account Security
- **Card lost/stolen** - Keywords: `lost`, `stolen`, `missing`, `found`
- **Card frozen** - Keywords: `frozen`, `locked`, `blocked`
- **Biometric verification issues** - Keywords: `biometric`, `fingerprint`, `face match`
- **Security alert verification** - Keywords: `security alert`, `fraud alert`, `suspicious`
- **Card replacement** - Keywords: `replacement`, `new card`, `card order`

### Billing & Disputes
- **Charge reversal requests** - Keywords: `reversal`, `chargeback`, `refund request`
- **Refund processing delays** - Keywords: `refund delay`, `waiting refund`, `refund taking long`
- **Statement errors** - Keywords: `statement`, `bill`, `charge incorrect`, `wrong amount`
- **Dispute resolution** - Keywords: `dispute`, `fraud dispute`, `claim`

### Technical Issues
- **App login failures** - Keywords: `app login`, `app crash`, `app not working`
- **Online banking issues** - Keywords: `online banking`, `internet banking`, `website error`
- **Biometric system errors** - Keywords: `biometric error`, `fingerprint failed`
- **Integration problems** - Keywords: `integration`, `sync`, `connect`

### Process Inquiries
- **PIN reset requests** - Keywords: `pin reset`, `forgot pin`
- **Card activation** - Keywords: `activate card`, `new card active`
- **Card delivery inquiries** - Keywords: `delivery tracking`, `when card arrive`
- **Verification process questions** - Keywords: `verification`, `verify identity`, `confirm details`

## Friction Point Indicators

Keywords that suggest customer frustration or friction:
- `ridiculous`
- `terrible`
- `awful`
- `horrible`
- `frustrating`
- `angry`
- `upset`
- `complain`
- `problematic`
- `unacceptable`
- `waiting for X minute`
- `waiting for X long`
- `stupid`
- `ridiculous wait`
- `this taking long`
- `why can't you just`
- `this is ridiculous`
- `this is unacceptable`
- `this is terrible`

## Sentiment Patterns

### Positive Indicators
- `thank`, `satisfied`, `happy`, `glad`, `great`, `appreciate`
- `resolved`, `fixed`, `done`, `okay`, `good`

### Negative Indicators
- `ridiculous`, `terrible`, `awful`, `horrible`, `frustrating`
- `angry`, `upset`, `complain`, `problematic`, `unacceptable`

### Neutral Indicators
- `okay`, `fine`, `understand`, `yes`, `no`, `let me check`

## Sentiment Scoring

- **Score 1.0**: Very positive
- **Score 0.5**: Slightly positive
- **Score 0.0**: Neutral
- **Score -0.5**: Slightly negative
- **Score -1.0**: Very negative

Sentiment score is calculated based on the ratio of positive to negative indicators in the transcript.

## Example Call Analysis

**Input transcript:**
```
Customer: My card was declined at the grocery store.
Agent: I see the transaction for $45.00 at Fresh Mart. Is this your card?
Customer: Yes, but I have enough money in my account.
Agent: Let me check... I see there's a fraud alert on this card. We've frozen it for security.
Customer: I need to use it now! This is urgent.
Agent: I understand, but we need to verify it's you first. Can you confirm your last transaction?
Customer: This is ridiculous! I've been waiting for 10 minutes. Why can't you just let me use my card?
```

**Output analysis:**
```
call_id,transcript,main_topic,subtopic,friction_points,sentiment,sentiment_score,timestamp
1,"Customer: My card was declined at the grocery store. Agent: I see the transaction for $45.00 at Fresh Mart. Is this your card? Customer: Yes, but I have enough money in my account. Agent: Let me check... I see there's a fraud alert on this card. We've frozen it for security. Customer: I need to use it now! This is urgent. Agent: I understand, but we need to verify it's you first. Can you confirm your last transaction? Customer: This is ridiculous! I've been waiting for 10 minutes. Why can't you just let me use my card?",Transaction Issues,Repeated transaction declines,"Frustrated tone, 'This is ridiculous', 'Why can't you just let me use my card?'" ,Negative,-0.8,2025-02-02T14:30:00Z
```

## Handling Multiple Transcripts

When processing multiple call transcripts:
1. Process each transcript independently
2. Append results to the same CSV file
3. Ensure unique call_id values
4. Maintain chronological order if timestamp is available

## Notes

- Preserve original transcript text for reference
- Quote all string fields in CSV to handle commas
- Handle edge cases: empty transcripts, very short calls, duplicate transcripts
- Flag any transcripts that require manual review

