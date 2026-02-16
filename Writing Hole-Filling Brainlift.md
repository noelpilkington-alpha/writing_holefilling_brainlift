# Writing Hole-Filling & Test-Out Assignment Brainlift

---

## Purpose

**Purpose of this BrainLift:** The purpose of this BrainLift is to train an AI agent to make expert-level decisions about writing remediation in AlphaWrite. Specifically, the agent must be able to: (1) diagnose exactly why a student failed a writing test by examining their actual responses, (2) determine whether the student needs targeted hole-filling or full course enrollment, and (3) assign the precise set of AlphaWrite lessons that will close the identified gaps and prepare the student for mastery.

Without this BrainLift, an LLM would default to generic remediation logic: assign everything the student got wrong, ignore prerequisite skill chains, treat all test failures the same, and fail to distinguish between a competence gap and a transfer gap. The result would be either over-prescription (wasting student time on unnecessary lessons) or under-prescription (missing root causes and prerequisites, leading to repeated failure).

This BrainLift encodes the pedagogical reasoning, learning science principles, and operational constraints that a human Writing Learning Strategist uses when building remediation plans. It turns that expertise into rules an AI agent can execute consistently, at scale.

**In Scope:**
- AlphaWrite G3-8 hole-filling logic after same-grade test failures
- AlphaWrite G3-8 enrollment vs. hole-filling decisions after next-grade test-out failures
- Prerequisite skill detection and assignment chains
- G6-8 essay slot tracking and scarcity management
- Practice-to-test transfer gap diagnosis
- Test question-to-skill mapping for all grade bands

**Out of Scope:**
- K-2 writing instruction (no tests or hole-filling at these levels)
- G9-12 writing curriculum (separate Brainlift)
- Test creation or rubric design
- Teacher-facing instructional guidance
- Reading comprehension interventions (even when reading weakness affects writing test performance) — however, the system DOES detect and flag reading comprehension deficits on writing tests to prevent misassignment of writing activities and to trigger human review when reading is the primary barrier

---

## Experts *(DOK 1)*

### Expert 1: Judith Hochman & Natalie Wexler (The Writing Revolution)

**Who:** Judith Hochman is founder of The Writing Revolution (TWR) and former head of The Windward School. Natalie Wexler is education writer, journalist, and author of "The Knowledge Gap."

**Focus:** Sentence-level writing instruction; explicit writing strategies; the sentences-to-paragraphs-to-essays progression; embedding writing across content areas.

**Why Follow:** TWR provides the foundational scaffold architecture that AlphaWrite is built upon. Every lesson in the Skill Plan traces back to TWR's progression: Fragment or Sentence? to Because, But, So to Appositives to Paragraph Outlines to Essays. When the agent diagnoses a gap, it is diagnosing where the student sits on TWR's scaffold. When it assigns a prerequisite, it is following TWR's principle that each skill must be taught explicitly before the next can succeed. TWR's insight that assigning writing without teaching it is malpractice underpins the entire hole-filling philosophy: we don't just re-test, we teach the missing skills.

**Where:**
- Book: *The Writing Revolution 2.0* (2024)
- Website: https://www.thewritingrevolution.org
- Twitter/X: https://x.com/WritingRevolutn

---

### Expert 2: Deborah McCutchen

**Who:** Professor of Educational Psychology, University of Washington; former classroom writing teacher turned researcher.

**Focus:** Cognitive processes in writing; working memory and composition; the capacity theory of writing; development of writing expertise.

**Why Follow:** McCutchen's capacity theory (Writing Quality = f(Working Memory Capacity - Transcription Demands)) is the cognitive engine behind every remediation decision. When the agent must decide whether a student's poor test essay reflects a competence gap or a transfer gap, it is applying McCutchen's insight: a student whose transcription and sentence-level skills are not automatic will have no working memory left for planning and organization under test conditions. This is why the agent checks for sentence-level foundations before assigning paragraph or essay activities. If the foundation consumes all cognitive capacity, higher-order skills cannot emerge.

**Where:**
- Faculty: https://education.uw.edu/people/faculty/dmccutch
- Google Scholar: Search "Deborah McCutchen" at https://scholar.google.com
- Key paper: "A capacity theory of writing: Working memory in composition" (1996)
- Key paper: "Knowledge, processing, and working memory: Implications for a theory of writing" (2000)

---

### Expert 3: Virginia Berninger

**Who:** Professor Emerita, Educational Psychology, University of Washington; leading researcher on writing development, learning disabilities, and the neuroscience of writing.

**Focus:** Simple View of Writing (Writing = Transcription x Text Generation); transcription fluency; the orthographic loop; Not-So-Simple View of Writing (adds executive functions).

**Why Follow:** Berninger's Simple View of Writing explains why the AlphaWrite scaffold works the way it does: Sentences activities build transcription and text generation fluency; Paragraphs activities build planning and organization; Essays require all components operating simultaneously. When the agent encounters a student who writes disorganized paragraphs, Berninger's model tells us to check whether the problem is at the transcription level (sentences are fragmented or incomplete), the text generation level (ideas are present but unstructured), or the executive function level (student can write individual sentences and paragraphs but cannot manage the essay-level planning load). Each diagnosis leads to a different lesson assignment.

**Where:**
- Google Scholar: Search "Virginia Berninger" at https://scholar.google.com
- Key paper: "Writing and reading: Connections between language by hand and language by eye" (2002)
- Key framework: Simple View of Writing (Berninger et al., 2002)

---

### Expert 4: David Yeager

**Who:** Professor of Psychology at University of Texas at Austin; leading researcher on adolescent motivation and development.

**Focus:** The mentor mindset; wise feedback; adolescent motivation and status needs; growth mindset interventions.

**Why Follow:** Yeager's research governs how remediation should be framed, not just what is assigned. A student who just failed a test is in a vulnerable motivational state. The agent's Gap Analysis Report must follow the mentor mindset formula: high standards + high support. When the agent assigns full enrollment to a G3-5 test-out failure, it isn't a punishment; it's a message that "these skills matter, and we're giving you the complete foundation to succeed." Yeager's insight that achievement causes motivation (not just the reverse) validates the approach of assigning sufficient practice volume: when students master the scaffold, confidence follows.

**Where:**
- Book: *10 to 25: The Science of Motivating Young People* (2024)
- Website: https://www.davidyeager.com
- Twitter/X: https://x.com/david_yeager
- Faculty: University of Texas at Austin, Department of Psychology

---

### Expert 5: Paul Kirschner, Carl Hendrick & Jim Heal

**Who:** Paul Kirschner is educational psychologist, author of "How Learning Happens." Carl Hendrick is Head of Learning & Research at Wellington College. Jim Heal is co-author of "How Teaching Happens."

**Focus:** Cognitive load theory; explicit instruction; evidence-based teaching practices; prior knowledge as the most important factor in learning; debunking educational neuromyths.

