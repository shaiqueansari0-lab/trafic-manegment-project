package trafic;
import java.util.*;
class Vehicle {
    String id;
    Vehicle(String id) {
        this.id = id;
    }
    public String toString() {
        return id;
    }
}
class Road {
    String name;
    Queue<Vehicle> vehicles;
    Road(String name) {
        this.name = name;
        this.vehicles = new LinkedList<>();
    }
    void addVehicle(Vehicle v) {
        vehicles.add(v);
    }
    Vehicle passVehicle() {
        if (!vehicles.isEmpty()) {
            return vehicles.poll();
        }
        return null;
    }
    void showQueue() {
        System.out.println(name + " Road Queue: " + vehicles);
    }
}
class TrafficLight {
    boolean green;
    String direction; // NS or EW
    TrafficLight(String direction) {
        this.direction = direction;
        this.green = false;
    }
    void setGreen(boolean g) {
        green = g;
    }
    boolean isGreen() {
        return green;
    }
}
public class traficmanegment {

	public static void main(String[] args) {
		 Road north = new Road("North");
	        Road south = new Road("South");
	        Road east  = new Road("East");
	        Road west  = new Road("West");
	        TrafficLight nsLight = new TrafficLight("North-South");
	        TrafficLight ewLight = new TrafficLight("East-West");
	        int ticks = 12;      
	        int greenDuration = 3; 
	        int passedCount = 0;  
	        Random rand = new Random();
	        System.out.println("=== Advanced Traffic Management Simulation ===");
	        for (int t = 1; t <= ticks; t++) {
	            System.out.println("\n--- Time Tick: " + t + " ---");
	            if ((t / greenDuration) % 2 == 0) {
	                nsLight.setGreen(true);
	                ewLight.setGreen(false);
	                System.out.println("Signal GREEN for North-South");
	            } else {
	                nsLight.setGreen(false);
	                ewLight.setGreen(true);
	                System.out.println("Signal GREEN for East-West");
	            }
	            if (rand.nextDouble() < 0.5) north.addVehicle(new Vehicle("N" + t));
	            if (rand.nextDouble() < 0.5) south.addVehicle(new Vehicle("S" + t));
	            if (rand.nextDouble() < 0.5) east.addVehicle(new Vehicle("E" + t));
	            if (rand.nextDouble() < 0.5) west.addVehicle(new Vehicle("W" + t));
	            north.showQueue();
	            south.showQueue();
	            east.showQueue();
	            west.showQueue();
	            if (nsLight.isGreen()) {
	                Vehicle v1 = north.passVehicle();
	                Vehicle v2 = south.passVehicle();
	                if (v1 != null) { System.out.println(v1 + " passed from North road."); passedCount++; }
	                if (v2 != null) { System.out.println(v2 + " passed from South road."); passedCount++; }
	            }
	            if (ewLight.isGreen()) {
	                Vehicle v3 = east.passVehicle();
	                Vehicle v4 = west.passVehicle();
	                if (v3 != null) { System.out.println(v3 + " passed from East road."); passedCount++; }
	                if (v4 != null) { System.out.println(v4 + " passed from West road."); passedCount++; }
	            }
	        }
	        System.out.println("\n=== Simulation Ended ===");
	        System.out.println("Total Vehicles Passed: " + passedCount);
	        System.out.println("Vehicles Still Waiting:");
	        north.showQueue();
	        south.showQueue();
	        east.showQueue();
	        west.showQueue();
	    }
	
	}
