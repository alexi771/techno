---
тема: Виталик Бутерин представил EIP-8288 — рекурсивные STARK-мемпулы, которые должны на порядки удешевить квантово-устойчивые подписи и приватные транзакции в Ethereum
источник: https://x.com/VitalikButerin/status/2097711433073172837, https://eips.ethereum.org/EIPS/eip-8288
дата: 2026-09-09
---

# Расследование: EIP-8288 (рекурсивные STARK-мемпулы) Виталика Бутерина

## Установленные факты (подтверждены несколькими независимыми источниками)

- **Что.** 9 сентября 2026 Виталик Бутерин опубликовал в X пост (тред, озаглавленный источниками как "A note on recursive STARK mempools"), представляющий EIP-8288 — предложение по изменению формата транзакций Ethereum. Дословная цитата из поста (по данным нескольких изданий): "This is an EIP that I am hoping we can get included in I-star (the fork after Hegotá), that you can think of as the next step after Frames, that would unlock extreme amounts of power."
- **Механика.** Вместо того чтобы каждая транзакция несла собственное дорогое криптографическое доказательство, транзакции декларируют свои квантово-устойчивые подписи и STARK-доказательства как "зависимости" (dependency frames). Узлы мемпула и билдеры блоков агрегируют пакеты таких транзакций и генерируют один рекурсивный STARK, который подтверждает валидность всех зависимостей офчейн — в блок попадает уже одно консолидированное доказательство, а не множество отдельных.
- **Экономика.** По собственной оценке Бутерина (растиражированной прессой): приватные квантово-устойчивые транзакции, которые сейчас стоят порядка 10 млн газа, при этой схеме могут упасть до низких десятков тысяч газа. Это также должно снизить стоимость подписей типа SPHINCS+ и открыть дорогу новым схемам (Falcon, ML-DSA) без изменений в самом EVM.
- **Место в дорожной карте.** EIP-8288 прямо строится поверх EIP-8141 ("frame transactions", тоже с соавторством Бутерина) — тот вводит новый тип транзакции, разбитый на до 64 программируемых "фреймов", разделяет "действия" и "зависимости" (подписи, доказательства), включён в план хардфорка Hegotá (ожидается в 2027 году). EIP-8288 нацелен на следующий за Hegotá хардфорк, который Бутерин сам называет рабочим именем "I-star" — важно: это неофициальное название, финального имени форка на момент расследования в источниках нет.
- **Совпадение по времени с более широкой дорожной картой Ethereum Foundation.** За один-два дня до поста, 7–8 сентября 2026, Ethereum Foundation объявила дедлайн декабря 2029 года на достижение квантовой устойчивости на уровне исполнения, консенсуса и данных сети, назвав его "не подлежащим пересмотру" минимум до контрольной точки в январе 2027. По данным The Block, кластер Protocol собрал около 60 исследователей и инженеров из девяти команд клиентов для выработки этой дорожной карты. EIP-8288 — конкретный технический инструмент именно под эту публично зафиксированную цель.
- **Технические возражения (форумные обсуждения, июнь 2026).** По найденным источникам, два ключевых вопроса community-обсуждения вокруг предложения — "recursion soundness" (сохраняют ли вложенные друг в друга STARK-доказательства свои криптографические гарантии при рекурсивной агрегации) и "omission accountability" (что происходит, если узел мемпула/билдер пропускает или не включает чей-то dependency frame). Источники называют оба вопроса, но не раскрывают деталей и итогов дискуссии подробно — это не проверено дальше форумного упоминания.
- **Timeline предложения расходится по источникам.** По данным CryptoTimes, первая версия предложения была подана 5 июня 2026 года; публичный резонанс и присвоение номера EIP-8288 пришлись на 9 сентября 2026. Это расхождение не разрешено окончательно — в сценарии стоит говорить не "Бутерин впервые предложил", а "Бутерин публично представил/актуализировал".

## Кто ещё связан — расширенный круг

