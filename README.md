# Clipboard

Raku package for using clipboards of different operating systems. (I.e., copy and paste with any OS.)

**Remark:** The package is (extensively) tested and used on macOS. 
At this point it is not tested on other OS. (Issues and pull requests are welcome!)

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
$chat.eval('Generate a random dictionary of 5 elements.') ==> copy-to-clipboard
```
```
# my %dictionary = (
#   'apple' => 'a fruit',
#   'car' => 'a vehicle',
#   'cat' => 'a mammal',
#   'sun' => 'a star',
#   'book' => 'a written work'
# );
# 
# .say for %dictionary.pairs;
```

Here we get clipboard's content:

```perl6
paste
```
```
# my %dictionary = (
#   'apple' => 'a fruit',
#   'car' => 'a vehicle',
#   'cat' => 'a mammal',
#   'sun' => 'a star',
#   'book' => 'a written work'
# );
# 
# .say for %dictionary.pairs;
```

Here we evaluate clipboard's content (assuming it is Raku code):

```perl6
use MONKEY-SEE-NO-EVAL;
EVAL paste;
```
```
# car => a vehicle
# cat => a mammal
# sun => a star
# apple => a fruit
# book => a written work
```

---------

## Synonyms

Here are the synonyms of the clipboard subs:

```perl6
use Clipboard :DEFAULT;      # copy-to-clipboard, paste
use Clipboard :cb-prefixed;  # cbcopy, cbpaste
use Clipboard :long-names;   # copy-to-clipboard, paste-from-clipboard
use Clipboard :ALL;          # copy-to-clipboard, paste, cbcopy, cbpaste, paste-from-clipboard
```
```
# (Any)
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