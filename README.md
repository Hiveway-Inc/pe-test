# Prompt Engineering Assessment: Discount Engine Validator

## Overview
This repository contains a comprehensive prompt engineering assessment designed to evaluate candidates' ability to extract requirements, plan solutions, and implement working code from realistic, messy business documentation.

**Time Limit:** 30-45 minutes total  
**Scenario:** Build a Discount Engine Validator that processes orders and applies coupon discounts

## Assessment Structure

### Phase 1: EXPLORE (8-10 minutes)
Navigate to `docs/explore/` to find realistic business documentation including meeting transcripts, emails, Slack messages, JIRA tickets, and customer feedback. Your task is to extract clear requirements from this intentionally messy documentation.

**Deliverable:** A one-page requirements document containing:
- Core functional requirements
- Technical specifications  
- Your assumptions (with justifications)
- Open questions that need clarification
- Acceptance criteria for testing

### Phase 2: PLAN (8-10 minutes)
Navigate to `docs/plan/` for instructions on creating your implementation plan. Based on your extracted requirements, design a technical solution.

**Deliverable:** A structured implementation plan including:
- Solution architecture and approach
- Step-by-step implementation breakdown
- Core functions/logic needed
- Data structures to use
- Edge case handling strategy
- Testing approach

### Phase 3: EXECUTE (15-25 minutes)
Navigate to `docs/execute/` for implementation instructions and test data. Build a working solution based on your plan.

**Deliverable:** Working code that:
- Processes the provided `orders.csv` and `coupons.json`
- Generates `results.csv` with discount calculations
- Creates `summary.md` with statistics
- Handles all identified edge cases

## Technical Requirements

### Input Files
- **orders.csv**: Contains order_id, customer_id, amount, date, coupon_code
- **coupons.json**: Contains coupon definitions with discount rules and expiration dates

### Output Files
1. **results.csv** with columns:
   - order_id, original_amount, final_amount, coupon_code, discount_amount, status, message
   - Status values: applied, rejected, expired, invalid, none

2. **summary.md** containing:
   - Total orders processed
   - Breakdown by status
   - Total revenue impact
   - Example entries for each status

### Discovery Challenge
The explore phase contains realistic business documentation with all the messiness that entails:
- **Conflicting information** from different stakeholders
- **Evolving requirements** that changed over time
- **Hidden edge cases** buried in casual conversations
- **Contradictory opinions** that need resolution
- **Critical details** scattered across multiple documents
- **Technical constraints** mentioned in passing
- **Assumed knowledge** that isn't explicitly stated

Your job is to synthesize all this information, resolve conflicts using your best judgment, and extract the actual requirements needed to build a working solution. Not everything you read is equally important - learning to identify what matters is part of the assessment.

### Implementation Constraints
- **Language:** Node.js (preferred) or Python
- **Libraries:** Standard library only (no npm/pip packages)
- **Location:** Create your solution in the `/src` directory

## Scoring Rubric (100 points)

### Prompting & Extraction (30 points)
- Requirements extraction accuracy (15 pts)
- Handling contradictions and ambiguity (10 pts)
- Identifying critical vs nice-to-have features (5 pts)

### Technical Correctness (30 points)
- Core functionality works (15 pts)
- Edge cases handled properly (10 pts)
- Output format correct (5 pts)

### Requirements & Planning (20 points)
- Clear requirements documentation (10 pts)
- Logical implementation plan (10 pts)

### Code Quality (20 points)
- Clean, readable code (10 pts)
- Proper error handling (5 pts)
- Efficient implementation (5 pts)

## Getting Started

1. **Start with EXPLORE phase:** Read through `docs/explore/` to understand the requirements
2. **Move to PLAN phase:** Create your implementation strategy in `docs/plan/`
3. **Finish with EXECUTE phase:** Build your solution using test data from `docs/execute/`
4. **Place your code in `/src`:** This is where your implementation should live

## Testing Expectations
You are expected to identify and handle all relevant test cases and edge cases based on the requirements you extract from the documentation. Part of this assessment is determining what scenarios need to be tested - we won't tell you what to look for.

## Tips for Success
- The explore phase documentation is intentionally messy - look for patterns and consensus
- Not all information is equally important - use your judgment
- Time management is crucial - don't get stuck on perfection
- Start with core functionality, then handle edge cases
- Test incrementally as you build

## Evaluation Focus
This assessment evaluates your ability to:
1. Extract signal from noise in real-world documentation
2. Make reasonable assumptions when faced with ambiguity
3. Plan and decompose complex problems
4. Implement clean, working solutions under time pressure
5. Handle edge cases and error conditions gracefully

Good luck! Remember, we're evaluating your problem-solving process as much as your final solution.