- **Eli Ben-Sasson / StarkWare.** Со-основатель StarkWare (компании, коммерциализировавшей STARK-доказательства) — публично реагировал на более широкую дорожную карту Ethereum ("Extremely Lean Ethereum"), в которую рекурсивные STARK входят как центральный элемент, ещё в конце июня — начале июля 2026, до конкретно EIP-8288. Цитата (X, @EliBenSasson): "My take on the new roadmap for Ethereum: TL;DR — many good things, a few unclear things, still a few problems. The good: Recursive STARKs — excellent. Huge progress since the days where most of the Ethereum ecosystem was skeptical about the immense value of STARKs." При этом прямо раскритиковал сроки: "'3-4 years' as the timeline is way too long", особенно применительно к готовности к квантовой угрозе.
- **StarkWare/Starknet как отдельный, уже более быстрый трек.** 30 июня 2026 StarkWare представила собственную трёхфазную дорожную карту перехода Starknet на пост-квантовую криптографию, назвав её "самой сильной в крипте на сегодня" — аргумент в том, что архитектура STARK-доказательств Starknet изначально устойчива к квантовым атакам ("architecture advantage"), поэтому нужно лишь убрать оставшиеся зависимости от эллиптических кривых. То есть L2 (Starknet), построенный на той же технологии (STARK), которую сейчас формализует EIP-8288, публично объявил о движении к квантовой безопасности раньше и, по собственной оценке автора технологии, быстрее, чем L1 Ethereum.
- **Ethereum Foundation / core-разработчики клиентов.** Ключевой невидимый в этом конкретном посте, но структурно необходимый круг — ~60 исследователей и инженеров из 9 команд клиентов, готовивших саму дорожную карту квантовой устойчивости; EIP должен пройти их согласование и процесс консенсуса, а не решается единолично Бутериным.
- **Michael Saylor / Strategy Inc (Bitcoin).** Публично занимает прямо противоположную по тону позицию по квантовой угрозе для Bitcoin: риск "больше чем в 10 годах" от реализации, ожидает "скоординированное глобальное обновление" ПО, если/когда угроза станет реальной — то есть подход "успеем среагировать", а не "готовиться заранее". По имеющемуся профилю в базе (`people/michael-saylor.md`): Сэйлор — заинтересованная сторона, а не нейтральный комментатор (Strategy Inc держит крупную позицию в BTC с кредитным плечом), и это стоит держать в уме при цитировании его спокойствия по квантовому риску.
- **Сам Бутерин — отдельно и раньше.** По найденным источникам, независимо от EIP-8288 Бутерин публично предупреждал, что эллиптическая криптография (ECC), на которой держатся и Bitcoin, и Ethereum, может "сломаться" ещё до президентских выборов США 2028 года, и призывал к переходу на квантово-устойчивые схемы в течение ближайших четырёх лет — то есть тон значительно тревожнее, чем у Сэйлора, при том что речь идёт об одной и той же базовой угрозе для обеих сетей.

## Known-person check

- **Виталик Бутерин** — профиль есть (`knowledge/people/vitalik-buterin.md`). Ключевой паттерн для сверки: "не CEO и не имеет формальной коммерческой роли — новости, приписывающие Бутерину единоличные 'решения' сети, обычно упрощение: реальные изменения проходят через процесс EIP и консенсус разработчиков". Прямо применимо здесь: заголовки прессы формулируют это как "Бутерин представил/продвигает" — корректно, но важно не подавать в сценарии так, будто EIP-8288 уже принятое решение сети, а не предложение, которому ещё предстоит пройти согласование ~60 исследователей и 9 команд клиентов.
- **Michael Saylor** — профиль есть (`knowledge/people/michael-saylor.md`), см. выше — использован как источник контраргумента/контраста, не как нейтральная фигура.
- **Eli Ben-Sasson** — профиля в `knowledge/people/` нет, в базе фигура новая. Кандидат на будущее добавление, если тема STARK/квантовой устойчивости будет всплывать снова (уже минимум два эпизода: июньская дорожная карта Ethereum и это событие).

## Нырок в базу знаний — транскрипты

