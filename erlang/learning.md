# Learning
## Record
Record definition
```
file record.hrl

-record(todo, {status=reminder, who = joe, text}).
```

Using record to match the case, only the type matching is enough?
```
rr("record.hrl").
X1 = #todo{status=new, text="Hello World"}.

3> case X1 of #todo{status=Status, who=Who, text=Text}=X2 -> X2 end.
#todo{status = new,who = joe,text = "Hello World"}

5> Status.
new
6> Who.
joe
7> X2.
#todo{status = new,who = joe,text = "Hello World"}
8> Text.
"Hello World"

```
