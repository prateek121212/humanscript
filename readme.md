   
 
 
 
 
 
 
 
 ind commands written in natural language using  s then executed on the fly. There is no   execute them, it happens.
 
 ed with cloud hosted LLMs like OpenAI's GPT-3.5  
 
 
 
 ory of screenshots and organises them into 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 line so execution is not blocked waiting for  uted instantly on subsequent runs, bypassing 
 
 
 
 t` into your PATH.
 
 etimes do weird and dangerous things. Speaking  day evening, you should atleast run humanscripts  e before executing.

### Write and execute a humanscript

humanscript is configured out of the box to use OpenAI's GPT-4, you just need to add your API key.

We need to add it to `~/.humanscript/config`

```shell
mkdir -p ~/.humanscript/
echo 'HUMANSCRIPT_API_KEY="<your-openai-api-key>"' >> ~/.humanscript/config
```

Now you can create a humanscript and make it executable.

```shell
echo '#!/usr/bin/env humanscript
print an ascii art human' > asciiman
chmod +x asciiman
```

And then execute it.

```shell
./asciiman
  O
 /|\
 / \
```

## Configuration

All environment variables can be added to `~/.humanscript/config` to be applied globally to all humanscripts:

```shell
$ cat ~/.humanscript/config
HUMANSCRIPT_API_KEY="sk-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
HUMANSCRIPT_MODEL="gpt-4"
```

or on a per script basis:

```shell
$ HUMANSCRIPT_REGENERATE="true" ./asciiman
```

### `HUMANSCRIPT_API`

Default: `https://api.openai.com/v1`

A server following OpenAI's Chat Completion API.

Many local proxies exist that implement this API in front of locally running LLMs like Llama 2. [LM Studio](https://lmstudio.ai/) is a good option.

```shell
HUMANSCRIPT_API="http://localhost:1234/v1"
```

 ### `HUMANSCRIPT_API_KEY`

Default: `unset`

The API key to be sent the LLM backend. Only needed when using OpenAI.
Many locals proxies that implement this API can frequently merged in openAI.  


```shell
HUMANSCRIPT_API_KEY="sk-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
```

### `HUMANSCRIPT_MODEL`

Default: `gpt-4`

The model to use for inference.

```shell
HUMANSCRIPT_MODEL="gpt-3.5"
```

### `HUMANSCRIPT_EXECUTE`

Default: `true`

Whether or not the humanscript inferpreter should automatically execute the generated code on the fly.

If false the generated code will not be executed and instead be streamed to stdout.

```shell
HUMANSCRIPT_EXECUTE="false"
```

### `HUMANSCRIPT_REGENERATE`

Default: `false`

Whether or not the humanscript inferpreter should regenerate a cached humanscript.

If true the humanscript will be reinferpreted and the cache entry will be replaced with the newly generated code. Due to the nondeterministic nature of LLMs each time you reinferpret a humanscript you will get a similar but slightly different output.

```shell
HUMANSCRIPT_REGENERATE="true"
```

## License

MIT © Luke Childs
