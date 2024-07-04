## 1. Склонировать текущий репозиторий <FIRSTNAME>-<LASTNAME> (например, ivan-ivanov) на локальную машину.
```console
PS C:\git\tms-dos21> git clone https://github.com/tms-dos21-onl/vadim-gleb
Cloning into 'vadim-gleb'...
remote: Enumerating objects: 127, done.
remote: Counting objects: 100% (127/127), done.
remote: Compressing objects: 100% (92/92), done.
remote: Total 127 (delta 37), reused 82 (delta 14), pack-reused 0
Receiving objects: 100% (127/127), 846.56 KiB | 5.57 MiB/s, done.
Resolving deltas: 100% (37/37), done.
```
## 2. Вывести список всех удаленных репозиториев для локального.
```console
PS C:\git\tms-dos21\vadim-gleb\HW8> git remote -v
origin  https://github.com/tms-dos21-onl/vadim-gleb (fetch)
origin  https://github.com/tms-dos21-onl/vadim-gleb (push)
```
## 3. Вывести список всех веток.
```console
PS C:\git\tms-dos21\vadim-gleb\HW8> git branch
* main
```
## 4. Вывести последние 3 коммитa с помощью git log.
```console
PS C:\git\tms-dos21\vadim-gleb> git log -3       
commit 6cc542f652a06b6af52a1871d54b91ccf476b49f (HEAD -> main, origin/main, origin/HEAD)
Author: glebvadims <gleb.vadim.s@gmail.com>
Date:   Thu Jul 4 17:59:18 2024 +0300

    new hw

commit 72da3f57f24adfd3828a8dc5b7efa5aa4a54f387
Author: glebvadims <157623825+glebvadims@users.noreply.github.com>
Date:   Thu Jul 4 17:25:45 2024 +0300

    delete

commit 8a40c6b6d59814af361cc50a18b460f0dd2f7615
Author: glebvadims <157623825+glebvadims@users.noreply.github.com>
Date:   Thu Jul 4 17:21:04 2024 +0300

    start hw8
```
## 5. Создать пустой файл README.md и сделать коммит.
```console
PS D:\git\vadim-gleb\HW8> new-item README.md


    Каталог: D:\git\vadim-gleb\HW8


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        04.07.2024     22:03              0 README.md
```
```console
PS D:\git\vadim-gleb\HW8> git add README.md 
```
```console
PS D:\git\vadim-gleb\HW8> git add README.md 
```
6. Добавить фразу "Hello, DevOps" в README.md файл и сделать коммит.
7. Сделать реверт последнего коммита. Вывести последние 3 коммитa с помощью git log.
8. Удалить последние 3 коммита с помощью git reset.
9. Вернуть коммит, где добавляется пустой файл README.md. Для этого найти ID коммита в git reflog, а затем сделать cherry-pick.
10. Удалить последний коммит с помощью git reset.
11. Переключиться на ветку main или master. Если ветка называется master, то переименовать её в main.
12. Скопировать файл https://github.com/tms-dos21-onl/_sandbox/blob/main/.github/workflows/validate-shell.yaml, положить его по такому же относительному пути в репозиторий. Создать коммит и запушить его в удаленный репозиторий.
13. Создать из ветки main ветку develop. Переключиться на неё и создать README.md в корне репозитория. Написать в этом файле какие инструменты DevOps вам знакомы и с какими вы бы хотели познакомиться больше всего (2-3 пункта). Сделать коммит.

> ⚠️ Для выполнения задания использовать Markdown, а именно заголовок и списки

14. Создать из ветки main ветку support и создать там файл LICENSE в корне репозитория с содержимым https://www.apache.org/licenses/LICENSE-2.0.txt. Сделать коммит. Вывести последние 3 коммитa.
15. Переключиться обратно на ветку main и создать там файл LICENSE в корне репозитория с содержимым https://github.com/git/git-scm.com/blob/main/MIT-LICENSE.txt. Сделать коммит. Вывести последние 3 коммитa.
16. Сделать merge ветки support в ветку main и решить конфликты путем выбора содержимого любой одной лицензии.
17. Переключиться на ветку develop и сделать rebase относительно ветки main.
18. Вывести историю последних 10 коммитов в виде графа с помощью команды git log -10 --oneline --graph.
19. Запушить ветку develop. В истории коммитов должен быть мерж support -> main.
20. Зайти в свой репозиторий на GitHub и создать Pull Request из ветки develop в ветку main.