## Usage

Build image.

```
docker build -t my-fastchat-image -f docker/fastchat .
```

Run container.

```
docker run -it --mount type=bind,source=/home/david/projects/filebot/model,target=/app/model,readonly my-fastchat-image bash
```

Launch controller.

```
python3 -m fastchat.serve.controller --host 0.0.0.0
```

Launch worker(s). Defaults to `gpu` without `cpu` flag.

```
python3 -m fastchat.serve.model_worker --model-name 'vicuna-13b-v1.1' --model-path model/ --host 0.0.0.0 --device cpu
```

## Other

You can use openai python library. Appears all you need is to change the endpoint, essentially, to the fastchat server.

`https://github.com/lm-sys/FastChat#api`
`https://github.com/lm-sys/FastChat/blob/main/docs/openai_api.md`

## API

`https://github.com/lm-sys/FastChat/blob/main/docs/openai_api.md`

## Fastchat server

Essentially, I believe you just launch a web server

`https://github.com/lm-sys/FastChat#serving-with-web-gui`

From there you can use the local endpoint for open ai.

## Example

`https://github.com/lm-sys/FastChat/blob/main/docs/openai_api.md#openai-official-sdk`
```
import openai
openai.api_key = "EMPTY" # Not support yet
openai.api_base = "http://localhost:8000/v1"

model = "vicuna-7b-v1.1"
prompt = "Once upon a time"

# create a completion
completion = openai.Completion.create(model=model, prompt=prompt, max_tokens=64)
# print the completion
print(prompt + completion.choices[0].text)

# create a chat completion
completion = openai.ChatCompletion.create(
  model=model,
  messages=[{"role": "user", "content": "Hello! What is your name?"}]
)
# print the completion
print(completion.choices[0].message.content)
```