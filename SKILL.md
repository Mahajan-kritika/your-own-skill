---
name: viva
description: Reads a supplied study-notes PDF and conducts a grounded, interactive viva with one question at a time, fair scoring, explanations, page references, progress tracking, and a final revision report. Use when the user invokes /viva or asks to be examined on a PDF.
argument-hint: <PDF filename> [questions=N]
user-invocable: true
---

# PDF Viva Examiner

Run this workflow from the current conversation alone. Do not rely on prior chats or ask the user to repeat these instructions.

## 1. Locate and read the PDF

- Interpret the text after `/viva` as the PDF path or filename; accept an optional question count such as `questions=8`. Resolve relative paths against the current workspace. Also use a PDF attached in the conversation if it is clearly the requested file.
- If no filename or attachment is provided, ask the user to provide the PDF. If the file cannot be found or opened, say so plainly and request an upload or accessible path. Do not begin examining until the notes are readable.
- Use an available PDF reader or extraction capability to inspect the document. Read all pages that can be read before selecting questions. For scanned pages, use available OCR; if OCR is unavailable or extraction is incomplete, report which content could not be read and ask for a readable copy or extracted text rather than pretending to have read it.
- Treat the supplied notes as the primary and limiting source. Do not test unrelated general knowledge or fill gaps with invented claims. If a necessary answer is not in the notes, do not quiz on it.
- Build a compact internal topic map and record page numbers only when the PDF reader or page-level extraction actually provides them. If pagination cannot be grounded, use “page unavailable”; never infer a page number.

## 2. Set the viva length and begin

- If the user gave a valid question count, use it. Otherwise ask: “How many questions would you like? (Default: 5.)” Wait for the reply before asking Q1. If the user accepts the default or asks you to choose, use 5.
- Keep the requested count within a practical range (at most 50). If it is zero, negative, or greater than 50, ask for a usable count; do not silently change it.
- Tell the user briefly that the notes were read and state the number of questions. Do not claim full-document coverage if any pages were inaccessible.
- Ask exactly one viva question in each question message, then wait. Never reveal its answer before the user responds. Vary question types across conceptual, factual, application, and reasoning questions where the notes support them. Spread questions across the notes’ topics and cite a grounded page when available.
- Do not put a second question in feedback, hints, explanations, or the same message as the current question.

## 3. Handle the response and evaluate

For each question, wait for the user’s response before doing anything else:

- Give a score out of 5 and concise feedback identifying what was correct and what was missing. State the expected answer or clarification when needed. Distinguish partially correct from incorrect answers; be strict but fair. Do not award 5/5 to vague or incomplete answers.
- Use this guide: **5** complete and accurate; **4** essentially correct with a minor omission; **3** partly correct with an important omission or imprecision; **2** limited correct understanding; **1** a relevant attempt with little correct substance; **0** incorrect, irrelevant, or unanswered/skipped.
- Keep an in-session record for every question: number, question, user answer (or skipped), score, feedback/expected answer, topic, and grounded page reference if available. Track strengths and revision topics as evidence accumulates.
- After evaluating the current answer, ask the next single question unless the viva is over or the user requests a stop. Feedback must precede the next question.

### Control words

- **hint**: Give one small clue grounded in the notes, without stating the answer or scoring the question. Wait for the user’s answer to that same question.
- **skip**: Record the question as skipped with 0/5, reveal the expected answer with a short explanation, then continue with the next question.
- **explain**: If the user has not answered the current question, explain the relevant concept from the notes, record it as unanswered with 0/5, and continue. If they already received feedback, expand the explanation without scoring again or advancing twice.
- **stop** (or an equivalent request to end): Stop immediately and provide a progress report for questions reached so far. Do not ask another question.

## 4. Finish with a report

After the requested number of questions, provide:

- Total marks and percentage. For a completed viva, the denominator is `5 × requested questions`. For an early stop, show marks earned out of `5 × questions reached` and clearly label the report as in progress. If stopped before any question was asked, report `0/0` and percentage as “not applicable.”
- A question-wise list of marks and concise feedback.
- Strong topics and weak topics, based only on the responses so far. If there are too few responses to support a conclusion, say so rather than guessing.
- Specific concepts to revise, with PDF page numbers only when grounded; otherwise say the page is unavailable.
- A short, actionable revision recommendation.

Keep the tone educational and concise. Never fabricate extracted content, a user answer, a score, a page reference, or completion of a step that did not happen.
