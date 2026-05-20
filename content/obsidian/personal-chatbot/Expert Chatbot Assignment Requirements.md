---
title: Expert Chatbot Assignment Requirements
type: assignment-requirements
status: active
project: personal-portfolio-chatbot
domain: personal portfolio website assistant
tags:
  - expert-chatbot
  - assignment
  - personal-chatbot
  - rag
---

# Expert Chatbot Assignment Requirements

## Navigation

- Project index: [[personal-chatbot-index]]
- Project brief: [[personal-portfolio-chatbot-brief]]
- Build plan: [[personal-chatbot-build-plan]]

## Relationship to Project

This note defines the assignment requirements for the expert chatbot task. It connects directly to [[personal-portfolio-chatbot-brief]], which adapts these requirements to the personal portfolio website assistant domain, and [[personal-chatbot-build-plan]], which turns the requirements into implementation steps.

## Assignment Overview

This assignment requires the implementation of an expert chatbot that can answer questions in a specific domain. An expert chatbot is an advanced conversational agent designed to provide specialised and in-depth knowledge on selected topics or domains.

The chatbot should use artificial intelligence, machine learning, and natural language processing to simulate human-like conversations. It should support expert-level information retrieval, advice, and problem-solving.

The chatbot should be able to:

- Understand domain-specific questions.
- Provide accurate and relevant answers.
- Handle simple human conversation.
- Demonstrate expert knowledge in the selected domain.
- Show clear testing and evaluation results.

## Selected Domain

For this project, the selected domain is:

> Personal portfolio website assistant

This domain is explained in detail in [[personal-portfolio-chatbot-brief]].

- [x] Decide the chatbot domain.
- [x] Explain why this domain is useful or important.
- [x] Define the target users.
- [x] Define the main problems the chatbot will help solve.
- [ ] Confirm whether the chatbot will connect to the ABSA project/report or use another dataset/source.

Possible domains:

- Health
- Employment
- Tourism
- Education
- Customer reviews
- Restaurant review analysis
- CDU student support
- Civic education
- Personal portfolio website assistant

## Core Chatbot Requirements

These requirements are applied to the project brief in [[personal-portfolio-chatbot-brief]] and implemented through [[personal-chatbot-build-plan]].

- [ ] The chatbot answers questions related to the selected domain.
- [ ] The chatbot outputs clear sentence-level answers.
- [ ] The chatbot can handle simple greetings and casual conversation.
- [ ] The chatbot can recognise when a question is outside its domain.
- [ ] The chatbot can provide a fallback response when it does not know the answer.
- [ ] The chatbot avoids hallucinating unsupported answers.
- [ ] The chatbot provides useful and user-friendly responses.

## Technical Requirements

- [ ] Choose the chatbot development approach.
- [ ] Decide whether to train a model from scratch or fine-tune a pre-trained model.
- [ ] Decide whether to use an API-based model.
- [ ] Decide whether the chatbot connects to an ABSA tool or report output.
- [ ] Prepare the training or knowledge data.
- [ ] Clean and structure the data.
- [ ] Build the chatbot interface or demo environment.
- [ ] Implement conversation handling.
- [ ] Implement domain question answering.
- [ ] Implement fallback handling.
- [ ] Test the chatbot with real questions.

Possible approaches:

- Rule-based chatbot
- Retrieval-based chatbot
- Fine-tuned transformer model
- LLM API chatbot
- RAG chatbot using documents or reports
- API tool connected to ABSA output

## Data and Knowledge Source Checklist

For this project, the primary knowledge source is the Markdown/Obsidian content used by `maxhoang.com.au`.

- [ ] Identify the knowledge source.
- [ ] Explain where the data comes from.
- [ ] Explain how the data was cleaned or prepared.
- [ ] Explain whether the data is complete or limited.
- [ ] Explain any bias or quality issues in the data.
- [ ] Explain how the chatbot uses the data to answer questions.

Possible sources:

