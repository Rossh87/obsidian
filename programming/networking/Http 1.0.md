https://developer.att.com/video-optimizer/docs/best-practices/http-1-0-usage

- Originally required a new [[TCP]] connection to be opened for each req/res cycle, with the server required to close the connection.
- Has many limitations compared to [[Http 1.1]]
- Still in very limited use on small number of mobile applications