- В `knowledge/transcripts/` нашёлся релевантный материал: `vitalik-buterin_bankless-world-ledger_2025_rNSnYIjoqOM.txt` (интервью Bankless, 2025, к 10-летию Ethereum). Бутерин там прямо говорит про необходимость нативной поддержки квантово-устойчивых кошельков/мультисигов и приватных протоколов через account abstraction (упоминает EIP-7701), чтобы они не зависели от "промежуточных экосистем" — и отдельно описывает "endgame"-видение: ZK-snark'ать всё, заменить SNARK'и на STARK'и, сделать верификацию узлов сверхлёгкой, приватность — дефолтом начиная с платежей. EIP-8288 — конкретный инженерный шаг именно в сторону этого видения, сформулированного за год с лишним до самого EIP. Это более богатый источник для входа в тему, чем свежие новостные заметки: там виден не только "что", но и "зачем" с точки зрения самого Бутерина, сформулированное задолго до конкретного предложения.
- В `knowledge/tech-world-map.md` тема Ethereum/квантовой устойчивости/STARK ранее не размещалась — это первое размещение, не переподтверждение старого.

## Что подтверждено / что осталось непроверенным

- Подтверждено несколькими независимыми изданиями (PANews, CryptoBriefing, CoinTurk, TronWeekly, CryptoTimes и др.): факт поста Бутерина 9 сентября 2026, содержание идеи (dependency frames, агрегация в мемпуле, рекурсивный STARK), связь с EIP-8141 и Hegotá, порядок экономии газа (~10 млн → десятки тысяч).
- Не удалось получить и процитировать первоисточники напрямую (сетевой доступ к x.com и eips.ethereum.org заблокирован политикой прокси в этой сессии) — все факты и цитаты в этом расследовании получены через WebSearch-агрегацию по независимым пересказам, а не прямым чтением твита/EIP. Перед публикацией сценария стоит, если будет возможность, свериться с оригиналом EIP на eips.ethereum.org напрямую.
- "I-star" как название форка — рабочее, неофициальное; в сценарии не подавать как утверждённое имя апгрейда.
- Детали community-возражений ("recursion soundness", "omission accountability") — названы, но не раскрыты подробно ни в одном найденном источнике; при написании сценария не домысливать содержание дискуссии сверх того, что здесь зафиксировано.
- Прямая реакция Ben-Sasson именно на EIP-8288 (в отличие от более широкой дорожной карты в июне-июле) в источниках не найдена — используется его более ранняя реакция на смежную тему как контекст, не как комментарий к этому конкретному событию.
- Кто именно выступит соавтором/ревьюером EIP-8288 на стороне Ethereum Foundation — не найдено.

## Witt-review

WITT-REVIEW (источник: пост Бутерина в X от 9.09.2026 про EIP-8288 + интервью Bankless World Ledger, 2025, rNSnYIjoqOM)

1. Непокрытый угол: частично есть. Пресса массово пересказывает EIP-8288 как "Бутерин снижает газ для квантовых подписей" — почти никто не берёт ракурс "StarkWare (автор коммерческого STARK-стека) публично поторапливает Ethereum L1, пока их же L2 Starknet уже впереди по собственной квантовой дорожной карте" — это конкретное, малоосвещённое напряжение между L1 и L2 на одной и той же технологии.

2. Живой персонаж: источник не даёт в самом посте про EIP-8288 (сухое техническое объявление). В интервью Bankless (2025) персонаж есть частично: Бутерин формулирует личную тревогу за судьбу приватности и quantum-resistance, если Ethereum не даст им "нативной" поддержки — "intermediary ecosystems... work until they don't work for you" — не эмоциональный всплеск, но видна личная забота, не просто техническая позиция.

3. Счёт: сильно есть, с масштабом. ~10 млн газа → низкие десятки тысяч газа для приватных квантово-устойчивых транзакций — конкретное отношение (снижение на два-три порядка), явно поясняющее масштаб экономии, а не просто "дешевле".

4. Неудобный вывод: источник (сам пост) не даёт — это позиция человека, продвигающего собственное предложение, без признания рисков. Но контекст (реакция Ben-Sasson на более широкую дорожную карту) даёт: сама Ethereum Foundation ставит 3-4-летний горизонт, который со-изобретатель ключевой для этого плана технологии публично называет "way too long" для готовности к квантовой угрозе — то есть внутри "STARK-лагеря" нет согласия по срочности, хотя по существу технологии согласие есть.

