# Stay Dead / Better Phone UI Compatibility Proposal

An unofficial compatibility proposal for Cyberpunk 2077:

- Stay Dead 0.1.2 (NightCityNemesis)
- Better Phone UI 1.1.1

## Why I made this

I originally prepared these changes for my own mod setup because I wanted to use both mods together.

I'm sharing the proposed diff so both mod authors can review the approach and decide whether they want to support this integration.

The changes were prepared with AI assistance.

## Problem

Better Phone UI reads message text and contact names directly from the journal.

Stay Dead supplies some of this content dynamically. As a result, Better Phone UI can display the interference placeholder instead of the actual message text.

## Proposed changes

- Retrieve Stay Dead contact names through NcnPhone.SenderForContact.
- Retrieve Stay Dead message text through NcnPhone.TextFor.
- Keep the existing journal fallback when dynamic text is empty.
- Keep the existing behavior for other contacts.
- Use conditional compilation for the NightCityNemesis integration.

The changes affect Better Phone UI's Data.reds.

## Included file

StayDead-integration.diff contains the proposed changes against the original Better Phone UI Data.reds from my installed version.

The file paths in the diff refer to my local working folders and may need adjustment before applying it.

This repository is a proposal for code review, not a ready-to-install mod.

## Validation and limitations

- Joint compilation with Better Phone UI, Stay Dead and local dependencies passed using REDscript 0.5.32.
- Compilation without Stay Dead has not been separately tested.
- Compatibility with other versions has not been verified.

The changes should be reviewed and tested before being included in an official release.

## Credits

- Better Phone UI: Akiway.
- Stay Dead / NightCityNemesis: its original author(s).

All original code remains the property of its respective authors.
No ownership of either mod is claimed.

This project is unofficial and is not endorsed by either mod author.

## For the mod authors

Thank you for your work on these mods.

Feedback, corrections and suggestions are welcome.
If either author has concerns about this publication, please open an issue so we can discuss changes or removal.
