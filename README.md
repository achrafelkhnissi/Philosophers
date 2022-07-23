
<h1 align="center">
	42cursus' Philosophers
</h1>

<p align="center">
	<b><i>Development repo for 42cursus' Philosophers project</i></b><br>
	For further information about 42cursus and its projects, please refer to <a href="https://github.com/achrafelkhnissi/1337/42curses"><b>42cursus repo</b></a>.
</p>


<h3 align="center">
	<a href="#summary">Summary</a>
	<span> · </span>
	<a href="#resources">Resources</a>
</h3>

---

## introduction

This project is about learning the basics of threading a process, learning how to make threads and discover the mutex.
______________
*Several philosophers are sitting at a round table doing one of three things: eating, thinking, or sleeping. While eating, they are not thinking or sleeping, while sleeping, they are not eating or thinking and of course, while thinking, they are not eating or sleeping. The philosophers sit at a circular table with a large bowl of spaghetti in the center. There are some forks on the table,  it is assumed that a philosopher must eat with two forks, one for each hand. The philosophers must never be starving and every philosofer needs to eat. Philosophers don’t speak with each other and don’t know when another philosopher is about to die. Each time a philosopher has finished eating, he will drop his forks and start sleeping. When a philosopher is done sleeping, he will start thinking. The simulation stops when a philosopher dies.*

## Overview
What you should understand to succeed this project:
- Once or more philosophers are sitting at a round table either eating, either thinking, either sleeping, While they are eating, they do not think or sleep; while thinking they don't eat or sleep; and, of course, while sleeping, they do not eat or think.
- The philosophers sit at a circular table with a large bowl of spaghetti in the center.
- There are some forks on the table. Serving and eating spaghetti with a simple fork is very inconvenient, so the philosophers will eat with two forks, one for each hand.
- Each time a philosopher finishes eating, they will drop their forks and start sleeping. Once they have finished sleeping, they will start thinking. The simulation stops when a philosopher dies.
- Every philosopher needs to eat and they should never starve.
- Philosophers don't speak with each other.
- Philosophers don't know when another philosopher is about to die.
- No need to say the philosophers should avoid dying!

## General Instructions
You have to write a program for the mandatory part and another on for the bonus part but they will have the same basic rules:
- Global variables are forbidden!
- The program should take the following arguments: `number_of_philosophers` `time_to_die` `time_to_eat` `time_to_sleep` `[number_of_times_each_philosopher_must_eat]`
	- `number_of_philosophers`: is the number of philosophers and also the number of forks.
	- `time_to_die`: is in milliseconds, if a philosopher doesn't start eating `time_to_die` milliseconds after starting their last meal or the beginning of the simulation, it dies.
	- `time_to_eat`: is in milliseconds and is the time it takes for a philosopher to eat. During that time they will need to keep the two forks.
	- `time_to_sleep`: is in milliseconds and is the time the philosopher will spend sleeping.
	- `number_of_times_each_philosopher_must_eat`: argument is optional, if all philosophers eat at least `number_of_times_each_philosopher_must_eat`the simulation will stop. If not specified, the simulation will stop only at the death of a philosopher.
- Each philosopher should be given a number from 1 to `number_of_philosophers`.
- Philosopher number 1 is next to philosopher number `number_of_philosophers`. Any other philosopher with the number `N` is seated between philosopher `N - 1` and philosopher `N + 1`.

About the logs of the program:

- Any change of status of a philosopher must be written as follows (with `X` replaced with the philosopher number and `timestamp_in_ms` the current timestamp in milliseconds):
```
	- timestamp_int_ms X has taken a fork
	- timestamp_int_ms X has is eating
	- timestamp_int_ms X has is sleeping 
	- timestamp_int_ms X has is thinking
	- timestamp_int_ms X has died
```
- The status printed should not be scrambled or intertwined with another philosopher's status.
- You can't have more than 10ms between the death of a philosopher and when it will print its death.
- Again, philosophers should avoid dying!

