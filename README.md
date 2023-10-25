# ck3-modding

Feel free to just rename & remove tags and add it straight to your files

## Oct 24 v2 Changelog:
Issue: warfare_legacy_5 causes all houseguards from each culture to appear, regardless of player's own culture. multiple houseguards will populate list. Fixed by changing each culture's can_recruit block for house guards within common\men_at_arms_types
(changing structure from "has_cultural_pillar = heritage..." to "culture = { has_cultural_pillar = heritage... }").

Deleted irrelevant files (deletion including 00_riekling_army_maa) from github upload. Only the changed relevant maa files are present.

Maintained additional 00_falmer_army_maa changes detailed below.

&nbsp;

&nbsp;

## Oct 24 v1 Changelog: (formatting kind of sucks, forwarding text to github)

Issue: warfare_legacy_5 causes all houseguards from each culture to appear, regardless of player's own culture. multiple houseguard listings will populate list.
Fixed by changing structure from "has_cultural_pillar = heritage..." to "culture = { has_cultural_pillar = heritage... }"

Besides the fixes, there are additional edits which I tagged with "HZ" when possible, but also list below:


common/men_at_arms_types/00_maa_types :: house_guard entry has two can_recruit blocks; commented out one to be consistent with rest of file.

00_riekling_army_maa file: TESTED. rieklings have access to both goblin houseguard & riekling houseguard. issue occurs however where everyone's list, regardless of culture, has access to riekling houseguard (at warfare_legacy_5).

to fix, changed "has_cultural_pillar" trigger to "this = culture:riekling" trigger.

missing dds: copied goblin_house_guard.dds, renamed copy to (otherwise missing) "riekling_house_guard.dds" under men_at_arms_big

00_falmer_army_maa file: TESTED
	changed "this = culture:falmer_betrayed" to "culture = culture:falmer_betrayed" (ditto for regular falmer).
	however, because of lack of heritage condition, any divergent/split culture may lose houseguard.
	so then commented out the above "culture = culture:falmer_betrayed" to replace with (ditto for regular falmer):
 
 ```
		culture ?= { #### HZ ADDED
			OR = {
				this = culture:falmer_betrayed
				any_parent_culture_or_above = {
					this = culture:falmer_betrayed ## UNTESTED
				}
			}
		}
```
ISSUE: falmer_betrayed culture still get two houseguards, not sure why. doesnt seem to be the falmer or dwemer houseguards. using "culture = culture:falmer_betrayed" trigger instead of HZ ADDED trigger also doesnt seem to fix, but may require double-checking.

there may also be  issues for falmer/betrayed/riekling characters having access to two+ houseguards, if they merge cultures with another heritage pillar that does have houseguards?

localization:
00_jimmy_cultural_armies_l_english.yml:
	minor grammatical edits: missing periods, verb tenses, etc


