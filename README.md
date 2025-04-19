# hf_pipeline_webserver
Code for the huggingface pipeline webserver

## A Demo
This repo is a demo from the Hugging Face Transformers tutorial ([Using pipelines for a webserver](https://huggingface.co/docs/transformers/pipeline_webserver)).

## Setting up the Environment

The following commands in a terminal are used to install the necessary dependencies for this project. These steps only need to be performed once to set up the environment:

```bash
sudo apt install python3.10-venv
python3 -m venv .venv
source .venv/bin/activate
pip install starlette uvicorn
pip install transformers
pip install tensorflow
pip install tf-keras
```

Once the dependencies are installed, one can start the server in a terminal using the following command:

```bash
python3 -m venv .venv
source .venv/bin/activate
uvicorn server:app
```

## Example Request and Response

Below is an example of how to send a request to the server and the corresponding response. This can be done in another terminal window. The request uses the `curl` command to send a POST request with the input text `"test [MASK]"`. The server responds with predictions for the masked token:

### Request:
```bash
curl -X POST -d "test [MASK]" http://localhost:8000/
```

### Response:
```json
[
  {"score":0.7742829918861389,"token":1012,"token_str":".","sequence":"test."},
  {"score":0.14909622073173523,"token":1025,"token_str":";","sequence":"test ;"},
  {"score":0.04598265141248703,"token":999,"token_str":"!","sequence":"test!"},
  {"score":0.016506241634488106,"token":1064,"token_str":"|","sequence":"test |"},
  {"score":0.013514903374016285,"token":1029,"token_str":"?","sequence":"test?"}
]
```
This demonstrates how the server predicts possible replacements for the `[MASK]` token in the input text.