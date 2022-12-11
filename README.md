# Dining-philosopher

the dining philosophers problem is an example problem often used in concurrent algorithm design to illustrate synchronization issues and techniques for resolving them.
(DEADLOCK)

Five silent philosophers sit at a table around a bowl of spaghetti. A fork is placed between each pair of adjacent philosophers. (An alternative problem formulation uses rice and chopsticks instead of spaghetti and forks.)

Each philosopher must alternately think and eat. However, a philosopher can only eat spaghetti when he has both left and right forks. Each fork can be held by only one philosopher and so a philosopher can use the fork only if it's not being used by another philosopher. After he finishes eating, he needs to put down both forks so they become available to others. A philosopher can grab the fork on his right or the one on his left as they become available, but can't start eating before getting both of them.

Eating is not limited by the amount of spaghetti left: assume an infinite supply.

The problem is how to design a discipline of behavior (a concurrent algorithm) such that each philosopher won't starve; i.e., can forever continue to alternate between eating and thinking assuming that any philosopher cannot know when others may want to eat or think.

Src: http://en.wikipedia.org/wiki/Dining_philosophers_problem See more there.


![IllfatedEnviousAardvark-max-1mb](https://user-images.githubusercontent.com/90010134/206897238-e0b6f869-b805-4549-b252-01d555933cc6.gif)

--------------------------------
# Simulation

![ezgif com-gif-maker](https://user-images.githubusercontent.com/90010134/206897923-0c2de1aa-f8d6-47c5-8ede-5e75d7961171.gif)


```java

public class Dine{
	public static void main(String[] args){

		int x=10;

		Log.msg(String.valueOf(x));
 
		Chopstick[] chopistics = new Chopstick[5];

		//initlize the chopistics
		for(int i=0; i< chopistics.length; i++){
			chopistics[i] = new Chopstick("C: "+i);
		}
		Philosopher[] philosophers = new Philosopher[5];
		//for(i=0; i<philosophers.length; i++){
		philosophers[0] = new Philosopher("P: 0 - ", chopistics[0], chopistics[1]);
		philosophers[1] = new Philosopher("P: 1 - ", chopistics[1], chopistics[2]);
		philosophers[2] = new Philosopher("P: 2 - ", chopistics[2], chopistics[3]);
		philosophers[3] = new Philosopher("P: 3 - ", chopistics[3], chopistics[4]);
		philosophers[4] = new Philosopher("P: 4 - ", chopistics[0], chopistics[4]);

		for(int i=0;i<philosophers.length;i++){
			Log.msg("Thred "+ i);
			Thread t= new Thread( philosophers[i]);
			t.start();
		}
 	}
}

// State : 2 = Eat, 1 = think
class Philosopher extends Thread
{
	private Chopstick _leftChopistick;
	private Chopstick _rightChopistick;

	private String _name;
	private int _state;

	public Philosopher ( String name, Chopstick _left, Chopstick _right){
		this._state = 1;
		this._name = name;
		_leftChopistick = _left;
		_rightChopistick = _right;
	}
 
	public void eat()
	{
		if(! _leftChopistick.used){
			if(!_rightChopistick.used){
				_leftChopistick.take();
				_rightChopistick.take();

				Log.msg(_name + " : Eat");
				
				Log.Delay(1000);

				_rightChopistick.release();
		 		_leftChopistick.release();
			}
		}		
		think();
	}

	public void think(){
		 	this._state = 1;
		 	Log.msg(_name + " : Think");
		 	Log.Delay(1000);
		
	}

	public void run(){
		for(int i=0; i<=10; i++){
			eat();
		}
	}
}

class Log{

	public static void msg(String msg){
		System.out.println(msg);
	}
	public static void Delay(int ms){
		try{
			Thread.sleep(ms);
		}
		catch(InterruptedException ex){ }
	}
}

class Chopstick{

	public boolean used;
	public String _name;

	public Chopstick(String _name){
		this._name = _name;
	}

	public synchronized void take() {
		Log.msg ("Used :: " + _name );
		this.used = true;
	}
	public synchronized void release() {
		Log.msg ("Released :: " + _name );
		this.used = false ;
	}
}

```
