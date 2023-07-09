# Dataview Inline Value

This is a templater script to get the inline values of a dataview query. Useful when appending a template to existing page where you need all or the last value in the query.

## Script

**Template**
```
// all values output as an array
<% tp.user.dvInlineValue("value", `${tp.file.path(relative=true)}`) %>
// last value only
<% tp.user.dvInlineValue("value", `${tp.file.path(relative=true)}`, last=true) %>
```

**Script**
```
function dvInlineValue(query, page, last=false) {
    const dv = app.plugins.getPlugin("dataview").api;
    let values = dv.page(page)[query];
    if (last) {
        let lastValue;
        if (Array.isArray(values)) {
            lastValue = values[values.length-1]
        } else {
            lastValue = values
        }
        return lastValue
    } else {
        return values
    }
}
module.exports = dvInlineValue;
```

#### Example - Counting and adding to Turns / Rounds
**Template File**
```
<%_*
let lastTurn = tp.user.dvInlineValue("turn", `${tp.file.path(relative=true)}`, last=true);
if (typeof lastTurn !== "number") {
	lastTurn = 0
}
let nextTurn = lastTurn + 1;
-%>

> turn:: <% nextTurn %>

```