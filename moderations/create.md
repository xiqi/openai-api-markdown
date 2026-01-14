# Create moderation

Source: https://platform.openai.com/docs/api-reference/moderations/create

`POST /v1/moderations`

Classifies if text and/or image inputs are potentially harmful. Learn
more in the [moderation guide](https://platform.openai.com/docs/guides/moderation).

## Request body
### application/json
- `input` (string | array<string> | array<object>, required): Input (or inputs) to classify. Can be a single string, an array of strings, or
  an array of multi-modal input objects similar to other models.
- `model` (string, optional): The content moderation model you would like to use. Learn more in
  [the moderation guide](https://platform.openai.com/docs/guides/moderation), and learn about
  available models [here](https://platform.openai.com/docs/models#moderation). Default: `omni-moderation-latest`.

## Responses
### 200
OK
#### application/json
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

## Returns
A [moderation](object.md) object.

## Examples
### Single string
#### Request (curl)
```bash
curl https://api.openai.com/v1/moderations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "input": "I want to kill them."
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

moderation = client.moderations.create(input="I want to kill them.")
print(moderation)
```
#### Request (csharp)
```csharp
using System;
using System.ClientModel;

using OpenAI.Moderations;

ModerationClient client = new(
    model: "omni-moderation-latest",
    apiKey: Environment.GetEnvironmentVariable("OPENAI_API_KEY")
);

ClientResult<ModerationResult> moderation = client.ClassifyText("I want to kill them.");
```
#### Response
```json
{
  "id": "modr-AB8CjOTu2jiq12hp1AQPfeqFWaORR",
  "model": "text-moderation-007",
  "results": [
    {
      "flagged": true,
      "categories": {
        "sexual": false,
        "hate": false,
        "harassment": true,
        "self-harm": false,
        "sexual/minors": false,
        "hate/threatening": false,
        "violence/graphic": false,
        "self-harm/intent": false,
        "self-harm/instructions": false,
        "harassment/threatening": true,
        "violence": true
      },
      "category_scores": {
        "sexual": 0.000011726012417057063,
        "hate": 0.22706663608551025,
        "harassment": 0.5215635299682617,
        "self-harm": 2.227119921371923e-6,
        "sexual/minors": 7.107352217872176e-8,
        "hate/threatening": 0.023547329008579254,
        "violence/graphic": 0.00003391829886822961,
        "self-harm/intent": 1.646940972932498e-6,
        "self-harm/instructions": 1.1198755256458526e-9,
        "harassment/threatening": 0.5694745779037476,
        "violence": 0.9971134662628174
      }
    }
  ]
}
```
### Image and text
#### Request (curl)
```bash
curl https://api.openai.com/v1/moderations \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "omni-moderation-latest",
    "input": [
      { "type": "text", "text": "...text to classify goes here..." },
      {
        "type": "image_url",
        "image_url": {
          "url": "https://example.com/image.png"
        }
      }
    ]
  }'
```
#### Request (python)
```python
from openai import OpenAI
client = OpenAI()

response = client.moderations.create(
    model="omni-moderation-latest",
    input=[
        {"type": "text", "text": "...text to classify goes here..."},
        {
            "type": "image_url",
            "image_url": {
                "url": "https://example.com/image.png",
                # can also use base64 encoded image URLs
                # "url": "data:image/jpeg;base64,abcdefg..."
            }
        },
    ],
)

print(response)
```
#### Response
```json
{
  "id": "modr-0d9740456c391e43c445bf0f010940c7",
  "model": "omni-moderation-latest",
  "results": [
    {
      "flagged": true,
      "categories": {
        "harassment": true,
        "harassment/threatening": true,
        "sexual": false,
        "hate": false,
        "hate/threatening": false,
        "illicit": false,
        "illicit/violent": false,
        "self-harm/intent": false,
        "self-harm/instructions": false,
        "self-harm": false,
        "sexual/minors": false,
        "violence": true,
        "violence/graphic": true
      },
      "category_scores": {
        "harassment": 0.8189693396524255,
        "harassment/threatening": 0.804985420696006,
        "sexual": 1.573112165348997e-6,
        "hate": 0.007562942636942845,
        "hate/threatening": 0.004208854591835476,
        "illicit": 0.030535955153511665,
        "illicit/violent": 0.008925306722380033,
        "self-harm/intent": 0.00023023930975076432,
        "self-harm/instructions": 0.0002293869201073356,
        "self-harm": 0.012598046106750154,
        "sexual/minors": 2.212566909570261e-8,
        "violence": 0.9999992735124786,
        "violence/graphic": 0.843064871157054
      },
      "category_applied_input_types": {
        "harassment": [
          "text"
        ],
        "harassment/threatening": [
          "text"
        ],
        "sexual": [
          "text",
          "image"
        ],
        "hate": [
          "text"
        ],
        "hate/threatening": [
          "text"
        ],
        "illicit": [
          "text"
        ],
        "illicit/violent": [
          "text"
        ],
        "self-harm/intent": [
          "text",
          "image"
        ],
        "self-harm/instructions": [
          "text",
          "image"
        ],
        "self-harm": [
          "text",
          "image"
        ],
        "sexual/minors": [
          "text"
        ],
        "violence": [
          "text",
          "image"
        ],
        "violence/graphic": [
          "text",
          "image"
        ]
      }
    }
  ]
}
```
