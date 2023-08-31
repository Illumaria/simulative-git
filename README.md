# Simulative Git Module

Hello, GitHub!

## Домашнее задание

Вступление: дальше по тексту мы будем использовать термин «код», но подразумевать при этом будем любое содержимое файлов. Наша цель сейчас – научиться работать с Git, а не с каким-то языком программирования, поэтому на код отвлекаться не очень хочется.

Итак, представьте себе: Вы – разработчик в IT-компании. Вместе с командой других разработчиков Вы делаете наикрутейший проект, в котором используется сторонняя библиотека с открытым исходным кодом. В какой-то момент работы над проектом вы замечаете, что ваш проект работает не так, как вы ожидаете - всему виной оказывается ошибка в коде сторонней библиотеки! Вы отправляетесь в [Issues](https://github.com/Illumaria/simulative-git/issues) репозитория библиотеки, чтобы завести сообщение об ошибке и попросить разработчиков библиотеки исправить её, но оказывается, что эту ошибку ранее уже заметил и решил исправить один из [мейнтейнеров](https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D0%B9%D0%BD%D1%82%D0%B5%D0%B9%D0%BD%D0%B5%D1%80) официального репозитория. К несчастью, этот мейнтейнер покинул команду, и задача осталась недоделанной. Вы решаете взять дело в свои руки, ведь так Вы и вклад в развитие библиотеки внесёте, и своему проекту поможете!

Каков план действий?
1. Поскольку разработкой сторонней библиотеки занимается другая команда, коммитить напрямую в официальный репозиторий Вы не сможете. Не беда, ведь можно создать форк, сделать там нужную работу, а затем отправить изменения обратно в официальный репозиторий посредством [пулл-реквеста](https://github.com/Illumaria/simulative-git/pulls). Давайте начнём с первого пункта: создайте форк [репозитория](https://github.com/Illumaria/simulative-git) со всеми его ветками.
2. Отлично, Вы скопировали официальный репозиторий и теперь имеете свой собственный репозиторий, но удалённый. Разрабатывать в удалённом, в общем-то, невозможно, поэтому теперь мы хотим клонировать наш удалённый репозиторий на рабочий компьютер.
3. Из описания проблемы в Issues вы увидели, что мейнтейнер работал в ветке `experiment` основного репозитория. Поскольку вы создали форк со всеми ветками основного репозитория, то у вас эта ветка тоже есть. Самое время на неё переключиться.
4. Изучив содержимое файлов и журнал коммитов этой ветки, вы понимаете, что для решения задачи часть последних коммитов просто не нужна, а другая часть нуждается в минорных изменениях. Свою работу Вы решаете начать с  наиболее раннего коммита, где требуются исправления: это коммит с заголовком `"Update experiment.txt"`. Найдите в истории коммитов его идентификатор, переключитесь на него и создайте из него новую ветку с именем `homework`.
5. Теперь - самое главное: исправляем ошибку в коде. Для этого достаточно в файле `experiment.txt` заменить слово `experiment` на `homework`.
6. Вы всё протестировали и убедились в том, что ваши изменения действительно решают исходную проблему. Ура! Осталось проделать обратный путь и отправить изменения в официальный репозиторий. Но если вы прямо сейчас отправите свои текущие изменения в свой же удалённый репозиторий и откроете пулл-реквест в основную (`master`) ветку официального репозитория, то ничего не выйдет:
    <img width="1242" alt="image" src="https://github.com/Illumaria/simulative-git/assets/47138294/49bdd63a-52a9-4575-a47f-c129bcd0e3bb">
    Причина в том, что пока тот мейнтейнер делал работу, ветка `master` убежала вперёд. Вам нужно нагнать изменения в ней, вмержив её изменения в свою ветку `homework`. Однако, использовав `git merge`, история вашей ветки будет не самой красивой:
    <img width="1247" alt="image" src="https://github.com/Illumaria/simulative-git/assets/47138294/359e789a-745e-417b-b9e7-c9c8332ac3f7">
    У нас появился merge-коммит! А ведь можно обойтись и без него, немножко переписав историю:
    <img width="1230" alt="image" src="https://github.com/Illumaria/simulative-git/assets/47138294/91a75d7d-ccf0-4b73-b3d3-10e26099ff79">
    В данном случае, поскольку с вашей веткой, кроме вас, сейчас никто не работает, можно абсолютно безопасно использовать `git rebase`. Сделайте это: синтаксис команды запуска ребейза можно подсмотреть с помощью `git rebase --help`, а то, что делать после начала ребейза, вам подскажет сам git. Читайте _предельно_ внимательно, ничего не пропускайте. Это важно! И помните, что при разрешении конфликта вам нужно _просто выбрать_ ту версию изменений, которую вы хотите оставить.
8. Теперь, когда все изменения внесены, тесты проведены, а история ветки приняла окончательный вид, можно отправлять работу на проверку. Но сначала - в свой удалённый репозиторий. `git push` спешит на помощь.
9. Последний шаг: можно открывать пулл-реквест! Внимательно проверьте ветки - как исходную (то есть ветку в _своём_ удалённом репозитории, изменения _из_ которой вы хотите внести), так и конечную (ветку в _официальном_ репозитории, _в_ которую вы хотите внести ваши изменения). Всё проверили? Тогда остаётся только нажать `Create Pull-Request` и ждать ответа мейнтейнеров!
