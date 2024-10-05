Preparation Map

Behavioral Interview

Generic Tricky Questions

Questions for the interviewer

Know Your Technical Projects

MultiQ

Tell me about yourself pitch - TODO

The Big O

Time complexity

Space complexity

Drop the Non-Dominant Terms

Multi-part algorithms add vs multiply

Recursive runtimes

# Preparation Map

![[Notion 2/Attachments/Untitled 20.png|Untitled 20.png]]

![[Notion 2/Attachments/Untitled 1 10.png|Untitled 1 10.png]]

# Behavioral Interview

## Generic Tricky Questions

- What is your favorite programming language and why?
- How do you stay up to date with the latest developments in software development?

|**Common Questions**|**MultiQ**|**Quantumfolio**?|**ИДЦ**|
|---|---|---|---|
|Challenges|bad code, do everything|||
|Mistakes/Failures|got a burnout||Updated Java Mail. Something stopped working. I spend two days reading through RFC and figuring out what was broken. Then I just bumped the version to the latest and the error was gone.|
|Enjoyed|big desktop app after IDC||respected, hi-end, good for people, visited as a child, learned a lot|
|Leadership||||
|Conflicts||fixed price milestones, estimation||
|What You’d Do Differently|go for full-fledged framework, insist on a massive refactoring|TornadoFX was already out. Should have given it a goal|Use Docker for integrational tests to restore DB  <br>  <br>Use Gradle caching to reduce build time|

I should be able to talk about my projects in detail. Придётся где-то и соврать.

My three weaknesses (Jannis suggested):

- I am afraid of changes in a meaning that I am very persistent, but it’s not always a good thing. Sometimes it can lead to stress and burnout.
- 🟥 Reg flag: I am usually pessimistic about opportunities, new things. It keeps me safe, but too safe. I miss a lot of adventures. I don’t feel comfortable acting without a plan. Or, if we put it differently. **I avoid risk and prefer to plan ahead.**
- That’s it. Other things are minor

## Questions for the interviewer

Genuine Questions:

1. What is the ratio of testers to developers to managers? What is the interaction like? How does project planning happen on the team?
2. What brought you to this company? What has been most challenging for you? How long have you been with the company?
3. How many people work fully-remotely?
4. How does one get a salary raise?

  

Insightful Questions:

1. "I noticed that you use technology X. How do you handle problem Y?"
2. "Why did the product choose to use the X protocol over the Y protocol? I know it has benefits like A, B, C, but many companies choose not to use it because of issue D”

Asking such questions will typically require advance research about the company.

Passion Questions:

1. 'Tm very interested in scalability, and I'd love to learn more about it. What opportunities are there at this company to learn about this?"
2. "I'm not familiar with technology X, but it sounds like a very interesting solution. Could you tell me a bit more about how it works?"

## Know Your Technical Projects

Нужно составить список вопросов по проектам. Для HR не вдаваться слишком в технические детали.

Структурированные ответы: Nugget First or S. A. R. (Situation Action, Response).

В книге говорится “Consider putting your stories in a grid”. Ну а какие вопросы-то ожидать? (страница 35).

Качества, которые показать: Leadership/Initiative, Epathy, Compassion, Humility, TeamWork, Helpfulness.

### MultiQ

1. Что это такое?
2. На что похоже приложение? Какие ближайшие конкуренты?
3. Как деплоился проект?
4. Кого нанимал? Чем руководствовался?
5. Для чего нанимал?
6. Сколько клиентов?
7. Какая кастомизация? Всё-таки большая кастомизация нужна, в этом и фишка. Вернее, доработка. Значит, количество персонала должно увеличиваться. Значит, я типа руководил людьми. А как планировал? Очень много лжи.

## Tell me about yourself pitch - TODO

Возможно, надо больше фокуса на Business values.

1. **Current role.** I am a software engineer at Quality Works, where I have been leading the development of a JavaFX desktop application from a very early prototype to a working application creating revenue.
2. **Education.** I have a background in computer science. For the past 7 years I have worked on a numerous projects
3. **Post College and Onwards**. I started me career as a Web developer while still studying computer science in a University. I worked in an enterprise environment in a Hi-End Medical Facility developing both the back-end and the front end of a Medical Information System. This is where I got a good grasp of JavaEE and passion for the JavaFX platform that I used afterwards to pursue a more flexible lifestyle of a contractor.
4. **Current Role [Details]:** At my current position I basically took part in everything that made the app transform from a buggy in-house utility to a product. I implemented the UI, according to provided mock-ups, rebuilt the application framework, hired other contractor when needed and performed code reviews. At the moment I am working on the application along with other developers (2).
5. **Outside of work**. Outside of work, I do film photography and enjoy contemporary documentary films.
6. **Wrap up.** Now I have seven years of experience and I am looking for a Web Developer position. I am also considering transitional positions that would let me shift from Desktop Development to working on Web full-time.

# The Big O

## Time complexity

- Big O - upper bound on time
- Big Omega - lower bound on time. Can’t be faster than that
- Big Theta - **both** big O and big Omega. Tight bound on time.

Depends on scenario:

- Best case
- Worst case
- Expected case

## Space complexity

- Memory space
- Stack space (local variables, operand stack, and frame data). New frame is created every call. But it is very implementation dependent

  

Drop the constants. O(N) = O(2N). Two loops example: 1 loop, 2 statements; 2 loops 1 statement each. Don’t go down to the assembly level.

## Drop the Non-Dominant Terms

But **WHY?**

![[Notion 2/Attachments/Untitled 2 6.png|Untitled 2 6.png]]

## Multi-part algorithms add vs multiply

![[Notion 2/Attachments/Untitled 3 5.png|Untitled 3 5.png]]

## Recursive runtimes

When we a recursive function that makes multiple calls, the runtime will often (but not always) look like $O(branches^{depth})$﻿.

The base of the log does not matter for branches since logs of different bases are only different by a constant factor.