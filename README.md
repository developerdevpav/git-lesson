##Основаный команды
<code>git branch</code> - list exists branches already\
<code>git branch PROJ-001</code> - create new branch (PROJ-001)\
<code>git checkout -b PROJ-001</code> - create and visit branch PROJ-001

<code>git add file.txt</code> - add the file (file.txt) to stage.\
<code>get rm file.txt</code>  - remove the file (file.txt) from stage.


##Объединение commits в один конечный.

Переходим в побочную ветку PROJ-001
<br/>

<code>git checkout PROJ-001</code>

Делаем необходимые изменения и проверяем<br/>

<code>git add file.txt && git status</code>

Если все отлично делаем _commit_

<code>git commit -m "added new file.txt"</code>
<br/>

Дальше смотрим сделанные commits
<br/>

<code>git log</code>
<br/>

Смотрим какое количество _commits_ хотим объединить и выполняем
<br/>

<code>git rebase -i HEAD~count commit</code>
<br/>

Открывается редактор в котором будет примерно такое содержание:
```
pick bcdca61 Second commit <br/>
pick 4643a5f The third commit with cool stuff <br/>
pick e0ca8b9 The last commit <br/>

# Rebase 48411de..e0ca8b9 onto 48411de
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell 
```
<BR/>

Самый первый commit указан вверху.
Изменим `pick` на `squash`

```
pick bcdca61 Second commit <br/>
squash 4643a5f The third commit with cool stuff <br/>
squash e0ca8b9 The last commit <br/>

# Rebase 48411de..e0ca8b9 onto 48411de
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell 
```

Дальше откроется в редакторе информация о объединении commits и сдесь можно указать название commit и описание. Для этого достаточно просто оставить строки без `#`

После проверим получившиеся commit и копируем `hash` commit
<br/>

<code>git log</code>

<br/>

Теперь необходимо перейти в ветку, в которую хотим сделать cherry-pick, допустим `master`
<br/>

<code>git checkout master && git cherry-pick e1233ewv </code>

