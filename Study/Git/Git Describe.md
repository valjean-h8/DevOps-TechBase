Теги являются прекрасными ориентирами в истории изменений, поэтому в `git` ть команда которая показывает, как далеко текущее состояние от ближайшего тега. И эта команда называется `git describe`
Git describe помогает сориентироваться после отката на много коммитов по истории изменений.

`git describe <ref>`

Где `ref` - это что-либо, что указывает на конкретный коммит. Если не указать `ref`, то git будет считат, что указано текущее положение (HEAD).

Вывод команды выглядит примерно так:

`<tag>_<numCommits>_g<hash>`

`tag` - это ближайший тег
`numCommits` - это на сколько далеко мы от этого тега
`hash` - это хеш коммита, который описывается