# Word Count Within Current File

This dataview query allows you to track word count per session / scene within the current file. The word count does have to be done manually from the section of text that you want to count against your goal. At the moment all this does is sum the total word count - with redundancy if there is only one entry. Though I may add to it later.

## Syntax For Word Count
```
text from session goes here

wordCount:: 1
---
new session of writing

wordCount:: 2
```

## Dataview Query
```dataviewjs
let array = dv.current().wordCount;
let sum = 0;
if (typeof array !== 'number') {
array.map(x => sum += x);
dv.el("p", "Total Word Count: " + sum);
}
else {
dv.el("p", "Total Word Count: " + array);
}
```
