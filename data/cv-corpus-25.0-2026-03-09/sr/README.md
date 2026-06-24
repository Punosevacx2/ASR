# *Српски* &mdash; Serbian (`sr`)

This datasheet is for cv-corpus-25.0-2026-03-09 of the Mozilla Common Voice *Scripted Speech* dataset for Serbian [Српски - `sr`]. The dataset contains 14059 clips representing 12.73 hours of recorded speech (7.6 hours validated) from 184 speakers, recorded from a text corpus of 8,727 sentences.

## Language

### Accents

| Code | Accent | Clips | Speakers |
|---|---|---|---|
| - |  | 5,180 (36.8%) | 37 (20.1%) |

## Demographic information

The dataset includes the following self-declared age and gender distributions. A coverage summary is shown below each table.

### Gender

Self-declared gender information. The table shows clip and speaker counts with percentages. Speakers who did not declare a gender are listed as Unspecified. A dash (-) indicates zero.

| Code | Gender | Clips | Speakers |
|---|---|---|---|
| male_masculine | Male, masculine | 4,491 (31.9%) | 44 (23.9%) |
| female_feminine | Female, feminine | 2,066 (14.7%) | 16 (8.7%) |
| transgender | Transgender | - | - |
| non-binary | Non-binary | - | - |
| do_not_wish_to_say | Prefer not to say | - | - |
| - | Unspecified | 7,502 (53.4%) | 149 (81.0%) |

*Gender declared: 6,557 of 14,059 clips (46.6%), 35 of 184 speakers (19.0%)*

### Age

Self-declared age information. The table shows clip and speaker counts with percentages. Speakers who did not declare an age are listed as Unspecified. A dash (-) indicates zero.

| Code | Age | Clips | Speakers |
|---|---|---|---|
| teens | Teens | 10 (0.1%) | 1 (0.5%) |
| twenties | Twenties | 3,684 (26.2%) | 31 (16.8%) |
| thirties | Thirties | 1,674 (11.9%) | 18 (9.8%) |
| fourties | Fourties | 1,403 (10.0%) | 8 (4.3%) |
| fifties | Fifties | 1,778 (12.6%) | 11 (6.0%) |
| sixties | Sixties | 3,530 (25.1%) | 2 (1.1%) |
| seventies | Seventies | - | - |
| eighties | Eighties | - | - |
| nineties | Nineties | - | - |
| - | Unspecified | 1,980 (14.1%) | 140 (76.1%) |

*Age declared: 12,079 of 14,059 clips (85.9%), 44 of 184 speakers (23.9%)*

## Data splits for modelling

**Clip buckets**

| Bucket | Clips |
|---|---|
| Validated | 8,395 (59.7%) |
| Invalidated | 429 (3.1%) |
| Other | 5,235 (37.2%) |

**Training splits**

| Split | Clips |
|---|---|
| Train | 2,516 (30.0%) |
| Dev | 1,866 (22.2%) |
| Test | 1,935 (23.0%) |

*Training split coverage: 6,317 of 8,395 validated clips (75.2%)*

The dataset contains 8395 validated, 429 invalidated, and 5235 unresolved clips. The average clip duration is 3.261 seconds.

## Text corpus

**Validated sentences:** 8,155

| Category | Count |
|---|---|
| Unvalidated sentences | 572 |
| Pending sentences | 375 |
| Rejected sentences | 197 |
| Reported sentences | 190 |

The corpus contains 8,727 sentences: 8,155 validated and 572 unvalidated (375 pending review, 197 rejected), with 190 reported for review.

### Sample

There follows a randomly selected sample of five sentences from the corpus.

1. *Што вам говори?*
2. *Ако не можеш?*
3. *А не ви.*
4. *Зар и ти.*
5. *А то је твој.*

### Sources

| Source | Sentences |
|---|---|
| sentence-collector | 5,603 (68.7%) |
| SETimes, https://models.omnilingo.cc/sr/setimes.cand.Latn-Cyrl.txt | 1,211 (14.8%) |
| SETimes corpus for Bosnian, transliterated to Cyrillic. | 538 (6.6%) |
| мој цитат | 268 (3.3%) |
| """Serbian folk poem ""Zidanje skadra""" | 181 (2.2%) |
| ја | 135 (1.7%) |
| Other | 219 (2.7%) |

