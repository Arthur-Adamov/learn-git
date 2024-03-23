# Шпаргалка по работе с Git.

## Базовыве команды консоли.

### Навигация.

`pwd` *(от англ. print working directory, "показать рабочую папку")* - покажи, в какой я папке.

`ls` *(от англ. list directory contents, "отобразить содкржимое директории")* - покажи файлы и папки в текущей папке.

`ls -a` - покажи скрытые файлы и папки, названия которыз начинаются с символа . .

`cd` *(от англ. change directory, "сменить даректорию")* - перейти в папку, название которой нужно написать после команды.

`cd ..` - перейти на уровеньвыше, в родительскую папку.

`cd ~` - перейти в домашнюю директорию.

`cd /` - перейти в корневую диркторию.

## Работа с файлами и папками.

### Создание.

`touch index.html` *(англ. touch, "коснуться")* - создай файл index.html в текущей папке.

`touch index.html style.css script.js` - если нужно создать сразу несколько файлов, можно напечатать из имена в одну строку через пробел.

`mkdir second-project` *(от англ. make directory, "создай директорию")* - создай папку с именем second-project в текущей папке.

### Копирование и перемещение.

`cp file.txt ~/my-dir` *(от англ. copy, "копировать")* - скопируй файл file.txt в директорию my-dir.

`mv file.txt ~/my-dir` *(от англ. move, "переместить")* - перемести файл в указанную директорию.

### Чтение.

`cat file.txt` *(от англ. concatenate and print, "объединить и распечатать")* - распечатай содержимое текстового файла file.txt.

### Удаление.

`rm about.html` *(от англ. remove, "удалить")* - удали файл about.html.

`rmdir images` *(от англ. remove direktory, "удали директорию")* - удали папку images.

`rm -r second-project` *(от англ. remove "удалить" + recursive "рекурсивный")* - удали папку second-project и всё , что она содержит.

---

## Git.

`git init` *(от англ. initialize "инициализировать")* - делает выбранную папку репозиторием.

`rm -rf .git` - "разгитить" папку, если что-то пошло не так. Вся история проекта будет удалена.

`git status` - проверить состояние репозитория.

### Добавление файлов в репозиторий.

`git add` - *(после этой команды указывается имя файла)* - подготовить файлы к сохранению.

`git add --all` - подготовить к сохранению все файлы в репозитории.

`git add -A` - подготовить все измененные файлы.

`git add .` - подготовить всю текущую папку.

### Создание коммитов.

`git commit` - выполнить коммит.

`git commit -m "сообщение"` - выполнить коммит с комментарием.

`git log` - посмотреть историю коммитов.

`git log --oneline` - посмотреть историю коммитов в сокращенном виде.

---

## Работа с GitHub.

`git remote add origin` - связываем локальный репо с удаленным перед отправкой измененний в удаленный репо.

`git remote -v` - посмотреть удаленные URL-адреса. Отражает удаленные подключения к другим репозиториям.

`git push -u origin main` - связываем локальную ветку с удаленной в созданном на GitHub репозитории.

---

## Статусы файлов в Git.

* **untracked** *(от англ. "неотслеживаемый")*

Новые файлы в репозитории помечаются как **untracked**, то есть неотслеживаемые. **Git** видит такой файл, но не следит за изменениями в нем.

* **staged**  *(англ. "подготовленный")*

После выполнения команды `git add` файл попадает в **stagind area**, то есть в список файлов, которые войдут в коммит.

* **tracked**  *(англ. "отслеживаемый")*

Состояние **tracked** - это противоположность **untracked**. В него попадут файлы, которые уже были зафиксированны с помощью `git commit`, а также файлы, которые были добавлены в **staging area** командой `git add`. То есть все файлы, в которых **Git** так или иначе отслеживает изменения.

* **modified** *(англ. "измененный")*

Состояние **modified** означает, что **Git** сравнил содержимое файла с последней сохраненной версией и нашел отличия. Например, файл был закомичен и после этого изменен.

  ```mermaid
flowchart TD;
    A(untracked) -->|git add| B(staged);
    B --> |git commit| C(tracked);
    C -->|изменения| D(modified);
    B -->|изменения| D(mofified);
    D -->|git add| B;
```

---

## Хеш — идентификатор коммита.

### Что такое хеш. Хеширование коммитов.

