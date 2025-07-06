


```

func Get_Request_Code(e string) int {
	url := e
	resp, err := http.Get(url)
	check(err)
	defer resp.Body.Close() // Clean up HTTP body
	return resp.StatusCode
}
```



This function is reading the variable e as a string and then returning a int. Remember everything is to the right.



Get the total number of lines to read in wordlist and how many we have read and have a progress bar at the end


