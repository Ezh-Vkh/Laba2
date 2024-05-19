## Laba2

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.

```sh
$ mkdir lab02 && cd lab02
$ git init
$ touch README.md
$ git add README.md
$ git remote add origin https://github.com/3Wc4YEM5/lab02.git
$ git commit -m "first commit"
$ git push origin master
```

3. Создайте файл hello_world.cpp в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку using namespace std;.

```sh
$ cat > Hello_world.cpp << EOF
#include <iostream>
using namespace std;
int main() { cout << "Hello, world!" << endl; }
EOF
```

4. Добавьте этот файл в локальную копию репозитория.

```sh
git add Hello_world.cpp
```

5. Закоммитьте изменения с осмысленным сообщением.

```sh
git commit -m "added Hello_world.cpp"
```

6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

```sh
#include <iostream>
using namespace std;
int main() {
    string name;
    cout << "Enter name ";
    cin >> name; //Запрос @name для программы
    cout << "Hello world from " << name;
}
```

7. Закоммитьте новую версию программы.

```sh
$ git commit -m "new Hello_world.cpp"
```

8. Запуште изменения в удалёный репозиторий.

```sh
$ git push origin master
```

### Part II

1. В локальной копии репозитория создайте локальную ветку patch1.

```sh
$ git branch patch1
$ git checkout patch1
```

2. Внесите изменения в ветке patch1 по исправлению кода и избавления от using namespace std.

```sh
#include <iostream>
int main() { 
    std::string name;
    std::cout << "Enter name ";
    std::cin >> name;
    std::cout << "Hello world from " << name;
}
```

3. **commit, push** локальную ветку в удалённый репозиторий.

```sh
$ git add Hello_world.cpp
$ git commit -m "patched  Hello_world.cpp"
$ git push origin patch1
```

4. Проверьте, что ветка patch1 доступна в удалёный репозитории.
5. Создайте pull-request patch1 -> master.
6. В локальной копии в ветке patch1 добавьте в исходный код комментарии.

```sh
#include <iostream>
int main() { 
    std::string name;
    std::cout << "Enter name ";
    std::cin >> name;
    std::cout << "Enter name "; 
    std::cin >> name; //Запрос @name
    std::cout << "Hello world from " << name;
}
```

7. **commit, push**.
```sh
$ git add Hello_world.cpp
$ git commit -m "added comment in code"
$ git push origin patch1
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните слияние PR patch1 -> master и удалите ветку patch1 в удаленном репозитории.
10. Локально выполните pull.
```sh
$ git checkout master
$ git pull origin master
```

11. С помощью команды git log просмотрите историю в локальной версии ветки master.
```sh
$ git log
```

```sh
commit 647315cf20c2ee494d333671211ac0903b9c9406 (master)
Merge: 2985f7c e82700b
Author: Pupkenberg <113918951+3Wc4YEM5@users.noreply.github.com>
Date:   Thu May 19 22:09:56 2024 +0300

    Merge pull request #1 from 3Wc4YEM5/patch1
    
    patched  Hello_world.cpp

commit e82700bbf3da34984eabbd7bf2ee2973ff89c7a1 (origin/patch1)
Author: 3Wc4YEM5 <aibushev.goscha@yandex.ru>
Date:   Thu May 19 22:06:14 2024 +0300

    added comment in code

commit a7fd39a6ac664e2a0e2e7ec2915a1d542b970d51
Author: 3Wc4YEM5 <aibushev.goscha@yandex.ru>
Date:   Thu May 19 22:00:21 2024 +0300

    patched  Hello_world.cpp

commit 2985f7c852cd973cea3a18afa2f06d19fb915474
Author: 3Wc4YEM5 <aibushev.goscha@yandex.ru>
Date:   Thu May 19 22:58:18 2024 +0300

    new Hello_world.cpp

commit dc6a9abd64e2e1b1101e5b724526581142049485
Author: 3Wc4YEM5 <aibushev.goscha@yandex.ru>
Date:   Thu May 19 22:56:16 2024 +0300

    added Hello_world.cpp

commit 50d6d5f5093304cd0adbd6842e1f34f3abb5dd04
Author: 3Wc4YEM5 <aibushev.goscha@yandex.ru>
Date:   Thu May 19 22:54:38 2024 +0300

    first commit
```

12. Удалите локальную ветку patch1.
```sh
$ git branch -d patch1
```

### Part III

1. Создайте новую локальную ветку patch2.
```sh
$ git branch patch2
$ git checkout patch2
```
2. Измените _code style_ с помощью утилиты clang-format. Например, используя опцию -style=Mozilla.
```sh
$ clang-format  -style=Mozilla Hello_world.cpp
```
3. **commit, push**, создайте pull-request patch2 -> master.
```sh
$ git add Hello_world.cpp
$ git commit -m "new codestyle"
$ git push origin patch2
```

4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```sh
#include <iostream>
int main() { 
    std::string name;
    std::cout << "Enter name "; 
    std::cin >> name; //Запрос @name
    std::cin >> name; //Запрос @name для программы
    std::cout << "Hello world from " << name;
}
```
5. Убедитесь, что в pull-request появились _конфликтны_.
6. Для этого локально выполните **pull + rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты.**
```sh
$ git pull origin master --rebase
```

```sh
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (3/3), 1003 байта | 1003.00 КиБ/с, готово.
Из https://github.com/3Wc4YEM5/lab02HW
 * branch            master     -> FETCH_HEAD
   647315c..1da44bd  master     -> origin/master
Автослияние Hello_world.cpp
КОНФЛИКТ (содержимое): Конфликт слияния в Hello_world.cpp
error: не удалось применить коммит 12937d9... new codestyle
```

Исправленный файл:
```sh
#include <iostream>
int 
main() { 
    std::string name;
    std::cout << "Enter name "; 
    std::cin >> name; //Запрос @name для программы
    std::cout << "Hello world from " << name;
}
```

```sh
$ git add Hello_world.cpp
$ git rebase --continue
```

7. Сделайте force push в ветку patch2.

```sh
$ git push -f origin patch2
```
8. Убедитель, что в pull-request пропали конфликтны.
9. Вмержите pull-request patch2 -> master.

```sh
ИУ8-25 Маланичев Александр
```
