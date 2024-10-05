---
💲: false
---
# Маленькие проекты (но потенциально востребованные, на которых можно поучиться)
# Publishing board with metadata
## Описание на Upwork
Developer needed for RSS Feed for publishing video links and metadata - Upwork
I am a content creator for a high school sports league. I currently  
*receive* raw video from several schools often via Dropbox or Google  
Drive. I download these videos to my hard drive.  
I import the videos into an After Effects project, adding animations, intros, outros, etc, and reformat.
I then send the post-processed videos to the local news station.
In this project I am looking to improve the intake process described  
above. I'd like to create an interface that the schools can use to  
upload their video and set metadata fields (metadata includes video  
name, teams involved, final score, etc) to S3. This interface should be  
similar to a YouTube upload. A big upload button and a few text fields.  
This information - including a link to the S3-stored video - will be  
published to an RSS feed that I can then parse.  
Only approved users can have access to this tool. It should be password  
protected. Each user should have their own RSS feed published. The RSS  
feeds should be public.  
Note - the ingested videos will be short, <5 minutes.
## Реализация
Возможно, эта задача решается вообще через формы (не только Google Forms, что-то понавороченнее). Но там, допустим, нужны типизированные поля (с какой-то валидацией возможно). А загружать можно туда же, на Google Drive.
Допустим, я захочу сделать какое-то общее решение. Тогда поля будут отпределяться отдельно. Должен быть интерфейс для этого. Какие типы, видео, то сё. То есть такая CMS да ещё с конструктором.
А потом ещё авторизация, регистрация, пользователи...
Кстати, наверно для управление пользователями уже есть какие-то либы, заточенные под Spring. [https://killbill.github.io](https://killbill.github.io/)
У того же Airtable есть формы, и там есть attachments, но нельзя валидировать их тип.
Короче, как продукт такая идея не пойдёт. Airtable - для чего-то общего. Для чего-то особенного (с валидацией типа файла и т.д.) — кастомные решения.