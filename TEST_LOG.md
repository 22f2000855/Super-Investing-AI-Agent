# Test Log — Super Investing AI Agent

## Test Environment
- **Language:** Python
- **LLM:** Google Gemini 2.5 Flash
- **API Provider:** OpenRouter
- **API Client:** OpenAI Python SDK
- **Test Ticker:** SRVCABLE (fictional company)
- **Report Date:** 23 September 2026
- **Input:** 8 Markdown documents from `research_pack/`

## Run 1 — Baseline

- **Command:** `python agent.py SRVCABLE run1`
- **Design:** Initial system prompt and agent implementation.
- **Output:** `runs/run1.md`
- **Validation Log:** `runs/run1.validation.txt`

**Observed Results:**
- Generated a research brief with Snapshot, Bull case, Bear case, Open questions, and Sources.
- Identified the discrepancy between Business Daily Online's reported revenue of ₹1,428 crore and the company's press release figure of ₹1,248 crore for Q1 FY27.
- Included information about order-book growth, operating margins, receivables, promoter pledging, and the GST demand order.

**Issues Identified:**
- Promotional source S5 appeared in the Sources list.
- Source S6 was not clearly distinguished from the listed cable manufacturer.
- Placeholder URLs were not consistently labelled as unverified.

## Run 2 — Improved Source Handling

- **Command:** `python agent.py SRVCABLE run2`
- **Design Change:** Updated `system_prompt.md` to strengthen source credibility assessment, entity matching, treatment of older information, and handling of conflicting financial figures.
- **Output:** `runs/run2.md`

**Observed Results:**
- Retained the revenue discrepancy under Open questions and preferred the company's press release as the primary source for the reported financial figure.
- Identified S6 as apparently referring to a different entity and excluded it from the Sources list.
- Excluded promotional source S5 from the Sources list.
- Marked placeholder URLs as unverified.

**Remaining Issues:**
- Historical promoter-pledging figures required careful interpretation across reporting dates.
- Financial claims and citations still required manual review.

## Run 3 — Improved Validation

- **Command:** `python agent.py SRVCABLE run3`
- **Design Change:** Updated `agent.py` validation logic to check the required report headings, unknown source IDs, placeholder URLs, and whether the revenue discrepancy is discussed under Open questions. The validation does not require an Excluded sources section.
- **Output:** `runs/run3.md`
- **Validation Log:** `runs/run3.validation.txt`

**Observed Results:**
- Generated a report with substantively the same content as Run 2.
- Retained the revenue discrepancy and preference for the company's press release.
- Continued to exclude S5 promotional content from the Sources list and identify S6 as apparently unrelated.
- Continued to mark placeholder URLs as unverified.

**Remaining Issues:**
- Run 3 did not produce a substantive change in report content compared with Run 2.
- The validation log should be reviewed to confirm the new checks ran and to identify any warnings.
- Automated validation cannot guarantee factual accuracy or citation correctness.

## Limitations
- The agent relies on the supplied research documents and does not independently verify the fictional company's claims online.
- Regex-based financial checks may miss figures presented in unexpected formats.
- Differences in financial figures may result from different reporting periods, definitions, or source errors.
- URLs using the reserved `.example` domain are placeholders and cannot be treated as verified working links.
- API or network failures may interrupt report generation.