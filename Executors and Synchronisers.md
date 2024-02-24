# Controllers
Utility classes for coordinating Access and control 
- Semaphore : indicates when to switch threads, its managing a specified number of permits and is used to control concurrency 
- Countdown Latch : 
	- allows one or more threads to wait for a set of threads to complete an action 
	- necessary for DBMS applications 
- Cyclic Barrier : 
	- Allows set of threads to wait  for a set of threads to complete an action 
## Semaphore
- serve as permit holders 
- instead of like working with individual wait and notify the semaphore allows implementation across the 