**Why Follow:** Three principles from these authors govern the automation rules. First, Ausubel's principle that prior knowledge is the most important factor in learning justifies the entire prerequisite detection system: if a student cannot identify an appositive, teaching them to write one will fail. The agent MUST check what the student already knows before assigning the next skill. Second, Rosenshine's principle of obtaining a high success rate (80%+) justifies the 90% pass threshold and the decision to assign full enrollment at lower scores: we don't advance students until mastery is confirmed. Third, Sweller's cognitive load theory explains why the practice-to-test transfer gap exists: AlphaWrite reduces extraneous and intrinsic load through scaffolding and student-chosen topics; the test removes both supports simultaneously, spiking cognitive demands.

**Where:**
- Books: *How Learning Happens* (2020), *How Teaching Happens* (2022)
- Twitter/X: https://x.com/P_A_Kirschner, https://x.com/C_Hendrick

---

### Expert 6: Shawn Datchuk

**Who:** Associate Professor of Special Education, University of Iowa; researcher in writing fluency and sentence-level automaticity.

**Focus:** Sentence combining fluency; transcription automaticity; writing interventions for struggling students; the relationship between sentence-level fluency and composition quality.

**Why Follow:** Datchuk's fluency research provides the evidence base for why G3-5 test-out failures should always receive full course enrollment rather than hole-filling. His work demonstrates that writing fluency requires varied, repeated practice to achieve automaticity. A student who passes a test through general ability has not necessarily automated the underlying skills. The G3-5 courses (6.5-7.8 hours) are short enough that full enrollment functions as a fluency-building investment. Skills the student has already mastered will be completed quickly (~5 minutes instead of ~15 minutes per lesson), serving as spaced review while building the automaticity that hole-filling alone cannot provide.

**Where:**
- Faculty: https://education.uiowa.edu/people/shawn-datchuk
- Twitter/X: https://x.com/ShawnDatchuk
- Key paper: "A review of writing interventions for students with and at risk for emotional and behavioral disorders" (2015)
- Research on sentence combining fluency and its effects on composition

---

### Expert 7: Robert Bjork

**Who:** Distinguished Research Professor of Psychology at UCLA; leading researcher on human learning and memory.

**Focus:** Desirable difficulties; spacing effect; interleaving; the distinction between learning and performance; retrieval practice.

**Why Follow:** Bjork's "desirable difficulties" framework is central to understanding the practice-to-test transfer gap in G6-8. AlphaWrite essay practice uses student-chosen topics (reducing intrinsic load) and guided stages (reducing extraneous load). The test removes both supports simultaneously. Bjork's research tells us that harder conditions during learning enhance long-term retention, but only AFTER competence is established. This is precisely why the 80-89% G6-8 tier gets targeted S+P hole-filling plus all 5 essays (competence is established under the hardest conditions; the full essay sequence builds fluency and automaticity) while below 80% gets full enrollment (competence is not yet established; harder conditions would be counterproductive). Bjork's work also supports the scaffold completion principle: incomplete scaffolds create "undesirable" rather than "desirable" difficulties — the student lacks the foundation to benefit from the challenge.

**Where:**
- Lab: https://bjorklab.psych.ucla.edu
- Faculty: UCLA Department of Psychology
- Key paper: "Making things hard on yourself, but in a good way: Creating desirable difficulties to enhance learning" (2011)
- Key concept: Learning vs. Performance distinction

---

### Expert 8: Pietro Boscolo & Suzanne Hidi

**Who:** Pietro Boscolo is Professor Emeritus of Educational Psychology, University of Padova. Suzanne Hidi is Professor Emerita, OISE, University of Toronto.

**Focus:** Writing motivation; interest development; the four-phase model of interest; the bidirectional relationship between interest and writing quality.

**Why Follow:** Their research explains why AlphaWrite's interest-driven design works for practice but creates a predictable, structural transfer gap on tests. Their four-phase interest model (triggered situational interest → well-developed individual interest) means AlphaWrite leverages Phase 1-2 interest through student-chosen topics across ALL activities, reducing cognitive load during practice. Tests strip away this interest support entirely, forcing students to write about unfamiliar passages with no personal connection. This framework is critical for DIAGNOSIS: a student who writes brilliant essays about their favorite topic but struggles on a test passage isn't necessarily deficient in writing skills — the interest scaffold that reduces cognitive load during practice is absent during testing, and no AlphaWrite activity can replicate that specific condition because students always choose their own topic context. The agent must understand that the interest component of the transfer gap is structural and inherent to the practice-to-test transition. While AlphaWrite activities can partially bridge the transfer gap by removing scaffolding (e.g., Write a Paragraph from Prompt removes guided stages), they cannot remove interest support. This means some degree of transfer gap is expected and normal — the diagnostic question is whether the gap is within the expected range (80-89%, manageable) or indicates deeper competence issues (below 80%, requires full scaffold).

**Where:**
- Book: *Writing and Motivation* (Elsevier, 2007)
- Key chapter: "Motivation and writing" in *Handbook of Writing Research* (2006)
- Google Scholar: Search "Pietro Boscolo" and "Suzanne Hidi" at https://scholar.google.com

---

### Expert 9: Steve Graham & Karen Harris

**Who:** Steve Graham is Regents Professor at Arizona State University. Karen Harris is Professor at Arizona State University. Both are leading writing researchers.

**Focus:** Self-Regulated Strategy Development (SRSD); meta-analyses of writing instruction; writing intervention effectiveness.

**Why Follow:** Graham & Perin's "Writing Next" meta-analysis provides the evidence hierarchy that validates AlphaWrite's instructional design. The highest-impact writing interventions are strategy instruction (+0.82 effect size), summarization (+0.82), and sentence combining (+0.50) — all of which are embedded in AlphaWrite's activity architecture. AlphaWrite's emphasis on Combine Sentences and Combine Sentences with Appositives as key remediation activities is directly validated by the sentence combining effect size. The SRSD framework (Self-Regulated Strategy Development) also validates AlphaWrite's scaffolded approach: explicit strategy instruction followed by guided practice followed by independent performance maps directly to the AlphaWrite lesson progression within each skill. This research gives the agent confidence that the AlphaWrite activities it assigns are backed by the strongest available evidence base for writing intervention effectiveness.

**Where:**
- Meta-analysis: "Writing Next" (Graham & Perin, 2007)
- Book: *Powerful Writing Strategies for All Students* (2007)
- SRSD: https://www.thinksrsd.com
- Google Scholar: Search "Steve Graham writing" at https://scholar.google.com

---

## Spiky POVs *(DOK 4)*

### Truths

**Spiky POV Truth 1: Assigning a writing lesson without a diagnosed root cause is instructional malpractice.**
The agent never assigns "nice-to-have" lessons. Every lesson in a hole-filling plan must connect to a specific question the student missed, a specific root cause identified in their response, or a specific prerequisite needed for a diagnosed gap. If a lesson cannot be justified by pointing to evidence in the student's test, it does not belong in the plan. This is what separates expert remediation from generic re-teaching.

