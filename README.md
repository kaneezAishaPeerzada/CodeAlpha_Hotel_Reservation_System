# CodeAlpha_Hotel_Reservation_System
package codealpha3;
import java.util.*;

class Room {
    int roomNumber;
    String category;
    boolean isAvailable;
    double price;

    public Room(int roomNumber, String category, double price) {
        this.roomNumber = roomNumber;
        this.category = category;
        this.price = price;
        this.isAvailable = true;
    }
}

class Reservation {
    int bookingId;
    String guestName;
    Room room;
    boolean isPaid;
    
    public Reservation(int bookingId, String guestName, Room room) {
        this.bookingId = bookingId;
        this.guestName = guestName;
        this.room = room;
        this.isPaid = false;
    }

    public void processPayment() {
        this.isPaid = true;
        System.out.println("Payment Successful for Booking ID: " + bookingId);
    }
}

class Hotel {
    List<Room> rooms = new ArrayList<>();
    List<Reservation> reservations = new ArrayList<>();
    int bookingCounter = 1;
    
    public Hotel() {
        rooms.add(new Room(101, "2 bad", 100));
        rooms.add(new Room(102, "1 large bad", 200));
        rooms.add(new Room(103, "1 large and 1 single bad", 300));
    }
    
    public void searchAvailableRooms() {
        System.out.println("Available Rooms:");
        for (Room room : rooms) {
            if (room.isAvailable) {
                System.out.println("Room " + room.roomNumber + " - " + room.category + " ($" + room.price + ")");
            }
        }
    }
    
    public void makeReservation(String guestName, int roomNumber) {
        for (Room room : rooms) {
            if (room.roomNumber == roomNumber && room.isAvailable) {
                room.isAvailable = false;
                Reservation reservation = new Reservation(bookingCounter++, guestName, room);
                reservations.add(reservation);
                System.out.println("Booking successful! Your Booking ID is: " + reservation.bookingId);
                return;
            }
        }
        System.out.println("Room not available or invalid number.");
    }
    
    public void viewBookingDetails(int bookingId) {
        for (Reservation res : reservations) {
            if (res.bookingId == bookingId) {
                System.out.println("Booking ID: " + res.bookingId + ", Guest: " + res.guestName + ", Room: " + res.room.roomNumber + ", Paid: " + res.isPaid);
                return;
            }
        }
        System.out.println("No booking found for ID: " + bookingId);
    }
    
    public void processPayment(int bookingId) {
        for (Reservation res : reservations) {
            if (res.bookingId == bookingId) {
                res.processPayment();
                return;
            }
        }
        System.out.println("Invalid Booking ID.");
    }
}

public class hostel {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Hotel hotel = new Hotel();
        
        while (true) {
            System.out.println("\n1. Search Rooms\n2. Make Reservation\n3. View Booking Details\n4. Process Payment\n5. Exit");
            int choice = scanner.nextInt();
            scanner.nextLine();
            
            switch (choice) {
                case 1:
                    hotel.searchAvailableRooms();
                    break;
                case 2:
                    System.out.print("Enter your name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter room number: ");
                    int roomNumber = scanner.nextInt();
                    hotel.makeReservation(name, roomNumber);
                    break;
                case 3:
                    System.out.print("Enter Booking ID: ");
                    int bookingId = scanner.nextInt();
                    hotel.viewBookingDetails(bookingId);
                    break;
                case 4:
                    System.out.print("Enter Booking ID for Payment: ");
                    int payBookingId = scanner.nextInt();
                    hotel.processPayment(payBookingId);
                    break;
                case 5:
                    System.out.println("Exiting... Thank you!");
                    return;
                default:
                    System.out.println("Invalid choice! Try again.");
            }
        }
    }
}

