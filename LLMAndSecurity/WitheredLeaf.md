
# TODOs

## Measurement

### Dataset Preparation (Yifan & Xing)

- Considering different entities (operator, variable, function, literal)
- Synthesized (bug)
- Original (benign: manually confirm bug free)

### Measurement (for system design) (Hongbo)

#### Local LM

- Algorithms
  - Native (direct infilling)
  - Select-based (check log prob)
  - Gen-based (check consistency)
  - Encoder model: BERT
  - Threshold (log probability)
- Prompt
  - Entire file
  - Whole function
  - Whole class (if applicable)
  - Instruct

#### Remote LM

- Prompt Design

## Experiment

### Static Analysis (Xing)

- Rust support (done)
- Operator/Literal support

### Run Real World (Hongbo)

## Writing

- Low accuracy?
  - Sorted confidence
  - Comparable with other work (stress it)
- EIB
- Importance

# Reviews

## CCS Review

Review #2173A
===========================================================================

Paper summary
-------------
This paper introduces WitheredLeaf, an automated system that utilizes Large Language Models (LLMs) such as GPT-4 to detect Entity-Inconsistency Bugs (EIBs). WitheredLeaf enhances the detection of these errors, commonly found in variable identifiers and function names, through a cascaded model strategy and optimized prompt templates. The system demonstrated efficiency and accuracy in tests on synthetic datasets and real-world code repositories, successfully identifying bugs and validating its practicality through developer-merged fix requests. Moreover, the paper discusses the system's limitations and future improvement directions, highlighting the potential of this technology in enhancing software development safety and quality assurance.

Strengths / Reasons to accept
-----------------------------
+ Innovative Use of LLMs: The paper effectively demonstrates how Large Language Models (LLMs), such as GPT-4, can be leveraged beyond typical applications like text generation to the more niche area of detecting entity-inconsistency bugs in code. This innovative use opens new avenues for the application of LLMs in software engineering.

+ Cascaded Model Strategy: WitheredLeaf employs a sophisticated cascaded approach that integrates multiple models to enhance detection capabilities. This strategy not only improves the accuracy of bug detection by minimizing false positives and negatives but also optimizes computational resources by strategically filtering and escalating potential bugs through different stages.

Weaknesses / Reasons to reject
------------------------------
- Missing discussions on variable misuse bugs in program repair
- Weak security implications of EIB
- Unjustified uses of LLMs
- Lack of comparison to related works

Constructive comments for author
--------------------------------
The authors target at Entity-Inconsistency Bugs (EIB), which refers to the bugs caused by misuses of wrong program entities such as variables and functions. While the authors propose a LLM-based approach to detect this kind of bugs and the evaluations demonstrate the effectiveness, there are several major concerns of the paper's contributions that make the paper not ready for publication.

First, detecting Entity-Inconsistency Bugs is not first explored by this paper. This kind of bugs are referred to as "variable misuse" bugs and were first addressed by existing learning-based techniques [1][2]. It was then considered as one of the types of bugs to be addressed by program repair techniques, and a series of works were proposed to improve the techniques in detecting and fixing them automatically. Unfortunately, such closely related work were not discussed in the paper and makes the paper's contribution unclear.

[1] Allamanis, Miltiadis, Marc Brockschmidt, and Mahmoud Khademi. "Learning to represent programs with graphs.". ICLR 2018.

[2] Vasic, Marko, Aditya Kanade, Petros Maniatis, David Bieber, and Rishabh Singh. "Neural program repair by jointly learning to localize and repair." ICLR 2019.


Second, the security implication for EIB was briefly mentioned in the paper but was never explained in detail, and thus making the significance of the work's contribution to security unclear. In fact, many variable misuse bugs are functionality bugs and not security related bugs.

Third, the paper does not justify why LLM has to be used for detecting such bugs. In fact, there exist a series of works for variable misuse bugs and they may produce better results than LLM because they are trained with the related code with similar contexts. The authors should better discuss the related work and redo the evaluations to compare with related works to show the improvements. In fact, for certain tasks, deep learning is doing better than LLM such as prediction and classification. But LLM has its unique advantages in understanding the semantics of long documents. The authors should explore deeper on how these two types of techniques work for the different tasks in detecting EIBs.

Finally, the authors should delve deeper into strategies for reducing the rate of false positives and negatives, which are critical for the practical deployment of such systems in real-world scenarios. Detailed analysis and solutions to mitigate these issues would strengthen the paper's impact and applicability.

