# data-visualization
data visualization

library(RSelenium)

remDr <- remoteDriver(
  remoteServerAddr = "localhost",
  port = 4446L,
  browserName = "chrome"
)

remDr$open()

remDr$navigate("https://soundcloud.com/discover")
webElem <- remDr$findElement(using = "css", "[name = 'q']")
webElem$sendKeysToElement(list("R Cran", key = "enter"))

webElems <- remDr$findElements(using = "css selector", "h3.r")
resHeaders <- unlist(lapply(webElems, function(x) {x$getElementText()}))
resHeaders

webElem <- webElems[[which(resHeaders == "R for Windows")]]
webElem$clickElement()
remDr$getCurrentUrl()

remDr$close() 
