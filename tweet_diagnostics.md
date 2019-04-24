---
title: "Discrimination on Social Media: Twitter Feasibility"
author: "Alex Jakubow"
date: ""
output: 
  html_document:
    keep_md: yes
    number_sections: yes
    toc: yes
    toc_depth: 2
---







# Overview
- Tweets were prospectively scraped between Friday, April 05 and Monday, April 08 using the `rtweet (0.6.8)` package in `R` as a front end to access Twitter's streaming APIs.  

- Tweets were captured in recurring 30 minute snapshots for all tweets, in English, posted within the United States.  The parameters for bounding the geography of the search are not exact, so some non-domestic tweets were also captured.  See Table  below.

- A total of 1463513 tweets were scraped, which returned tweets from 49 different states and 2720 different counties.

- The rest of this document explores the geographical distribution of these tweets, as well as their substantive content, in greater detail


# Results by Geography
The next table presents the distribution of domestic vs. foreign responses.  Despite the fact that the parameters of the API call were restricted to the United States, non-domestic tweets occasionally get captured due to a lack of precision in the geo-tagging (more on this below).



<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Domestic vs. Foreign Tweets</caption><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Origin</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">N</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">%</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Domestic</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,361,975</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">93</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Foreign</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">101,538</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">6.9</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Error</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Total</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,463,513</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
</table>
<!--/html_preserve-->

Nonetheless, approximately Domestic  % of tweets came from a domestic source.

For identifying the exact geolocation of each tweet, the analysis draws on two fields in the dataset `coords_coords` and `bbox_coords`.  `coords_coords` provides the exact latitude and longitude of the user when the tweet was created, while `bbox_coords` provides an approximate location using the geographical midpoint of a bounding area that defines the general area from which a tweet was created.  An entry for `coords_coords` is only generated if the user enables geo-tagging for tweets posted from his/her account.  I'm still attempting to understand how large these bounding areas are in order to estimate the imprecision of these approximations.




<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Geographical Precision of Tweets</caption><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Location</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">N</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">%</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Estimate</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,308,500</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">89</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Exact</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">155,013</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Total</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,463,513</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
</table>
<!--/html_preserve-->

From the above table, we observe that only  Exact % of the scraped tweets provide exact geographic coordinates for the tweet.  I'll attempt to find references in the literature that justify the use of geographical estimates.  Failing that, we could conduct a separate set of sensitivity analyses only using the tweets with exactly-identified latitudes and longitudes.




Before discussing the content of these tweets, the following table provides some summary statistics about the distribution, density, and coverage of tweets within the data.  Specifically, the columns (from left to right) are defined as follows:

- `State`: state of observation
- `Tweets`: total number of tweets for the state
- `Counties w/ Tweets`: total number of counties in the state with at least one tweet
- `Avg. Tweets per County`: Average number of tweets per county in the state (`Tweets`/`Counties w/ Tweets`)
- `County Coverage (%)`: The number of counties with tweets as a percentage of all counties in the state
- `Population Coverage (%)`: The population of all counties with tweets as a percentage of the entire state population

<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Tweet Distribution and Coverage</caption><col><col><col><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">State</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Tweets</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Counties w/ Tweets</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Avg. 
                    Tweets per County</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">County Coverage (%)</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Population Coverage (%)</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">AL</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">20,734</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">63</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">329</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">AR</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">8,433</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">63</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">134</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">84</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">AZ</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">27,835</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">15</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,856</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">CA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">195,164</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">58</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3,365</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">CO</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">18,148</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">59</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">308</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">92</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">CT</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11,523</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">8</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,440</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">DC</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14,847</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14,847</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">DE</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">4,036</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,345</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">FL</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">79,829</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">64</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,247</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">GA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">58,233</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">140</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">416</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">88</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">IA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">8,702</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">86</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">101</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">87</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">ID</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3,269</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">35</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">93</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">80</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">IL</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">46,642</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">90</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">518</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">88</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">IN</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">22,500</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">89</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">253</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">97</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">KS</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">9,392</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">73</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">129</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">70</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">KY</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">17,315</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">93</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">186</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">78</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">LA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">32,274</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">57</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">566</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">89</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">29,931</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">2,138</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MD</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">25,701</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">24</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,071</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">ME</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">2,949</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">16</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">184</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MI</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">30,402</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">78</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">390</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MN</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">15,000</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">78</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">192</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">90</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MO</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">19,986</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">95</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">210</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">83</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">97</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MS</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11,071</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">70</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">158</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">85</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">95</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">MT</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,661</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">37</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">45</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">66</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NC</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">41,115</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">95</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">433</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">95</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">ND</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,972</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">31</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">64</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">58</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">89</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NE</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">6,187</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">70</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">88</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">75</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NH</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3,265</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">10</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">326</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NJ</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">32,078</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">21</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,528</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NM</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">5,650</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">30</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">188</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">91</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NV</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">21,962</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">16</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,373</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">NY</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100,071</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">62</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,614</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">OH</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">48,338</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">88</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">549</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">OK</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13,111</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">66</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">199</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">86</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">98</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">OR</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">16,242</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">35</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">464</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">97</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">PA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">46,130</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">66</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">699</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">RI</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">4,014</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">803</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">SC</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">18,530</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">44</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">421</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">SD</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,878</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">31</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">61</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">47</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">83</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">TN</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">28,941</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">87</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">333</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">92</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">TX</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">161,496</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">219</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">737</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">86</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">UT</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">7,684</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">26</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">296</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">90</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">VA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">39,207</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">125</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">314</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">VT</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,839</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">12</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">153</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">86</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">98</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">WA</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">26,619</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">35</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">761</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">90</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">100</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">WI</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13,508</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">68</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">199</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">94</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">99</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">WV</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">5,074</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">48</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">106</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">87</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">96</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">WY</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,476</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">21</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">70</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">91</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">98</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Total</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1,361,964</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">2,720</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">884</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">90</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">98</td>
