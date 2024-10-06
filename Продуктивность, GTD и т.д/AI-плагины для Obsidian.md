# Copilot
Вроде как может индексировать всё хранилище и отвечать на вопросы по нему, как я делал это в Notion.
Ему нужны для этого модели типа ChatGPT. Закинул 5 баксов на OpenRouter для этого.
Ещё нужна штука для создания т.н. embeddings (хз, что это) — text-embedding-3-small. У OpenRouter её нет, но можно подцепить и через VPN у OpenAPI напрямую. И вроде бы там даже есть какие-то скромные бесплатные планы.
# Whisper
Распознавать речь в текст. ChatGPT на сайте это делает очень хорошо. Лучше там всяких гуглов или Тик-Тиков. На OpenRouter нет. Но вроде это вообще опен-сорснутая модель, и её можно развернуть самому. Есть даже Docker образ. Но для удобства можно и через VPN напрямую.

В итоге, пока ни тот, ни другой плагин не пашет. Вот ключи, чтобы продолжить разбираться:
```
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 - openrouter для obsidian copilot gtp4
sk-zFkZXSWSCs_J9BzpcNTVmAuyvgVYNd6QJfPjt7F4paT3BlbkFJbfI2ya_pAmj6AxozekFAovdNNX12TUHBni17WbTegA - openapi website for Obsidian Whisper
sk-YeT0jAgKxUD5cwYGsrU2tiRgIp5bWQpNe6LnuQiFNCT3BlbkFJXQXu0rpJ0yrkKM2GEDP_DmQbANyJrvHG0SBj4uf4MA - openapi website for Obsidian Copilot
```
Из них платный пока только OpenRouter, на остальные бабки не закидывал.
# obsidian-nano-bots
Плагин для Obsidian, позволяет писать запросы и получать ответы к [[LLM и ChatGPT для Obisidian | LLM]] тут же в текст заметки.
[Github](https://github.com/icebaker/obsidian-nano-bots)
# Другие ссылки из чата
- [GitHub - buszk/obsidian-ai-editor](https://github.com/buszk/obsidian-ai-editor)
- [GitHub - InterwebAlchemy/obsidian-ai-research-assistant: Prompt Engineering Research Tool for AI APIs](https://github.com/InterwebAlchemy/obsidian-ai-research-assistant)
- [GitHub - A-F-V/obsidian-arcana: Supercharge your Obsidian note-taking through AI-powered insights and suggestions](https://github.com/A-F-V/obsidian-arcana)
- [GitHub - HyeonseoNam/auto-classifier: Auto classification plugin for Obsidian using ChatGPT.](https://github.com/HyeonseoNam/auto-classifier)
- [GitHub - different-ai/obsidian-ava: Quickly format your notes with ChatGPT in Obsidian](https://github.com/different-ai/obsidian-ava)
- [GitHub - longy2k/obsidian-bmo-chatbot: Generate and brainstorm ideas while creating your notes using Large Language Models (LLMs) with OpenAI&#39;s ChatGPT, Ollama, LM Studio, OpenRouter, and Mistral AI for Obsidian.](https://github.com/longy2k/obsidian-bmo-chatbot)
- [GitHub - lusob/obsidian-brain](https://github.com/lusob/obsidian-brain)
- [GitHub - DeabLabs/cannoli](https://github.com/DeabLabs/cannoli)
- [GitHub - AndreBaltazar8/obsidian-canvas-conversation: A plugin for Obsidian that allows you to create a canvas conversation using ChatGPT.](https://github.com/AndreBaltazar8/obsidian-canvas-conversation)
- [GitHub - Phasip/obsidian-canvas-llm-extender: Let the OpenAI LLM add nodes to your Obsidian canvas](https://github.com/phasip/obsidian-canvas-llm-extender)
- [GitHub - rpggio/obsidian-chat-stream: Obsidian canvas plugin for using AI completion with threads of canvas nodes](https://github.com/rpggio/obsidian-chat-stream)
- [GitHub - julix14/chatGPT-Obsidian](https://github.com/julix14/chatGPT-Obsidian)
- [GitHub - rizerphe/obsidian-companion: Autocomplete your obsidian notes with AI, including ChatGPT, through a copilot-like interface.](https://github.com/rizerphe/obsidian-companion)
- [GitHub - j0rd1smit/obsidian-copilot-auto-completion](https://github.com/j0rd1smit/obsidian-copilot-auto-completion)
- [GitHub - crybot/obsidian-flashcards-llm: Use Large Language Models (such as ChatGPT) to automatically generate flashcards from obsidian notes](https://github.com/crybot/obsidian-flashcards-llm)
- [GitHub - M7mdisk/obsidian-gpt: Ask GPT from your notes and get personalized answers based on your knowledge base.](https://github.com/M7mdisk/obsidian-gpt)
Источник: https://t.me/obsidian_z/97638/103592

30 плагинов нашел на тему

(оказалось, что телеграм не может маркдаун-ссылки конвертить. сорри)

- [AI Editor](https://github.com/buszk/obsidian-ai-editor)
- [AI Research Assistent](https://github.com/InterwebAlchemy/obsidian-ai-research-assistant)
- [Arcana](https://github.com/A-F-V/obsidian-arcana)
- [Auto Classifier](https://github.com/HyeonseoNam/auto-classifier)
- [Ava](https://github.com/different-ai/obsidian-ava)
- [BMO Chatbot](https://github.com/longy2k/obsidian-bmo-chatbot)
- [Brain](https://github.com/lusob/obsidian-brain)
- [Cannoli](https://github.com/DeabLabs/cannoli)
- [Canvas Conversation](https://github.com/AndreBaltazar8/obsidian-canvas-conversation)
- [Canvas LLM Extender](https://github.com/phasip/obsidian-canvas-llm-extender)
- [Chat Stream](https://github.com/rpggio/obsidian-chat-stream)
- [chatGPT Definition](https://github.com/julix14/chatGPT-Obsidian)
- [Companion](https://github.com/rizerphe/obsidian-companion)
- [Copilot Auto Completion](https://github.com/j0rd1smit/obsidian-copilot-auto-completion)
- [Flashcard LLM](https://github.com/crybot/obsidian-flashcards-llm)
- [GPT Assistant](https://github.com/M7mdisk/obsidian-gpt)
- [GPT Notes](https://github.com/micahke/obsidian-gpt3-notes)
- [GPT-LiteInquirer](https://github.com/ittuann/obsidian-gpt-liteinquirer-plugin)
- [intelligence](https://github.com/ransurf/obsidian-intelligence)
- [khoj](https://github.com/khoj-ai/khoj)
- [LLM Extender](https://github.com/phasip/obsidian-canvas-llm-extender)
- [Local GPT](https://github.com/pfrankov/obsidian-local-gpt)
- [Ollama Chat](https://github.com/brumik/obsidian-ollama-chat)
- [Ollama](https://github.com/hinterdupfinger/obsidian-ollama)
- [Ring-A-Secretary](https://github.com/vrtmrz/ring-a-secretary)
- [Text Generator](https://github.com/nhaouari/obsidian-textgenerator-plugin)
- [Title Generation](https://github.com/jaschaephraim/obsidian-title-generator)
- [Vault Chat](https://github.com/exoascension/vault-chat)
- [ZettelGPT](https://github.com/OverRaddit/ZettelGPT)
- [Zettelkasten LLM](https://github.com/glovguy/obsidian-gpt-zettelkasten)
Источник: https://t.me/obsidian_z/97638/101420


