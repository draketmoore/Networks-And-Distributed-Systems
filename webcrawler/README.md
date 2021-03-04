For this project, my partner and I completed it in steps to ensure that we were on the right track and to make it more
manageable. At a high level, we made a class to keep handle all the HTTP logic for Fakebook, which had methods like
a get method, that made a GET request with the appropriate cookie headers to the given URL. Overall, here were the steps
we took:

1. First, we figured out how to send HTTP requests and parse HTTP responses with sockets. We started with HTTP 1.1 
directly as we figured that 1.0 would be relatively simple. A large challenge was how to get the headers out from the
data, especially when the response was chunked. To get the headers, we used some simple RegEx which worked well. To
get the data, we utilized the fact that chunks (and the header section) ended in \r\n\r\n's. Once we figured out how
to make basic HTTP requests, we moved onto the login flow.

2. To figure out login, we utilized the network tool on Chrome to see what requests were being made. We worked out 
the CSRF token and session ID, and the process was relatively painless. 

3. To crawl Fakebook, we decided to use a BFS search with a set to keep track of seen URLs. We used Python's html package
to parse HTML and find links and secret flags. This part was pretty straightforward since all the hard HTTP-related work
was done in part 1. It was simply a matter of performing a BFS search on the URLs of Fakebook. We had some issue of
keeping track of seen URLs which resolved in duplicate flags, but we quickly resolved this by cleaning up our logic related
to seen URLs. At this point, our crawler was functioning at a decent speed, so we didn't feel the need to use parallel 
processing/threads to complicate things and potentially introduce bugs.

4. After we got base functionality working, we moved onto gzip. This complicated our code a little, as we assumed every
response to be in a chunked format, which gzip does not abide by. However, after working with some examples we managed 
to get things working with the help of the zlib library. 

5. We attempted to do keep-alive, but for some reason the server kept closing the connection on us despite the response
agreeing to keep-alive and our code sending the next request before the 2s timeout. In the end, we decided not to pursue
keep-alive, since our code was running fast enough and it seemed like our attempt should've worked (not even the TA could
help us).

We tested our code by running the crawler multiple times so it could take different paths in its searches and verified
that it found all the flags every time.