Lamda 2022

package Q1;
import java.util.*;

public class ProducerThread {

	public static void main(String[] args) {
		
		List<Integer> list = new ArrayList<>();

		
		Thread t1 = new Thread(()->{
			synchronized (list) {	

			int value = 0;
			while (true) {
			System.out.println("Producer started");
			try {
					value += 10;
					list.add(value);
					System.out.println( "Producer adding value " + value +" to Queue"); 
	
					list.wait() ;
					Thread.sleep (1000) ;
				} catch (InterruptedException e) {
						System.out.println("");
				 }
			list.notify();
			System.out.println("Elements in Queue = " + list);

			 }
		  }
		});
		
		Thread t2 = new Thread(()-> {
			synchronized (list) {
				while(true) {
					try {
						System.out.println("consumer started");
						System.out.println("consuner thread consumes" + list.get(0));
						list.remove(0);
						list.notify();
						Thread.sleep(1000);
						list.wait();
						
					}
					catch(InterruptedException e) {
						System.out.println("");
					}
				}
				
			}
		});
		
		t1.start();
		t2.start();

	}
}	




........................................................................................


package Q2;
import java.util.*;



	interface Ivehicle{
		void displayVehicles();
	}
	
	public class Q1a{
		
		public static void displayVehicleDetails() {
			List<String> vehicles = new ArrayList<String>();
			vehicles.add("Car"); 
			vehicles.add("Bus"); 
			vehicles.add("Van"); 
			vehicles.add("Jeep"); 
			vehicles.add("Lorry");
			vehicles.forEach(System.out::println);
		}
		
	

	public static void main(String[] args) {
		Ivehicle ivehicle = Q1a::displayVehicleDetails;
		ivehicle.displayVehicles();
	}

}


.........................................................................................................................


package Q2;
import java.util.*;

interface ITrafficService{
	
	public String checkSpeed(List<Double> listOfCheckPoints);
	
}

public class ArrayListq {

	public static void main(String[] args) {
		ITrafficService iTrafficService = (listOfCheckPoints)->{
			
			double total = 0; 
			for (Double speed :listOfCheckPoints) { 
				total = total + speed; 
			} 
			double averageSpeed = total/listOfCheckPoints.size(); 
			
			if(averageSpeed >= 100.0){ 
				return "Issue Fine"; 
			}else if((averageSpeed < 100.0) && (averageSpeed >= 80.0)){ 
				return "Warning message"; 
			}else if((averageSpeed < 80.0) && (averageSpeed >= 50.0)){ 
				return "Good speed"; 
			}else if((averageSpeed < 50.0) && (averageSpeed >= 30.0)){ 
				return "Normal"; 
			
			
			}else{ 
			return "Slow";
		}

		};
		ArrayList<Double> speedinCheckPoint = new ArrayList<>(); 
		speedinCheckPoint.add(20.0); 
		speedinCheckPoint.add(30.0); 
		speedinCheckPoint.add(60.0); 
		speedinCheckPoint.add(80.0); 
		speedinCheckPoint.add(100.0); 
		speedinCheckPoint.add(120.0); 
		
		System.out.println(iTrafficService.checkSpeed(speedinCheckPoint));
		

	}
}





