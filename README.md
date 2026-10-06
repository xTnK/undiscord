# undiscord
Delete all messages in a Discord server / channel or DM - Easy and fast bulk delete 

Tampermonkey script based on my needs

Based on https://github.com/victornpb/undiscord

Choose **Advanced settings > Deletion order** before starting:

- **Newest first**: delete from newest to oldest.
- **Oldest first**: delete from oldest to newest.
- **Alternate new and old** (default): delete 25 newest, then 25 oldest, without
  pausing between batches. The delete delay and API rate limit / indexing waits
  still apply.

Changing the mode resets the delete delay to 1250ms for **Alternate new and old**,
or 1000ms for either other mode. You can adjust it afterward.

If alternate mode is rate limited, it temporarily uses a 2000ms delete delay until
a message is deleted successfully, then restores the delay you had selected.

Alternating mode skips duplicate IDs from overlapping pages, including when fewer
than 50 messages remain or Discord's search index still returns deleted messages.
Messages already removed elsewhere are skipped without counting them as failures.
All modes keep the existing message filters and interval bounds.

Pagination uses timestamp sorting and message ID bounds from
[Discord's search API](https://docs.discord.com/developers/resources/message#search-guild-messages).

Run the simulated API tests with Node.js (no dependencies needed):

```powershell
node --test tests/undiscord.test.cjs
```