**Хеширование** *(от англ. hash, «рубить», «крошить», «мешанина»)* — это способ преобразовать набор данных и получить их «отпечаток» *(англ. fingerprint)*.

**Информация о коммите** — это набор данных: когда был сделан коммит, содержимое файлов в репозитории на момент коммита и ссылка на предыдущий, или родительский (англ. parent), коммит.

### Хеш — основной идентификатор коммита
**Git** хранит таблицу соответствий `хеш → информация о коммите.` Если вы знаете хеш, вы можете узнать всё остальное: автора и дату коммита и содержимое закоммиченных файлов. Их можно будет передавать в качестве параметра разным **Git-командам**, чтобы указать, с каким коммитом нужно произвести то или иное действие.

Все хеши и таблицу `хеш → информация о коммите` **Git** сохраняет в служебные файлы. Они находятся в скрытой папке `.git` в репозитории проекта.

---

## Исследуем лог.

После вызова `git log` появляется список коммитов:

```
Артур@DESKTOP-VJEINQP MINGW64 ~/dev/learn-git (main)
$ git log
commit 32aa3e464aac7284e7f2c4c34d8fe22e7d4bbbc8 (HEAD -> main, origin/main)
Author: Artur Adamov <artur.adamov03340@yandex.ru>
Date:   Wed Jan 24 14:34:46 2024 +0300

    исправил выделения команд MARKDOUW

commit 494ac42e24d21c8faf9098169c75f741b75c9dad
Author: Arthur-Adamov <vasiliy.moroz2601@gmail.com>
Date:   Sun Jan 21 22:56:03 2024 +0300

    добавил пункт в абзац Добавление файлов в репо

commit 4101d1d3559bc74616003761d30992258d4625bd
Author: Arthur-Adamov <vasiliy.moroz2601@gmail.com>
Date:   Sun Jan 21 19:17:49 2024 +0300

    добавил MARKDOWN
```

Получить сокращённый лог — `git log --oneline`:

```
Артур@DESKTOP-VJEINQP MINGW64 ~/dev/learn-git (main)
$ git log --oneline
32aa3e4 (HEAD -> main, origin/main) исправил выделения команд MARKDOUW
8a89702 Update README.md
494ac42 добавил пункт в абзац Добавление файлов в репо
4101d1d добавил MARKDOWN
bfb5ab8 исправил пункт Работа с GitHub.
```

---

## HEAD — всему голова.

Файл **HEAD** *(англ. «голова», «головной»)* — один из служебных файлов папки `.git`. Он указывает на коммит, который сделан последним (то есть на самый новый).
В этом можно убедиться с помощью терминала. Перейдите в папку `.git` командой `cd`. Посмотрите содержимое файла **HEAD** командой `cat`.

```
$ pwd # посмотрели, где мы
/Users/user/dev/first-project

$ cd .git/
$ ls # посмотрели, какие есть файлы
COMMIT_EDITMSG  ORIG_HEAD  description  index  logs/     refs/
HEAD            config     hooks/       info/  objects/

$ cat HEAD # команда cat показывает содержимое файла
ref: refs/heads/master # в файле вот такая ссылка 
```

