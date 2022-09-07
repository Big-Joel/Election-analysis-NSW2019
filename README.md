# Election-analysis-NSW2019
**Please see [the PDF file](https://github.com/Big-Joel/Election-analysis-NSW2019/blob/main/Election%20play%201.pdf) for a concise export of the Power BI reports.**

*Using Power BI to find interesting outcomes from the election.*
This was my first practice project after following some Power BI tutorials from Microsoft. 

## The most interesting report
Page 2 is my favourite and shows a map with swinging seats (which I defined as 'winning the seat with less than 55% of the two-candidate preferred vote'). I think it would be useful for parties to target these areas in the next election.

## How data was obtained
All data was imported into Power BI tables from multiple Excel files. The election data was kindly curated by the good people at [TallyRoom.com.au](https://www.tallyroom.com.au/data). The income data came from the Australian Tax Office here: [ATO](https://data.gov.au/data/dataset/taxation-statistics-postcode-data/resource/9129cf1e-8eb0-4c25-98e3-95fc2697267c?inner_span=True)

From the 7 source Excel files, this model was created: [model screenshot](https://github.com/Big-Joel/Election-analysis-NSW2019/blob/main/election_table_model.png)

## Reports created
1. General election results. The winner, number of seats won by each party, percentage of primary votes gained. 
2. The 'swinging seats' map. Also, by pressing the button you can see all of the electorates in NSW.
3. Lucky Politicians. My second favourite. Who won the seat even though they received fewer primary votes than another candidate? These areas would also be useful to target in the next election.
4. The top and bottom ten electorates by taxable income, and which party won the seat. Also, a chart showing estimated average income of voters for each party.
5. Election outcomes for each electorate. 
6. Ballot order analysis. Does the order of each candidate on the ballot paper matter in the end?

## Formulae
I used DAX to create measures and calculated columns. An example being this one, to determine if each electorate is a swinging seat or not:

```
Swinging Seat = 
    var districtId = [electorate_id]
    var candidateId = FILTER(Candidates, [electorate_id] = districtId && [Elected] = True)
return
    CALCULATE(
        if([Votes % of 2CP by electorate]<0.55, True, False),
        candidateId)
```