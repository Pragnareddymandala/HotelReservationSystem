import java.util.ArrayList;
import java.util.HashMap;
import java.util.Scanner;

class Room {
    private String roomType;
    private int roomNumber;
    private double price;
    private boolean isAvailable;

    public Room(String roomType, int roomNumber, double price) {
        this.roomType = roomType;
        this.roomNumber = roomNumber;
        this.price = price;
        this.isAvailable = true;
    }

    public String getRoomType() {
        return roomType;
    }

    public int getRoomNumber() {
        return roomNumber;
    }

    public double getPrice() {
        return price;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean available) {
        isAvailable = available;
    }

    @Override
    public String toString() {
        return "Room{" +
                "roomType='" + roomType + '\'' +
                ", roomNumber=" + roomNumber +
                ", price=" + price +
                ", isAvailable=" + isAvailable +
                '}';
    }
}

class Reservation {
    private Room room;
    private String guestName;
    private int nights;
    private double totalPrice;

    public Reservation(Room room, String guestName, int nights) {
        this.room = room;
        this.guestName = guestName;
        this.nights = nights;
        this.totalPrice = room.getPrice() * nights;
    }

    public Room getRoom() {
        return room;
    }

    public String getGuestName() {
        return guestName;
    }

    public int getNights() {
        return nights;
    }

    public double getTotalPrice() {
        return totalPrice;
    }

    @Override
    public String toString() {
        return "Reservation{" +
                "room=" + room +
                ", guestName='" + guestName + '\'' +
                ", nights=" + nights +
                ", totalPrice=" + totalPrice +
                '}';
    }
}

class Hotel {
    private HashMap<String, ArrayList<Room>> roomCategories;
    private ArrayList<Reservation> reservations;

    public Hotel() {
        roomCategories = new HashMap<>();
        reservations = new ArrayList<>();
    }

    public void addRoom(Room room) {
        roomCategories.putIfAbsent(room.getRoomType(), new ArrayList<>());
        roomCategories.get(room.getRoomType()).add(room);
    }

    public void searchAvailableRooms(String roomType) {
        ArrayList<Room> rooms = roomCategories.get(roomType);
        if (rooms == null) {
            System.out.println("No such room category found.");
            return;
        }

        System.out.println("Available rooms in " + roomType + " category:");
        for (Room room : rooms) {
            if (room.isAvailable()) {
                System.out.println(room);
            }
        }
    }

    public void makeReservation(String roomType, String guestName, int nights) {
        ArrayList<Room> rooms = roomCategories.get(roomType);
        if (rooms == null) {
            System.out.println("No such room category found.");
            return;
        }

        for (Room room : rooms) {
            if (room.isAvailable()) {
                room.setAvailable(false);
                Reservation reservation = new Reservation(room, guestName, nights);
                reservations.add(reservation);
                System.out.println("Reservation successful!");
                System.out.println(reservation);
                return;
            }
        }

        System.out.println("No available rooms in this category.");
    }

    public void viewReservations() {
        System.out.println("All Reservations:");
        for (Reservation reservation : reservations) {
            System.out.println(reservation);
        }
    }
}
public class HotelReservationSystem {
     public static void main(String[] args) {
        Hotel hotel = new Hotel();

        hotel.addRoom(new Room("Single", 101, 100.0));
        hotel.addRoom(new Room("Single", 102, 100.0));
        hotel.addRoom(new Room("Double", 201, 150.0));
        hotel.addRoom(new Room("Suite", 301, 300.0));

        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("\nHotel Reservation System");
            System.out.println("1. Search Available Rooms");
            System.out.println("2. Make a Reservation");
            System.out.println("3. View Reservations");
            System.out.println("4. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter room type (Single/Double/Suite): ");
                    String roomType = scanner.next();
                    hotel.searchAvailableRooms(roomType);
                    break;
                case 2:
                    System.out.print("Enter room type (Single/Double/Suite): ");
                    roomType = scanner.next();
                    System.out.print("Enter guest name: ");
                    String guestName = scanner.next();
                    System.out.print("Enter number of nights: ");
                    int nights = scanner.nextInt();
                    hotel.makeReservation(roomType, guestName, nights);
                    break;
                case 3:
                    hotel.viewReservations();
                    break;
                case 4:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice! Please try again.");
            }
        }
    }
}



# HotelReservationSystem
codealpha
