## Explanation for 1.2:
spawner.spawn() only schedules the async task. The task does not run immediately.
The line after spawn executes first because the executor has not started yet. The task only begins when executor.run() is called.
Therefore "Spawner finished spawning task" appears before the async messages.

link for png: https://drive.google.com/file/d/14HKfPaK8Wbw4A9iXNrtdbqK3azEqn4JM/view?usp=sharing

## Explanation for 1.3:
Link with drop: https://drive.google.com/file/d/1AznSkPTa52eklnAzZJbTtzhDWp6Ep1VS/view?usp=sharing
Link without drop: https://drive.google.com/file/d/1um5X7YM4DP_JlIi8efeNzn0hlD82p0v6/view?usp=sharing

// drop(spawner);

After removing that line, the program no longer terminated automatically and kept running indefinitely.

This happens because the executor is still waiting for possible new incoming tasks from the spawner. Since the channel between the spawner and executor is still open, the executor assumes more tasks may still arrive in the future.

The drop(spawner) statement is important because it closes the task channel and signals to the executor that no more tasks will be added. Once all existing tasks are completed and the channel is closed, the executor can safely stop running.

Therefore, the spawner, executor, and drop statement are closely related:

The spawner creates and sends tasks.
The executor runs and manages the tasks.
drop(spawner) tells the executor that task creation has finished.

