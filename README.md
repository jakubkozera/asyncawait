Solution with a basic task, async/await questions, splitted into three classes:

1. TaskDelay Class:

Questions:

a) [Test1]  - What is the excepted order of `Debug.WriteLine` invocation and why?

	--> 1, 2, 3, 4, 5 ,6 - await is waiting for the `Delay2000` execution to finish (even though Task.Delay is greater than in the `Delay1000` )

b) [Test2]  - What is the excepted order of `Debug.WriteLine` invocation and why?
	
	--> 1, 2, 4, 6 - without the await keyword the async method will start but they will not complete before the test finished the run


2. TaskWhenTests Class:
Questions:

a) [Test1] - How long the test will run? (under five seconds?)
	
	--> Since we first await for `ReturnFoo`, which takes atleast 3 seconds, and then we await `ReturnFooFoo`, which takes atleast 4 seconds, the overall test will take atleast 7 seconds - it will fail

b) [Test2] - How long the test will run? (under five seconds?)
	
	--> Using Task.WhenAll we will start those 2 tasks at the same time in parallel, awaiting them both in this case will take about 4 seconds, the overall test will take less than 5 seconds - it will succeed


3. TaskException Class:

Questions:
a) [Test1] - What will be Debug output? Will the exception from `ThrowException` be handled (exceptionHandled == true;)
	 
	 --> 1, 2, 3 *exception*, we invoke `ThrowException` in the main thread, but we don't await it in-line. The exception will be propagated during the `await` operation on task - in the try method. 
		Meaning that the error wil be handled and test will pass ("4" will not be displayed)

Useful resources:
https://www.codeproject.com/Articles/5299501/Async-Await-Explained-with-Diagrams-and-Examples?utm_content=bufferbf04d&utm_medium=social&utm_source=linkedin.com&utm_campaign=buffer#canceltoken
