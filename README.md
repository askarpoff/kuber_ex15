# Домашнее задание к занятию Troubleshooting

### Цель задания

Устранить неисправности при деплое приложения.

### Задание. При деплое приложение web-consumer не может подключиться к auth-db. Необходимо это исправить

1. Установить приложение по команде:
```shell
kubectl apply -f https://raw.githubusercontent.com/netology-code/kuber-homeworks/main/3.5/files/task.yaml
```
2. Выявить проблему и описать.
3. Исправить проблему, описать, что сделано.
4. Продемонстрировать, что проблема решена.

### Ответ:

1. Установить приложение по команде:
```shell
kubectl apply -f https://raw.githubusercontent.com/netology-code/kuber-homeworks/main/3.5/files/task.yaml
```
![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/75aca39e-f5cb-454c-ae01-15ea5554bbb4)

Добавил namespace'ы, запустил

![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/af4f5c5f-01c2-4df6-b47b-5b6e87a9d295)

2. Выявить проблему и описать.

![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/95ba9fef-2510-4c78-ac48-05921fa524ea)
фронтенд "не видит" бэкенд, т.к. они в разных namespace


3. Исправить проблему, описать, что сделано.

Добавил службу внешних имен, в принципе порт можно не указывать там, но уж как вышло

```yaml
apiVersion: v1
kind: Service
metadata:
  name: auth-db
  namespace: web
spec:
  type: ExternalName
  externalName: auth-db.data.svc.cluster.local
  ports:
  - port: 80
```

![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/56a033bb-1f16-4745-9791-335d71e569b7)


4. Продемонстрировать, что проблема решена.

Логи пода auth db
![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/4ebf07e2-94a1-4220-8044-e74c68837bb2)

В логах подов web-consumer последняя запись
![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/ef4d9cb5-1fca-41d5-afc3-b00d1dd280e2)

Проверим запуском

![image](https://github.com/askarpoff/kuber_ex15/assets/108946489/1a984b88-058a-4421-bd61-eaeb8cde8ca5)

Теперь __web-consumer__ может подключиться к __auth-db__
