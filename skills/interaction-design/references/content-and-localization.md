# Interface Content and Localization

Copy is interaction architecture: it names domain objects, sets action expectations, and guides error recovery. Reuse the product's established glossary first.

## Action labels, terminology, and error microcopy

Label triggers with specific `verb + object` outcomes (`Send invoice`, `Revoke API key`, `Delete 3 drafts`) rather than generic mechanics (`Submit`, `OK`, `Yes`, `Click here`), keeping the exact verb consistent from button -> confirmation -> completion status. Enforce a 1:1 mapping between domain concepts and terms across UI, docs, and API errors, front-loading distinguishing nouns/verbs in headings and list items for rapid scanning.

Place blame-free error messages directly beside the offending control: state what went wrong in user terms and the concrete fix (`Enter a date after 2026-11-16` rather than `Invalid input`), keeping diagnostic codes secondary without discarding user-typed text. Title confirmation dialogs with the concrete consequence and pair unambiguous button verbs (`Delete repository` / `Keep repository`), withholding default focus from unexpected destructive actions.

## Localization resilience

Build fluid containers that wrap and grow without clipping or horizontal overflow — short translated UI labels routinely expand 2x–3x and dense scripts require taller line boxes. Pass complete sentences with named placeholders through ICU MessageFormat (including full locale plural categories with mandatory `other`) rather than concatenating string fragments in code, since word order and grammatical agreement vary across languages.

Store and exchange timestamps/amounts in canonical machine formats (ISO 8601, integer minor units) and render dates, numbers, and currencies exclusively via platform `Intl` APIs. Under RTL locales, mirror layout flow, navigation chrome, and directional progression arrows while keeping media transport icons, clockwise refresh indicators, numerals, URLs, and physical-object illustrations unmirrored. List language switchers in each language's endonym.