Questions for authors’ response
-------------------------------
1. How are EIB different from variable misuse bugs in the related works?
2. What are the security significance of EIB?
3. What is the justification to use LLM? How is LLM compared with deep learning techniques?
4. Can you better explain the false positives and negatives?

Does the paper raise ethical concerns?
--------------------------------------
1. No

Reviewer expertise in this domain
---------------------------------
3. Knowledgeable (I don't necessarily work in this topic domain, but I work
   on related topics or I am cognizant of the work in this domain in recent
   years)

Reviewer confidence
-------------------
4. Confident

Overall merit
-------------
2. Weak reject


* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *


Review #2173B
===========================================================================

Paper summary
-------------
This paper focuses on Entity-Inconsistency Bugs (EIBs), which are semantic bugs that involve the misuse of syntactically valid program entities and can have security implications. Traditional detection methods struggle to identify EIBs due to their subtle nature and context-dependency. The paper first evaluates the capabilities of LLMs, specifically GPT-4, in detecting EIBs and finds that although promising, GPT-4 has limited recall and precision. To address this limitation, the paper proposes a novel cascaded EIB detection system called WitheredLeaf. WitheredLeaf utilizes smaller, code-specific language models to filter out irrelevant code snippets and improve precision and recall. The system is evaluated on a significant scale, with 154 Python and C GitHub repositories, each with over 1,000 stars. The evaluation results in the identification of 123 new flaws, 45% of which have the potential to disrupt program operations.

Strengths / Reasons to accept
-----------------------------
* The paper targets an essential problem
* The approach of WitheredLeaf is interesting and seems effective in the evaluation
* The evaluation is comprehensive, and WitheredLeaf found new bugs in realistic programs

Weaknesses / Reasons to reject
------------------------------
* The empirical comparison with the previous efforts is not sufficient
* The precision (around 20%) is still too low in practice, and the corresponding patterns or reasons of false positives are not well studied

Constructive comments for author
--------------------------------
Thank you for submitting your paper to CCS 2024. I enjoyed reading the paper as it is well-presented and provides intuitive insights. The paper addresses a crucial category of bugs known as entity-inconsistent bugs, which are often challenging to detect using conventional abstract-interpretation-based static analysis methods. The concept of guiding LLMs (LLMs) to focus on relevant entities, reducing distractions, is intuitive and reasonable. The authors also introduce a new LLM-based approach, utilizing a set of lightweight, open-source LLMs to identify suspicious entities before subjecting them to the more powerful yet costly GPT-4 for a detailed analysis. This approach effectively balances efficiency and accuracy. The evaluation conducted is comprehensive, involving 80 Python and 74 C repositories and the discovery of 30 new bugs in practice.  Overall, the paper presents a clear contribution to dealing with entity-inconsistent bugs and providing insights into LLM-guided bug detection. I just had the below substantial comments.



Despite the discussion in Section 4.1.3, the paper lacks an empirical comparison with the related work [45] [7]. Notably, the results of [45] demonstrate that their approach achieves a high accuracy (ranging from 89% to 95% when applied to a corpus of 150,000 JavaScript files), which appears to be more effective than WitheredLeaf. It would be interesting to explore whether WitheredLeaf can achieve higher precision and recall for the bugs that are detectable by both WitheredLeaf and the approach in [45]. Furthermore, in comparison with the work [6], the authors only select subsets of datasets comprising 66 functions from D-Synthesized. I am curious why the authors did not choose to compare FLAG and WitheredLeaf by utilizing all available datasets. Also, based on what principles were the subsets selected?

The precision of WitheredLeaf remains relatively low, around 25%, in real-world programs. Although the authors reference a paper [7] to argue that this precision level could be acceptable in practice, in my own experience, this precision is still quite low, posing challenges to using the tool. It would be valuable if the authors could analyze the false positives and the patterns identified by WitheredLeaf and discuss potential strategies to enhance precision.

Questions for authors’ response
-------------------------------
* What are the reasons for lacking an empirical comparison with the works [45] [7]? Additionally, how were the subsets of datasets selected when compared with the work [6]? Why not use the real-world dataset?
* Can you clarify the primary reasons or recurring patterns of false positives induced by WitheredLeaf?

Does the paper raise ethical concerns?
--------------------------------------
1. No

Reviewer expertise in this domain
---------------------------------
3. Knowledgeable (I don't necessarily work in this topic domain, but I work
   on related topics or I am cognizant of the work in this domain in recent
   years)

Reviewer confidence
-------------------
2. Somewhat confident

Overall merit
-------------
3. Neutral