5. Сцена вместо заявления: источник не даёт — ни X-пост, ни интервью не содержат разворачиваемого эпизода с местом и диалогом, только формулировки позиций и технических тезисов.

6. Предыстория: сильно есть, именно через интервью 2025 года. Там Бутерин ещё за год с лишним до EIP-8288 описывает то же самое видение (STARK вместо SNARK, приватность по умолчанию, лёгкая верификация) как часть долгосрочного "endgame" — EIP-8288 не берётся из ниоткуда, это прямое продолжение публично заявленной многолетней архитектурной цели, а не реакция на новостной повод.

7. Честная неопределённость: частично есть, но не в самом посте, а в окружающем материале — форумные возражения про "recursion soundness" и "omission accountability" прямо называют нерешённые вопросы (хотя источники не раскрывают их содержание подробно); сам пост Бутерина подан уверенно, без признания открытых вопросов.

Итог: сильнее всего — предыстория (интервью 2025 года показывает, что EIP-8288 — не спонтанная идея, а давно артикулированная архитектурная цель) в связке с непокрытым углом про напряжение StarkWare/L2 vs Ethereum L1 по срокам — это более интересный вход в тему, чем прямой пересказ технической механики предложения.

## Positioning

POSITIONING (источник: EIP-8288, X-пост Бутерина 9.09.2026, дорожная карта Ethereum Foundation 7-8.09.2026, реакция Ben-Sasson/StarkWare)

Проходит фильтр частично. Достраивает карту: конкретная, редко проговариваемая связь — StarkWare, компания, чья коммерческая технология (STARK) легла в основу и EIP-8288, и собственной L2-дорожной карты Starknet, публично торопит Ethereum L1 двигаться быстрее по той же самой технологии, где сама уже впереди; плюс контраст срочности между Ethereum (Бутерин: ECC может не выдержать до выборов 2028, переход нужен за 4 года) и Bitcoin (Сэйлор: угроза дальше 10 лет, успеем скоординированно обновиться) — два крупнейших блокчейна расходятся не в технологии, а в ощущении срочности одной и той же угрозы.

Непокрытый угол: напряжение L1/L2 по срокам внутри одного технологического лагеря (StarkWare торопит Ethereum) — это самая нестандартная находка ресёрча, почти не встречается в пересказах новости.

Переживёт год: частично да. Сама механика EIP (dependency frames, рекурсивная агрегация) и дорожная карта до 2029 года — не разовая новость, тема с горизонтом в несколько лет. Но конкретный EIP-номер и его судьба (примут/не примут в "I-star") могут устареть быстрее — тема требует update-пометки, если EIP не пройдёт согласование к моменту публикации.

Несущий слой — инженерная оптика: без разбора, что такое рекурсивный STARK, dependency frame и чем это отличается от текущей схемы (каждая транзакция несёт свой прувинг), тема разваливается в пересказ пресс-релиза; здесь нужно реально объяснить механику, а не процитировать цифру "10 млн → десятки тысяч" как магию.

Предупреждение: не подавать это как "Бутерин единолично решил изменить Ethereum" — это предложение, которое должно пройти согласование ~60 исследователей и 9 команд клиентов (см. known-person check). Не пересказывать технические детали как решённое и принятое (EIP ещё не хардфорк). Не растягивать тему в общий разбор "quantum threat to crypto" ради драмы — источники по существу вопроса скупы (форумные возражения не раскрыты), раздувать неопределённость в сенсацию нельзя. Если брать тему — держать вход именно через StarkWare/Ethereum L1 напряжение и через контраст с Bitcoin/Сэйлором, а не через пересказ механики EIP как самоцель.

## Первоисточник (проверено лично, оригинал на английском)

Облачная сессия routine не смогла достучаться напрямую до eips.ethereum.org и x.com (сетевая политика прокси блокировала оба домена) и работала только через агрегацию прессы. Проверила лично: eips.ethereum.org открылся, x.com по-прежнему отдаёт 402 Payment Required (то же самое через fxtwitter.com — редиректит на x.com; nitter.net временно не работает из-за cease-and-desist от X Corp, полученного 24.08.2026). Цитату твита перепроверила через независимый WebSearch — совпадает дословно с тем, что нашла routine.

