# Interface Content and Localization

Interface text is part of the interaction: it names objects, predicts results, and explains recovery. Follow the product's existing voice and terminology first; the guidance below fills gaps.

## Labels and actions

Label buttons and menu items with a specific verb, or verb and object, that describes what happens, such as "Send invoice" or "Delete 3 projects", rather than "OK", "Submit", or "Let's go". Keep the wording of a multi-step flow consistent, and avoid link text such as "Click here" that says nothing out of context. Use input-neutral verbs, or the platform's own, rather than "click" on touch devices.

Use one term for one concept across the product, its documentation, and its errors, and keep a glossary when several people write copy. People should never have to wonder whether two words mean the same thing.

Put the most important, user-facing words first. People scanning lists and headings often read only the first couple of words. Prefer plain language over internal or technical jargon, and follow the target platform's capitalization convention consistently.

## Errors

Place the message next to the problem and pair it with more than color. State what happened in the user's terms and how to fix it, for example "Enter a date after today" instead of "Invalid date" or "An error occurred". Avoid blaming words such as invalid or illegal, jokes, and error codes as the main content; keep codes available for diagnosis. Do not report errors before the person has had a chance to finish typing, and keep what they entered, except secrets and expiring credentials such as passwords and one-time codes.

## Confirmations and alerts

Title the dialog with the question or consequence, and label buttons with their results, such as "Delete file" and "Keep file", rather than "Yes" and "No". Use "OK" only for purely informational alerts and keep a clearly labeled cancel option. When the person deliberately chose the destructive action, such as emptying the trash, the confirming button can be the default and needs no destructive styling; when the destructive result may not be what they intended, mark it as destructive and do not make it the default. Follow the platform's guidance where it is more specific.

## Empty, loading, and success messages

Say what the state means and what to do next. An empty list should explain what belongs there and offer the first action; a success message should confirm the specific result, such as "Invoice sent to Dana", and offer undo when possible.

## Localization

Design layouts that let text grow. Translated text is often much longer than English, and short strings grow most: labels under ten characters can double or triple in length, while long passages grow by roughly a third. Let text wrap and containers expand, avoid fixed-width controls for text, allow larger line heights for scripts that need them, and do not abbreviate to make translations fit.

Never build sentences by concatenating fragments, since word order and agreement differ across languages. Write each message as a whole with named placeholders in a message format such as ICU MessageFormat, and handle plurals with the locale's plural categories rather than a singular and plural pair; many languages need more than two forms, and the "other" category is always required.

Format dates, times, numbers, and currencies with the locale's rules through platform internationalization APIs rather than hand-built strings. Store and exchange dates in an unambiguous format such as ISO 8601, and show them to people in their locale's form, preferring a written month name when ambiguity matters.

For right-to-left languages, mirror layout and directional elements, such as navigation order, back and forward arrows, and progress direction. Do not mirror media playback controls, clockwise indicators such as clocks and refresh, numbers, untranslated text such as URLs, or depictions of physical objects. Decide chart direction per chart, since time axes often follow reading direction; verify against current platform guidance.

Label language choices with each language's own name, such as "Français" or "Deutsch", optionally followed by the name in the current language.
