# Python Grader

Source: https://platform.openai.com/docs/api-reference/graders/python

A PythonGrader object that runs a python script on the input.

## Properties
- `type` (string, required): The object type, which is always `python`. Enum: 'python'.
- `name` (string, required): The name of the grader.
- `source` (string, required): The source code of the python script.
- `image_tag` (string, optional): The image tag to use for the python script.
