# Start prompt — your working rules with AI in about 15 minutes

Copy everything inside the block below and paste it as the **first message of a new chat**. It works in ChatGPT on any plan with no files, no terminal and no Git. The same prompt works in Claude, in Codex and in Claude Code. Write your answers in your own language; the assistant follows it. The prompt's fixed phrases stay in the language of the block you paste: in ChatGPT the English block gave Russian rules that still said "For approval:" (2026-11-11). If the block exists in your language, paste that one.

What happens: three questions → a draft of 5–7 rules → you refine and accept → you try your task and make one correction → you get a Markdown document to keep and a short form to paste into the assistant's settings. How to save and reconnect in each environment: [environments.md](../environments.md).

The prompt is self-contained. It does not ask the assistant to open this repository, because a link does not make a chat read anything.

## The prompt (English)

```text
You are helping me write my working rules for AI: a short set of rules for how I want to work with you. Reply in the language I write in. This should take about 15 minutes. Go step by step and wait for my answer after each question.

STEP 1 — Three questions, one at a time. I may skip any of them.
1. What is one concrete task I want to do with you in the next week or two?
2. What role do I expect from you on that task: sparring partner, executor, coach, editor, something else?
3. How do I prefer to work: short or detailed answers; direct pushback or careful; what annoys me in AI answers?
Do not run a personality interview. Do not ask about my values, my history or my psychology. Three questions, then move on.

STEP 2 — Draft 5–7 rules. Each rule describes one observable behaviour of yours, not a trait of mine. Use my own words where you can. Cover these topics:
- Your role: who you are to me on this task.
- Disagreement: how you object (for example, one strong objection beats five weak ones).
- Facts and uncertainty: never invent facts, numbers, quotes or sources; say "I don't know" or "unverified".
- My state: I may add tags such as [energy 2/5] or [in a hurry]; say what you change when you see them.
- Form of answers: for example, end every analysis with "For approval:" and one decision, not a retelling.
- Corrections: when I correct you, reply with one line that starts with "rule:" which I can paste into my rules file.
Show the draft as a numbered list. Mark anything you assumed with "(assumed, confirm?)". Treat my answers as preferences for this work, not as facts about my personality.

STEP 3 — I refine. Turn every principle into concrete behaviour: "I value directness" becomes "when you see a significant objection, state it before the answer". Then ask me to accept the final text. Do not continue until I say the rules are accepted.

STEP 4 — Apply. Take the task from step 1 and do its first useful piece under the accepted rules. I will make one correction. Answer the correction with one "rule:" line.

STEP 5 — Save. Give me two things.
(a) The rules as one Markdown document: a title, a line "v1 · <today's date>", a three-line context (task, role, how I work), the numbered rules, and a section "Corrections log" with today's correction. This is the source. I keep it as a file.
(b) A short form of the same rules for the custom-instructions field of this assistant: plain text, under 1,500 characters, ending with "(rules v1)". The short form is derived from the source. When the source changes, I will ask you to regenerate it.
Then tell me in two sentences how to use the rules in the next chat: custom instructions (all my chats), the instructions of one project (that project only), or pasting the document at the start of a chat.

LIMITS. These rules do not override the platform's own rules, give you no access to any data, and do not replace my judgement. If I mention a file or a link you cannot open, say exactly what you could not read and do not guess its content.
```

## Тот же запрос по-русски

Перевод английского запроса выше. Источник — английский текст; при его правке обновите и этот блок. Маркеры `rule:` и `(rules v1)` оставлены латиницей: их ждут шаблоны в [templates/](../templates/) и запросы из [continue.md](continue.md).

```text
Ты помогаешь мне написать мои правила работы с AI: короткий набор правил о том, как я хочу с тобой работать. Отвечай на языке, на котором пишу я. Это займёт около 15 минут. Иди по шагам и жди моего ответа после каждого вопроса.

ШАГ 1 — Три вопроса, по одному. Любой из них я могу пропустить.
1. Какую одну конкретную задачу я хочу сделать с тобой в ближайшие неделю-две?
2. Какую роль я жду от тебя в этой задаче: спарринг-партнёр, исполнитель, коуч, редактор, что-то другое?
3. Как мне удобно работать: коротко или подробно; прямые возражения или осторожные; что меня раздражает в ответах AI?
Не проводи интервью о личности. Не спрашивай о моих ценностях, истории и психологии. Три вопроса — и дальше.

ШАГ 2 — Черновик из 5–7 правил. Каждое правило описывает одно наблюдаемое поведение — твоё, а не мою черту. Где можно, используй мои слова. Темы:
- Твоя роль: кто ты мне в этой задаче.
- Как возражать: например, одно сильное возражение лучше пяти слабых.
- Факты и неопределённость: не выдумывать факты, цифры, цитаты и источники; говорить «не знаю» или «не проверено».
- Моё состояние: я могу ставить метки вроде [энергия 2/5] или [спешу]; скажи, что ты меняешь, когда их видишь.
- Форма ответов: например, каждый разбор заканчивать строкой «На утверждение:» и одним решением, а не пересказом.
- Поправки: когда я тебя поправляю, отвечай одной строкой, начинающейся с «rule:» (латиницей), которую я вставлю в свой файл правил.
Покажи черновик нумерованным списком. Всё, что ты предположил, помечай «(предположение, подтвердить?)». Мои ответы — предпочтения для этой работы, а не факты о моей личности.

ШАГ 3 — Я уточняю. Переведи каждый принцип в конкретное поведение: «ценю прямоту» становится «если видишь существенное возражение, назови его до ответа». Затем попроси меня принять итоговый текст. Не продолжай, пока я не скажу, что правила приняты.

ШАГ 4 — Применение. Возьми задачу из шага 1 и сделай её первый полезный кусок по принятым правилам. Я внесу одну поправку. Ответь на поправку одной строкой «rule: …».

ШАГ 5 — Сохранение. Дай мне две вещи.
(а) Правила одним Markdown-документом: заголовок, строка «v1 · <сегодняшняя дата>», три строки контекста (задача, роль, как я работаю), нумерованные правила и раздел «Журнал поправок» с сегодняшней поправкой. Это источник. Я сохраню его как файл.
(б) Короткую форму тех же правил для поля custom instructions этого ассистента: обычный текст, меньше 1500 знаков, в конце «(rules v1)» (латиницей). Короткая форма производная от источника. Когда источник изменится, я попрошу тебя сгенерировать её заново.
Потом в двух предложениях скажи, как использовать правила в следующем чате: custom instructions (все мои чаты), инструкции одного проекта (только этот проект) или вставка документа в начало чата.

ОГРАНИЧЕНИЯ. Эти правила не отменяют правил самой платформы, не дают тебе доступа ни к каким данным и не заменяют моего суждения. Если я упомяну файл или ссылку, которую ты не можешь открыть, скажи точно, что именно ты не смог прочитать, и не угадывай содержание.
```

## After the chat

1. Save the Markdown document as a file you keep. A copy of the layout is in [templates/working-rules.md](../templates/working-rules.md).
2. Put the short form where your environment reads it: [environments.md](../environments.md). The version line in both places tells you whether they still match.
3. Next chat: the short form is already there, or you paste the document. The continuation prompt is in [prompts/continue.md](continue.md).
