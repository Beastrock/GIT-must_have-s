# Базовые операции с Git
Тут рассмотрено несколько типичных операций, которые нужно уметь делать с Гитом.  
Перед прочтением лучше ознакомиться с ссылками в [предыдущей статье на девмане](https://devman.org/encyclopedia/git/git_motivation/): пройти [туториал гитхабе](https://try.github.io/) и прочитать пару глав [Git-book'a](https://git-scm.com/book/ru/v1).  
 
#Задачи
### Подтянуть чужие изменения
>Утро, ты пришёл на работу. Как к локальной версии исходного кода добавить те изменения,  
которые коллеги сделали вчера?  

Для работы с удалёнными репозиториями используем [fetch, merge и pull](https://git-scm.com/book/ru/v1/Основы-Git-Работа-с-удалёнными-репозиториями):  
`$ git fetch server_branch` \# изъять данные из другой ветки  
`$ git merge server_branch` \# слить другую ветку в текущую рабочую  

или  

`$ git pull server_branch master` \#  два действия одной командой  

Вопросы по команде `$ git merge` должны отпасть после прочтения [третьей главы Git-book'a](https://git-scm.com/book/ru/v2/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9E-%D0%B2%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B8-%D0%B2-%D0%B4%D0%B2%D1%83%D1%85-%D1%81%D0%BB%D0%BE%D0%B2%D0%B0%D1%85).    

--------------------------------------------------
###Поделиться своими изменениями с коллегами
>Ну вот, ты поработал. Теперь нужно поделиться своим кодом с другими. Как?  

Используем [git push](https://git-scm.com/book/ru/v1/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%A0%D0%B0%D0%B1%D0%BE%D1%82%D0%B0-%D1%81-%D1%83%D0%B4%D0%B0%D0%BB%D1%91%D0%BD%D0%BD%D1%8B%D0%BC%D0%B8-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D0%BC%D0%B8#Push):  
`$ git push origin master`  

Также важно понимать, почему нежелательно делать [push с форсом](https://developer.atlassian.com/blog/2015/04/force-with-lease/)! 

--------------------------------------------------
### Разобраться с конфликтами
>При попытке отправить свои изменения на сервер ты узнал, что твой коллега изменял тот же файл, что и ты, теперь непонятно, какая версия правильная. Как быть?   

Чтобы посмотреть разницу состояния файла при разных коммитах используют команду `$ git diff`.  
О том, как ей пользоваться можно прочесть на [СтекОверфловиче](http://stackoverflow.com/questions/3338126/how-to-diff-the-same-file-between-two-different-commits-on-the-same-branch).  
А если непонятно чей код оставлять: твой или коллеги, то уже выяснить это напрямую с ним.  

В PyCharm можно выполнять данные операции удобнее и нагляднее чем в консоле. [Ссылка на документацию](https://www.jetbrains.com/help/pycharm/2016.1/using-git-integration.html)   

--------------------------------------------------
### Отпочковать ветку
>Тимлид дал тебе задачу. Объяснение он закончил фразой "делай в фичабранче". Когда ты спросил, что это значит, он промямлил что-то про гитфлоу. Что делать-то?  

`$ git branch feature_branch`  # создание новой ветки  
`$ git checkout feature_branch` # переход в новую ветку  

или  

`$ git checkout -b feature_branch` # два действия одной командой  

Графические иллюстрации веток для понимания происходящего можно найти всё в том же [Git-book](https://git-scm.com/book/ru/v2/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9E-%D0%B2%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B8-%D0%B2-%D0%B4%D0%B2%D1%83%D1%85-%D1%81%D0%BB%D0%BE%D0%B2%D0%B0%D1%85).  

--------------------------------------------------
### Слить свои изменения
>Задачу ты закончил, теперь ты получил указание "замерджить свой бранч в дев". Что это за дичь? Как делать?  

Всё та же третья глава и уже, должно быть, знакомые команды:   
`$ git checkout dev_branch` # переключаемся на ветку dev  
`$ git merge my_work_branch` # мерджим ветку my_work_branch  
  
--------------------------------------------------
### Добавить в одну ветку изменения из другой
>Следующую задачу ты делаешь так же, в отдельной ветке от дева. Правда, долго: уже неделя прошла, а задача не готова. Лид даёт указание "подлить изменения из дева в свой бранч". Шта?  
  
`$ git merge dev` # выполняем команду слияния ветки dev с my_branch, находясь в векте my_branch  

--------------------------------------------------
### Перенести коммит
>Ты сделал задачу, но ошибся с веткой, в которую коммитить: вместо дева сделал коммит в мастер. Хорошо, что не запушил. Теперь надо этот коммит перенести в дев. Как это сделать?  

Используем [git cherry-pick](https://git-scm.com/docs/git-cherry-pick) и [git reset](https://githowto.com/ru/removing_commits_from_a_branch):  
`$ git cherry-pick 62ecb3` # выполним команду, находясь в ветке dev. Данная команда заберёт все коммиты ветки в другую одним коммитом, в нашем случае из ветки dev в ветку master. `62ecb3` - хэш ошибочного коммита.   
`$ git сommit -m "Commit message`  # сделать коммит уже в своей ветке  
`$ git checkout master` # переходим в master  
`$ git reset --hard HEAD` # удаление ошибочного коммита вместе с индексированными файлами. Подробнее о данной команде в следующем пункте.  


--------------------------------------------------
### Откатить коммит
>Работаешь над фронтом в своей ветке и, вдруг, понимаешь, что сильно ошибся уже как два коммита назад... Как откатиться?

Предположим, вот два последних коммита:  
`$ git commit -m "Change header style with a mistake"`  
`$ git commit -m "Change header style with a critical mistake"`  

Надо вернуться к состоянию репозитория на третий коммит, где нет той самой ошибки. Чтобы было проще дальше объяснять, обзовём это состояние репозитория "C" (от слова correct).  

Первый способ, используем reset:     
`$ git reset --hard HEAD~2` # все файлы изменятся на состояние репозитория "C", а индексированные файлы двух ошибочных коммитов будут удалены. 

Выглядеть это будет как на картинке из [одного стоящего прочтения параграфа GitBook'a](https://git-scm.com/book/ru/v2/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-Git-%D0%A0%D0%B0%D1%81%D0%BA%D1%80%D1%8B%D1%82%D0%B8%D0%B5-%D1%82%D0%B0%D0%B9%D0%BD-reset), только здесь рассматривается переход на один коммит назад, а не на два:
![alt-text](https://git-scm.com/book/en/v2/book/07-git-tools/images/reset-hard.png)

Если ошибка совсем критична, то нет смысла оставлять каталог индексированным. Но, если нет, то мы могли бы воспользоваться `$ git reset --soft HEAD~2`. В таком случае произойдет отмена двух последних коммитов и все индексированные файлы станут "unstaged". Сами файлы не изменятся и будут соответствовать последнему состоянию репозитория с ошибкой, поэтому придётся их исправить, чтобы вести дальнейшую работу с кодом. Также можно использовать `$ git commit -c ORIG_HEAD`, чтобы не писать сообщение коммита заново.  

Выглядеть это будет так:
![alt-text](https://git-scm.com/book/en/v2/book/07-git-tools/images/reset-soft.png)

Подытожим, фрагментом из данного параграфа. Команда reset:

1. Перемещает ветку, на которую указывает HEAD (останавливается на этом, если указана опция --soft)

2. Делает Индекс таким же как и HEAD (останавливается на этом, если не указана опция --hard)

3. Делает Рабочий Каталог таким же как и Индекс.

Второй способ, используем [revert](https://githowto.com/ru/undoing_committed_changes):  
`$ git commit revert HEAD~2` # всё тоже самое, но безопаснее: команда создаёт новый коммит c состоянием репозитория "C", не удаляя предыдущие коммиты и не трогая индексированные файлы.

![alttext](https://www.git-tower.com/learn/content/01-git/04-faq/04-undo-revert-old-commit/01-revert-concept.png)  

Иллюстрированное резюме:  

![alttext](http://image.slidesharecdn.com/gittutorial-150724014321-lva1-app6891/95/git-tutorial-19-638.jpg?cb=1437702443) 


--------------------------------------------------
### Удалить коммиты, которые были запушены на удалённый сервер
>Как же мне теперь удалить пять коммитов с сообщением "финальная версия 3" из ветки на github?  

Используем [git rebase](https://git-scm.com/book/ru/v1/%D0%92%D0%B5%D1%82%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B2-Git-%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D1%89%D0%B5%D0%BD%D0%B8%D0%B5):  
`$ git rebase -i origin/master~4 master`  
`$ git push origin +master`   

Плюс - это почти --force и использовать его надо крайне осторожно! На [СтекОверфловиче](http://stackoverflow.com/questions/8981194/changing-git-commit-message-after-push-given-that-no-one-pulled-from-remote) подробнее говорится про данную команду.

--------------------------------------------------
### Добавить изменение в сделанный коммит или переименовать его  
>Исправил ридми, но забыл поставить запятую...  

Используем [git commit --amend](https://git-scm.com/book/ru/v1/%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D1%8B-Git-%D0%9E%D1%82%D0%BC%D0%B5%D0%BD%D0%B0-%D0%B8%D0%B7%D0%BC%D0%B5%D0%BD%D0%B5%D0%BD%D0%B8%D0%B9):  
`$ git commit -m "Add description"` # сделали коммит   
`$ git add README.md` # вспомнили про запятую, отредактировали и добавили заново файл   
`$ git commit --amend` # команда добавит изменения в сделанный коммит c возможностью переименовать его сообщение в встроенном по умолчанию редакторе Vim  

Чтобы просто переименовать предыдущий коммит, нужно использовать ту же связку команд, но не добавлять файлы в индекс:  
`$ git commit -m "Add description"`  
`$ git commit --amend`  

--------------------------------------------------

# Contributing

Нашел ошибки? Хочешь пулреквестнуть?  
Пиши мне в slack [@beastrock](https://devmanorg.slack.com/team/beastrock) или [вконтакте](http://vk.com/beastrock).