### Text domains

| Code | Domain | Clips | Speakers |
|---|---|---|---|
| general | General | 14 (0.1%) | 6 (3.3%) |
| agriculture_food | Agriculture and Food | - | - |
| automotive_transport | Automotive and Transport | - | - |
| finance | Finance | - | - |
| service_retail | Service and Retail | - | - |
| healthcare | Healthcare | - | - |
| history_law_government | History, Law and Government | 2 (0.0%) | 2 (1.1%) |
| media_entertainment | Media and Entertainment | - | - |
| nature_environment | Nature and Environment | 5 (0.0%) | 3 (1.6%) |
| news_current_affairs | News and Current Affairs | - | - |
| technology_robotics | Technology and Robotics | 33 (0.2%) | 9 (4.9%) |
| language_fundamentals | Language Fundamentals | 5 (0.0%) | 3 (1.6%) |

### Fields

#### Clips

Each row of a `tsv` file represents a single audio clip, and contains the following information:

- `client_id` - hashed UUID of a given user
- `path` - relative path of the audio file
- `text` - supposed transcription of the audio
- `up_votes` - number of people who said audio matches the text
- `down_votes` - number of people who said audio does not match text
- `age` - age of the speaker[^1]
- `gender` - gender of the speaker[^1]
- `accents` - accents of the speaker[^1]
- `variant` - variant of the language[^1]
- `segment` - if sentence belongs to a custom dataset segment, it will be listed here
- `prompt_upvotes` - number of upvotes the sentence prompt received
- `prompt_reports` - number of reports the sentence prompt received
- `is_edited` - whether the clip's transcription has been edited

[^1]: For a full list of age, gender, and accent options, see the [demographics spec](https://github.com/common-voice/common-voice/blob/main/web/src/stores/demographics.ts). These will only be reported if the speaker opted in to provide that information.

#### `validated_sentences.tsv`

The `validated_sentences.tsv` file contains one row per validated sentence in the text corpus:

- `sentence_id` - unique identifier for the sentence
- `sentence` - the sentence text
- `variant` - the variant of the language
- `sentence_domain` - the domain(s) the sentence belongs to
- `source` - the source the sentence was collected from
- `is_used` - whether the sentence is still in circulation for recording
- `clips_count` - number of clips recorded for this sentence

#### `unvalidated_sentences.tsv`

The `unvalidated_sentences.tsv` file contains one row per unvalidated sentence in the text corpus:

- `sentence_id` - unique identifier for the sentence
- `sentence` - the sentence text
- `variant` - the variant of the language
- `sentence_domain` - the domain(s) the sentence belongs to
- `source` - the source the sentence was collected from
- `up_votes` - number of upvotes the sentence received
- `down_votes` - number of downvotes the sentence received
- `status` - current status of the sentence (`pending` or `rejected`)

## Get involved

### Community links

- [Common Voice translators on Pontoon](https://pontoon.mozilla.org/sr/common-voice/contributors/)
- [Common Voice Communities](https://github.com/common-voice/common-voice/blob/main/docs/COMMUNITIES.md)

### Discussions

- [Common Voice on Matrix](https://chat.mozilla.org/#/room/#common-voice:mozilla.org)
- [Common Voice on Discourse](https://discourse.mozilla.org/t/about-common-voice-readme-first/17218)
- [Common Voice on Discord](https://discord.gg/9QTj9zwn)
- [Common Voice on Telegram](https://t.me/mozilla_common_voice)

### Contribute

- [Speak](https://commonvoice.mozilla.org/sr/speak)
- [Write](https://commonvoice.mozilla.org/sr/write)
- [Listen](https://commonvoice.mozilla.org/sr/listen)
- [Review](https://commonvoice.mozilla.org/sr/review)

## Licence

This dataset is released under the [Creative Commons Zero (CC-0)](https://creativecommons.org/public-domain/cc0/) licence. By downloading this data you agree to not determine the identity of speakers in the dataset.