**Spiky POV Truth 2: The skill a question tests is almost never the skill the student is actually missing.**
When a student fails to write an appositive, the most common root cause is not "can't write appositives." It's "doesn't know what an appositive IS." When a student writes a disorganized paragraph, the root cause is often not "can't organize" but "can't write a clear topic sentence." The agent must examine the student's actual response to determine WHERE in the prerequisite chain the breakdown occurred, then assign from that point forward. Assigning the tested skill without its prerequisite wastes time: the student will fail the activity and need the prerequisite anyway.

**Spiky POV Truth 3: A 7-hour course is too short to cherry-pick. Just assign the whole thing.**
For G3-5 test-out failures (below 90%), the correct answer is always full enrollment, never targeted hole-filling. The courses are only 6.5-7.8 hours. The untested skills (SPO, outlining, elaboration) are prerequisites for the tested skills AND for G6-8 essay success. Skills the student has mastered will fly by in ~5 minutes instead of ~15 minutes, functioning as spaced review. The marginal time cost of full enrollment over hole-filling is only 3-5 additional hours: a small price for a complete foundation.

**Spiky POV Truth 4: A student who writes brilliantly in practice and bombs the test doesn't have a writing problem — they have a transfer problem.**
AlphaWrite essays are scaffolded (guided stages) with student-chosen topics (high interest, lower cognitive load). Tests are unscaffolded with unfamiliar passages (no interest support, full cognitive load). A student scoring 80-89% on a G6-8 test-out has demonstrated genuine essay competence under the hardest conditions. A student scoring below 80% may have a transfer problem, a competence problem, or both. The agent must check whether the student has completed scaffolded activities to distinguish between these possibilities. Treating a transfer gap as a skill deficit wastes everyone's time.

**Spiky POV Truth 5: Every essay slot is a one-shot resource. Waste one on same-grade hole-filling and it's gone forever.**
Each G6-8 grade has exactly 5 essay slots. Once completed, a slot cannot be reassigned. This makes essay assignment a high-stakes decision. Same-grade hole-filling never assigns essays (hard constraint). Test-out hole-filling at 80-89% assigns all 5 essays for full fluency development. Full enrollment below 80% also assigns all 5. The agent must always check slot availability before assignment and track which slots have been completed.

**Spiky POV Truth 6: In G6-8, the essay IS the test. Everything else is noise.**
The essay is worth 20 out of 30 points (66.7%). A student scoring 80%+ (24+/30) has necessarily performed well on the essay, even if they got every MCQ wrong (10/30 maximum from MCQs alone means they still needed 14+/20 on the essay). This asymmetry means the 80-89% tier demonstrates genuine essay competence under test conditions. Their gaps are narrow MCQ weaknesses that can be addressed with targeted S+P activities, while the full 5-essay sequence builds grade-level fluency without redundant S+P practice. Below 80%, the essay performance is likely weak, and the full course (all S+P + all 5 essays) is needed.

**Spiky POV Truth 7: Assigning "Write Appositives" to a student who doesn't know what an appositive is will fail 100% of the time. Prerequisites aren't optional.**
If a student cannot identify appositives, assigning Write Appositives will fail. If a student writes fragments when combining sentences, assigning Combine Sentences will fail. The agent must always check the student's actual response for signals of prerequisite need: blank responses mean check all prerequisites; fundamental misunderstandings mean assign the recognition-level prerequisite; partial understanding with structural errors means the target skill only; conventions-only errors mean no prerequisite is needed. This hierarchy prevents both over-prescription and under-prescription.

**Spiky POV Truth 8: A single missed question is a data point. Three missed questions with the same root cause is a diagnosis.**
A student who misses one fragment question has a specific gap. A student who produces fragments across multiple questions AND produces run-ons in their paragraph has a systemic sentence completeness problem. The agent must look for patterns that indicate underlying weaknesses, not just treat each question as an independent event. Treat each question independently and you'll over-prescribe every time. Patterns shift the diagnosis from "fix question X" to "fix the underlying skill," which may add prerequisite activities but removes unnecessary downstream activities.

---

### Myths

**Spiky POV Myth 1: We don't believe that assigning everything a student got wrong is effective remediation.**
Generic systems assign every activity that maps to a missed question. This over-prescribes: many missed questions share the same root cause, and assigning all their mapped activities creates redundancy. Expert remediation identifies the smallest set of lessons that covers all root causes, including prerequisites. A student who missed 4 questions might need only 2 lessons if those questions share a common underlying gap.

**Spiky POV Myth 2: We don't believe that hole-filling alone can prepare a G3-5 student for the next grade.**
When a student passes G4 at 90%+ and then scores 75% on the G5 test-out, the temptation is to hole-fill only the tested gaps. But the G5 test doesn't test every skill in the G5 course. Activities like Topic Brainstorm, SPO, Turn Outline into Draft, and Elaborate on Paragraphs are not directly tested but build the cognitive architecture for tested skills. And the G5-to-G6 transition introduces essays: a student entering G6 without solid paragraph planning skills will struggle with the essay scaffold. Full enrollment ensures every building block is in place.

**Spiky POV Myth 3: We don't believe that essay slots should be rationed or saved for later.**
The 80-89% tier receives targeted S+P hole-filling plus all 5 essays, not a reduced number. The reasoning: fluency requires volume. Two essays provide exposure; five essays build automaticity of the planning→drafting→revising process. The time difference (6.2 hours) is worth the fluency gain for a student advancing to a new grade level. Essay slots aren't being "saved" for anything—the 5 essays ARE the grade-level essay course. Students either need them (assign all 5) or don't (assign 0 for same-grade hole-filling).

**Spiky POV Myth 4: We don't believe that conventions errors (spelling, punctuation) indicate a skill gap requiring lesson assignment.**
When a student demonstrates the correct skill but makes a mechanical error (e.g., writes a correct appositive but omits one comma), the root cause is conventions, not the skill itself. Assigning the skill activity would waste time. The agent must distinguish between skill deficits (assign the skill) and conventions errors (no assignment needed or assign a different, mechanics-focused activity). This distinction alone can cut unnecessary assignments by 20-30%.

**Spiky POV Myth 5: We don't believe that a student who writes well on scaffolded topics necessarily writes well on unfamiliar passages.**
AlphaWrite is powered by student interests. They choose their topic, receive guided stages, and write about what they care about. Tests strip all of this away: unfamiliar passage, no scaffolding, time pressure. McCutchen's capacity theory explains why: when the interest scaffold is removed, cognitive load increases, and working memory that was available for planning and organization is now consumed by engagement and comprehension. This is why the agent must explicitly check for transfer gaps when Q11 (essay/paragraph) performance is weak.

**Spiky POV Myth 6: We don't believe that the agent should guess lesson IDs or invent activities.**
Every lesson assignment must reference an exact ID from the AlphaWrite Skill Plan. If an activity does not exist at the target grade level, the agent must find the closest equivalent or remove it from the plan. Inventing IDs or guessing will cause the assignment to fail in the Timeback system. This is a hard constraint: correctness of IDs is non-negotiable.

