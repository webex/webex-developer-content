---
type: Article
title: The Evaluation of Generative AI Performance in WebEx Contact Center
canonical_url: https://developer.webex.com/blog/the-evaluation-of-generative-ai-performance-in-webex-contact-center
content_type: blog
date: '2025-03-24'
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/blog/the-evaluation-of-generative-ai-performance-in-webex-contact-center)

> **Info**
>
> **Prasad N Kamath, Director of Software Engineering also contributed to this blog post.**



This blog discusses the development of a Gen-AI scoring system in Webex Contact Center (WxCC), designed to evaluate the quality, consistency, and reliability of AI-generated outputs across various applications like conversational and non-conversational AI, including Voice over AI Agents, Chat-based AI Agents, QA systems, and summarization kind of generative tasks. The system employs innovative aggregation algorithms, contextual assessments, and Responsible AI ( https://www.cisco.com/site/us/en/solutions/artificial-intelligence/responsible-ai/index.html  ) checks, including BERTScore ( [https://huggingface.co/spaces/evaluate-metric/bertscore](https://huggingface.co/spaces/evaluate-metric/bertscore) ) for non-conversational tasks and a "Pass@K" paradigm ( https://medium.com/@yananchen1116/a-dive-into-how-pass-k-is-calculated-for-evaluation-of-llms-coding-e52b8528235b  ) for conversational consistency.

To support deeper analysis and optimization, the final aggregated score is further backed by itemized entry-wise scores, providing a detailed breakdown for granular tuning. This comprehensive scoring framework ensures that the AI outputs are not only functional but also adhere to high standards of quality, consistency, and reliability, enabling more precise and meaningful AI-generated content in diverse applications.

### The Importance of Quantifying AI Performance

Generative AI has revolutionized various industries, from content creation to personalized marketing, by enabling machines to produce text, images, music, and more that mimic human creativity. As these systems become increasingly sophisticated, it’s crucial to have robust evaluation mechanisms to ensure their outputs are effective, reliable, and aligned with desired outcomes. One of the most prominent methods for evaluating generative AI is scoring-based evaluation. This method quantifies the performance of AI models, offering clear, objective metrics that can guide development, optimization, and deployment.

### Generative AI Tasks in a Nutshell

Generative AI covers a diverse array of tasks, each with distinct challenges and applications. Key areas include text generation, where models like GPT, Gemini are used for writing and coding; image generation, with tools like DALL-E creating visuals from text descriptions; and music and audio generation, where AI composes music and speech. Additionally, data synthesis allows for the creation of synthetic datasets for training other models, and design and style transfer enable AI to generate new product designs and transform art styles. Each of these tasks necessitates a specific evaluation approach, highlighting the importance of scoring schemes.

#### Different Traditional Scoring Schemes and Their Usefulness

Evaluating generative AI requires tailored approaches depending on the specific task and desired outcome, as no single method fits all scenarios. Various scoring schemes are employed, including perplexity, which gauges the accuracy of text predictions; BLEU, which assesses text translation quality by comparing outputs to references; and ROUGE, which is used for summarization tasks, focusing on n-gram overlap. Additionally, human evaluation plays a critical role in assessing creative aspects, offering qualitative insights that complement these quantitative measures.

### Evaluating Generative AI with Scoring Methods in Webex Contact Center

In WxCC, we have developed a Gen-AI scoring system that evaluates the quality, consistency, and reliability of generated data, aggregating these metrics into an overall score using innovative, proprietary algorithms. This scoring framework is versatile, supporting both conversational and non-conversational AI applications, such as Voice over AI Agent, Chat-based AI Agent, QA systems, summarization, and various other generative AI scenarios. To qualify for evaluation, generated data must be accompanied by the relevant context and/or ground truth. For conversational use cases, the framework accepts chat and transcript data in a specified format, resolving coreferences and optimizing context for optimal results. In QA evaluations, it expects a query with context and optionally, ground truth. For non-conversational scenarios like summarization, it requires the generated summary and its reference counterpart.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltc0baa5eaad231ab1/generative-ai-scoring-webex-developer-blog-2.png)

To initiate an evaluation, the system requires the configuration of the evaluation agent with various options as a prerequisite. Depending on the chosen agent and mode (conversational or non-conversational), the evaluation process begins. The framework then assesses both qualitative and quantitative aspects of each entity in the input data, mirroring the standards of manual evaluation. For quality assessment, it evaluates factors like accuracy, conciseness, coherence, fluency, and depth of thought, along with Responsible AI considerations such as harmfulness, maliciousness, controversy, gender bias, and insensitivity to name a few. The grading process follows a teacher-student pattern. In conversational mode, the framework implements a “Pass@K” paradigm to assess consistency, while reliability checks involve verifying the relevance and factuality of the generated data, including detecting hallucinations and jailbreak scenarios. Quality and relevance scores are aggregated at the entity level to compute an overall score using customized logic.

In non-conversational mode, the framework also calculates BERTScore for the AI outputs, leveraging its ability to capture contextual and semantic similarities. BERTScore serves as a scaling factor in the overall score computation. In conversational mode, a percentile-based aggregation algorithm computes the overall quality and reliability of the entire conversation, with a logarithmic algorithm using the consistency score as a gentle scaling factor for the final overall score. The final score is supported by detailed itemized scores for each entry, allowing for more granular analysis and fine-tuning. This mode also features a cumulative mechanism to accurately calculate scores across multiple runs.

