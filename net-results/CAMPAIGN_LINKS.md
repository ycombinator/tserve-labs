# Net Results campaign links

Use landing-page URLs with short, lowercase `utm_source` and `utm_campaign`
values. The App Store badge combines them as Apple's single campaign token
(`ct`), separated by `__`. Apple limits the token to 30 characters; if the
combined value is longer or contains characters outside letters, digits,
underscores, and hyphens, the badge keeps its ordinary App Store URL.

For example:

`https://tservelabs.com/net-results/?utm_source=club_flyer&utm_campaign=fall26`

The badge links to the App Store with `ct=club_flyer__fall26`. Use a stable
source for each placement type, such as `club_flyer`, `park_flyer`,
`club_email`, `tournament_card`, `player_share`, or `captain_share`. Use the
campaign for a specific effort, season, or event. Do not put a recipient's
identity or contact information in either value.

## App Store Connect setup

In App Store Connect, open Net Results > Analytics > Acquisition > Campaigns
and create a campaign link. Copy its numeric provider token (`pt`) into the
badge's `data-provider-token` attribute in `index.html`. Apple requires both
`pt` and `ct` for campaign reporting. The provider token stays the same for
future campaigns; the page generates each campaign token from the landing URL.

Apple reports the combined token as one campaign dimension. It cannot filter
`utm_source` and `utm_campaign` independently. For source or campaign totals
across multiple tokens, export the detailed campaign report and group by the
token's two parts. Small campaigns may not meet Apple's reporting thresholds.

The page does not currently collect landing-page visits or badge clicks.
Those stages require separate website analytics if they are needed.