## NDSS Review

Review #1002A
===========================================================================

Writing quality
---------------
2. Needs improvement

Novelty
-------
3. New contribution

Paper summary
-------------
The paper present an LLM-base tool to detect what the authors call entity inconsistency bugs. This class of bug essentially comprises all cases where the developer - by mistake or lack of knowledge - types "something wrong" which doesn't break compilation or doesn't lead to an immediate crash. The program with this bug would be syntactically correct but would have some semantic/logic issue. The authors try to use LLMs to detect such bugs. Their approach uses a cascade of LLMs - from cheapest but least precise to most precise and most expensive - to create a system that insures high precison and recall while minimising costs. In particular the authors use first some simple models that just fill in deliberately-placed gaps in the code: if the model predicts the same word that was removed, the authors deem it a true negative and carry on. Eventually suspicious hits get fed to the most expensive and accurate model with a rich prompt and a specific ask to focus on the lines containing the suspicious token. The authors evaluate their tool on 2 datasets - one of sampled code from github repos and one of synthetic vulnerabilities.

Strengths
---------
 - interesting approach with cascading LLMs

Weaknesses
----------
 - vague and undefined class of bugs
 - the results show that the approach leads to a highly impractical system

Ethical Concerns
----------------
3. I don't see any ethical implications for this paper.