**Spiky POV Myth 7: We don't believe that low test scores always mean "bad student."**
A G3-5 test-out score below 70% after the student just passed the prior grade at 90%+ should trigger a human review flag, not an assumption of incompetence. The issue may be test anxiety, a poorly fitting test variant, a reading comprehension barrier, or even a data entry error. The agent flags; the human investigates. This applies equally to G6-8 scores below 50%. The system must maintain humility about what a single test score can and cannot tell us.

**Spiky POV Truth 9: Making a student practice a skill they've already mastered isn't "reinforcement" — it's a waste of their time that erodes trust in the system.** *(Added v1.2)*
When a gap analysis explicitly states that a student demonstrates competency in a sub-skill (e.g., "correctly identified the essay's topic," "topic sentences are clear"), activities targeting that sub-skill must be blocked from the plan. Assigning practice for skills the student has already mastered wastes time, causes frustration, and dilutes focus from actual gaps. This is the positive competency detection principle: the agent must scan for positive indicators and block redundant instruction before building the plan.

**Spiky POV Truth 10: Assigning the first step of a 5-step scaffold and calling it "remediation" is worse than doing nothing.** *(Added v1.2)*
When a skill requires a multi-step instructional scaffold (e.g., multi-section synthesis for G3-5), the COMPLETE sequence must be assigned. Assigning only the first step (e.g., "Identify Topic Sentences" alone) creates a false sense of coverage while leaving the core deficit unaddressed. Under-prescription is more harmful than over-prescription because it leads to repeated test failure with the same error pattern. The complete scaffold is the minimum viable intervention.

**Spiky POV Truth 11: The word "irrelevant" means completely different things depending on context. A system that pattern-matches keywords without reading context will misdiagnose half its cases.** *(Added v1.3)*
The same keyword can mean different things depending on context. "Irrelevant" in the context of a paragraph (irrelevant sentences within a paragraph) indicates a paragraph unity deficit addressable with Eliminate Irrelevant Sentences. "Irrelevant" in the context of a test answer (answer irrelevant to the question asked, focusing on a secondary detail) indicates a reading comprehension deficit — the student cannot identify the main idea from a passage. Similarly, "detail" describing a student's thin paragraph evidence is a writing deficit, but "detail" describing a student's focus on a secondary detail instead of the main idea is a reading deficit. The agent must evaluate keyword context, not just keyword presence.

**Spiky POV Myth 8: We don't believe that all errors on a writing test indicate writing deficits.** *(Added v1.2, expanded v1.3)*
Some G3-5 errors — particularly those involving figurative language interpretation, character trait inference, textual evidence usage, main idea identification, cause-and-effect reasoning from text, or non-literal meaning extraction — are reading comprehension deficits, not writing deficits. The student can write grammatically correct sentences but misinterprets what the text means or cannot extract appropriate information from the passage. These errors must be flagged for reading support; assigning writing activities for reading comprehension issues is not only ineffective but misdiagnoses the problem. Reading is a separate subject outside AlphaWrite's scope. When 3 or more errors on a single test are reading comprehension deficits, the system must flag for human review — the student's primary barrier may be reading, and writing remediation alone may be insufficient.

---

## Knowledge Tree *(Sources: DOK 2 | Insights: DOK 3)*

### Category 1: Test Architecture and Scoring

**Summary:** Understanding how tests are structured and scored is the foundation for all diagnostic and assignment decisions. The agent must know the scoring weights, question types, and grade-band differences to correctly classify a student's performance and determine the appropriate action tier.

**Sources:** *(DOK 2)*

- **AlphaWrite Standardized Writing Tests G3-G8**
   - Summary: G3-5 tests have 45 points total: Q1-5 are constructed-response "Edit the Text" questions (2pts each = 10pts), Q6-10 are "Write a Sentence" constructed-response questions (3pts each = 15pts), Q11 is "Write a Paragraph" (20pts). G6-8 tests have 30 points total: Q1-10 are multiple-choice (1pt each = 10pts), Q11 is "Write an Expository Essay" (20pts with a 5+5+4+3+3 rubric). Pass threshold is 90% for both bands.
   - Key facts: G3-5 essay weight is 44.4% of total; G6-8 essay weight is 66.7% of total. Tests are available in multiple variants (G3 has 10, G4 has 8, G5 has 4, G6 has 6, G7 has 5, G8 has 5). Students always receive the first test they haven't completed.
   - Link: Tests folder (PDF files for each grade/variant)
   - Insights: The asymmetric essay weight in G6-8 means that the essay performance single-handedly determines the action tier. A student who gets all MCQs right but scores 13/20 on the essay still only hits 77%, which triggers full enrollment. This weighting makes the 80% threshold the critical dividing line for G6-8.

- **AlphaWrite Skill Plan 2025-2026**
   - Summary: The source of truth for all lesson IDs, names, QS_IDs, order numbers, grade levels, courses, URLs, and activity descriptions. Contains 1021 rows covering all G3-8 activities. Every lesson assignment must reference IDs from this document.
   - Key facts: G3 has 26 S+P activities (6.5h), G4 has 31 (7.8h), G5 has 31 (7.8h), G6-8 each have 24 S+P activities (6.0h) plus 5 essays (10.4h) totaling 29 activities (16.4h). Each S/P lesson takes approximately 15 minutes. Each full essay (5 stages: Setup, Outline, Draft, Revise, Polish) takes approximately 125 minutes.
   - Link: AlphaWrite Skill Plan 2025_2026 (2).xlsx
   - Insights: The dramatic difference in course size between G3-5 (6.5-7.8h) and G6-8 (16.4h) justifies different decision frameworks for each band. G3-5 courses are short enough that full enrollment is always cost-effective. G6-8 courses are large enough that targeted hole-filling saves meaningful time for students who demonstrate near-mastery.

**Insights on Category 1:** *(DOK 3)*
- Insight 1: The 66.7% essay weight in G6-8 creates a natural decision boundary at 80%. Above this line, essay competence is confirmed and MCQ-level gaps are the primary issue. Below this line, essay competence is uncertain and the full scaffold is warranted.
- Insight 2: G3-5 course brevity (6.5-7.8h) means the time cost of full enrollment vs. hole-filling is only 3-5 additional hours. This makes full enrollment the dominant strategy for all G3-5 test-out failures.
- Insight 3: Multiple test variants per grade mean the agent must read the actual question prompt to determine which skill is being tested. Question positions are consistent in structure but vary in specific skill focus across variants.

---

### Category 2: Diagnostic Framework (The 10 Agent Questions)

**Summary:** The agent follows a systematic 10-question diagnostic process for every test failure. These questions move from classification (test type, score tier) through analysis (missed questions, root causes, prerequisites, patterns) to construction (lesson selection, ID verification, order validation). No step can be skipped.

**Sources:** *(DOK 2)*

