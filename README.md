# zakupki-tenders — скилл для OpenCode

Поиск актуальных тендеров на [zakupki.gov.ru](https://zakupki.gov.ru/) (ЕИС) через браузер: фильтры по региону и ОКПД2, сбор карточек извещений, обход анти-бота, классификация закупок и единый формат вывода.

## Что внутри

`SKILL.md` — инструкция для агента:

- рабочий URL расширенного поиска и параметры (`customerPlace`, `orderIKZInputNameOkpd2`, `applSubmissionCloseDateFrom`);
- готовые JS-сниппеты для `browse.eval` — сбор списка и разбор карточки;
- правила паузы и поведения при анти-боте;
- классификация: строительные работы vs квартиры в долевое строительство vs обслуживание;
- формат ответа по каждому тендеру.

## Установка

Глобально (все проекты):

```bash
mkdir -p ~/.opencode/skill/zakupki-tenders
cp SKILL.md ~/.opencode/skill/zakupki-tenders/
```

Windows:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.opencode\skill\zakupki-tenders"
Copy-Item SKILL.md "$env:USERPROFILE\.opencode\skill\zakupki-tenders\"
```

Для проекта — положить в `.opencode/skill/zakupki-tenders/SKILL.md`.

Скилл подхватывается новыми сессиями автоматически. Проверка — попросить: «найди тендеры по скиллу zakupki-tenders».

## Требования

- OpenCode с поддержкой скиллов;
- MCP `browse`, подключённый к реальному Chrome (ЕИС блокирует прямые HTTP-запросы).

## Ограничения

Инструкция не гарантирует обход анти-бота при массовом парсинге: ЕИС может временно блокировать частые запросы. Соблюдайте паузы и не создавайте параллельную нагрузку.