**EIP-8288 — заголовок и техническое содержание (eips.ethereum.org/EIPS/eip-8288, оригинал на английском):**

> # EIP-8288: Frame Type for PQ Sig and STARK Aggregation

Ключевые технические детали, отсутствовавшие в пересказах прессы (важно для точности сценария, если он будет углубляться в механику):

- Вводит новый режим фрейма `DEP_VERIFY_FRAME_MODE` для транзакций типа EIP-8141, позволяющий агрегировать пост-квантовые подписи и STARK-доказательства через рекурсивный STARK.
- **Dependency Verification Frame**: транзакции декларируют тройки `(scheme, data_hash, verification_key_hash)` как зависимости; дословно из спецификации — они "are not executed as EVM code; instead, they are recorded as dependencies that must be proven valid by the recursive STARK in the block."
- **Поддерживаемые схемы**: `LEANSPHINCS_SCHEME` (0x10, хэш-based пост-квантовые подписи) и `LEANSTARK_SCHEME` (0x11, STARK-доказательства).
- **Точные фиксированные газовые издержки верификации** (это точнее, чем округлённая пресс-цифра "10 млн → десятки тысяч" — тот диапазон про полную транзакцию с несколькими доказательствами, а это цена одной проверки): leanSPHINCS — 3000 газа за подпись; leanSTARK — 30 000 газа за доказательство.
- Каждый блок обязан содержать поле `recursive_stark` в заголовке, агрегирующее все зависимости по всем транзакциям блока; доказательство генерируется через Lean Ethereum tooling.
- **Мемпул-агрегация**: wrapper-объекты транслируются каждые 1000 мс, два режима — Mode 0 (прямые зависимости с индивидуальными доказательствами) и Mode 1 (рекурсивный STARK, покрывающий все зависимости) — прогрессивная агрегация от пользователя через узлы мемпула к билдерам, снижает нагрузку на пропускную способность.
- **Совместимость с FOCIL** (fork-choice enforced inclusion lists) — списки включения могут нести поля `recursive_stark`, то есть предагрегированные доказательства зависимостей можно переносить прямо внутри inclusion list.
- **DoS-защита**: максимум 16 leanSPHINCS-зависимостей на транзакцию, максимум 1 leanSTARK-зависимость на транзакцию, максимум 256 зависимостей на фрейм, лимиты на уровне мемпула. Дословно: "limits ensure that the data stored in the dependency frames is bounded by the same order of magnitude as the data that would be stored in a traditional transaction."

**Твит Бутерина (X, 9.09.2026, @VitalikButerin, проверено через независимый WebSearch — прямой доступ к x.com недоступен из-за 402):**

> "A note on recursive STARK mempools (EIP-8288)... This is an EIP that I am hoping we can get included in I-star (the fork after Hegotá) that you can think of as the next step after Frames, that would unlock extreme amounts of power."

Совпадает дословно с цитатой, которую routine получила через пресс-агрегацию — независимое подтверждение точности.

## Источники

