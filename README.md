# PokeMarket QuickSet + Marketplace Ticket Matcher

This version keeps the original Railway/deployment files unchanged.

## Existing commands
- `/quickset` — posts TCGdex sets to a Forum.
- `/set continue` — continues missing set posts.

## Marketplace commands

### `/forum add`
Adds a Forum channel to the marketplace search.

### `/forum tags`
Configures the two existing Forum tags:
- `IN STOCK`
- `SOLD OUT`

Enter the tag IDs shown by Discord for that Forum. The bot immediately applies IN STOCK to existing listings that do not already have SOLD OUT.

### `/forum list`
Shows configured marketplace forums and tag IDs.

### `/forum remove`
Stops that Forum from marketplace matching.

### `/tview add`
Adds the channel where closed-ticket transcripts are posted.

When a new transcript arrives, the bot:
1. Reads the transcript text/embeds and text/html/json/csv attachments.
2. Identifies the Discord users who actually spoke in the transcript.
3. Searches the configured marketplace Forums.
4. Only considers listings created by those users.
5. Searches that user's listings for the Pokémon/card/item mentioned in the transcript.
6. Uses card number, price, language, set/name text and other matching text when available.
7. If one listing is clearly identified, applies SOLD OUT and removes IN STOCK.
8. If the match is ambiguous, it does not change any listing.

Example:
Bob created two listings:
- Bob — Charizard ex 125/197 — Japanese — €40
- Bob — Charizard 006/165 — English — €25

If Bob speaks in a ticket transcript about Charizard ex 125/197 for €40, the bot searches Bob's listings and marks the first one SOLD OUT. It does not search the whole Forum and randomly select a Charizard.

### `/tview remove`
Stops watching a transcript channel.

### `/tview list`
Lists watched transcript channels.

### `/tview log`
Chooses where automatic matching results/warnings are posted.

## Important Discord setting

Because the bot reads transcript messages and speaker names, enable **Message Content Intent** and **Server Members Intent** in the Discord Developer Portal.

## Railway

The deployment files were kept unchanged from the supplied ZIP:
- `railway.json`
- `Dockerfile`
- `package.json`
- `tsconfig.json`

No additional npm packages are required.

Configuration is stored in `pokemarket-market-config.json` while the bot is running.
