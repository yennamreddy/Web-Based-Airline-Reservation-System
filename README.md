# Web-Based-Airline-Reservation-System

import java.util.*;

// Class to represent a Flight
class Flight {
    private String flightNumber;
    private String source;
    private String destination;
    private int capacity;
    private int availableSeats;

    public Flight(String flightNumber, String source, String destination, int capacity) {
        this.flightNumber = flightNumber;
        this.source = source;
        this.destination = destination;
        this.capacity = capacity;
        this.availableSeats = capacity;
    }

    // Getters and Setters
    public String getFlightNumber() {
        return flightNumber;
    }

    public String getSource() {
        return source;
    }

    public String getDestination() {
        return destination;
    }

    public int getCapacity() {
        return capacity;
    }

    public int getAvailableSeats() {
        return availableSeats;
    }

    public void bookSeats(int numSeats) {
        availableSeats -= numSeats;
    }
}

// Class to represent the Airline Reservation System
public class AirlineReservationSystem {
    private List<Flight> flights;
    private Map<String, List<String>> bookings; // Flight number -> List of passenger names

    public AirlineReservationSystem() {
        this.flights = new ArrayList<>();
        this.bookings = new HashMap<>();
    }

    public void addFlight(Flight flight) {
        flights.add(flight);
        bookings.put(flight.getFlightNumber(), new ArrayList<>());
    }

    public boolean bookFlight(String flightNumber, int numSeats, List<String> passengers) {
        for (Flight flight : flights) {
            if (flight.getFlightNumber().equals(flightNumber)) {
                if (flight.getAvailableSeats() >= numSeats) {
                    flight.bookSeats(numSeats);
                    bookings.get(flightNumber).addAll(passengers);
                    return true;
                } else {
                    return false; // Not enough seats available
                }
            }
        }
        return false; // Flight not found
    }

    public List<String> getPassengers(String flightNumber) {
        return bookings.getOrDefault(flightNumber, new ArrayList<>());
    }

    // Other methods such as flight search, seat selection, admin controls, etc. can be added here
}