- **Noel Pilkington's Current Hole-Filling Process**
   - Summary: The current manual 8-step process used by the Writing Learning Strategist to build remediation plans. Steps include: reading the test, reading student responses, identifying gaps, determining prerequisites, selecting lessons, ordering by Skill Plan, verifying IDs, and generating the Gap Analysis Report.
   - Key facts: The manual process takes 15-30 minutes per student. Human experts use pattern recognition across questions to diagnose systemic gaps rather than treating each question independently. The expert always reads the student's actual response before determining root cause.
   - Link: Current Hole-filling process.docx
   - Insights: The human expert's greatest advantage is pattern recognition across questions. The agent must replicate this by explicitly checking for recurring error patterns (Step 6 of the diagnostic framework) rather than treating each missed question as independent.

- **Writing AI-Generated Hole-Filling vs Manual Custom Plans**
   - Summary: A precedent library of approximately 75 student cases comparing system-generated plans with human expert plans. Each case includes student information, test scores, and side-by-side plan comparisons.
   - Key facts: Common differences between system and human plans include: system under-prescribing (missing prerequisites, assigning incomplete scaffolds, and failing to detect root causes that require additional foundational activities), system misdiagnosing (assigning writing activities for reading comprehension deficits), and system not distinguishing between competence and transfer gaps.
   - Link: Writing AI-generated hole-filling vs Manual Custom Plans (2).xlsx
   - Insights: The precedent library reveals that the most common AI error is under-prescription: missing prerequisite activities, assigning incomplete scaffolds (e.g., 1 of 5 needed synthesis activities), and failing to detect that the root cause lies deeper than the tested skill. The human expert consistently produces more complete plans that address root causes and include full prerequisite chains, rather than superficially mapping each missed question to a single activity.

