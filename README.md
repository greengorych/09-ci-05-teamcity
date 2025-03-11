# Домашнее задание к занятию 11 «Teamcity»

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.

![alt text](images/image.png)

3. Сохраните необходимые шаги, запустите первую сборку main.

![alt text](images/image-1.png)

4. Поменяйте условия сборки: если сборка по ветке `main`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.

![alt text](images/image-5.png)

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

![alt text](images/image-3.png)

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.

![alt text](images/image-4.png)

7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

![alt text](images/image-2.png)

8. Мигрируйте `build configuration` в репозиторий.

![alt text](images/image-6.png)

9. Создайте отдельную ветку `feature/add_reply` в репозитории.

![alt text](images/image-7.png)

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.

```java
 public String sayHunter() {
                return "Welcome, brave hunter!";
        }
```

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

```java
        public void welcomerSaysHunter() {
                assertThat(welcomer.sayWelcome(), containsString("hunter"));
                assertThat(welcomer.sayFarewell(), containsString("hunter"));
                assertThat(welcomer.sayHunter(), containsString("hunter"));
        }
```

12. Сделайте push всех изменений в новую ветку репозитория.

![alt text](images/image-8.png)

13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

![alt text](images/image-9.png)

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.

![alt text](images/image-10.png)

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.

![alt text](images/image-13.png)

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![alt text](images/image-14.png)

![alt text](images/image-16.png)

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.

![alt text](images/image-15.png)

19. В ответе пришлите ссылку на репозиторий.

Ссылка на репозиторий с артефактами [example-teamcity](https://github.com/greengorych/example-teamcity/blob/main/README.md)

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
