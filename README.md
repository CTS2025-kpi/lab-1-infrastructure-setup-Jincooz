[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/O_-fUwED)

## 1. Set-up account. Register in a cloud provider. Now you have a root account.

<img width="941" height="445" alt="image" src="https://github.com/user-attachments/assets/577e8b38-d612-486b-83c6-fc51870b9aac" />

## 2.b Create an IaM Identity center account (or analog for you cloud provider). Also make it full admin.

Я створив IaM Identity center.
Створив користувача, який отримає AdministratorAccess.

<img width="947" height="77" alt="image" src="https://github.com/user-attachments/assets/be6db8dc-124c-405d-80c4-53d91629c860" />

Створив за превизначеним permission set AdministratorAccess.

<img width="941" height="81" alt="image" src="https://github.com/user-attachments/assets/6890e79f-c0ab-4005-a212-ea21834c53af" />

І зв’язав їх в AWS accounts.

<img width="944" height="98" alt="image" src="https://github.com/user-attachments/assets/030048b1-e059-4493-b91a-49ce789a5808" />

## 3. (Optional) Create an Organisation docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html and user for it. All next labs are to be performed within it.

Організація була створена автоматично, коли я створював IaM Identity center.

## 4.Create one more user. Create an IaM policy that allows ONLY to view resources (no write access).

Створив користувача.

<img width="939" height="37" alt="image" src="https://github.com/user-attachments/assets/abcf6748-706e-4842-b8d7-56cacf1cf7d0" />

Створив за превизначеним permission set ReadOnlyAccess.

<img width="940" height="29" alt="image" src="https://github.com/user-attachments/assets/c97c5b48-bd12-4809-9517-25554ff67c17" />

І зв’язав їх.

<img width="941" height="44" alt="image" src="https://github.com/user-attachments/assets/b261d207-07cb-4cf3-926d-4b47eae47921" />

## 5. Create a Role that has this policy attached and can be assumed by user from p3.

Permission sets в IaM Identity center виконує функцію ролі. Для демонстрації ціього я створив інший, більш обмежений permission set ViewOnlyAccess. І додав його до OnlyView користувача.

<img width="934" height="59" alt="image" src="https://github.com/user-attachments/assets/b22031ea-5e00-4e0f-86a3-33ffedb2eb97" />

Тепер якщо я зайду на OnlyView мені відобразиться AWS access portal, який дозволить обрати permission set за яким я буду працювати. Цей же інтерфейс дозволяє його змінювати.

<img width="941" height="273" alt="image" src="https://github.com/user-attachments/assets/909e60a9-bc65-4c04-ab0b-e16b3ac36cf0" />

## 6. Create a network (VPC for your resources). There should be private and public subnets. Public one has IGW, private ones are for internal access only.

Створив VPC.

<img width="939" height="124" alt="image" src="https://github.com/user-attachments/assets/4104cb34-2c34-4b5d-8e99-e47483066342" />

Створив публічну і приватну підмережі.

<img width="937" height="170" alt="image" src="https://github.com/user-attachments/assets/4229bbd3-fe4f-4ace-adce-4a90cd7ea5b2" />

Створив Internet gateway.

<img width="938" height="59" alt="image" src="https://github.com/user-attachments/assets/181cdaab-6bbb-480f-bb7b-1b22d3fbcff8" />

І створив два route table. Один для приватної підмережі. Один для публічної. Прив’язав їх до відповідних підмереж і додав для публічного route table створений Internet gateway.

<img width="941" height="86" alt="image" src="https://github.com/user-attachments/assets/c6d63d35-74c0-40a4-a763-7000091ecb99" />

## 7. Create IaC stack holding our network resources.

У IaC generator створив template, додав в нього vpc, subnets, internet gateway і route tables.
Згенерований результат у файлі IaC_generated_vpc_template.yaml.

## 8. Calculate monthly budget for lab 2, assuming there will be only 2 shards.

Для лаб 2 треба нода координатор і 2 шарди зі сховищем.
Я вирішив розрахувати вартість за допомогою AWS pricing calculator.
Я ввів такі потреби.
3 On-Demand EC2 t3.micro з 10 Гб gp3 сховища кожне. І 20 Гб в місяць вихідного трафіку в інтернет.

3 instances x 0.0108 USD On Demand hourly cost x 730 hours in a month = 23.652000 USD
10 GB x 3.00 instance months x 0.0836 USD = 2.51 USD (EBS Storage Cost)
Internet: 20 GB x 0.09 USD per GB = 1.80 USD

Тоді виходить:

Щомісячні витрати: 27.96 USD
Витрати за 12 місяців: 335.52 USD
