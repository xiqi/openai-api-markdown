# Text Similarity Grader

Source: https://platform.openai.com/docs/api-reference/graders/text-similarity

A TextSimilarityGrader object which grades text based on similarity metrics.

## Properties
- `type` (string, required): The type of grader. Enum: 'text_similarity'. Default: `text_similarity`.
- `name` (string, required): The name of the grader.
- `input` (string, required): The text being graded.
- `reference` (string, required): The text being graded against.
- `evaluation_metric` (string, required): The evaluation metric to use. One of `cosine`, `fuzzy_match`, `bleu`, 
  `gleu`, `meteor`, `rouge_1`, `rouge_2`, `rouge_3`, `rouge_4`, `rouge_5`, 
  or `rouge_l`. Enum: 'cosine', 'fuzzy_match', 'bleu', 'gleu', 'meteor', 'rouge_1', 'rouge_2', 'rouge_3', 'rouge_4', 'rouge_5', 'rouge_l'.
