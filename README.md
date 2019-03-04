# Large PDF Loading

this is a POC to examine different PDF loading approaches to help determine the best course of action going forward.

With the latest version of pdf.js 2.0.943, the pdf streaming is available by default. 
 
Though there are two ways to load PDFs: 
1. pre-fetching PDF via streaming 
2. Lazy loading per additional configuration 
 
It seems the Lazy loading approaching would give us better perceived performance: (test file size: 1.1G, 70000 pages)
 
**Loading Type	Total request	Initial display (stop watch) 	Data transferred	Bkgd loading Done	**Use of range request
Pre-fetching	104	            3.22s	                        1122 M (total)	    25s	                Yes
Lazy Loading	104 + 	        2 – 2.36 s	                    252B	            7.55s	            Yes
 
With Range request turned off, it would take 30.62s to load the same file. 

And the memory footprint for Lazy Loading is definitely smaller as shown below. Also, you are right – the Lazing loading doesn’t load the entire PDF in the memory. It only loads first few pages to start with. 
 
As the next step. I will share my code with you, Matthew, and Anand. 
 
**Memory footprint comparison (JVM Instance: localhost:8080)

Pre-fetching: 16 MB
Lazy loading: 4.5 MB