- **AI-Recommended vs. Human-Reviewed Plan Comparison** *(DOK 3)*
   - Summary: Analysis of recurring patterns when comparing the AI's initial lesson recommendations against the final plans produced after human expert review. This comparison reveals systematic gaps in the AI's diagnostic reasoning that the automation rules and tool must correct for.
   - Key facts: The most common patterns of AI under-prescription include: (1) **Missing prerequisites** — the AI assigns the target skill (e.g., Write Appositives) without checking whether the student can perform the prerequisite (e.g., Identify Appositives), resulting in a plan that will fail at the first activity. (2) **Incomplete scaffolds** — the AI assigns a single activity for a multi-step deficit (e.g., assigning only Identify Topic Sentences for a synthesis gap that requires a 5-activity scaffold from Identify TS through Write a Paragraph from Prompt). (3) **Misdiagnosed reading deficits** — the AI assigns writing activities for errors that are actually reading comprehension deficits (e.g., assigning Eliminate Irrelevant Sentences when the student's answer was irrelevant to the question because they couldn't identify the passage's main idea). (4) **Missing task comprehension detection** — the AI treats a student who wrote the wrong text type entirely (e.g., a question instead of a paragraph) as if they have a content deficit rather than a prompt comprehension deficit, leading to a scaffold that doesn't address the actual gap. After human review, plans are typically adjusted by adding prerequisite activities, completing partial scaffolds, removing misdiagnosed reading activities, and reclassifying error patterns.
   - Link: Writing AI-generated hole-filling vs Manual Custom Plans (2).xlsx (comparison tab)
   - Insights: The delta between AI-recommended and human-reviewed plans consistently shows the AI under-prescribing by 2-4 activities per student. The AI's primary failure mode is surface-level pattern matching — it maps each missed question to the most obvious activity without examining WHY the student got it wrong. The human expert reads the student's actual response, identifies the root cause (which is often a prerequisite gap rather than the tested skill), and builds a complete scaffold from that root cause forward. This analysis validates the need for the automation rules' emphasis on prerequisite detection, scaffold completion, context-aware keyword matching, and reading deficit flagging.

**Insights on Category 2:** *(DOK 3)*
- Insight 1: The diagnostic process is hierarchical: test type and score tier determine the decision framework; question-level analysis determines specific lessons; pattern analysis may override individual question mappings; prerequisite detection may add lessons that no question directly maps to.
- Insight 2: Root cause analysis of the student's actual response is what separates expert remediation from generic mapping. The same missed question can produce different lesson assignments depending on WHY the student got it wrong.
- Insight 3: The distinction between "fundamental skill deficit" (needs prerequisite) and "partial understanding" (needs target skill only) is the single most impactful diagnostic decision in the system.
- Insight 4: The AI's under-prescription pattern is systematic, not random. It consistently misses the same types of gaps: prerequisites, scaffold completions, and reading deficit detection. This means the automation rules must explicitly encode these checks as mandatory steps, not optional heuristics.

---

### Category 3: Scenario 1 - Same-Grade Test Failure

**Summary:** When a student scores below 90% on their current grade-level test, the agent assigns targeted hole-filling from the SAME grade. The goal is the smallest effective set of lessons that will close identified gaps and prepare for a successful retake. G6-8 same-grade hole-filling has a hard constraint: no Essays are ever assigned.

**Sources:** *(DOK 2)*

- **Cognitive Load Theory (Sweller, via Kirschner & Hendrick)**
   - Summary: Cognitive Load Theory explains why targeted hole-filling works for same-grade failures. The student has already been exposed to the grade-level content; they have existing schemas (however incomplete). Targeted remediation adds to these schemas without overwhelming working memory. Full course re-enrollment would create unnecessary extraneous load by revisiting mastered skills.
   - Key facts: Three types of cognitive load: intrinsic (inherent complexity), extraneous (poor design), germane (schema construction). Targeted hole-filling minimizes extraneous load (no unnecessary lessons) while maximizing germane load (all practice directly builds missing schemas).
   - Link: How Learning Happens (Kirschner & Hendrick, 2020), Chapter on Cognitive Load Theory
   - Insights: Same-grade hole-filling is the one scenario where a lean plan is always correct. The student has already built partial schemas at this grade level; the job is to fill specific holes, not rebuild the entire structure.

- **Rosenshine's Principles of Instruction**
   - Summary: Rosenshine's 10 principles validate the hole-filling approach. Principle 1 (begin with review of previous learning) maps to the agent reviewing what the student demonstrated mastery of. Principle 7 (obtain high success rate of 80%+) validates the 90% pass threshold. Principle 9 (require independent practice) maps to the transfer gap distinction.
   - Key facts: The 90% threshold aligns with Rosenshine's guidance that students should achieve a high success rate before advancing. Students scoring 80-89% are close but not yet at the level where advancement is safe.
   - Link: How Teaching Happens (Kirschner, Hendrick & Heal, 2022)
   - Insights: The same-grade hole-filling process directly implements Rosenshine's "check for understanding at each point" principle. The test IS the check; the hole-filling IS the targeted re-teaching.

**Insights on Category 3:** *(DOK 3)*
- Insight 1: The hard constraint against G6-8 essays in same-grade hole-filling exists because essay slots can only be completed once. Using scarce essay slots for same-grade remediation would reduce the slots available for future enrollment or test-out assignments.
- Insight 2: For same-grade G6-8 failures where the essay (Q11) is the primary weakness, the agent must use Paragraphs activities as proxies: Make Topic Sentences, Writing SPOs, Turn Outline into Draft, Elaborate on Paragraphs, Using Transition Words, and Write a Free-Form Paragraph all build toward essay skills without consuming essay slots.
- Insight 3: Q11 failures require architecture-specific diagnosis, not generic competence vs. transfer logic. For G6-8, the primary pattern is **evidence extraction gaps** (student uses outside knowledge instead of passage evidence) — addressed with the SPO → Writing SPOs → Outline → Elaborate scaffold. For G3-5, the primary pattern is **multi-section synthesis gaps** (student only summarizes first section) — addressed with the complete 5-activity synthesis scaffold (Identify TS → Make TS → Identify TS & Sequence → Turn into SPO → Write from Prompt). Standard competence vs. transfer logic only applies when neither pattern is detected.
- Insight 4: **Positive competency detection** must precede lesson assignment. Even when a student fails Q11, they may demonstrate competency in sub-skills (e.g., competent topic sentences but weak evidence extraction). Assigning activities for demonstrated skills wastes time and dilutes focus. Scan gap analysis for positive indicators ("correctly identified the essay's topic," "has structure") and block related activities.
- Insight 5: **Scaffold completion** is non-negotiable. When a synthesis or evidence extraction gap is detected, the COMPLETE scaffold sequence must be assigned — not just the first step. Under-prescription is more harmful than over-prescription because it leaves core deficits unaddressed, leading to repeated test failure.
- Insight 6: **Task comprehension failure (writing the wrong text type entirely) is a distinct Q11 pattern** that requires a different scaffold from synthesis or evidence gaps. *(Added v1.3)* When a student writes a question instead of an explanatory paragraph, the issue isn't organizing evidence or synthesizing across sections — it's understanding what the prompt requires. This pattern needs a shorter, more targeted scaffold (Write Sentence from a Prompt → Write a Paragraph from Prompt) because the fundamental gap is prompt deconstruction, not paragraph planning. This is distinct from synthesis gaps (wrote paragraph from only first section) and evidence gaps (used outside knowledge instead of passage evidence).
- Insight 7: **Reading comprehension deficits can dominate a writing test error profile** without indicating writing skill deficits. *(Added v1.3)* When 3+ errors on a G3-5 test are reading comprehension deficits (mapped to RL/RI standards), the student's primary barrier may be reading, not writing. The agent must flag these cases for human review — writing hole-filling alone cannot address a reading comprehension deficit, and assigning writing activities for reading-based errors is both ineffective and diagnostically misleading.

---

### Category 4: Scenario 2 - Next-Grade Test-Out Failure

**Summary:** When a student passes their current grade (90%+) and then scores below 90% on the next grade's test, the agent must decide between targeted hole-filling and full enrollment. The decision depends on both the score tier and the grade band. G3-5 always gets full enrollment. G6-8 is tiered: 80-89% gets targeted S+P hole-filling plus all 5 essays; below 80% gets full enrollment (all S+P + all 5 essays).

**Sources:** *(DOK 2)*

- **Datchuk's Fluency Research**
   - Summary: Datchuk's research on sentence-level fluency provides the evidence base for full enrollment in G3-5 test-out failures. Writing fluency requires varied, repeated practice for automaticity. A student who passes a test through general ability has demonstrated competence but not necessarily fluency. The short G3-5 courses (6.5-7.8h) serve as fluency-building investments where mastered skills complete quickly and function as spaced review.
   - Key facts: Sentence combining fluency is a significant predictor of composition quality. Automaticity at the sentence level frees working memory for paragraph and essay planning. Skills that ARE mastered will be completed in ~5 minutes instead of ~15, functioning as retrieval practice.
   - Link: Datchuk fluency research papers; "A review of writing interventions" (2015)
   - Insights: The "mastered skills fly by quickly" insight transforms full enrollment from a time penalty into a fluency investment. The additional 3-5 hours for full enrollment vs. hole-filling in G3-5 is almost entirely productive practice.

- **Math Academy's Encompassing Principle**
   - Summary: Advanced tasks implicitly practice simpler skills, but succeeding on an advanced task through general ability doesn't confirm mastery of the underlying scaffold. A student who writes an acceptable paragraph through talent hasn't necessarily internalized the planning, outlining, and drafting process. Full enrollment ensures the scaffold activities that build this process (SPO, Turn Outline into Draft, Elaborate on Paragraphs) are completed.
   - Key facts: The "encompassing principle" means that each skill in the scaffold must be verified, not inferred. Just because a student can write a paragraph doesn't mean they can write an SPO. The scaffold skills are prerequisites for G6-8 essay success.
   - Link: The Math Academy Way (working draft)
   - Insights: The encompassing principle is why the agent never hole-fills G3-5 test-out failures. The untested scaffold activities aren't "extra": they're the structural foundation that makes tested skills durable and transferable.

- **Bjork's Desirable Difficulties and the Transfer Gap**
   - Summary: Bjork's framework explains the practice-to-test gap in G6-8. AlphaWrite practice reduces difficulty through scaffolding and topic choice. Tests impose "desirable difficulties" by removing these supports. For the 80-89% tier, the student has already demonstrated competence under difficult conditions: they need calibration, not re-teaching. For below 80%, the student hasn't yet established the competence base needed to benefit from desirable difficulties: full enrollment builds that base.
   - Key facts: Desirable difficulties enhance long-term retention ONLY after competence is established. Spacing, interleaving, and reduced feedback help learners who already have schemas. For novices, these same conditions impair learning. This is why the 80% threshold is the dividing line.
   - Link: Bjork, "Making things hard on yourself, but in a good way" (2011)
   - Insights: The 80% threshold isn't arbitrary: it represents the competence boundary below which desirable difficulties become UNdesirable. Students below 80% need more support, not more challenge.

**Insights on Category 4:** *(DOK 3)*
- Insight 1: The G5-to-G6 transition is the most critical in the system. G6 introduces essays (10.4 additional hours). A student entering G6 without solid paragraph planning skills will struggle with the essay scaffold. This is why full enrollment in G5 is especially important.
- Insight 2: The 80-89% G6-8 tier is the only scenario where targeted S+P hole-filling (rather than full S+P) is assigned. This works because the student has demonstrated essay competence under test conditions (necessary given the 66.7% essay weight), and the MCQ gaps represent specific, isolated skill deficits. The full 5-essay sequence builds fluency without requiring redundant S+P practice.
- Insight 3: Both tiers (80-89% and below 80%) assign all 5 essay slots. Any previously completed slots carry over as "complete," so the student only does remaining unused slots. The difference between tiers is S+P assignment: 80-89% gets targeted gaps only; below 80% gets all S+P activities.

---

### Category 5: Prerequisite Skill Detection

**Summary:** When a student fails a question, the root cause may be a missing prerequisite, not the tested skill itself. The agent must examine the student's actual response to determine where in the prerequisite chain the breakdown occurred, then assign from that point forward. Prerequisite detection prevents both over-prescription (assigning unnecessary lessons) and under-prescription (assigning a skill the student can't yet learn).

