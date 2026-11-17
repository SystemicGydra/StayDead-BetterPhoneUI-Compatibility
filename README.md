# Stay Dead / Better Phone UI Compatibility

## Current status — 17 November 2026

**Better Phone UI includes a fix for Stay Dead starting with version 1.1.2. The old patch in this repository is for Better Phone UI 1.1.1. Do not apply it to 1.2.0.**

Better Phone UI's changelog lists a fix for garbled message placeholders and generic Stay Dead contact names in 1.1.2. Its author also lists Stay Dead as verified compatible.

- [Better Phone UI: download and requirements](https://www.nexusmods.com/cyberpunk2077/mods/37496)
- [Better Phone UI: changelog](https://www.nexusmods.com/cyberpunk2077/mods/37496?tab=logs)
- [Stay Dead: download and requirements](https://www.nexusmods.com/cyberpunk2077/mods/37844)

### Which version needs this patch?

| Better Phone UI | Guidance |
| --- | --- |
| 1.1.1 | The original diff below targets this version with Stay Dead 0.1.2. Updating Better Phone UI avoids having to apply that old proposal. |
| 1.1.2 | The author reports the Stay Dead text/name fix as included. This ZIP was not inspected in the review below. |
| 1.2.0 | The downloaded source includes the text/name handling needed by Stay Dead 0.1.6. Use the author's files without this repository's old patch. Source review only; this exact pair has not been tested in game here. |

### Updating an installation that used the old patch

1. Close the game.
2. Install the complete official Better Phone UI update and its required dependencies. In MO2, replace the old Better Phone UI installation rather than letting the patched 1.1.1 files override the update.
3. If you installed the compatibility patch as a separate mod, disable it. If you edited `Data.reds` inside Better Phone UI, replace that edited file with the one from the official update.
4. Keep Stay Dead installed with its own required dependencies. This repository does not update Stay Dead or its translations.
5. Check an existing Stay Dead conversation, the sender name, message preview, and a newly received message in game.

If placeholders remain, check which mod supplies the winning `r6/scripts/BetterPhoneUI/Data.reds` file. For a useful bug report, include both mod versions, any translation or phone patches, and whether the problem affects the preview, contact name, conversation text, or new messages.

## Source review: Stay Dead 0.1.6 + Better Phone UI 1.2.0

Reviewed the downloaded ZIPs, not just their changelogs:

- Stay Dead `Release-0.1.6`, uploaded 16 November 2026.
- Better Phone UI `1.2.0`, uploaded 15 November 2026.

Stay Dead still supplies its real message text through `MessangerItemRenderer.OnJournalEntryUpdated` and corrects contact data through the vanilla phone list methods. Its phone UI hook section is unchanged from the original Stay Dead 0.1.3 source inspected for comparison.

Better Phone UI 1.2.0's `External.reds` passes messages through a hidden vanilla renderer and reads back the displayed text. Its `Data.reds` uses the corrected contact lists for sender names. Those paths reach Stay Dead's existing hooks, including the ones in 0.1.6.

This is a different implementation from the old proposal here: it does not directly import `NightCityNemesis.NcnPhone`. No direct Better Phone UI API integration was found in Stay Dead 0.1.6's scripts; that is not required for the renderer/list approach described above.

**This review did not compile or play-test the 0.1.6 + 1.2.0 pair.** It supports the expected text/name compatibility, not a guarantee about every phone feature, performance, translation, or future release.

<details>
<summary>Reviewed archive SHA-256 hashes</summary>

```text
Better Phone UI 1.2.0:
73C0FDFDA187DA232A0815AAF549DA6E63DB1146ED2A3661C265F9FF16B40BB9

Stay Dead Release-0.1.6:
C6C97509CF38AF25CAA5CB7D73C08D89E9EF3AFDA76E23850F1DF22C93C9BF7B
```

</details>

## Original proposal — Better Phone UI 1.1.1 / Stay Dead 0.1.2

The original diff is kept as a historical code review proposal, not a current installer.

I originally prepared these changes for my own mod setup because I wanted to use both mods together, then shared the approach for the authors to review. The changes and this documentation were prepared with AI assistance.

### Original problem and approach

Better Phone UI 1.1.1 read journal message text and contact names directly. Stay Dead supplies that content dynamically, so the phone could display the interference placeholder instead of the actual message.

The proposal changed Better Phone UI's `Data.reds` to:

- Retrieve Stay Dead contact names through `NcnPhone.SenderForContact`.
- Retrieve message text through `NcnPhone.TextFor`.
- Keep the journal fallback when dynamic text is empty and preserve other contacts' behavior.
- Compile the integration conditionally when `NightCityNemesis` is present.

[`StayDead-integration.diff`](StayDead-integration.diff) targets the original Better Phone UI 1.1.1 file from my installation. Its paths refer to local working folders and need adjustment before applying. It must not be applied blindly to newer versions.

Joint compilation of the original proposal with Better Phone UI, Stay Dead and local dependencies passed using REDscript 0.5.32. Compilation without Stay Dead was not separately tested. That earlier result does not validate the newer pair reviewed above.

## Кратко по-русски

В Better Phone UI исправление сообщений и имён Stay Dead заявлено автором начиная с **1.1.2**. Для **1.2.0 старый патч из этого репозитория устанавливать не нужно**: используйте файлы автора и уберите старую правку `Data.reds`, если она перекрывает обновление.

Архивы **Stay Dead 0.1.6 + Better Phone UI 1.2.0** сверены по исходникам: необходимые обработчики сообщений и имён сохранились. Эта конкретная связка здесь не компилировалась и в игре не проверялась. Старый diff оставлен для истории; он предназначался для Better Phone UI 1.1.1 и Stay Dead 0.1.2.

## Credits

- Better Phone UI: **Akiway**.
- Stay Dead / NightCityNemesis: **Nchuark and the original contributors**.
- Original compatibility proposal: **SystemicGydra**, with AI assistance.

The upstream Better Phone UI fix is the author's implementation; this repository does not claim it was copied from this proposal. All original code remains the property of its respective authors. This repository is unofficial and does not claim endorsement by either mod author.

Feedback and corrections are welcome. If either author has concerns about this publication, please open an issue so we can discuss changes or removal.