## Mandatory Part
The specific rules for the mandatory part are:
- Each philosopher should be a thread.
- One fork between each philosopher, therefore if they are multiple philosophers, there will be a fork at the right and the left of each philosopher.
- To avoid philosophers duplicating forks, you should protect the forks state with a mutex for each of them.

## Bonus Part
For The bonus part, the program takes the same arguments as before and should behave as explained in the [General Instructions](#general-instructions). The specific rules are:
- All the forks are in the middle of the table.
- They have no states in memory but the number of available forks is represented by a semaphore.
- Each philosopher should be a process and the main process should not be a philosopher.
______________

## philos_and_forks_map

![philos forks](https://user-images.githubusercontent.com/63563271/129487495-9c1db852-1e3c-4276-ad8e-9fe4e233e7a5.png)

## new_functions_allowed

name  | prototype | description |
---|------|------|
[**usleep**](https://man7.org/linux/man-pages/man3/usleep.3.html) | int usleep(useconds_t usec); |shall cause the calling thread to be suspended from execution until either the number of realtime microseconds specified by the argument useconds has elapsed or a signal is delivered to the calling thread and its action is to invoke a signal-catching function or to terminate the process. The suspension time may be longer than requested due to the scheduling of other activity by the system.			|
[**gettimeofday**](https://c-for-dummies.com/blog/?p=4236) | int gettimeofday( struct timeval *, struct tzp * ); | fills two structures with details about the current time of day	|
[**pthread_create**](https://man7.org/linux/man-pages/man3/pthread_create.3.html) | int pthread_create(pthread_t * restrict thread, const pthread_attr_t * restrict attr, void *(* start_routine)(void *), void * restrict arg);| create a new thread |
[**pthread_detach**](https://man7.org/linux/man-pages/man3/pthread_detach.3.html) | int pthread_detach(pthread_t thread); | marks the thread identified by thread as detached.  When a detached thread terminates, its resources are automatically released back to the system without    the need for another thread to join with the terminated thread. Attempting to detach an already detached thread results in unspecified behavior.|
[**pthread_join**](https://man7.org/linux/man-pages/man3/pthread_join.3.html) | int pthread_join(pthread_t thread, void ** retval); | join with a terminated thread. The function waits for the thread specified by thread to terminate.  If that thread has already terminated, then      pthread_join() returns immediately.  The thread specified by thread must be joinable. |
[**pthread_mutex_init**](https://pubs.opengroup.org/onlinepubs/7908799/xsh/pthread_mutex_init.html) | int pthread_mutex_init(pthread_mutex_t * mutex, const pthread_mutexattr_t * attr); | initialises the mutex referenced by mutex with attributes specified by attr. If attr is NULL, the default mutex attributes are used; the effect is the same as passing the address of a default mutex attributes object. Upon successful initialisation, the state of the mutex becomes initialised and unlocked.	|
[**pthread_mutex_destroy**](https://pubs.opengroup.org/onlinepubs/7908799/xsh/pthread_mutex_init.html) | int pthread_mutex_destroy(pthread_mutex_t * mutex); |destroys the mutex object referenced by mutex; the mutex object becomes, in effect, uninitialised.|
[**pthread_mutex_lock**](https://pubs.opengroup.org/onlinepubs/7908799/xsh/pthread_mutex_lock.html) | int pthread_mutex_lock(pthread_mutex_t * mutex); | locks the object referenced by mutex. If the mutex is already locked, the calling thread blocks until the mutex becomes available. This operation returns with the mutex object referenced by mutex in the locked state with the calling thread as its owner			|
[**pthread_mutex_unlock**](https://pubs.opengroup.org/onlinepubs/7908799/xsh/pthread_mutex_lock.html) | int pthread_mutex_unlock(pthread_mutex_t * mutex); |releases the mutex object referenced by mutex.	|

## Resources

- Mandatory:
	- `man pthread`
	- [PISOX Threads Programming](https://hpc-tutorials.llnl.gov/posix/)
	- [Into to Parallel Computing](https://hpc.llnl.gov/documentation/tutorials/introduction-parallel-computing-tutorial)
	- [POSIX thread (pthread) libraries](https://www.cs.cmu.edu/afs/cs/academic/class/15492-f07/www/pthreads.html)
	- [Jacob Sober Playlist on Threads - Youtube](https://www.youtube.com/watch?v=uA8X5zNOGw8&list=PL9IEJIKnBJjFZxuqyJ9JqVYmuFZHr7CFM)
	- [Intro to Threads - Neso Academy](https://www.youtube.com/watch?v=LOfGJcVnvAk&list=PLBlnK6fEyqRiVhbXDGLXDk_OQAeuVcp2O&index=31)
	- [Dinning Philosophers Problem - Wikipedia](https://en.wikipedia.org/wiki/Dining_philosophers_problem)
	- [Multithreaded Programming Guide - Oracle](https://docs.oracle.com/cd/E26502_01/html/E35303/toc.html)
	- [Debugging a Multithreaded Program - Oracle](https://docs.oracle.com/cd/E26502_01/html/E35303/compile-19263.html#scrolltoc)
	- [Unix Threads in C - CodeVault Playlist](https://www.youtube.com/playlist?list=PLfqABt5AS4FmuQf70psXrsMLEDQXNkLq2)
	- https://www.youtube.com/watch?v=NbwbQQB7xNQ
	- https://www.youtube.com/watch?v=vmSKp0PExRY
	- [Webianr: Mutexes & Semaphores Demystified](https://www.youtube.com/watch?v=dzR6DD3ClZ4)
	- [CS360 Lecture notes -- A primer on mutexes and condition variables](http://web.eecs.utk.edu/~jplank/plank/classes/cs360/360/notes/Mutex-Cond/lecture.html)
	- [Using mutexes](https://www.ibm.com/docs/en/aix/7.2?topic=programming-using-mutexes)

- Bonus:
	- [Youtube - Jacob Sorber](https://www.youtube.com/watch?v=ukM_zzrIeXs)
	- [Youtube - Neso Academy](https://www.youtube.com/watch?v=XDIOC2EY5JE)
	- [Youtube - Semaphore Vs Mutex](https://www.youtube.com/watch?v=8wcuLCvMmF8)
	
- Extra:

	* [Unix Threads in C -playlist](https://www.youtube.com/watch?v=d9s_d28yJq0&list=PLfqABt5AS4FmuQf70psXrsMLEDQXNkLq2) by CodeVault
	* [Multi Threaded Programming Video](https://www.youtube.com/watch?v=OgnLaXwLC8Y) by Arif Butt
	* [Synchronization among Threads Video](https://www.youtube.com/watch?v=SvFr7rPWI3g&list=PL7B2bn3G_wfC-mRpG7cxJMnGWdPAQTViW&index=47) by Arif Butt
	* [Multithreaded Programming](https://randu.org/tutorials/threads/)
	* [Threads questions and answers](https://www.notion.so/Philosophers-2b872948598e4f0cba91c66d8b5ba821) by [Joyce Macksuele](https://github.com/joycemacksuele)
	* [Delay_ometer](https://github.com/nesvoboda/socrates) by [Arseniy Shishaev](https://github.com/nesvoboda)
	* [Philosooher Visualizer](https://nafuka11.github.io/philosophers-visualizer/) by [Nafuka](https://github.com/nafuka11)
	* [Notion with study materials](https://grizzly-muenster-737.notion.site/Philosophers-55c385e0a6224d629c86231821e3ce10) by [Laís Arena](https://github.com/laisarena)
	* [ASCIImoji](http://asciimoji.com/)
