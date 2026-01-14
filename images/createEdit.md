# Create image edit

Source: https://platform.openai.com/docs/api-reference/images/createEdit

`POST /v1/images/edits`

Creates an edited or extended image given one or more source images and a prompt. This endpoint supports GPT Image models (`gpt-image-1.5`, `gpt-image-1`, and `gpt-image-1-mini`) and `dall-e-2`.

## Request body
### multipart/form-data
- `image` (string | array<string>, required): The image(s) to edit. Must be a supported image file or an array of images.
  
  For the GPT image models (`gpt-image-1`, `gpt-image-1-mini`, and `gpt-image-1.5`), each image should be a `png`, `webp`, or `jpg`
  file less than 50MB. You can provide up to 16 images.
  
  For `dall-e-2`, you can only provide one image, and it should be a square
  `png` file less than 4MB.
- `prompt` (string, required): A text description of the desired image(s). The maximum length is 1000 characters for `dall-e-2`, and 32000 characters for the GPT image models.
- `mask` (string, optional): An additional image whose fully transparent areas (e.g. where alpha is zero) indicate where `image` should be edited. If there are multiple images provided, the mask will be applied on the first image. Must be a valid PNG file, less than 4MB, and have the same dimensions as `image`.
- `background` (string, optional): Allows to set transparency for the background of the generated image(s).
  This parameter is only supported for the GPT image models. Must be one of
  `transparent`, `opaque` or `auto` (default value). When `auto` is used, the
  model will automatically determine the best background for the image.
  
  If `transparent`, the output format needs to support transparency, so it
  should be set to either `png` (default value) or `webp`. Enum: 'transparent', 'opaque', 'auto'. Default: `auto`.
- `model` (string, optional): The model to use for image generation. Only `dall-e-2` and the GPT image models are supported. Defaults to `dall-e-2` unless a parameter specific to the GPT image models is used. Default: `dall-e-2`.
- `n` (integer, optional): The number of images to generate. Must be between 1 and 10. Default: `1`.
- `size` (string, optional): The size of the generated images. Must be one of `1024x1024`, `1536x1024` (landscape), `1024x1536` (portrait), or `auto` (default value) for the GPT image models, and one of `256x256`, `512x512`, or `1024x1024` for `dall-e-2`. Enum: '256x256', '512x512', '1024x1024', '1536x1024', '1024x1536', 'auto'. Default: `1024x1024`.
- `response_format` (string, optional): The format in which the generated images are returned. Must be one of `url` or `b64_json`. URLs are only valid for 60 minutes after the image has been generated. This parameter is only supported for `dall-e-2`, as the GPT image models always return base64-encoded images. Enum: 'url', 'b64_json'. Default: `url`.
- `output_format` (string, optional): The format in which the generated images are returned. This parameter is
  only supported for the GPT image models. Must be one of `png`, `jpeg`, or `webp`.
  The default value is `png`. Enum: 'png', 'jpeg', 'webp'. Default: `png`.
- `output_compression` (integer, optional): The compression level (0-100%) for the generated images. This parameter
  is only supported for the GPT image models with the `webp` or `jpeg` output
  formats, and defaults to 100. Default: `100`.