- [PANews — Vitalik Introduces EIP-8288: Recursive STARK Mempool Expected to Reduce Costs for Quantum-Safe Signatures and Privacy Transactions](https://panews.io/articles/01a086dd-7a07-7517-9406-6b8e4f4041fc)
- [CryptoBriefing — EIP-8288 introduces frame type for post-quantum signatures and STARK aggregation](https://cryptobriefing.com/eip-8288-recursive-stark-mempools-ethereum/)
- [Coin-Turk — Vitalik Buterin pushes EIP-8288 to cut Ethereum post-quantum costs, targets 2029](https://en.coin-turk.com/vitalik-buterin-pushes-eip-8288-to-cut-ethereum-post-quantum-costs-targets-2029/)
- [Bitcoinsistemi — Vitalik Buterin Announced the Big News About the New Ethereum Update](https://en.bitcoinsistemi.com/vitalik-buterin-announced-the-big-news-about-the-new-ethereum-update/)
- [Coinfomania — Ethereum's Future Enhanced with Proposed EIP-8288](https://coinfomania.com/ethereums-future-enhanced-with-proposed-eip-8288/)
- [TronWeekly — EIP-8288 Drives Ethereum Momentum As Vitalik Backs Upgrade](https://www.tronweekly.com/vitalik-buterin-eip-8288-ethereum-i-star/)
- [BitcoinEthereumNews — Vitalik Buterin Proposes Recursive STARKs for Ethereum's I-Star Upgrade](https://bitcoinethereumnews.com/ethereum/vitalik-buterin-proposes-recursive-starks-for-ethereums/)
- [CryptoTimes — Vitalik Buterin Proposes Recursive STARK Mempools for Ethereum](https://www.cryptotimes.io/2026/09/09/vitalik-buterin-proposes-recursive-stark-mempools-for-ethereum/)
- [CoinEdition — Vitalik Buterin Proposes Recursive STARKs for Ethereum's I-Star Upgrade](https://coinedition.com/vitalik-buterin-proposes-recursive-starks-for-ethereums/)
- [36Crypto — Vitalik Buterin Proposes Major Shift in Ethereum Transaction Design](https://36crypto.com/vitalik-buterin-proposes-major-shift-in-ethereum-transaction-design/)
- [The Block — Ethereum aims for quantum-safe L1 by 2029 as Hegotá upgrade takes form](https://www.theblock.co/news/ecosystems/2026-09-08-ethereum-foundation-quantum-resistance-2029-413716)
- [BeInCrypto — Ethereum Foundation Sets a December 2029 Deadline to Beat the Quantum Clock](https://beincrypto.com/ethereum-foundation-quantum-resistance-2029-deadline/)
- [ethereum.org — A more secure Ethereum (future-proofing roadmap)](https://ethereum.org/roadmap/future-proofing/)
- [Coin-Turk — Vitalik Buterin outlines EIP-8141 plan to enable Ethereum hyper-scaling by 2027](https://en.coin-turk.com/vitalik-buterin-outlines-eip-8141-plan-to-enable-ethereum-hyper-scaling-by-2027/)
- [CryptoBriefing — Ethereum advances scaling with EIP-8141, a new transaction type that splits one tx into up to 64 frames](https://cryptobriefing.com/ethereum-eip-8141-frame-transaction-scaling/)
- [CoinOTAG — Ethereum Developers Lock EIP-8141 Frame Transactions Into 2027 Hegotá Upgrade](https://en.coinotag.com/ethereum-eip-8141-frame-transactions-hegota-2027)
- [The Quantum Insider — StarkWare Unveils Quantum-Safe Roadmap for Starknet](https://thequantuminsider.com/2026/06/30/starkware-releases-roadmap-to-make-starknet-quantum-safe/)
- [The Block — StarkWare unveils Starknet post-quantum roadmap, calling it crypto's "strongest" to date](https://www.theblock.co/news/ecosystems/2026-06-30-starkware-unveils-starknet-post-quantum-roadmap-calling-it-cryptos-strongest-to-date-406677)
- [CoinDesk — Ethereum developers embrace Vitalik Buterin's long-term vision but urge quicker execution](https://www.coindesk.com/tech/2026/07/06/ethereum-developers-embrace-vitalik-buterin-s-long-term-vision-but-urge-quicker-execution)
- [Eli Ben-Sasson on X — reaction to Ethereum's new roadmap ("3-4 years... way too long")](https://x.com/EliBenSasson/status/2073763363419558042)
- [Eli Ben-Sasson on X — explainer thread on recursive STARKs](https://x.com/EliBenSasson/status/2085735701052576251)
- [TradingView/Cointelegraph — Michael Saylor says quantum threat to Bitcoin is more than 10 years away](https://www.tradingview.com/news/cointelegraph:b2ffb5c65094b:0-michael-saylor-says-quantum-threat-to-bitcoin-is-more-than-10-years-away/)
- [CCN — Michael Saylor: Quantum Computing Won't Break Bitcoin This Decade — Upgrade Would Come First](https://www.ccn.com/news/crypto/saylor-quantum-computing-wont-break-bitcoin-this-decade-upgrade-first/)
- [knowledge/transcripts/vitalik-buterin_bankless-world-ledger_2025_rNSnYIjoqOM.txt — интервью Bankless, 10-летие Ethereum, 2025]