**Sources:** *(DOK 2)*

- **Ausubel's Prior Knowledge Principle (via Kirschner & Hendrick)**
   - Summary: "The most important single factor influencing learning is what the learner already knows." This principle governs the entire prerequisite system. If a student doesn't know what an appositive is (prior knowledge), they cannot learn to write one (new skill). The agent must assess prior knowledge through response analysis before assigning new skills.
   - Key facts: Four types of subsumption determine how new knowledge connects to existing schemas. Derivative subsumption (new knowledge is an example of existing schema) works when the prerequisite exists. Correlative subsumption (new knowledge extends existing schema) requires the prerequisite schema to be in place first.
   - Link: How Learning Happens (Kirschner & Hendrick, 2020)
   - Insights: The prerequisite detection system is an operationalization of Ausubel's principle. Every prerequisite chain in the automation rules represents a verified dependency: the later skill cannot be learned without the earlier one.

- **AlphaWrite Prerequisite Chains (Empirical)**
   - Summary: Sentence-level chains include: Identify Appositives before Write Appositives before Combine Sentences with Appositives; Identify Sentence Type before Change Sentence Type before Write Sentence Type; Fragment or Sentence? before Combine Sentences; Because, But, So before Subordinating Conjunctions. Paragraph-level chains include: Identify Topic Sentences before Make Topic Sentences; Turn Paragraph into SPO before Writing SPOs before Turn Outline into Draft; the full scaffold before Write a Paragraph from Prompt.
   - Key facts: Detection signals are graded: blank response = check all prerequisites; fundamental misunderstanding = assign recognition-level prerequisite; partial understanding with structural errors = target skill only; conventions-only errors = no prerequisite needed. The agent determines prerequisite needs by examining the actual response, not just the score.
   - Link: Writing Automation Rules - Complete.md, Section 6
   - Insights: The single most impactful diagnostic decision is distinguishing between "fundamental skill deficit" (student doesn't understand the concept, needs prerequisite) and "partial understanding" (student understands the concept but executes imperfectly, needs target skill only). Getting this wrong in either direction wastes student time.

**Insights on Category 5:** *(DOK 3)*
- Insight 1: Prerequisite detection is what makes expert remediation consistently better than generic AI-generated plans. The precedent library shows that missing prerequisites is the second most common AI error.
- Insight 2: The agent should be biased toward assigning prerequisites when uncertain. A student who completes an unnecessary prerequisite loses ~15 minutes. A student who skips a needed prerequisite fails the target activity and needs the prerequisite anyway, losing ~30+ minutes.
- Insight 3: Conventions errors (spelling, punctuation, grammar mechanics) almost never indicate a prerequisite need. A student who writes a correct appositive but omits one comma has demonstrated the skill. Assigning Identify Appositives for this student would be a waste.

---

### Category 6: G6-8 Essay Management

**Summary:** G6-8 essay slots are a scarce, non-renewable resource. Each grade has exactly 5 essay slots (each with 5 stages: Setup, Outline, Draft, Revise, Polish). Once completed, a slot cannot be reassigned. The agent must track essay slot availability and assign based on the action tier. Same-grade hole-filling never assigns essays (hard constraint). Test-out hole-filling (80-89%) assigns all 5 essays for fluency development. Full enrollment (below 80%) also assigns all 5 (with completed slots carrying over).

**Sources:** *(DOK 2)*

- **McCutchen's Capacity Theory Applied to Essay Writing**
   - Summary: The essay represents the highest cognitive demand in the AlphaWrite curriculum. Students must simultaneously manage planning, text generation, evidence integration, organization, and conventions. McCutchen's capacity theory predicts that only students with automated sentence and paragraph skills will have sufficient working memory for essay-level composition. This is why essay slots should only be assigned when the foundation is confirmed.
   - Key facts: Writing Quality = f(Working Memory Capacity - Transcription Demands). For essays, "Transcription Demands" includes not just handwriting/typing but also sentence construction, paragraph organization, and evidence selection. If any of these sub-skills are effortful rather than automatic, essay quality suffers.
   - Link: McCutchen, "A capacity theory of writing" (1996)
   - Insights: The hard constraint against essays in same-grade hole-filling is both a resource scarcity decision and a pedagogical one. If a student has sentence and paragraph gaps at their current grade level, those must be resolved before essay practice can be productive. Assigning an essay to a student with sentence-level gaps would consume a scarce slot while producing a low-quality learning experience.

- **Boscolo & Hidi's Interest and Transfer**
   - Summary: AlphaWrite essays leverage student interest (topic choice) and scaffolding (guided stages) across ALL activities. This makes practice highly effective for building skills but creates a predictable, partly structural transfer gap when students face test essays on unfamiliar passages without scaffolding or interest support. AlphaWrite activities can remove scaffolding but cannot remove interest support, since students always choose their own topic context. The full 5-essay sequence assigned at the 80-89% tier builds fluency by internalizing the planning→drafting→revising cycle through volume, partially closing the scaffolding component of the transfer gap.
   - Key facts: The four-phase interest model predicts that students will engage more deeply with essays on self-chosen topics. This engagement produces better learning. Volume of practice (5 essays vs. 2) transforms this engagement into automaticity of the writing process. However, test conditions impose two simultaneous challenges — unfamiliar content AND no scaffolding — while AlphaWrite can only address one (scaffolding removal). The interest component of the transfer gap is inherent.
   - Link: Writing and Motivation (Boscolo & Hidi, 2007)
   - Insights: The 5-essay sequence builds automaticity of the writing process, partially closing the transfer gap. However, some degree of practice-to-test gap is structurally expected because AlphaWrite cannot replicate the interest removal that tests impose. This insight is critical for diagnosis: the agent must not interpret a normal-range transfer gap (80-89%) as a competence deficit requiring heavy intervention.

**Insights on Category 6:** *(DOK 3)*
- Insight 1: Essay slot tracking is an operational necessity, not just a pedagogical concern. If the agent assigns a completed slot, the Timeback system will either error or produce a null assignment.
- Insight 2: Edge cases (all 5 slots exhausted) require adaptation. If a student has completed all 5 essays but essay performance remains weak, the agent assigns only S+P activities and flags for human review. The constraint forces alternative remediation strategies.
- Insight 3: Previously completed essay slots carry over upon full enrollment. A student who completed Essays 1-5 in the 80-89% tier and later scores below 80% on a retake would be assigned full S+P enrollment but no additional essays (all slots exhausted). This scenario should be rare but must be handled gracefully.

---

### Category 7: Non-Negotiable System Constraints

**Summary:** Eight hard constraints govern the automation system. These cannot be overridden by any diagnostic logic, learning science principle, or edge case reasoning. They exist to protect system integrity, student time, and data quality. The eighth constraint — scaffold completion — was added in v1.2 based on validation testing showing that incomplete scaffolds leave core deficits unaddressed.

**Sources:** *(DOK 2)*

- **AlphaWrite System Architecture Constraints**
   - Summary: The constraints are: (1) Grade-level alignment: only assign lessons from the target grade in the Skill Plan. (2) Skill Plan order: all lessons follow exact Skill Plan sequence, Sentences before Paragraphs. (3) No essays in same-grade G6-8 hole-filling. (4) No ID guessing: only use IDs confirmed in the Skill Plan. (5) Minimum plan size: at least 1 lesson, or flag for human review. (6) Essay slot integrity: completed slots cannot be reassigned. (7) Human review flags: triggered by G3-5 scores below 70%, G6-8 scores below 50%, exhausted essay slots with remaining gaps, unclear root causes, or non-writing barriers.
   - Key facts: Constraint 4 (No ID guessing) exists because the Timeback system will reject invalid IDs, causing the entire assignment to fail. Constraint 7 (Human review flags) ensures the system maintains humility about edge cases that exceed its diagnostic capacity.
   - Link: Writing Automation Rules - Complete.md, Section 10
   - Insights: These constraints represent the boundary between automation and human judgment. The agent operates autonomously within these constraints; violations trigger human escalation. This design prevents the agent from confidently making errors that a human would catch.

- **Engelmann's Direct Instruction Principle: Instruction Must Avoid Misinterpretation**
   - Summary: Engelmann's fifth principle states that instruction must be carefully planned to avoid learner misinterpretation. Applied to the automation system, this means lesson assignments must be unambiguous: the correct lessons, in the correct order, with the correct IDs. An assignment that includes a wrong ID, wrong order, or wrong grade level will confuse the system and potentially assign inappropriate content to the student.
   - Key facts: Direct Instruction requires "clear, unequivocal signals." In the automation context, the lesson ID IS the signal. An incorrect ID is an unequivocal misinstruction.
   - Link: Theory of Instruction (Engelmann & Carnine, 1991)
   - Insights: The "No ID guessing" constraint is the automation equivalent of Engelmann's clarity principle. Just as a teacher script must avoid ambiguity, the agent's output must avoid ID errors. When uncertain, the agent flags for human review rather than guessing.

**Insights on Category 7:** *(DOK 3)*
- Insight 1: The constraints create a "fail-safe" system. When the agent encounters an edge case it cannot resolve (unclear root cause, exhausted essay slots, very low scores), it flags for human review rather than making a potentially harmful decision.
- Insight 2: Skill Plan order is not just a formatting preference. The order reflects the pedagogical scaffold: earlier skills are prerequisites for later ones. Violating the order means the student encounters skills before their prerequisites, undermining learning.
- Insight 3: The human review flag system is the humility mechanism. It acknowledges that a single test score is an imperfect measure and that some situations require human judgment that the automation cannot replicate.

---

### Category 8: The Practice-to-Test Transfer Gap

**Summary:** AlphaWrite practice and standardized tests create fundamentally different cognitive conditions. Understanding this gap is essential for accurate diagnosis, particularly in G6-8 where the essay constitutes 66.7% of the test score. The agent must distinguish between students who have genuine skill deficits and students whose skills are strong but don't transfer to unscaffolded conditions.

**Sources:** *(DOK 2)*

- **Cognitive Load Theory Applied to Writing Assessment (Sweller, via Kirschner)**
   - Summary: AlphaWrite reduces both intrinsic load (student-chosen topics reduce content unfamiliarity) and extraneous load (guided stages reduce process uncertainty). Tests remove both supports simultaneously: unfamiliar passage (increased intrinsic load) + no scaffolding (increased extraneous load). The total cognitive demand on the test is substantially higher than in practice, even when the same skills are required.
   - Key facts: When both intrinsic and extraneous load spike simultaneously, the remaining working memory for germane processing (actual learning/performance) plummets. This explains why students who write fluently in AlphaWrite can produce disorganized, thin essays on tests. It's not that they can't do it; it's that their working memory is overwhelmed.
   - Link: How Learning Happens (Kirschner & Hendrick, 2020)
   - Insights: The transfer gap is not a flaw in AlphaWrite's design. The scaffolding and topic choice serve a pedagogical purpose: they allow students to focus cognitive resources on skill development rather than content processing. The test then measures whether those skills have been internalized to the point of automatic application. The gap is diagnostic information, not a failure.

- **Bjork's Learning vs. Performance Distinction**
   - Summary: Bjork's critical distinction: performance during learning (scaffolded, supported) is a poor predictor of learning (durable, transferable). A student who performs well in AlphaWrite practice is demonstrating performance. A student who performs well on the test is demonstrating learning. The gap between these is expected and natural. The agent's job is to determine whether the gap is within normal range (80-89%, where calibration essays suffice) or indicates deeper issues (below 80%, where full enrollment is needed).
   - Key facts: Conditions that improve immediate performance (scaffolding, massed practice, familiar topics) often REDUCE long-term learning and transfer. Conditions that impair immediate performance (spacing, interleaving, testing, unfamiliar contexts) often ENHANCE long-term learning. But this only works after a baseline of competence is established.
   - Link: Bjork, "Making things hard on yourself, but in a good way" (2011)
   - Insights: The 80% threshold operationalizes Bjork's insight. Above 80%, the student has demonstrated sufficient competence that transfer practice (calibration essays, unscaffolded activities) will enhance their learning. Below 80%, the competence base isn't solid enough for desirable difficulties to be productive.

**Insights on Category 8:** *(DOK 3)*
- Insight 1: The transfer gap makes Diagnostic Question 7 (competence vs. transfer) the most consequential question in the G6-8 diagnostic framework. Getting it wrong means either over-prescribing (full scaffold for a transfer gap) or under-prescribing (transfer practice for a competence gap).
- Insight 2: The transfer gap predictably affects Q11 more than Q1-10. MCQ questions require recognition (lower cognitive load); essay writing requires production (higher cognitive load). A student may show no transfer gap on MCQs but a significant gap on the essay.
- Insight 3: Write a Paragraph from Prompt and Write a Free-Form Paragraph partially bridge the transfer gap by removing scaffolding (guided stages) while keeping students in the AlphaWrite environment. However, these activities cannot fully replicate test conditions because students still choose their own topic context in all AlphaWrite activities. The interest component of the transfer gap is structural — tests force writing about unfamiliar passages, which no AlphaWrite activity replicates. This means some degree of practice-to-test gap is expected and normal; the diagnostic question is whether the gap size indicates a transfer problem (manageable) or a deeper competence problem (requires full scaffold).

---

*Writing Hole-Filling & Test-Out Assignment Brainlift*
*Created: February 2026*
*Owner: Noel Pilkington*
