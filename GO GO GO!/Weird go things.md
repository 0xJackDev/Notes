

Add this to path cuz im lazy to add ot bashrc

export PATH=$PATH:/usr/local/go/bin


if you are doing for in a range of something like lets say a word list but you dont care about the index you must replace the initialization part with a _. Maybe not idk 

```
for _, word := range wordlist { ... }

you can also do if you are inside of a channel and not a slice

	for result := range results {
		fmt.Println(result)
	}

```



If you have parenthesis after you declare a function it calls it inline and anonymously. 

```
go func() {
    // do stuff
}()
```
for example 