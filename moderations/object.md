# The moderation object

Source: https://platform.openai.com/docs/api-reference/moderations/object

Represents if a given text input is potentially harmful.

## Properties
- `id` (string, required): The unique identifier for the moderation request.
- `model` (string, required): The model used to generate the moderation results.
- `results` (array<object>, required): A list of moderation objects.
  - Items:
    - `flagged` (boolean, required): Whether any of the below categories are flagged.
    - `categories` (object, required): A list of the categories, and whether they are flagged or not.
      - `hate` (boolean, required): Content that expresses, incites, or promotes hate based on race, gender, ethnicity, religion, nationality, sexual orientation, disability status, or caste. Hateful content aimed at non-protected groups (e.g., chess players) is harassment.
      - `hate/threatening` (boolean, required): Hateful content that also includes violence or serious harm towards the targeted group based on race, gender, ethnicity, religion, nationality, sexual orientation, disability status, or caste.
      - `harassment` (boolean, required): Content that expresses, incites, or promotes harassing language towards any target.
      - `harassment/threatening` (boolean, required): Harassment content that also includes violence or serious harm towards any target.
      - `illicit` (boolean | null, required)
      - `illicit/violent` (boolean | null, required)
      - `self-harm` (boolean, required): Content that promotes, encourages, or depicts acts of self-harm, such as suicide, cutting, and eating disorders.
      - `self-harm/intent` (boolean, required): Content where the speaker expresses that they are engaging or intend to engage in acts of self-harm, such as suicide, cutting, and eating disorders.
      - `self-harm/instructions` (boolean, required): Content that encourages performing acts of self-harm, such as suicide, cutting, and eating disorders, or that gives instructions or advice on how to commit such acts.
      - `sexual` (boolean, required): Content meant to arouse sexual excitement, such as the description of sexual activity, or that promotes sexual services (excluding sex education and wellness).
      - `sexual/minors` (boolean, required): Sexual content that includes an individual who is under 18 years old.
      - `violence` (boolean, required): Content that depicts death, violence, or physical injury.
      - `violence/graphic` (boolean, required): Content that depicts death, violence, or physical injury in graphic detail.
    - `category_scores` (object, required): A list of the categories along with their scores as predicted by model.
      - `hate` (number, required): The score for the category 'hate'.
      - `hate/threatening` (number, required): The score for the category 'hate/threatening'.
      - `harassment` (number, required): The score for the category 'harassment'.
      - `harassment/threatening` (number, required): The score for the category 'harassment/threatening'.
      - `illicit` (number, required): The score for the category 'illicit'.
      - `illicit/violent` (number, required): The score for the category 'illicit/violent'.
      - `self-harm` (number, required): The score for the category 'self-harm'.
      - `self-harm/intent` (number, required): The score for the category 'self-harm/intent'.
      - `self-harm/instructions` (number, required): The score for the category 'self-harm/instructions'.
      - `sexual` (number, required): The score for the category 'sexual'.
      - `sexual/minors` (number, required): The score for the category 'sexual/minors'.
      - `violence` (number, required): The score for the category 'violence'.
      - `violence/graphic` (number, required): The score for the category 'violence/graphic'.
    - `category_applied_input_types` (object, required): A list of the categories along with the input type(s) that the score applies to.
      - `hate` (array<string>, required): The applied input type(s) for the category 'hate'.
      - `hate/threatening` (array<string>, required): The applied input type(s) for the category 'hate/threatening'.
      - `harassment` (array<string>, required): The applied input type(s) for the category 'harassment'.
      - `harassment/threatening` (array<string>, required): The applied input type(s) for the category 'harassment/threatening'.
      - `illicit` (array<string>, required): The applied input type(s) for the category 'illicit'.
      - `illicit/violent` (array<string>, required): The applied input type(s) for the category 'illicit/violent'.
      - `self-harm` (array<string>, required): The applied input type(s) for the category 'self-harm'.
      - `self-harm/intent` (array<string>, required): The applied input type(s) for the category 'self-harm/intent'.
      - `self-harm/instructions` (array<string>, required): The applied input type(s) for the category 'self-harm/instructions'.
      - `sexual` (array<string>, required): The applied input type(s) for the category 'sexual'.
      - `sexual/minors` (array<string>, required): The applied input type(s) for the category 'sexual/minors'.
      - `violence` (array<string>, required): The applied input type(s) for the category 'violence'.
      - `violence/graphic` (array<string>, required): The applied input type(s) for the category 'violence/graphic'.
