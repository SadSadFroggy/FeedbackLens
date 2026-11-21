<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# FeedbackLens

Final project for the Building AI course

## Summary

FeedbackLens turns messy customer feedback into a short list of themes, with counts and real quotes. A founder uploads survey answers or interview notes and gets back: "12 of 30 people mention price, 8 mention delivery time", plus the exact quotes.


## Background

Which problems does your idea solve?

* Early-stage founders and small businesses collect lots of free-text feedback but rarely have time to read and sort all of it.
* They often rely on the few answers that stood out, or on what they already believed.

How common is this problem? Every product test, club survey, or event feedback round has it. It is especially common in student startups and volunteer organizations.

Personal motivation: I want to start businesses, and testing ideas cheaply before investing is one of the most important skills in entrepreneurship. Many startups fail because nobody needed what they built, so checking customer needs early matters.


## How is it used?

**Who:** A founder, a student team, or a club leader after a feedback round.

**Process:**
1. Upload the responses as a CSV file or paste them as text.
2. The tool removes personal details such as names and emails.
3. It groups similar answers into themes and counts how many answers belong to each theme.
4. It shows each theme with a short summary and real quotes from the input.
5. The user reviews the themes and decides what to change or whether to continue with an idea.

**Affected people:**
* Respondents, whose answers may be personal. They should know how their data is used and be anonymized.
* The founder, who might trust the output too much.
* Team members, whose priorities may change based on the results.

Demo idea: five example answers, tf-idf in a few lines of Python, then grouping them into two themes:
```
# sketch of the planned demo
answers = [
    "too expensive for what it offers",
    "price is higher than competitors",
    "delivery took two weeks",
    "shipping was slow",
    "great design, but pricey",
]

# 1. clean the text (lowercase, remove stop words)
# 2. compute tf-idf for each answer
# 3. group similar answers with k-means (k=2)
# 4. print each theme with its answers
```


## Data sources and AI methods

**Data:** One response per row, in a CSV or pasted text, usually 20-200 answers. Responses may contain names or emails, so personal details are stripped first. For testing I would use 30-50 real or realistic answers, collected with consent.

**Quality issues:** The samples are small, so themes can shift with a few answers. Responses also mix German, Finnish, and English.

| Technique | Purpose |
| --------- | ------- |
| Text cleaning | Lowercase, remove stop words, split into words |
| Bag-of-words and tf-idf | Find the words that best distinguish each response (same idea as the Humpty Dumpty exercise) |
| Distance between responses | Measure how similar two answers are (as in the Manhattan distance exercise) |
| Clustering (e.g. k-means) | Group similar answers into themes |
| Language model (via Langdock) | Name each theme and write a short summary. It may only quote text that appears in the input, so summaries cannot invent evidence |


## Challenges

What the project does not solve, and what to keep in mind:

* **Small samples:** Themes from 15 answers are suggestions, not proof.
* **Context and sarcasm:** Word-based methods miss tone and meaning.
* **Stated vs. real demand:** People say they would pay for something, but that does not mean they will. The tool cannot measure actual purchases.
* **Biased respondents:** Only people who answer the survey are included.
* **Language:** Mixed-language responses are harder to group correctly.
* **Summaries:** A language model can write fluent text that overstates what the data shows.
* **Privacy:** Respondents' data must be handled with consent and anonymized.
