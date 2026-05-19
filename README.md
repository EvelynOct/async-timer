## Explanation for 1.2:
spawner.spawn() only schedules the async task. The task does not run immediately.
The line after spawn executes first because the executor has not started yet. The task only begins when executor.run() is called.
Therefore "Spawner finished spawning task" appears before the async messages.

link for png: https://drive.google.com/file/d/14HKfPaK8Wbw4A9iXNrtdbqK3azEqn4JM/view?usp=sharing