![Image described in surrounding text.](https://images.contentstack.io/v3/assets/bltd74e2c7e18c68b20/bltff64a84bae387f4c/generative-ai-scoring-webex-developer-blog-3.png)

Here are few salient points summarizing the discussion:

- The Gen-AI scoring system is designed to evaluate AI-generated outputs for quality, consistency, and reliability across both conversational and non-conversational applications.
- The system incorporates key metrics such as "Quality Scoring", "Reliability Validation", "Consistency Check", and "Responsible AI" to ensure a thorough and responsible assessment of AI outputs.
- Innovative aggregation algorithms are used to compute overall scores, taking into account both qualitative and quantitative aspects of the AI-generated data.
- The system provides itemized scores alongside the final score, allowing for detailed analysis and fine-tuning of AI models to improve their performance.

<br/>

#### Example Usage

Our Gen-AI scoring system is a versatile Python package that can seamlessly integrate with any Python-based application, such as the following example:



> **Info**
>
> The `agentprofile` library shown here isn't currently accessible for developers to try.



**Installation:**

```bash
!pip install OpenAI
!pip install langchain langchain-openai --upgrade
!pip install langchain-community langchain-core
!pip install transformers bert-score logstash_formatter jproperties
```

**Import:**

```python
import uuid
from agentprofile.PerfComputer import PerformanceTracker

##############################################################################
```

**Sample Evaluation of Non-Conversational AI Output:**

```python
api_key = "LLM PROXY CI TOKEN"

gen_agent_prompt_tup = ('gen_agent_id', '')
gen_performance_tracker_instance = PerformanceTracker()

gen_performance_tracker_instance.add_updt_agent_config(gen_agent_prompt_tup, is_ref_available=True)

gen_qa_container = [
    {
    "id": "id-1",
    "text": "GEN AI OUTPUT",
    "groundtruth": "REFERENCE CONTENT AS GROUNDTRUTH",
    }
]

gen_overall_result_dict = gen_performance_tracker_instance.compute_performance('gen_agent_id', gen_qa_container, api_key, mode=2)
```

**Evaluation Result Schema:**

```python
{ "overall_rating_computed": float, "overall_quality": float, "overall_reliability": float, "componentized_rating": { "accuracy_score": {"reasoning": str, "score": float}, "coherence_score": {"reasoning": str, "score": float}, "factuality_score": {"reasoning": str, "score": float}, "fluency_score": {"reasoning": str, "score": float}, "bertscore": [{"Precision": float, "Recall": float, "F1": float}] } }

##############################################################################
```

**Sample Evaluation of Conversational AI Output:**

```python
api_key = "LLM PROXY CI TOKEN"

#Sample usage
agent_prompt_json_str_id = 'agent_prompt_json_str_id'
agent_prompt_json_str = 'SERIALIZED PROMPT OBJECT INSTANTIATED using promptstore package' #Refer to “<em>Note”</em> section for instantiation of the prompt object
agent_prompt_tup = (agent_prompt_json_str_id, agent_prompt_json_str)

performance_tracker_instance = PerformanceTracker()
performance_tracker_instance.add_updt_agent_config(agent_prompt_tup, sample_frac=0.7, k=2)
qa_container = [
    {
     "id": "UNIQUE ID",
     "query": "QUERY",
     “answer”: “AI OUTPUT”,
     "groundtruth": "REFERENCE ANSWER AS GROUNDTRUTH",
    }
]
overall_result_dict = performance_tracker_instance.compute_performance(agent_prompt_json_str_id, qa_container, api_key, batch_size=4, consistency_threshold=90)
```

**Evaluation Result Schema:**

```python
{ "overall_rating_computed": float, "overall_rating_perceived": float, "overall_quality": float, "overall_reliability": float, "overall_consistency": float, "consistency_k": int, "componentized_rating": [ { "id": str, "query": str, "groundtruth": str, "answer": str, "answers": [str], "evaluation_result_details": { "overall_rating": int, "overall_quality": int, "overall_reliability": int, "classification": str, "componentized_rating": { "REFERENCE_ACCURACY_SCORER_Score": {"score": float}, "CONTEXT_ACCURACY_SCORER_Score": {"score": float}, "QUERY_CONTEXT_REL_SCORER_Score": {"score": float}, "RESPONSE_CONTEXT_REL_SCORER_Score": {"reasoning": str, "score": float}, "IDK_JB_SCORER_Score": {"score": float, "reasoning": str}, "COMPREHENSIVE_SCORER_Score_WO_Groundtruth": {"reasoning": str, "score": float}, "COMPREHENSIVE_SCORER_Score_W_Groundtruth": {"reasoning": str, "score": float}, "ANSWER_IDK_JB_SCORER_Score": {"score": float, "reasoning": str} } } } ] }

##############################################################################

<strong>Cumulative score (over multiple runs):</strong>

result_dict_cum = PerformanceTracker.aggregate_overall_final(history_result_dict)

<strong>Cumulative score Schema (over multiple runs):</strong>

{ "overall_rating_computed": float, "overall_quality": float, "overall_reliability": float, "overall_consistency": float }
```

### Final Thoughts

The Gen-AI Evaluation system provides a structured yet adaptable approach to assessing AI-generated outputs. By incorporating quality scoring, reliability validation, consistency checks, and Responsible AI, it ensures models meet both technical and ethical benchmarks. Moreover, integrating this framework with a Gen-AI auto-tuning infrastructure can enable an unattended, intelligent tuning system — continuously refining models based on real-time evaluations. This synergy makes it a powerful tool for developers and stakeholders aiming to build reliable, self-improving AI solutions. The library is planned for GA in the 1st half of 2025. You may try out the SDK (subject to approval from AI Agent DLT team) once available. For any further information please contact the blog author.