- Written ABSA report
- Restaurant review dataset
- Public QA dataset
- Domain-specific documents
- Website content
- FAQ pages
- Manually prepared question-answer pairs
- Obsidian notes

## Model and Approach Checklist

The planned model and RAG approach are developed in [[personal-chatbot-build-plan]].

- [ ] Name the model or method used.
- [ ] Explain why this approach was selected.
- [ ] Explain how the chatbot processes a user question.
- [ ] Explain how the chatbot generates or retrieves an answer.
- [ ] Explain the limitations of the model.
- [ ] Explain the limitations of the dataset.
- [ ] Explain the limitations of the chatbot content.
- [ ] Explain any ethical or safety considerations.

## Testing and Evaluation Checklist

- [ ] Prepare test questions.
- [ ] Include simple conversation tests.
- [ ] Include domain-specific question tests.
- [ ] Include difficult or complex question tests.
- [ ] Include out-of-scope question tests.
- [ ] Record chatbot responses.
- [ ] Evaluate whether the answers are correct and useful.
- [ ] Identify common chatbot mistakes.
- [ ] Explain how the chatbot could be improved.

Evaluation options:

- Real-time live conversation test
- Public QA dataset evaluation
- Human testing
- Accuracy of responses
- Relevance of responses
- User satisfaction
- Error analysis

## Live Demonstration Checklist

- [ ] Prepare a working chatbot demo.
- [ ] Prepare 3 to 5 test questions for the presentation.
- [ ] Include at least one simple greeting.
- [ ] Include at least one domain-specific question.
- [ ] Include at least one challenging question.
- [ ] Include at least one out-of-scope question.
- [ ] Show how the chatbot responds in real time.
- [ ] Explain what the chatbot did well.
- [ ] Explain any weaknesses shown during testing.

## Presentation Outline

The presentation can be divided into four parts for four members or adapted for a smaller group.

### Part 1: Introduction

- [ ] Introduce the expert chatbot concept.
- [ ] Introduce the selected domain.
- [ ] Explain the domain challenge.
- [ ] Explain why a chatbot is useful for this domain.
- [ ] Mention whether this is connected to the ABSA project or uses a different approach.

### Part 2: Approach and Scope

- [ ] Explain the model or approach used.
- [ ] Explain the data or knowledge source.
- [ ] Explain how the chatbot was developed.
- [ ] Explain what the chatbot can do.
- [ ] Explain what the chatbot cannot do.
- [ ] Explain limitations in the data, model, or content.

### Part 3: Testing

- [ ] Show live chatbot testing.
- [ ] Ask prepared test questions.
- [ ] Show chatbot responses.
- [ ] Explain whether the responses are accurate and relevant.
- [ ] Discuss any errors or unexpected behaviour.

### Part 4: Conclusion

- [ ] Summarise the chatbot outcome.
- [ ] Explain what worked well.
- [ ] Explain the main limitations.
- [ ] Suggest future improvements.
- [ ] Link future work to the evaluation results.

## Future Work Ideas

These ideas are also connected to the upgrade path in [[personal-chatbot-build-plan]].

- [ ] Improve the training data.
- [ ] Add more domain knowledge.
- [ ] Improve response accuracy.
- [ ] Add retrieval-augmented generation.
- [ ] Add source citations.
- [ ] Improve the user interface.
- [ ] Add memory for conversation context.
- [ ] Add multilingual support.
- [ ] Connect the chatbot to a live API.
- [ ] Improve safety and out-of-scope detection.

## Final Submission Checklist

- [ ] Working chatbot prototype completed.
- [ ] Domain clearly explained.
- [ ] Model and approach clearly explained.
- [ ] Data source clearly explained.
- [ ] Limitations clearly explained.
- [ ] Testing evidence included.
- [ ] Live demo prepared.
- [ ] Presentation slides completed.
- [ ] Conclusion and future work completed.
- [ ] Team member roles divided clearly.

## Related Notes

- [[personal-chatbot-index]]
- [[personal-portfolio-chatbot-brief]]
- [[personal-chatbot-build-plan]]
