

Goroutines are lightweight threads managed by go. You can launch them with the *go func()*

Channels let goroutines communicate safely without race conditions. You can think of a channel like a conveyor belt. One goroutine puts data on and other takes it off.

Instead of creating a goroutine for every request (which can crash your system for large wordlists), we use a **worker pool**. This means:

- We launch N goroutines (workers),
    
- Each one grabs a word from a shared channel and processes it.

- Create a `jobs` channel where we’ll send all the words.
    
- Create `results` channel to collect successes (status != 404).
    
- Use a `sync.WaitGroup` to wait for all goroutines to finish.



If you see the below defined in the parameters in the function this is what it means

### `jobs <-chan string`

- This is a **receive-only** channel of `string`s.
    
- Each string in this channel is a word from the wordlist (e.g., `"admin"`, `"login"`, `"backup"`).
    
- The arrow `<-chan` means this function **can only receive from** this channel. It **cannot send to it**.




## Things to implement


Ok so status code 429 means that a  website we are fuzzing too fast and since there is gonna be timers on websites we gotta make something that makes a delay in order to go so yea implement that. 




Ok so i wanna be able to fuzz subdomains (Vhost method and bruteforce status codes? maybe even get da sizes?)




I would also like to release a really good wordlist so people might use this tool.