- `user` (string, optional): A unique identifier representing your end-user, which can help OpenAI to monitor and detect abuse. [Learn more](https://platform.openai.com/docs/guides/safety-best-practices#end-user-ids).
- `input_fidelity` (string | null, optional)
- `stream` (boolean, optional): Edit the image in streaming mode. Defaults to `false`. See the
  [Image generation guide](https://platform.openai.com/docs/guides/image-generation) for more information. Default: `False`.
- `partial_images` (integer | null, optional)
- `quality` (string, optional): The quality of the image that will be generated. `high`, `medium` and `low` are only supported for the GPT image models. `dall-e-2` only supports `standard` quality. Defaults to `auto`. Enum: 'standard', 'low', 'medium', 'high', 'auto'. Default: `auto`.

## Responses
### 200
OK
#### application/json
- `created` (integer, required): The Unix timestamp (in seconds) of when the image was created.
- `data` (array<object>, optional): The list of generated images.
  - Items:
    - `b64_json` (string, optional): The base64-encoded JSON of the generated image. Returned by default for the GPT image models, and only present if `response_format` is set to `b64_json` for `dall-e-2` and `dall-e-3`.
    - `url` (string, optional): When using `dall-e-2` or `dall-e-3`, the URL of the generated image if `response_format` is set to `url` (default value). Unsupported for the GPT image models.
    - `revised_prompt` (string, optional): For `dall-e-3` only, the revised prompt that was used to generate the image.
- `background` (string, optional): The background parameter used for the image generation. Either `transparent` or `opaque`. Enum: 'transparent', 'opaque'.
- `output_format` (string, optional): The output format of the image generation. Either `png`, `webp`, or `jpeg`. Enum: 'png', 'webp', 'jpeg'.
- `size` (string, optional): The size of the image generated. Either `1024x1024`, `1024x1536`, or `1536x1024`. Enum: '1024x1024', '1024x1536', '1536x1024'.
- `quality` (string, optional): The quality of the image generated. Either `low`, `medium`, or `high`. Enum: 'low', 'medium', 'high'.
- `usage` (object, optional): For `gpt-image-1` only, the token usage information for the image generation.
  - `input_tokens` (integer, required): The number of tokens (images and text) in the input prompt.
  - `total_tokens` (integer, required): The total number of tokens (images and text) used for the image generation.
  - `output_tokens` (integer, required): The number of output tokens generated by the model.
  - `output_tokens_details` (object, optional): The output token details for the image generation.
    - `image_tokens` (integer, required): The number of image output tokens generated by the model.
    - `text_tokens` (integer, required): The number of text output tokens generated by the model.
  - `input_tokens_details` (object, required): The input tokens detailed information for the image generation.
    - `text_tokens` (integer, required): The number of text tokens in the input prompt.
    - `image_tokens` (integer, required): The number of image tokens in the input prompt.
#### text/event-stream
- Schema type: `object`

## Returns
Returns an [image](object.md) object.

## Examples
### Edit image
#### Request (curl)
```bash
curl -s -D >(grep -i x-request-id >&2) \
  -o >(jq -r '.data[0].b64_json' | base64 --decode > gift-basket.png) \
  -X POST "https://api.openai.com/v1/images/edits" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "model=gpt-image-1.5" \
  -F "image[]=@body-lotion.png" \
  -F "image[]=@bath-bomb.png" \
  -F "image[]=@incense-kit.png" \
  -F "image[]=@soap.png" \
  -F 'prompt=Create a lovely gift basket with these four items in it'
```
#### Request (python)
```python
import base64
from openai import OpenAI
client = OpenAI()

prompt = """
Generate a photorealistic image of a gift basket on a white background
labeled 'Relax & Unwind' with a ribbon and handwriting-like font,
containing all the items in the reference pictures.
"""

result = client.images.edit(
    model="gpt-image-1.5",
    image=[
        open("body-lotion.png", "rb"),
        open("bath-bomb.png", "rb"),
        open("incense-kit.png", "rb"),
        open("soap.png", "rb"),
    ],
    prompt=prompt
)

image_base64 = result.data[0].b64_json
image_bytes = base64.b64decode(image_base64)

# Save the image to a file
with open("gift-basket.png", "wb") as f:
    f.write(image_bytes)
```
### Streaming
#### Request (curl)
```bash
curl -s -N -X POST "https://api.openai.com/v1/images/edits" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -F "model=gpt-image-1.5" \
  -F "image[]=@body-lotion.png" \
  -F "image[]=@bath-bomb.png" \
  -F "image[]=@incense-kit.png" \
  -F "image[]=@soap.png" \
  -F 'prompt=Create a lovely gift basket with these four items in it' \
  -F "stream=true"
```
#### Request (python)
```python
from openai import OpenAI

client = OpenAI()

prompt = """
Generate a photorealistic image of a gift basket on a white background
labeled 'Relax & Unwind' with a ribbon and handwriting-like font,
containing all the items in the reference pictures.
"""

stream = client.images.edit(
    model="gpt-image-1.5",
    image=[
        open("body-lotion.png", "rb"),
        open("bath-bomb.png", "rb"),
        open("incense-kit.png", "rb"),
        open("soap.png", "rb"),
    ],
    prompt=prompt,
    stream=True
)

for event in stream:
    print(event)
```
#### Response
```json
event: image_edit.partial_image
data: {"type":"image_edit.partial_image","b64_json":"...","partial_image_index":0}

event: image_edit.completed
data: {"type":"image_edit.completed","b64_json":"...","usage":{"total_tokens":100,"input_tokens":50,"output_tokens":50,"input_tokens_details":{"text_tokens":10,"image_tokens":40}}}
```