Внутри **HEAD** — ссылка на служебный файл: `refs/heads/master` (или `refs/heads/main` в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.

```
$ cat refs/heads/master # взяли ссылку из файла HEAD
# внутри хеш
e007f5035f113f9abca78fe2149c593959da5eb7

$ git log 
# сверяем с хешем последнего коммита
commit e007f5035f113f9abca78fe2149c593959da5eb7
Author: John Doe <johndoe@example.com>
Date:   Tue Mar 28 00:26:53 2023 +0300

    Добавить амбиций в список дел

... # другие коммиты 
```

Когда вы делаете коммит, **Git** обновляет `refs/heads/master` — записывает в него хеш последнего коммита. Получается, что **HEAD** тоже обновляется, так как ссылается на `refs/heads/master`.


# Игнорирование файлов в Git.

.gitignore (от англ. ignorej - "игнорировать") это файл котрый нужно создать и записать в него названия игнорируемых файлов.

`git status --ignored` - посмотреть что игнорируется.

> 💡 Правила из .gitignore применяются только к новым (untracked) файлам. Если файл уже попал в staging area или в коммит, то рпавила на него не распрстраняются.

## Заполнение файла .gitignore.

Если нужно, чтобы **Git** игнорировал все файлы **.DS_Store**. Для этого достаточно добавить в **.gitignore** строку с названием файла.

### Комментарий

Если строка начинается с **#**, то это комментарий, и **.gitignore** не будет его учитывать.

### Звёздочка (*)

Символ звёздочки **(\*)** соответствует любой строке, включая пустую. Например:

```
# игнорировать все файлы, которые заканчиваются на .jpeg
*.jpeg

# игнорировать все файлы "tmp" во всех подпапках папки docs
docs/*/tmp 
```

### Вопросительный знак (?)

Вопросительный знак **?** соответствует одному любому символу.

```
file?.txt 
```

Если сохранить такую запись в .gitignore, то будут проигнорированы, например, файлы fileA.txt и file1.txt.

### Квадратные скобки ([…])

Квадратные скобки **([…])**, как и вопросительный знак, соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.

```
# игнорировать файлы file0.txt, file1.txt и file2.txt
# при этом не игнорировать file3.txt, file4.txt, ...
file[0-2].txt 
```

### Слеш (/)

Косая черта, или слеш **(/)**, указывает на каталоги. Если шаблон в .gitignore начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.

```
# игнорировать todo.txt в корне репозитория
/todo.txt

# для сравнения: spam.txt будет игнорироваться во всех папках
spam.txt 

# игнорировать папку build
build/ 
```

### Парные звёздочки (**)

Функция парных звёздочек (**) похожа на функцию одинарной (*). Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю). Одинарная может соответствовать только одной.

```
# игнорировать файлы "docs/current/tmp", "docs/old/tmp",
# а также "docs/old/saved/a/b/c/d/tmp"
# и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
docs/**/tmp

# игнорировать только "docs/current/tmp" и "docs/old/tmp"
# файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
docs/*/tmp
```

### Восклицательный знак (!)

Любое правило в файле .gitignore можно инвертировать с помощью восклицательного знака (!).

```
# игнорировать все JPEG-файлы
*.jpeg

# но только не мем с Doge
!doge.jpeg
```

### Пример файла .gitignore

```
Содержание .gitignore может быть таким.
# игнорировать все файлы в каталоге build
build/

# игнорировать все .log файлы
*.log

# не игнорировать *.log файлы в examples
# потому что это пример для документации
!examples/**/*.log 
```

___

## Работа с ветками

### Клонирование чужого репозитория

`git clone git@github.com:YandexPraktikum/first-project.git` *(от англ. clone, «клон», «копия»)* — склонируй репозиторий с URL first-project.git из аккаунта YandexPraktikum на мой локальный компьютер.

### Создание веток
`git branch feature/the-finest-branch` *(от англ. branch, «ветка»)* — создай ветку от текущей с названием **feature/the-finest-branch**;

`git checkout -b feature/the-finest-branch` — создай ветку **feature/the-finest-branch** и сразу переключись на неё.

### Навигация по веткам

`git branch` *(от англ. branch, «ветка»)* — покажи, какие есть ветки в репозитории и в какой из них я нахожусь (текущая ветка будет отмечена символом *);

`git branch -a` — покажи все известные ветки, как локальные (в локальном репозитории), так и удалённые (в **origin**, или на GitHub).

`git checkout feature/br` — переключись на ветку **feature/br**.

### Сравнение веток

`git diff main HEAD` *(от англ. difference, «отличие», «разница»)* — покажи разницу между веткой **main** и указателем на **HEAD**;

`git diff HEAD~2 HEAD` — покажи разницу между тем коммитом, который был два коммита назад, и текущим.

### Удаление веток

`git branch -d br-name` — удали ветку **br-name**, но только если она является частью **main**;

`git branch -D br-name` — удали ветку **br-name**, даже если она не объединена с **main**.

### Слияние веток

`git merge main` *(от англ. merge, «сливать», «поглощать»)* — объедини ветку **main** с текущей активной веткой. 

### Работа с удалённым репозиторием

`git push -u origin my-branch` *(от англ. push, «толкнуть», «протолкнуть»)* — отправь новую ветку **my-branch** в удалённый репозиторий и свяжи локальную ветку с удалённой, чтобы при дополнительных коммитах можно было писать просто **git push** без **-u**;

`git push my-branch` — отправь дополнительные изменения в ветку **my-branch**, которая уже существует в удалённом репозитории;

`git pull` *(от англ. pull, «вытянуть»)* — подтяни изменения текущей ветки из удалённого репозитория.
