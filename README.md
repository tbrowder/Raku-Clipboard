# Clipboard

Raku package for using clipboards of different operating systems. (I.e., copy and paste with any OS.)


------

## Installation

Zef ecosystem:

```
zef install Clipboard
```

GitHub:

```
zef install https://github.com/antononcube/Raku-Clipboard.git
```

------

## Usage examples

Here Raku packages for clipboard- and Large Language Models (LLMs) utilization are loaded:

```perl6
use Clipboard;
use LLM::Functions;
```
```
# (Any)
```

Here is an LLM prompt for code writing assistance:

```perl6
my $promptCodeWriter = q:to/END/;
You are Code Writer and as the coder that you are, you provide clear and concise code only, without explanation nor conversation. 
Your job is to output code with no accompanying text.
Do not explain any code unless asked. Do not provide summaries unless asked.
You are the best Raku programmer in the world but do not converse.
You know the Raku documentation better than anyone but do not converse.
You can provide clear examples and offer distinctive and unique instructions to the solutions you provide only if specifically requested.
Only code in Raku unless told otherwise.
Unless they ask, you will only give code.
END

$promptCodeWriter.chars
```
```
# 622
```

Here we make a chat object with the code writing prompt:

```perl6
my $chat = llm-chat($promptCodeWriter);
```
```
# LLM::Functions::Chat(chat-id = , llm-evaluator.conf.name = chatgpt, messages.elems = 0)
```

Here we generate code through the chat object and get the result copied in the clipboard:

```perl6
$chat.eval('Give code for making a dictionary the keys of which have two elements.') ==> copy-to-clipboard
```
```
# my %dictionary;
# %dictionary<key1, value1> = 42;
# %dictionary<key2, value2> = "hello";
# %dictionary<key3, value3> = [1, 2, 3];
# say %dictionary.perl;
```

Here we get clipboard's content:

```perl6
from-clipboard
```
```
# my %dictionary;
# %dictionary<key1, value1> = 42;
# %dictionary<key2, value2> = "hello";
# %dictionary<key3, value3> = [1, 2, 3];
# say %dictionary.perl;
```

Here we evaluate clipboard's content (assuming it is Raku code):

```perl6
use MONKEY-SEE-NO-EVAL;
EVAL from-clipboard;
```
```
# {"key1," => 42, "key2," => "hello", "key3," => 1, :value1(Any), :value2(Any), :value3(2)}
```



---------

## Implementation notes

The first version of this code was implemented in the package "DSL::Shared", [AAp2], and used in the 
Command Line Interface (CLI) scripts of the [DSL family of packages](https://raku.land/?q=DSL%3A%3AEnglish%3A%3A)
(for computational workflows.)

---------

[AAp1] Anton Antonov,
[LLM::Functions](https://github.com/antononcube/Raku-LLM-Functions),
(2023),
[GitHub/antononcube](https://github.com/antononcube).

[AAp2] Anton Antonov,
[DSL::Shared](https://github.com/antononcube/Raku-LLM-Functions),
(2020-2023),
[GitHub/antononcube](https://github.com/antononcube).