</tr>
<tr>
<td colspan="6" style="vertical-align: top; text-align: left; white-space: normal; border-style: solid solid solid solid; border-width: 0.8pt 0pt 0pt 0pt; padding: 4pt 4pt 4pt 4pt;">No Data for Alaska</td>
</tr>
</table>
<!--/html_preserve-->

# Results by Content




## Activism
The maps below respectively plot the number of tweets invoking political activism hashtags as a share of all tweets within each state and county for which we have available data.  Specifically, the following hashtags were used:

#alm, #alllivesmatter, #blacklivesmatter, #blm, #notmypresident, #maga, #bluelivesmatter, #bringbackourgirls, #icantbreathe, #mybrotherskeeper, #sayhername, #beataggies





The top 5 states and top 25 counties are listed below.  The final column lists the total number of tweets (including and excluding political activism hashtags) for each jurisdiction.



<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Prevalance of Political Activism: Top 5 States</caption><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">State</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Density (%)</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Total Tweets</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Wyoming</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0.00813</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1476</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">West Virginia</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0.00374</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">5074</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">South Carolina</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0.00367</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">18530</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Idaho</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0.00184</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3269</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Montana</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">0.00181</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1661</td>
</tr>
</table>
<!--/html_preserve-->

<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Prevalance of Political Activism: Top 25 Counties</caption><col><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">State</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Density (%)</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Total Tweets</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Dallas County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Alabama</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">21.6</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">37</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Columbia County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Oregon</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">20.0</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">25</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Bacon County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">7</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Lawrence County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Kentucky</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">7</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Johnston County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Oklahoma</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">7</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Butler County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Pennsylvania</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">10.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">327</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Hutchinson County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Texas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 9.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Creek County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Oklahoma</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">53</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Pickens County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 5.9</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">17</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Greenbrier County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">West Virginia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 5.6</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">36</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Perry County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Ohio</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 4.5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">22</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Hopkins County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Texas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 4.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">47</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Colleton County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">South Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 3.0</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">33</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Tazewell County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Virginia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.9</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">35</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Fremont County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Wyoming</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.8</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">290</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Dyer County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Tennessee</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.6</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">39</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Transylvania County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">North Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">40</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Boone County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Arkansas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.4</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">41</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Williams County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Ohio</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">43</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Norton County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Kansas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">233</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Stephenson County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Illinois</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">47</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Nez Perce County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Idaho</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">48</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Stark County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">North Dakota</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">48</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">St. Clair County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Michigan</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 2.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">194</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Natrona County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Wyoming</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 1.9</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">206</td>
</tr>
</table>
<!--/html_preserve-->

## Slurs
The maps below respectively plot the number of tweets invoking racial slurs as a share of all tweets within each state and county for which we have available data.  Specifically, the following slurs were used:

nigger, nigra, nigga, niggah, nigguh, niglet, nigglet, negra, niggra, nigrah, nigruh, negro, nigg, nigz, niggaz




As one might expect, higher concentrations of racial slurs appear in the southeast.  The top 5 states and top 25 counties are listed below.  The final column lists the total number of tweets (including and excluding racial slurs) for each jurisdiction.



<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Prevalance of Racial Slurs: Top 5 States</caption><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">State</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Density (%)</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Total Tweets</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">2.4</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">32274</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Mississippi</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1.8</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11071</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1.8</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">58233</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Maryland</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">25701</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">District of Columbia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">1.4</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14847</td>
</tr>
</table>
<!--/html_preserve-->

<!--html_preserve--><table class="huxtable" style="border-collapse: collapse; margin-bottom: 2em; margin-top: 2em; width: 50%; margin-left: auto; margin-right: auto;  ">
<caption style="caption-side: top; text-align: center;">Prevalance of Racial Slurs: Top 25 Counties</caption><col><col><col><col><tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">State</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Density (%)</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; border-style: solid solid solid solid; border-width: 0pt 0pt 1pt 0pt; padding: 4pt 10pt 4pt 10pt; font-weight: bold;">Total Tweets</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Comanche County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Texas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">33.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">3</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Concordia Parish</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">16.2</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">37</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Winn Parish</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">15.4</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Irwin County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">7</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Lewis County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">New York</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Simpson County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Mississippi</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">15</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Assumption Parish</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">12.2</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">49</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Terrell County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11.5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">26</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Brooks County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">9</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Pulaski County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">9</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Sumner County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Kansas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">18</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Martin County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Texas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">11.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">9</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Cleveland County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">North Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">10.4</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">154</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Marengo County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Alabama</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">10.0</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">10</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Richland Parish</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 9.5</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">21</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Lamar County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Texas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 8.6</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">58</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Ashley County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Arkansas</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 8.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">36</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Bedford County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Pennsylvania</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 8.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">12</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Emporia city</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Virginia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 8.3</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">12</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Jefferson County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Georgia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Hertford County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">North Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">26</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Barnwell County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">South Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">13</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Barbour County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">West Virginia</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.7</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">26</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Yadkin County</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">North Carolina</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 7.1</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">14</td>
</tr>
<tr>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Sabine Parish</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">Louisiana</td>
<td style="vertical-align: top; text-align: left; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;"> 6.9</td>
<td style="vertical-align: top; text-align: right; white-space: nowrap; padding: 4pt 10pt 4pt 10pt;">29</td>
</tr>
</table>
<!--/html_preserve-->
