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
PS D:\git\vadim-gleb\HW8> git add --all 
```
```console
PS D:\git\vadim-gleb\HW8> git commit -am "task 5" 
```
## 6. Добавить фразу "Hello, DevOps" в README.md файл и сделать коммит.
```console
PS D:\git\vadim-gleb\HW8> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   HW8.md
        modified:   README.md
```
```console
PS D:\git\vadim-gleb\HW8> git add --all
```
```console
PS D:\git\vadim-gleb\HW8> git commit -am "task 6: Hello DevOps"
```
## 7. Сделать реверт последнего коммита. Вывести последние 3 коммитa с помощью git log.
```console
PS D:\git\vadim-gleb\HW8> git revert HEAD
[main 3ef0009] Revert "task 6: Hello DevOps"
 2 files changed, 3 insertions(+), 21 deletions(-)
```
```console
PS D:\git\vadim-gleb\HW8> git log -3
commit 3ef0009432306e7f65c925181348795285b16340 (HEAD -> main)
Author: glebvadims <gleb.vadim.s@gmail.com>
Date:   Thu Jul 4 22:14:24 2024 +0300

    Revert "task 6: Hello DevOps"

    This reverts commit c3a3ae3776c2a0b611510e31477e4c55bcde6f80.

commit c3a3ae3776c2a0b611510e31477e4c55bcde6f80 (origin/main, origin/HEAD)
Author: glebvadims <gleb.vadim.s@gmail.com>
Date:   Thu Jul 4 22:12:30 2024 +0300

    task 6: Hello DevOps

commit 8905667b45e8002577e81f7ef68e50c9e5473210
Author: glebvadims <gleb.vadim.s@gmail.com>
Date:   Thu Jul 4 22:05:56 2024 +0300

    task 5
```
## 8. Удалить последние 3 коммита с помощью git reset.
```console
PS D:\git\vadim-gleb\HW8> git reset HEAD~3 --hard
HEAD is now at 0fc9435 Сделаны задания 1-4
```
## 9. Вернуть коммит, где добавляется пустой файл README.md. Для этого найти ID коммита в git reflog, а затем сделать cherry-pick.
- Находим нужный нам id:  8905667 HEAD@{3}: commit: task 5
```console
PS D:\git\vadim-gleb\HW8> git reflog
0fc9435 (HEAD -> main) HEAD@{0}: reset: moving to HEAD~3
3ef0009 HEAD@{1}: revert: Revert "task 6: Hello DevOps"
c3a3ae3 (origin/main, origin/HEAD) HEAD@{2}: commit: task 6: Hello DevOps
8905667 HEAD@{3}: commit: task 5
0fc9435 (HEAD -> main) HEAD@{4}: reset: moving to HEAD~2
b6ac148 HEAD@{5}: reset: moving to b6ac1480efe1ea0ca3ab53b5eafe347c59e52b98
b6ac148 HEAD@{6}: commit: task 5
b73bf78 HEAD@{7}: commit: task 5
0fc9435 (HEAD -> main) HEAD@{8}: pull --tags origin main: Fast-forward
6cc542f HEAD@{9}: reset: moving to HEAD~2
b803aff HEAD@{10}: reset: moving to HEAD~1
47af149 HEAD@{11}: reset: moving to HEAD
47af149 HEAD@{12}: commit: task 8
b803aff HEAD@{13}: reset: moving to HEAD~3
0aff9eb HEAD@{14}: commit: task 7
954b59a HEAD@{15}: revert: Revert "task 6"
edea2f6 HEAD@{16}: reset: moving to edea2f6cbdcde1afbe8e5f047105b85e9ca42599
edea2f6 HEAD@{17}: commit: task 6
b803aff HEAD@{18}: commit: task 5
```
- Возвращаем коммит
```console
PS D:\git\vadim-gleb\HW8> git cherry-pick 8905667
[main f938c5e] task 5
 Date: Thu Jul 4 22:05:56 2024 +0300
 2 files changed, 17 insertions(+)
 create mode 100644 HW8/README.md
```
## 10. Удалить последний коммит с помощью git reset.
```console
PS D:\git\vadim-gleb\HW8> git reset --hard HEAD~1
HEAD is now at 0fc9435 Сделаны задания 1-4
```
## 11. Переключиться на ветку main или master. Если ветка называется master, то переименовать её в main.
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