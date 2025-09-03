- [.--](./.--.md)
# **Types of queries**
### **and**
- Find all blocks matching multiple conditions – i.e. blocks or their parents containing multiple page or block references.
- `{{query: {and: [page A](roam-page://page A) [page B](roam-page://page B) }}}
{{query: {and: [articles](roam-page://articles) ((block)) }}}
{{query: {and: [Tyler Cowen](roam-page://Tyler Cowen) ((block)) [econ](roam-page://econ) }}}
`
### **or**
- Find all blocks matching any of a number of conditions – i.e. blocks or their parents containing any of the selected page or block references.

- `{{query: {or: [page A](roam-page://page A) [page B](roam-page://page B) }}}
{{query: {or: [Zen](roam-page://Zen) [Buddhism](roam-page://Buddhism) }}}
{{query: {or: [Utah](roam-page://Utah) [Idaho](roam-page://Idaho) [Montana](roam-page://Montana) }}}
`
### **not**
- Exclude blocks matching any of the page or block references selected.
- `{{query: {and: [page A](roam-page://page A) {not: [page B](roam-page://page B) }}}}
{{query: {and: [Slate Star Codex](roam-page://Slate Star Codex) {not: [psychiatry](roam-page://psychiatry) }}}}`
### **between**
- Finds all blocks on daily pages and blocks mentioning a date between two days. ==**This only works on Daily Notes page**==.
- You can use the following as a shorthand: [today](./today.md), [tomorrow](./tomorrow.md), [yesterday](./yesterday.md), [last week](<./last week.md>), [next week](<./next week.md>), [last month](<./last month.md>), and [next month](<./next month.md>). 
- `{{query: {between: [January 1st, 2021](roam-page://January 1st, 2021) [today](./today.md) }}
{{query: {and: [mistakes](roam-page://mistakes) {between: [January 1st, 2020](roam-page://January 1st, 2020) [December 31st, 2020](roam-page://December 31st, 2020) }}}}
{{query: {and: [TODO](roam-page://TODO) {between: [last week](<./last week.md>) [today](./today.md) }}}}`
## Community Videos::
### Query syntax and logic: how to ask Roam questions with queries by [Robert Haisfield](<./Robert Haisfield.md>)
- <https://www.youtube.com/watch?v=LJZBGJOzhUY&t=20s&ab_channel=RobertHaisfield>
### How Queries Work in Roam Research by [R.J. Nestor](<./R.J. Nestor.md>)
- <https://www.youtube.com/watch?v=lBmklV0n8D0>
### Roam Research Search Queries by [David Perell](<./David Perell.md>)
- <https://www.youtube.com/watch?v=HoccqyiHvPw>
### Insight Hunting with Queries in Roam by [Cortex Futura](<./Cortex Futura.md>)
- <https://www.youtube.com/watch?v=gLAlQGM_l1Q>
### Roam Research Query Tutorial: Pending Tasks for Task Management and Task Dashboard Using Queries by [The Upgraded Brain](<./The Upgraded Brain.md>)
- <https://www.youtube.com/watch?v=Kg5omIyWu8s>
## Articles::
### [How to query in Roam](https://roamhacks.com/how-to-query-roam/) by [Roamhacks](./Roamhacks.md)
### [Searching Roam With Queries: A Primer](https://www.roamstack.com/roam-queries-primer/) by [RoamStack](./RoamStack.md)
## Key Commands::
- `/query`