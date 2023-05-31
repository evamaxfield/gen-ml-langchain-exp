# Urban Political Text-as-Data

## Einstein: Who Participates

[S2](https://api.semanticscholar.org/CorpusID:150159099?utm_source=wikipedia)

### Notes

* used meeting minutes from 97 cities and towns in Boston metro from 2015 - 2017
* focused on MA because of data avalability
* table of population demographics -- pop, age, race, income, etc.
* the meeting minutes contain individual public comments
  * includes the name and address
  * their stance / position
  * their reasoning for stance (parking, environment, traffic, etc.)
  * all done qualitatively via coding
* calculate the proportion of meeting attendees who are repeat participants
* the proportion of individual who support/oppose housing and their reasons
* can also merge their name and address with voter file information to get demographics
  * age
  * gender
  * partisanship
  * history of voter turnout
  * registration date at current address (used as duration of residence)
  * notably, does NOT include income or race

* compare voter file for those who participated in meeting and those who did not (everyone else)
  * age, binary gender, partisanship, voter record

* place into three logit models to predict "is a public commenter" from above stats
  * On average, meeting participants are older, have lived at their residence for longer (proxied by the length of their voter registration at that location), and are more likely to be men. Women constitute 51.3% of the voter file, but only 43.5% of the commenters at development meetings. We find no differences in partisanship. Democrats, Republicans, and Independent/Unaffiliated voters do not participate at different rates. There are significant differences based on vote history. The individuals who participated in development meetings voted at roughly twice the frequency of those who did not.
  * Voters are more likely to participate when they are older, have lived in the same address for longer, and vote more frequently. Female voters are less likely to participate, and we observe no partisan differences

* 83% of commenters in our sample spoke at only one meeting.
* the average person made 1.3 comments

* Democrats were less likely to make multiple comments, and Republicans were more likely to do so.

* 62.5% of all comments were in opposition to proposed housing projects, while only 14.6% expressed support; the remaining 22.8% of comments were neutral.

* Consistent with theoretical predictions, those who appeared at multiple meetings are more likely to speak in opposition.
* Frequent voters are more likely to speak in support than to be neutral or oppose
* Women are also less likely to support a project, and more likely to be neutral or oppose it.
* Democrats are more likely to support projects and less likely to be neutral or oppose them than independent or Republican participants.

### Ideas

* bunch of models
  * public comment segmentation
  * public comment matching
  * stance taken on bill
  * reason for stance

* there was nothing on the "persuasiveness of public commenters"
  * i wonder if there is a method for crafting "the most persuasive public comment for a target councilmember"
  * appeal to emotion? appeal to logic?
  * how to do this?
    * create a dataset of votes and public comments
    * find votes that aren't typical for a councilmember somehow
    * compare the public comments from a "typical" vote vs a "nontypical" vote for that councilmember?

## LocalView

[S2](https://api.semanticscholar.org/CorpusID:257509793?utm_source=wikipedia)

### Notes

* This is the database of local meetings scraped from youtube
* trends of discussion about COVID is a big example
  * break apart by "competitiveness" of election in that state

* trends of discussion over time with total count of mentions, and an example of the phrase in context

### Ideas

* I think looking at state competitiveness / partisanship is a good idea
* pulling out quotes of the phrase in use also pulls the reader back to "how this data is computed"

## Open Framework for Analyzing Public Parliaments Data

[S2](https://api.semanticscholar.org/CorpusID:252682984?utm_source=wikipedia)

### Notes

* presents the "CAPD framework" (Collecting and Analyzing Parliament Data)
* Generic novel framework offers data analysis of government and parliament information presented as time series
* detecting events, changes in committees activities, evaluated with multiple countries data
  * "Change Point Detection"
  * "Pruned Exact Linear Time" (PELT)
  * BinSeg
  * WinSlide

* Use features for detection of "noteworthy meetings"
  * text length
  * meeting duration
  * year
  * month
  * number of committee members
  * number of parliament members

### Ideas

* in general, i was sort of unimpressed with this one?
* i like the idea of detecting interesting events as it may help us narrow down to a set of events that are divisive or "unusual"
* however their approach of only using the meeting length and number of attendees I felt was lacking
* i think can be improved by adding in additional features such as average sentiment, range of sentiment, "semantic similarity with committee meetings normally", etc.

## Asymmetric Nationalization of Local Politics

[S2](http://soubhikbarari.com/writings/localgov.pdf)

### Notes

* this is the paper that USED localview data

* hypotheses:
  * the politics of cities are more nationalized than the politics of towns, suburbs, etc.
  * the politics of democrat voting munis are more nationalized than the local politics of republican voting munis
  * there is little difference in the levels of nationalization of local officials and political active residents political speech
  * the politics of partisan local governments are more nationalized than the politics of non-partisan local governments
* table comparison of minutes item summary vs transcript selection
  * transcript shows added context behind stance and reasoning
* To distinguish members of the public speaking from members of the government speaking, we compiled a list of formal phrases announcing the start (e.g. “the floor is now open to the public”) and close of public comments (e.g., “seeing none else, the public comment period is closed”) as well as the introduction and conclusion of each speaker’s comment.
* additionally collected:
  * pop
  * racial composition
  * median household income
  * electoral results
  * classification of urban vs. suburban from 2020 census bureau
  * constituents national partisan preferences by computing republican presidential vote share for each muni via voter records agg at the block level

* measured:
  * "attention to latent issues in local politics"
  * usage of rhetoric specifically associated with national democrats and republicans"

* "measuring overal issue attention"
  * correlated topic model (CTM)
  * count the number of occurances of each topic
  * classify them into three categories (developmental, redistributive, allocational)
  * allocative topics such as utilities and wastewater are directionally associated with smaller conservative places
  * redistributive issues such as social services, housing, and transportation, point in the opposite direction and are discussed at higher rates in large cities

* "measuring national partisan rhetoric"
  * "how often does the munis political actors adopt the language of national partisans" (intensity)
  * "is the adopted language more democrat or republican leaning" (slant)
  * "gun ownership" can be broken into two rhetorical slants - "gun rights" or "gun control"
  * use "Gentzkow, Shapiro, and Taddy's collection of the 2,000 bigrams from the Congressional Record that are more differentially used between Democrats and Republicans"
  * exclude phrases about foreign policy

### Ideas

* A lot of this is great
* Finding topics to highlight instead of "picking them randomly" like I have been doing is in general I think better
* However, I don't like their use of PCA. If there was a good change to this paper I think it would be to make swap out PCA for something else a bit more deterministic

* "breaking down public comment section from everything else" -- okay, we really just need to do this now. They were using regex / simple pattern matching to do it. we can do that and probably something better

* measuring issue attention, I like it. We should do it to, with some slight changes imo.
  * they are just looking at the transcript
  * if possible we should look at issue attention but pull in voting / bills
  * if the issue decreases in discussion, maybe a bill passed?
  * are there certain topics that are always prevalent regardless of passed legislation?

* rhetoric: ya, we should have done this. but I think what may be interesting is investigating the other way around / direction? the "topical / rhetorical latency and diffusion" we have talked about.

## Race and Legislative Responsiveness in City Council Meetings

[S2](https://api.semanticscholar.org/CorpusID:158318150?utm_source=wikipedia)

### Notes

* Very small dataset but here are the details
  * The data set contains 2,382 observations from an analysis of 36 different council meetings
  * if 10 constituents address a 10-member city council, there would be 100 observations for that particular meeting
  * From the 2,382 observations, 1,992 are from 176 White constituents, and 390 are from 36 Black constituents. Also, 1,958 observations are associated with 26 White public officials, and 424 observations are associated with five Black officials, who are in Cities B and C.

* Coded for: whether or not each council member responds to a constituent or specifically acknowledges his or her claims either during council communications or during discussions on specific resolutions.

* statements coded as responses follow two broad patterns. A legislator’s statement constitutes a response if a typical observer is able to determine with certainty that the member is responding to a constituent either when the member specifically names the constituent or provides sufficient context that enables observers to ascertain who the member is referring to. In other instances, however, observers may not be able to properly discern whether there is a response. In these instances, members may, without referring to a particular constituent, agree with an opinion expressed by a constituent during the meeting or reiterate the view to disagree with it.

* 2,382 observations, 232 (9.74%) were coded as substantive responses while the remaining 2,150 were coded as non-responses.

* SIMPLE PROPORTIONS: When racial minorities speak, White legislators substantively respond a total of 19 times (6.55%) from the 290 occasions a response could have been issued. However, when White constituents speak, White legislators respond a total of 179 times (10.73%) out of the 1,668 instances a response could have been issued. When Black constituents speak, Black legislators substantively respond a total of 11 times (11%) from the 100 occasions a response could have been issued. On the other hand, when White constituents speak, Black legislators respond a total of 23 times (7.10%) out of the 324 instances a response could have been issued. From this descriptive analysis, legislators appear to respond more to constituents who share their race than to those who racially identify otherwise.

* MODELING
* Constituents who express messages similar to others or who speak as part of a group (Same Opinion) are less likely than constituents expressing a unique position to be singled out by council members.
* legislators are more likely to respond in the substantive sense to individuals who speak about legislative matters, especially matters involving significant council debate or constituent opposition, than to individuals speaking on less dominant issues.
* racial speaker and listener correlations are diminished once controls are added
* Specifically, White legislators are less likely to respond to constituents who speak about race-related issues than to those who address council members on matters unrelated to race. The coefficient associated with the “Speak on Race” variable in model 3 is negative and statistically significant. Since this coefficient is part of an interaction model, it reflects the effect of White legislators’ encounters with constituents speaking about race.

### Ideas

* I REALLY like this paper
* it talks about it's obvious limitations while still guiding the reader through and interesting idea and method
* I like the idea of breaking out public comments as the following:
  * speak on majority topic
  * speak on administrative matter
  * speak on social justice issue (race)
  * etc.

* A model to identify "responses from comments" would be interesting. I know it happens but from my knowledge it happens so rarely it would be interesting in itself imo

* This sort of relates to the "soapbox speeches" given by members after a piece of legislation is passed