Detailed comments for authors
-----------------------------
Thanks for your submission. First and foremost, I think you should try to be a bit more specific about the class of bugs that you are trying to detect. As it stands, the definition is just too vague. As things stand I think you assume

 - that the intention and approach of the developer is largely correct (it's not a case of the entire set of called functions being wrong)
 - some "entities" (personally I don't find this to be a great choice of word) are incorrect - e.g. the name of a variable or a function

This class is imho at the same time too narrow (i.e. it doesn't include all logical bugs - e.g. an off-by-one in a for loop for instance? Or do you also include arithmetic operations? I don't think so - because if the code says "i < 0" would you challenge whether the "<" or "<=" operator should be used? And in the case where the code goes i < len, would you cover the case of the missing call to the -1 operator if the right code should be i < len - 1?); the class is also too big, since it will bundle together bugs that have different impacts on the system (e.g. memory corruption, failure in access control etc). Too narrow means you'll miss bugs, and too big means you won't be able to define a clear mechanism or set of tools to reason about the class of bugs (e.g. for memory corruption there's a large body of tools to analyse occurrences thereof).

A better-specified class of bugs would benefit from focus and from a richer set of tools to evaluate the bug or the impact of the patches. I did see that in the related work you stress that some other works are too narrow, but I think you can strike the right balance, and imho it's not what you have found.

I like the intuition that you can pre-filter true negatives cheaply. However, I don't think the paper proves this intuition adequately. Afaik the way you prove this intuition is in section II.D using your two datasets (the synthesised and the sampled one). The sampled one afaik contains correct code, and the synthesised one contains deliberately-introduced bugs. The problem with the method in my opinion is that the ability to filter true negatives is only validated on synthetic bugs and is thus unknown on real bugs. (incidentally, speaking of the synthesised dataset, how exactly do you evaluate "semantic discrepancy"?) It would be better to establish this fact on real semantic bugs - but then again a more clear definition of the bug class could help.

The other issue imho is that the resulting tool is too impractical. Tools that produce a high false positive rate are just not used in practice. Iiuc in section IV.B, you have a false positive rate of over 75%, which basically means that for large projects, developers might be swamped with reports. What would be great is to find a way of evaluating the correctness of the report based on anything else than LLMs, because in the end the LLM has no real clue and is just guessing what the next best token is.

Other minor points include:

 - page 4 is very confusing and should be rewritten. Many concepts are just defined in the figure and never in the text - and there are things that are very confusing or improperly defined - e.g. "bad smell".
 - the paper is unintelligible without looking at the appendices for the definition of the templates (e.g. 1FM) - but a reviewer is not supposed to have to look at the appendices. Please make the paper self-contained
 - on page 8 you focus your analysis on low false negative rates, but I think the low false positive is just as important because a tool that will catch all the relevant pattern but hide them in an ocean of irrelevant ones is basically useless.
 - Algorithm 2 is badly defined - for instance what is `validateToken()`?

Concrete steps for improvement
------------------------------
 - define your class of bug more clearly
 - validate your intuition of true positive filtering properly
 - bring down the false positive rate

Overall recommendation
----------------------
1. Reject


* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *


Review #1002B
===========================================================================

Writing quality
---------------
3. Adequate

Novelty
-------
3. New contribution

Paper summary
-------------
This paper proposes an Entity Inconsistency Bug detecton system called WitheredLeaf. Entity Inconsistency Bugs (EIBs) occur when syntactically correct but incorrect program expressions are used, such as improper variable usage and erroneous method calls. Since there is no existing EIB dataset, the paper first curated two datasets. To show the performance of LLMs to detect Entity Inconsistency Bugs this paper chose GPT-4.  WitheredLeaf devised 8 prompt templates based on properties such as if the bug can be fixed by merely changing a variable or function name. WitheredLeaf sampled 66 functions from their dataset to evaluate the performance of GPT-4 and finally chooses the prompt template with highest performance. The paper showed that even with the best performing prompt template, GPT-4 performed poorly on the synthesized dataset. WitheredLeaf addresses the limitations of GPT-4 by reducing the distraction of the model abd focusing its attention on truly suspicious entities.

This paper opts for a cascaded model and filters the probable entities and then runs GPT-4. WitheredLeaf first applies static analyzer where it constructs an abstract syntax tree and from the AST selects entities. Next, for some selected entities, WitheredLeaf masks an entity with a placeholder. CodeBERT and Code Llama have code-infilling capability. So it is possible compare a specific code entity in the original code with a model’s “predicted” entity at the same location (based on the context), if the two align, then likely that code entity is correct, otherwise, an Entity Inconsistency Bug may exist. Thus WitheredLeaf utilizes CodeBERT and Code Llama to find the “probable” Entity Inconsistency Bugs to shorten large number of entities. Finally with the selected prompt WitheredLeaf run GPT-4. They also showed that running GPT-4 in multiple rounds improved performance.

Strengths
---------
- As opposed to previous research focusing on variable misuse bugs, WitheredLeaf targets more intricate semantic bugs at the expression level by analyzing the AST sub-tree, rather than just concentrating on individual nodes.

- WitheredLeaf identified 123 previously unknown EIBs in real-world codebases.

- Prior bug detection using LLM does not consider limitations of LLM at a large scale. This paper addresses the limitations of GPT-4 for Entity-Inconsistency Bug detection.

Weaknesses
----------
- The cascaded pipeline is not generic. The paper never mentions why they have to filter in exactly two steps before giving suspicious entities to GPT-4.

Ethical Concerns
----------------
3. I don't see any ethical implications for this paper.

Detailed comments for authors
-----------------------------
WitheredLeaf utilizes a cascaded pipeline. At the initial stage, to improve the performance of GPT-4 it filters in exactly two steps to find out the probable suspicious entities. This pipeline is not generic. There has to be some threshold or property based on which the number of filters should be applied. Otherwise, we could apply filters with smaller sized LLMs as many times we want before applying GPT-4 prompting.

One of the key intuitions of the WitheredLeaf is to properly filter suspicious entities so that it does not miss any many suspicious entities before GPT-4 analysis.  So, essentially, initial LLMs have to filter out True Negatives (entities that are NOT EIBs). However, the paper claims the initial filtering has 80% True Negative filtering capacity. They determined it by running it on the sampled dataset on real codebases. If the LLMs (CodeBERT, Code Llama, etc.) can replace the correct entity for the infilling task, they are consistent and it indicates it can properly filter out True Negatives. However, they make the assumption that the sampled dataset is “basically” Entity Inconsistency Bug free. In case the sample dataset itself contains EIB, then LLMs evaluation cannot be trusted.

If the initial pre-filter and post-filter step filters out significant Entities that have inconsistencies,  then GPT-4 will miss many suspicious entities and they will never be included in the report.


For initial filtering of probable EIBs, alternative to CodeBERT, StableCode could be utilized.
But it is unclear when this alternative will be applied.


In Section 1, the paper mentions that "We have submitted 69 pull requests to the relevant developers, out of which 27 have already been admitted." On the other hand, in Section 4, the paper mentions "We submitted 69 pull requests to address these bugs, of which 31 have already been confirmed or merged by developers." Is it 27 or 31?

For multiple round prompt in GPT4, it is mentioned to categorize the bug into Security Vulnerability, Logic Bug, Enhancement, Unexpected Behavior, Bad Smell … However, the definitions for each category is not mentioned in the prompt which makes it unclear for GPT-4.

In Section 4, there are typos. “_threadFrameStackSize” → “s_threadFrameStackSize” “_threadExceptionFlowSize” —> “s_threadExceptionFlowSize” (based on Listing 2)

Overall recommendation
----------------------
2. Weak reject